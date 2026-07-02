# Traceability Summary

Estimated Time: 5 minutes

## Source Map

| Workshop area | Primary source | Applied evidence |
| --- | --- | --- |
| Introduction | OCTO `README.md`; `site/architecture/correlation-contract.md`; current OCI service documentation | Defines applications-running-anywhere scope, seven focused services, four use cases, and shared identity fields. |
| Lab 1 | `docs/QUICKSTART.md`; `Makefile`; OCTO OKE Resource Manager release | Deploys the OKE reference path, runs `make doctor` and `make smoke`, and records resource identifiers. |
| Lab 2 | `deploy/oci/ensure_apm.sh`; `ensure_monitoring.sh`; `ensure_db_observability.sh`; Log Analytics Kubernetes and Security solution documentation | Connects OKE, VCN, Audit, APM, Monitoring, Database Management, Ops Insights, Events, and Resource Analytics prerequisites. |
| Lab 3 | `site/workshop/lab-01-first-trace.md`; `lab-02-trace-log-correlation.md`; correlation contract; Python and Java instrumentation | Creates a known W3C trace, inspects a browser checkout, identifies Java and database spans, and pivots to logs. |
| Lab 4 | `shop/server/modules/dashboard.py`; `site/workshop/lab-03-slow-sql-drill-down.md`; `lab-17-root-cause-apm-logan.md`; OCI database performance documentation | Uses the current read-only `/api/dashboard/n-plus-one` endpoint and diagnoses repeated SQL through APM, Ops Insights, and Database Management. |
| Lab 5 | `deploy/oci/ensure_monitoring.sh`; OCTO Events envelope; OCI Events and Resource Analytics references | Validates an alarm, routes a Resource Manager job-end event, verifies delivery metrics, and queries `OCIRA` views. |

## Source Priority

1. Current OCTO application code and deployment assets define runnable commands, endpoints, service names, and telemetry fields.
2. Current Oracle documentation defines product navigation, service behavior, metrics, and Resource Analytics views.
3. The original blog supplies the end-to-end observability narrative.
4. Stale OCTO workshop examples do not override current code.

The July 1, 2026 review used OCTO commit `50f78ebcff456f75ad7cafca7ff900f705cf11f3`. The review replaced a stale slow-query example with the current read-only N+1 endpoint.

## Oracle Database Validation

- APM identifies the application request, database span, statement metadata, and Oracle SQL ID.
- Ops Insights provides fleet and historical database or SQL trends.
- Database Management provides managed-database performance, Top SQL, waits, and plan detail.
- The lab compares execution count, elapsed time, waits, and runtime plan evidence before recommending a change.
- ASH, AWR, SQL Monitoring, and tuning features remain subject to database type, collection state, entitlement, and management-pack access.

## FreeSQL Decision

The workshop does not use FreeSQL. Resource Analytics queries require a tenancy-specific Resource Analytics Autonomous AI Database and the `OCIRA` schema.

## Asset and Runtime Gaps

- The workshop does not bundle local publishable screenshots. The labs use precise console paths and evidence fields.
- Live OCI ingestion, alarm state, Events delivery, and Resource Analytics population require a prepared workshop tenancy.
- Resource Analytics provisioning is outside the workshop because it creates chargeable Autonomous AI Database resources and may also create Oracle Analytics Cloud.

## Acknowledgements

* **Traceability Compiled By** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
