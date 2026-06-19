# Source Coverage Validation

## Introduction

This file cross-validates `end-to-end-observability.md` against the consolidated five-lab LiveLabs workshop. It records where each source topic appears in the workshop and flags any intentional asset gaps.

Estimated Time: 5 minutes

### Objectives

In this validation, you will:

- Confirm that each source section maps to one or more LiveLabs locations.
- Confirm that source-specific observability pivots are present in the five-lab flow.
- Identify gaps that require source assets or SME confirmation rather than more lab text.

## Coverage Matrix

| Source area | Source lines | LiveLabs coverage | Status |
| --- | --- | --- | --- |
| Opening customer problem: apps on VM, Kubernetes, Java service, Autonomous Database, and one end-to-end OCI view | `end-to-end-observability.md` lines 1-12 | Introduction; Lab 1 Task 5; Lab 3 Task 2; Lab 4 Task 5 | Covered |
| Sample checkout artifact: order `227977`, trace `fbd1747c757417b579a8cedf11dae886`, declined payment as business outcome | lines 7-10 | Lab 3 Task 1 and Task 2; Lab 4 Task 1 and Task 2 | Covered as sample-or-current-run evidence |
| OCTO Drone Shop flow: browse, search, filter, product detail, login, cart, checkout, idempotency, payment state machine, fraud detection, CRM sync | lines 16-29 | Lab 1 Task 4; Lab 3 Task 1 and Task 2; Lab 4 Task 1 | Covered |
| Shared ATP data model: products, orders, order items, customers, support tickets, campaigns, leads, shipments, audit logs, invoices | lines 31-42 | Lab 4 Task 4 | Covered |
| Invoice SecureFile BLOB, `invoices.pdf_data`, `db.write.invoice_pdf`, scheduled backlog, and manual reconcile evidence | lines 42-60 | Lab 4 Task 4 | Covered as validation checkpoint |
| Correlation contract: `oracleApmTraceId`, W3C `traceparent`, `service.name`, `service.namespace=octo`, `db.statement`, and `sql_id` | lines 64-73 | Introduction objectives; Lab 1 Task 5; Lab 3 Task 3 and Task 5; Lab 4 Task 2 and Task 3 | Covered |
| Direct OpenTelemetry SDK path for owned FastAPI services, OTLP to OCI APM, resource/span attributes, auto-instrumentation, log correlation | lines 81-113 | Lab 3 Task 3 and Task 4; Lab 5 Task 3 | Covered |
| Optional OpenTelemetry Collector `services/otel-gateway` for sampling and redaction policy | line 113 | Lab 3 Task 4 | Covered as optional checkpoint |
| OCI APM Java agent for the Spring Boot payment service, `-javaagent`, App Servers, Apdex, request rate, CPU, heap, and GC | lines 115-122 | Lab 3 Task 2 and Task 4 | Covered |
| Management Agent and native OCI collection for Stack Monitoring, Operations Insights, Database Management, load balancer, WAF, and database logs | lines 124-132 | Lab 2 Task 3 and Task 6; Lab 3 Task 4; Lab 4 Task 4 | Covered |
| Portable runtime contract across Compute and OKE, Resource Manager provisioning, APM domain, log groups, Log Analytics connector, Monitoring alarms, ATP, and OKE | lines 136-144 | Lab 1 Task 5; Lab 2 Task 2 and Task 6 | Covered |
| End-to-end service path: APM Trace Explorer, RUM, Log Analytics trace drilldown, Operations Insights, Database Management, `sql_id` bridge | lines 146-168 | Lab 2 Task 4; Lab 3 Task 2 and Task 5; Lab 4 Task 2 through Task 5 | Covered |
| Log source details: `trace-drilldown.sql`, `octo-shop-v2`, `octo-crm-v2`, `octo-waf`, Service Connector Hub, saved searches, command-center dashboards | lines 154-158 | Lab 2 Task 5 and Task 6; Lab 3 Task 5; Lab 4 Task 3 | Covered as source-name checkpoints |
| GenAI observability: `gen_ai.*` spans, `octo_genai` Monitoring namespace, Langfuse, token cost, judge score, and trace ID beside the answer | line 168 | Lab 5 Task 1 through Task 5 | Covered |
| Full OCI Observability surface: APM, Logging, Log Analytics, Monitoring, Stack Monitoring, Operations Insights, Database Management, Cloud Guard, Data Safe, Service Connector Hub, WAF | lines 172-188 | Introduction Learn More; Lab 2 Task 6; Lab 4 Task 3 and Task 4 | Covered |
| Supporting platform services: OKE, Compute, ATP 19c, OCIR, Vault/KMS, Notifications, Resource Manager, Load Balancer | line 188 and references | Introduction Learn More; Lab 1 Task 5; Lab 2 Task 6 | Covered |
| Original 18-lab try-it-yourself pivots collapsed into the requested five-lab format | lines 192-194 | Manifest; WORKSHOP-DETAILS; Labs 1-5 | Covered through consolidation |
| Takeaways: SDK where you own code, APM agent where you do not, Management Agent/native services for database and edge, shared IDs and SQL IDs | lines 198-207 | Introduction objectives; Lab 3 Task 4; Lab 4 Task 5 | Covered |
| References for OCI and OpenTelemetry services | lines 211-250 | Introduction Learn More | Covered |

## Asset Gaps

- The source markdown references five screenshot files under `screenshots/`.
- No local screenshot files were present in the workspace during validation.
- The LiveLab covers the screenshot content as textual checkpoints and avoids broken image links.

## Result

The five-lab workshop covers all source topics after consolidation. The only remaining gap is visual asset availability for the screenshots referenced by the source article.

## Documentation Expansion

Labs 2 through 5 now include OCI documentation-backed checkpoints and Learn More links for Logging, Log Analytics, OKE, APM, OpenTelemetry, RUM, Monitoring, Service Connector Hub, WAF, Stack Monitoring, Operations Insights, Database Management, Management Agent, Cloud Guard, Data Safe, Notifications, and Generative AI Agents.

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
