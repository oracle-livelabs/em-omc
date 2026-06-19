# How I get end-to-end visibility on OCI for an app running anywhere — with OpenTelemetry, the APM agent, and the Management Agent

A customer asked me a question I get a lot: *"My apps don't all run in the same place. Some are on a VM, some on Kubernetes, one is a Java service nobody wants to touch, and the database is Autonomous. How do I get a single end-to-end picture in OCI without rewriting everything?"*

So I built one. It's a working demo — an online drone shop, a back-office CRM, and a GenAI studio — wired into the full OCI Observability and Management stack. Everything you read below is running, not a slide.

Here is the artifact I always start with. A checkout produces order `227977` and trace `fbd1747c757417b579a8cedf11dae886`. That one trace id follows the request from the browser, through the load balancer and WAF, into a Python FastAPI service, across to a Java payment gateway, down to an Oracle Autonomous Database, and back. The payment span comes back `merchant_authorization_result = declined` with `is-fault = false` — the platform worked perfectly, the order was declined by the antifraud rule. That distinction (a business outcome, not a technical fault) is exactly what end-to-end visibility is supposed to give you, and you get it in under a minute.

![OCI APM Trace Explorer showing the full checkout waterfall for order 227977 — browser RUM, shop FastAPI, Java payment gateway, and ATP spans on one trace](screenshots/01-apm-trace-waterfall.png)
*The checkout trace in OCI APM: one trace id from the browser down to ATP, with the declined payment span expanded.*

In this article I'll walk you through what the demo does, what it writes to the database, how I instrumented it three different ways, and how the OpenTelemetry signals line up with OCI APM, Log Analytics, Operations Insights, and Database Management so the whole thing reads as one story.

---

## What the demo actually does

The front of the house is the **OCTO Drone Shop** — a Python 3.11 / FastAPI storefront selling commercial drones and parts (Skydio, Parrot, DJI-class gear, plus frames, motors, ESCs, batteries, FPV kit). It's a real e-commerce flow, not a "hello world":

- **Browse** the catalog, search, filter by category, open a product detail page.
- **Log in** through IDCS OIDC (Authorization Code + PKCE, RS256 JWKS verification) or a password fallback, with rate limiting and dedicated security spans.
- **Add to cart**, then **check out** — and this is where it gets interesting. Checkout runs an idempotency-token contract, a payment-gateway state machine (wallet decrypt → antifraud → network token → authorize → capture), and a fraud-detection step.
- **Sync the order** asynchronously to the **enterprise CRM**, propagating the W3C trace context across the service boundary so the order stays on the same trace.

Behind it sits the **CRM portal** (orders, customers, support tickets, invoices, campaigns, audit log) and an optional **GenAI studio** for the AI labs. The shop, the CRM, and the Java payment service all share one Oracle Autonomous Transaction Processing (ATP 19c) database.

The point of the shop isn't the drones. It's that a single user click fans out across Python, Java, an OIDC provider, a payment gateway, and a database — which is precisely the kind of distributed mess where observability either earns its keep or falls apart.

---

## What gets written to the database (and why the invoice matters)

If you want to follow a request all the way down, you have to follow it into the data. Here's what the shop and CRM actually persist in ATP:

- **`products`** — catalog: `sku` (unique), `name`, `price`, `stock`, `category`.
- **`orders`** — the busy table: `total`, `status`, `payment_status`, `payment_provider_reference`, `payment_gateway_request_id` (the span attaches this), plus a cross-system idempotency key `(source_system, source_order_id, idempotency_token)` and a **`correlation_id`** column that carries the APM trace id across the shop→CRM boundary.
- **`order_items`** — line items, `quantity` × `unit_price`.
- **`customers`**, **`support_tickets`**, **`campaigns`**, **`leads`**, **`shipments`** — the CRM side.
- **`audit_logs`** — every privileged action, with a **`trace_id`** column so a security event in the CRM ties back to the same APM trace as the request that caused it.
- **`invoices`** — and this is the one I like to show off.

The invoice table stores the actual PDF **inside Oracle** as a SecureFile BLOB:

```python
# crm/server/modules/invoices.py
# Invoice document stored directly in Oracle ATP as a SecureFile BLOB —
# showcases the database's native file-storage capability (no object store).
# Generation is triggered when an order is paid, and every step emits OTEL spans.
pdf_data        = Column(LargeBinary)   # the PDF bytes, in the row
pdf_filename    = Column(String(200))
pdf_size        = Column(Integer)
pdf_generated_at = Column(DateTime)
```

When an order flips to `paid`, a hook renders a real PDF with `fpdf2` (pure Python, no system libraries) and writes the bytes straight into the row inside a span called `db.write.invoice_pdf`. No object storage, no file server — Oracle holds the document. A CronJob drains any historical backlog every five minutes, and a manual reconcile endpoint is there for on-demand runs.

Why does this matter for observability? Because the trace that started at a browser click ends at a **file living in the database**, and you can see every hop in between — including the LOB write. That's the "user → DB" thread the customer asked me about, made literal.

![The CRM invoices page rendering a PDF served straight out of the Oracle ATP invoices.pdf_data BLOB column](screenshots/02-invoice-blob-pdf.png)
*The invoice PDF is generated on payment and stored as a SecureFile BLOB in ATP — no object store. The `db.write.invoice_pdf` span is on the same trace.*

---

## The hard part isn't collecting telemetry. It's correlating it.

Most observability demos show you a nice trace waterfall and stop. The real work is the join. A trace in APM, a log line in Log Analytics, a CPU metric in Monitoring, and a slow SQL statement in Database Management are four different services with four different data models. If they don't share a key, you're back to matching timestamps by eye.

So I gave them a shared key. Every request carries:

- **`oracleApmTraceId`** and the W3C `traceparent` context, stamped into every structured log line as the app handles the request.
- A stable **service identity**: `service.name` per workload and **`service.namespace = octo`** across the whole fleet, so APM groups the topology correctly.

That contract is the entire trick. From a Log Analytics record I pivot to its APM trace on the trace id. From an APM span I read the `db.statement` / Oracle `sql_id`, then jump to that SQL's history in Operations Insights, then to the session that ran it in Database Management. The bridge is deliberately boring — one field name, enforced everywhere by contract tests — and boring is what holds up at 2 a.m.

---

## Three ways in, one picture out

Real estates are never uniform, so I instrumented the demo three different ways on purpose. The user never sees the seam, because all three feed the same correlation contract.

### 1. Direct OpenTelemetry SDK — for code I own

The FastAPI services (shop, CRM, GenAI studio) instrument themselves with the **OpenTelemetry SDK** and export OTLP straight to OCI APM. No agent on the host, no sidecar. This is the path for code you control and can ship.

OCI APM speaks **native OTLP**, so there's no translation layer. The exporter points at the APM domain's private data-upload endpoint and authenticates with a data key:

```python
# shop/server/observability/otel_setup.py
otlp_endpoint = f"{base_url}/20200101/opentelemetry/private/v1/traces"
otlp_exporter = OTLPSpanExporter(
    endpoint=otlp_endpoint,
    headers={"Authorization": f"dataKey {apm_private_key}"},   # key from a secret, never in code
)
tracer_provider.add_span_processor(BatchSpanProcessor(otlp_exporter))
```

What OpenTelemetry actually buys me here, and how each piece lands in OCI:

| OpenTelemetry capability | What I do with it | Where it lands in OCI |
|---|---|---|
| **Traces / spans** | Manual spans for the payment state machine + auto-instrumentation for FastAPI, SQLAlchemy, httpx | OCI **APM** (Trace Explorer, topology) |
| **Resource attributes** | `service.name`, `service.namespace=octo`, `service.instance.id`, `deployment.environment`, `app.runtime` (oke/compute/local), `db.target=octo-atp` | APM service map + correlation keys |
| **Span attributes** | `payment.gateway.step`, `payment.gateway.request_id`, `workflow.id`, `http.url.path`, `db.statement` | APM span detail + Log Analytics fields |
| **W3C context propagation** | `traceparent` / `tracestate` extracted inbound, injected on every outbound call (incl. shop→CRM, shop→Java) | One trace id across all services |
| **Auto-instrumentation** | FastAPI, SQLAlchemy (DB spans with `sql_id`), httpx/requests, stdlib logging bridge | APM spans + log correlation |
| **Log correlation** | `oracleApmTraceId` / `oracleApmSpanId` stamped on every log record | OCI **Logging** → **Log Analytics** |

Metrics and logs don't go over OTLP in this build — they use the native OCI SDKs, which is the pragmatic choice today:

- **Metrics**: the app computes business KPIs (payment success rate, login failures, idempotency violations) and posts them to **OCI Monitoring** under the `octo_apm_demo` namespace, with a Prometheus `/metrics` endpoint alongside.
- **Logs**: structured JSON goes to **OCI Logging** through the ingestion SDK on a background queue, with PII masking (card numbers, CVV, email, phone) that is careful to *exempt* the correlation ids so the masker never eats a trace id.

If you'd rather centralize, there's an opt-in **OpenTelemetry Collector** (`services/otel-gateway`) you can drop in front of APM to own sampling and redaction policy — the apps just repoint their exporter at the collector. I keep it off by default so the default path stays simple: app → APM.

### 2. The OCI APM Java agent — for code I don't own

The payment gateway is a Spring Boot 3 service, and I instrument it **without touching its source**. The OCI **APM Java agent** attaches at the JVM (`-javaagent:...oracle-apm-agent.jar`) and produces spans through bytecode instrumentation. It reads its endpoint and data key from environment variables, extracts the inbound `traceparent`, and opens its server span as a child of the Python (or RUM) span that called it.

The payoff is the part the SDK can't give you: the agent populates APM's **App Servers** view with real JVM telemetry — Apdex, active server count, request rate, CPU load, heap, GC time. In the checkout trace you see the Java span sitting between the Python handler and the ATP queries, *and* you get JVM health for that same service. Same trace, same APM domain, zero code changes. That's the path for the framework you'd rather not fork.

![OCI APM App Servers view for the Java payment service, showing Apdex, JVM heap, and GC metrics from the APM Java agent](screenshots/03-apm-java-app-server.png)
*The APM Java agent gives the payment service an App Servers entry — JVM health the OTel SDK path doesn't produce — while still joining the same checkout trace.*

### 3. The Management Agent and OCI-native collection — for the database and the edge

Everything you can't (or shouldn't) instrument by hand reports through the **OCI Management Agent** and the native services themselves:

- **Stack Monitoring** watches ATP and host health (the span's `db.target=octo-atp` lines up with the Stack Monitoring resource).
- **Operations Insights** and **Database Management** are enabled on the ATP (`OCTOATP`) — SQL performance, wait events, execution plans, and capacity trends, with no application code involved.
- The **load balancer**, **WAF**, and **database** emit logs and metrics no app produces.

Three collection mechanisms — SDK, agent, native — and a trace that starts in an OTel-instrumented Python handler, crosses an agent-instrumented Java span, and ends at an agent-monitored database is still **one trace**.

---

## "Anywhere the app runs" is a contract, not a slogan

The same workloads run on two **runtimes** — a Compute VM running containers, or a managed Kubernetes cluster (OKE) — and the telemetry looks **identical** on both, because identity and correlation are defined by the service contract, not the host. `service.namespace = octo` is set the same way whether the process is a container on a VM or a pod in OKE, and `oracleApmTraceId` is stamped by the same logging code. Move the app from a VM to Kubernetes and not one dashboard breaks — they key off fields every topology emits, so they were never coupled to the host.

OCI **Resource Manager** is not a third place the app lives — it's *how* I stand the whole thing up. ORM is managed Terraform: it provisions the runtime and every observability resource in one apply (APM domain, log groups, the Log Analytics connector, Monitoring alarms, the ATP, OKE), so the correlation contract is wired by the deployment itself rather than clicked together afterwards. Same stack, repeatable, on either runtime.

That's the difference between "we have observability" and "we have *portable* observability." The first breaks every time you re-platform; the second is the asset.

---

## End to end, service by service: APM → Log Analytics → Ops Insights → DB Management

Let me make the customer's "follow it from the user to the DB" concrete. Someone reports that checkout is failing. Here's the path, and which OCI service answers each question:

1. **OCI APM (Trace Explorer)** — *Where did the request go and where did it break?* Filter `serviceName = octo-drone-shop AND http.status_code >= 500`, open the trace, read the waterfall: shop FastAPI → Java App Server → ATP spans. The failing span names the step, e.g. `payment.gateway.step = authorize`.

2. **OCI APM (RUM)** — *Did the user actually feel it?* RUM ties the browser session and page timing to the same `oracleApmTraceId`, so you know whether this was a real user or a synthetic probe.

![OCI Log Analytics showing all log records for a single oracleApmTraceId — shop, Java, and WAF lines on one screen](screenshots/04-loganalytics-trace-drilldown.png)
*Trace → log pivot: one `oracleApmTraceId` filters every log source in Log Analytics, so the shop, Java, and WAF lines line up on one screen.*

3. **OCI Log Analytics** — *What did the services say?* The saved search `trace-drilldown.sql` filters every log source on `oracleApmTraceId = <trace>` and returns the shop log, the Java log, and the WAF event on one screen. App logs land as `octo-shop-v2` / `octo-crm-v2`, WAF as `octo-waf`, all fed in by **Service Connector Hub** from OCI Logging. (There are 46 saved searches and a handful of command-center dashboards behind this — checkout correlation, payment security triage, DB slowness hotspots, GenAI cost, and so on.)

4. **Operations Insights** — *Is this SQL slow in general, or just now?* The APM DB span carries the `sql_id`. Drop that into OPSI and you get the statement's history, plan changes, and resource trend — is this a regression or a one-off spike under load?

5. **Database Management** — *What's the database actually doing right now?* From the same `sql_id` you get the live session, the wait event, the execution plan, and ASH/AWR context for the ATP. This is where "the app is slow" becomes "this statement is waiting on this event in this session."

![OCI Database Management performance hub for OCTOATP, with the sql_id from the APM span selected — wait events and execution plan for that statement](screenshots/05-dbmgmt-sqlid-drilldown.png)
*The `sql_id` carried on the APM DB span opens the exact statement in Database Management — wait events, plan, and session — closing the loop from user click to database.*

Five services, one trace id, one investigation. APM and Log Analytics cover the application and the edge; Operations Insights and Database Management cover the database; and the **`sql_id` on the APM span is the bridge** that joins the application story to the database story. You walk from a user complaint to the exact SQL — and, in the invoice case, to the exact BLOB write — without ever guessing at a timestamp.

GenAI rides the same rails: the studio emits `gen_ai.*` span attributes to APM, pushes token counts and cost to the `octo_genai` Monitoring namespace (and Langfuse), and prints the trace id next to the answer so you can follow an AI response from the browser to the model call to its cost. LLM calls aren't a separate island — they're spans like any other, with cost and a judge score attached.

---

## The full OCI Observability surface, and what each service answers

| OCI service | The question it answers | How it's fed |
|---|---|---|
| **APM** (incl. **RUM**) | Where did the request spend its time, from the browser down? | OTLP from the OTel SDK; the APM Java agent; RUM JS in the page |
| **Logging** | What did each service say, on which trace? | OCI Logging ingestion SDK (structured JSON) |
| **Log Analytics** | Search, correlate, and alert across all logs | Service Connector Hub from OCI Logging; 5 parsers, 46 saved searches |
| **Monitoring** | Is a business/runtime metric out of range? | App posts to `octo_apm_demo` / `octo_genai`; alarms + notifications |
| **Stack Monitoring** | Is the ATP / host healthy, and which wait event bites? | Management Agent + native; `db.target=octo-atp` ties it to spans |
| **Operations Insights** | How has this SQL / this capacity trended? | ATP registered (`OCTOATP`) |
| **Database Management** | What is the database doing *right now*? | ATP registered (`OCTOATP`) |
| **Cloud Guard** | Is the security posture drifting? | Detector/responder recipes, auto-remediation from Log Analytics rules |
| **Data Safe** | Is sensitive data exposed, who touched it? | Audit policy + assessment on the ATP target |
| **Service Connector Hub** | Get every log into one place | Routes OCI Logging → Log Analytics |
| **WAF** | Filter and record edge traffic | Detection mode by default; events as `octo-waf` in Log Analytics |

And the supporting cast that makes it run: **OKE** and **Compute** (the runtimes), **Autonomous Database (ATP 19c)** (the shared data tier and the BLOB invoice store), **OCIR** (images), **Vault + KMS** (secrets and the mTLS wallet), **Notifications** (alarm delivery), and **Resource Manager** (the stack form factor).

---

## Want to try the pivots yourself?

This isn't a screenshot tour — it ships with an 18-lab workshop (~9.5 hours, splittable) that walks the exact moves: capture your first trace (Lab 01), pivot trace→log on `oracleApmTraceId` (Lab 02), drill slow SQL into Operations Insights (Lab 03), register ATP in Stack Monitoring (Lab 08), run a full failed-checkout RCA (Lab 10), and the integrated APM + Log Analytics root-cause and payment-failure deep dives (Labs 17–18). The GenAI labs (12–16) follow an AI answer through APM, Langfuse, and an LLM-as-judge score.

---

## What I'd take away from this

End-to-end visibility doesn't come from buying every observability product. It comes from one decision, made early and enforced everywhere: **a shared identity and correlation contract that every collection path honors.**

- Instrument with the **OpenTelemetry SDK** where you own the code, and let OCI APM ingest OTLP natively.
- Attach the **APM agent** where you don't own the code — the JVM service still joins the same trace and gives you App Server health for free.
- Use the **Management Agent and the native services** for the database and the edge.
- Then make all three stamp the same `oracleApmTraceId` and the same `service.namespace`, and carry the `sql_id` on your DB spans so APM, Log Analytics, Operations Insights, and Database Management line up on one investigation.

Do that, and "where is the app running" stops being a question your telemetry has to answer. The trace runs from the user to the database and back — on a VM or in Kubernetes, provisioned the same way by Resource Manager — and it's always one trace.

---

## References — OCI services used in this project

**Observability & Management**

- OCI Application Performance Monitoring (APM) — https://docs.oracle.com/en-us/iaas/application-performance-monitoring/
- APM Real User Monitoring (RUM) — https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/use-real-user-monitoring.html
- OCI Logging — https://docs.oracle.com/en-us/iaas/Content/Logging/home.htm
- OCI Logging Analytics — https://docs.oracle.com/en-us/iaas/log-analytics/
- OCI Monitoring — https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm
- OCI Stack Monitoring — https://docs.oracle.com/en-us/iaas/stack-monitoring/
- OCI Operations Insights — https://docs.oracle.com/en-us/iaas/operations-insights/
- OCI Database Management — https://docs.oracle.com/en-us/iaas/database-management/
- OCI Management Agent — https://docs.oracle.com/en-us/iaas/management-agents/
- OCI Service Connector Hub — https://docs.oracle.com/en-us/iaas/Content/connector-hub/home.htm
- OCI Notifications — https://docs.oracle.com/en-us/iaas/Content/Notification/home.htm

**Security**

- OCI Cloud Guard — https://docs.oracle.com/en-us/iaas/cloud-guard/
- OCI Data Safe — https://docs.oracle.com/en-us/iaas/data-safe/
- OCI Web Application Firewall (WAF) — https://docs.oracle.com/en-us/iaas/Content/WAF/Concepts/overview.htm
- OCI Vault / KMS — https://docs.oracle.com/en-us/iaas/Content/KeyManagement/home.htm

**Platform**

- OCI Container Engine for Kubernetes (OKE) — https://docs.oracle.com/en-us/iaas/Content/ContEng/home.htm
- OCI Compute — https://docs.oracle.com/en-us/iaas/Content/Compute/home.htm
- Oracle Autonomous Database (ATP) — https://docs.oracle.com/en-us/iaas/autonomous-database/
- OCI Registry (OCIR) — https://docs.oracle.com/en-us/iaas/Content/Registry/home.htm
- OCI Resource Manager — https://docs.oracle.com/en-us/iaas/Content/ResourceManager/home.htm
- OCI Load Balancer — https://docs.oracle.com/en-us/iaas/Content/Balance/home.htm

**OpenTelemetry**

- OpenTelemetry — https://opentelemetry.io/
- OTLP specification — https://opentelemetry.io/docs/specs/otlp/
- W3C Trace Context — https://www.w3.org/TR/trace-context/
- Sending OpenTelemetry traces to OCI APM — https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/configure-open-source-tracing-systems.html

*This is a personal demo project and is not affiliated with or endorsed by Oracle.*
