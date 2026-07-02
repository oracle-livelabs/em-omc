# Source Coverage Validation

## Introduction

This file cross-validates `end-to-end-observability.md` and the OCTO APM Demo repository against the consolidated five-lab LiveLabs workshop. It records where each source topic appears in the workshop and flags any intentional asset gaps.

Estimated Time: 5 minutes

### Objectives

In this validation, you will:

- Confirm that each source section maps to one or more LiveLabs locations.
- Confirm that OCTO APM Demo repository concepts are present in the five-lab flow.
- Identify gaps that require source assets or SME confirmation rather than more lab text.

## Coverage Matrix

| Source area | Source | LiveLabs coverage | Status |
| --- | --- | --- | --- |
| OCTO APM Demo anchor repository | `https://github.com/adibirzu/octo-observability-demo`; `README.md` | Introduction; WORKSHOP-DETAILS; Lab 1 Learn More; TRACEABILITY | Covered |
| Quickstart deployment paths: Resource Manager, `make doctor`, `make tenancy-init`, `make deploy`, `make smoke`, local stack | `docs/QUICKSTART.md`; `site/getting-started/quickstart.md`; `Makefile` | Lab 1 Task 1 through Task 4 | Covered |
| Public endpoints and DNS pattern: `drones.${DNS_DOMAIN}`, `admin.${DNS_DOMAIN}`, `/ready` checks | `docs/QUICKSTART.md`; `deploy/oke/README.md`; `deploy/validate-deployment.sh` | Introduction prerequisites; WORKSHOP-DETAILS; Lab 1 Task 3 and Task 4; Lab 3 Task 1 | Covered |
| Service topology: OCTO Drone Shop, Enterprise CRM Portal, AI Studio, Java payment sidecar, OTEL Gateway, async worker, auto-remediator, shared ATP | `README.md`; `ARCHITECTURE.md`; `site/architecture/service-inventory.md` | Introduction; Lab 1 Task 5; Lab 2 Task 6; Lab 3 Task 2 and Task 4; Lab 5 Task 1 | Covered |
| OCI Observability surface map: APM, RUM, Logging, Log Analytics, Monitoring, Stack Monitoring, Service Connector Hub, WAF, Cloud Guard, Vault, GenAI, Langfuse | `README.md`; `deploy/oci/`; `site/observability/`; `site/observability-v2/` | Introduction Learn More; Lab 2 Task 1 through Task 6; Lab 4 Task 5 | Covered |
| OKE monitoring and Kubernetes evidence: `octo-apm-demo-oke`, `octo-drone-shop`, `enterprise-crm`, pod/container records, HPA and autoscaling searches | `deploy/oke/README.md`; `deploy/helm/octo-apm-demo/`; `tools/la-saved-searches/oke-*`; `site/workshop/lab-11-oke-autoscaling.md` | Lab 2 Task 2; Lab 4 Task 5 | Covered |
| Trace-log correlation contract: W3C `traceparent`, `trace_id`, `span_id`, `oracleApmTraceId`, `oracleApmSpanId`, `request_id`, `workflow_id`, `service.namespace=octo` | `site/architecture/correlation-contract.md`; `shop/server/observability/`; `crm/server/observability/` | Introduction objectives; Lab 1 Task 5; Lab 3 Task 2 through Task 6; Lab 4 Task 3 | Covered |
| OCTO Drone Shop flow: browse, search, filter, product detail, login, cart, checkout, idempotency, payment state machine, fraud detection, CRM sync | `end-to-end-observability.md`; `shop/README.md`; `site/workshop/lab-01-first-trace.md`; `site/workshop/lab-18-payment-failure-rca-apm.md` | Lab 3 Task 1 and Task 2; Lab 4 Task 1 and Task 2 | Covered |
| Java payment sidecar: Spring Boot service, OCI APM Java agent, App Servers, Apdex, request rate, CPU, heap, and GC | `README.md`; `services/apm-java-demo/`; `site/workshop/lab-18-payment-failure-rca-apm.md` | Lab 1 Task 4; Lab 3 Task 2 and Task 4 | Covered |
| Shared ATP data model: products, orders, order items, customers, support tickets, campaigns, leads, shipments, audit logs, invoices, LLMetry rows | `end-to-end-observability.md`; `crm/`; `shop/`; `services/genai-studio/db/` | Lab 4 Task 4; Lab 5 Task 4 | Covered |
| Invoice SecureFile BLOB, `invoices.pdf_data`, `db.write.invoice_pdf`, scheduled backlog, and manual reconcile evidence | `end-to-end-observability.md`; `site/workshop/lab-17-root-cause-apm-logan.md`; `site/workshop/lab-18-payment-failure-rca-apm.md` | Lab 4 Task 4 | Covered as validation checkpoint |
| Log Analytics saved searches, dashboards, detection rules, trace-to-log pivots, and security monitoring | `deploy/oci/log_analytics/`; `tools/la-saved-searches/`; `crm/deploy/observability/log-analytics-saved-searches.json`; `site/workshop/lab-02-trace-log-correlation.md`; `site/workshop/lab-06-waf-event-investigation.md` | Lab 2 Task 5 and Task 6; Lab 3 Task 6; Lab 4 Task 3 | Covered |
| Monitoring custom metrics and alarms: payment success, login failures, checkout idempotency, RUM error rate, HPA, GenAI token and cost metrics | `deploy/oci/ensure_monitoring.sh`; `tools/monitoring-alarms/`; `deploy/oci/monitoring-dashboards/genai-token-cost.json`; `site/workshop/lab-05-metric-and-alarm.md` | Lab 2 Task 4 and Task 6; Lab 4 Task 5; Lab 5 Task 5 | Covered |
| Security and WAF use cases: edge events, Cloud Guard, auto-remediation, edge-fuzz, container-lab, VM-lab | `deploy/oci/ensure_waf.sh`; `deploy/oci/ensure_cloud_guard*.sh`; `services/auto-remediator/`; `services/edge-fuzz/`; `services/container-lab/`; `services/vm-lab/` | Lab 2 Task 5; Lab 4 Task 3 | Covered |
| Root-cause flow: APM trace to Log Analytics to Operations Insights to Database Management to Stack Monitoring | `site/workshop/lab-17-root-cause-apm-logan.md`; `site/workshop/lab-10-failed-checkout.md`; `site/workshop/lab-18-payment-failure-rca-apm.md` | Lab 4 Task 2 through Task 6 | Covered |
| AI Studio and GenAI observability: `octo-genai-studio`, `studio.run_id`, `studio.mode`, `gen_ai.*`, Langfuse, Grafana, token cost, judge scores, RAG lineage | `services/genai-studio/README.md`; `services/genai-studio/app/main.py`; `site/workshop/lab-12-genai-agent-trace.md`; `site/workshop/lab-13-apm-langfuse-grafana-pivot.md`; `site/observability-v2/ai-studio-genai-monitoring.md` | Lab 5 Task 1 through Task 5 | Covered |
| Original 18-lab OCTO workshop collapsed into the requested five-lab LiveLabs format | `site/workshop/index.md`; `site/workshop/lab-*.md` | Manifest; WORKSHOP-DETAILS; Labs 1-5 | Covered through consolidation |
| Takeaways: SDK where you own code, APM agent for Java sidecar, Management Agent and native OCI services for database and edge, shared IDs and SQL IDs | `end-to-end-observability.md`; `README.md`; `site/architecture/correlation-contract.md` | Introduction objectives; Lab 3 Task 4; Lab 4 Task 6 | Covered |

## Asset Gaps

- The source markdown references five screenshot files under `screenshots/`.
- No local screenshot files were present in the workspace during validation.
- The LiveLab covers the screenshot content as textual checkpoints and avoids broken image links.

## Result

The five-lab workshop now anchors on `adibirzu/octo-observability-demo` and covers the source article. It maps the OCTO repository quickstart, service topology, correlation contract, OCI observability assets, and workshop flow into LiveLabs format. The only remaining gap is visual asset availability for the source screenshots.

## Documentation Expansion

Labs 2 through 5 include OCI documentation-backed checkpoints and Learn More links for Logging, Log Analytics, OKE, APM, OpenTelemetry, RUM, Monitoring, Service Connector Hub, WAF, Stack Monitoring, Operations Insights, Database Management, Management Agent, Cloud Guard, Data Safe, Notifications, and Generative AI Agents.

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 19, 2026
