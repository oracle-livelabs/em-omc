# Traceability Summary

Estimated Time: 5 minutes

| Workshop Area | Source | Evidence Type | Notes |
| --- | --- | --- | --- |
| Introduction | `end-to-end-observability.md`; `https://github.com/adibirzu/octo-observability-demo`; `README.md`; `ARCHITECTURE.md` | mixed | Establishes the learner goal: deploy OCTO APM Demo and enable OCI Observability and Management services for end-to-end monitoring. |
| Lab 1 | `docs/QUICKSTART.md`; `site/getting-started/quickstart.md`; `Makefile`; `deploy/validate-deployment.sh`; Resource Manager release URL | runbook | Uses the OCTO quickstart pattern: configure `.env` from `env.template`, run `make doctor`, choose Resource Manager or `make` deployment, run `make smoke`, and verify `drones.${DNS_DOMAIN}` plus `admin.${DNS_DOMAIN}`. |
| Lab 2 | `README.md`; `deploy/bootstrap.sh`; `deploy/oci/ensure_apm.sh`; `deploy/oci/ensure_log_analytics_connectors.sh`; `deploy/oci/ensure_monitoring.sh`; `deploy/oci/ensure_stack_monitoring.sh`; `deploy/oci/ensure_waf.sh`; `deploy/oke/README.md`; `tools/la-saved-searches/` | runbook and component metadata | Covers the OCTO observability surface: APM, RUM, OCI Logging, Log Analytics, Service Connector Hub, OKE monitoring, WAF, Monitoring, Stack Monitoring, Operations Insights, and Database Management. |
| Lab 3 | `end-to-end-observability.md`; `site/workshop/lab-01-first-trace.md`; `site/workshop/lab-02-trace-log-correlation.md`; `site/architecture/correlation-contract.md`; `shop/server/observability/`; `crm/server/observability/`; `services/apm-java-demo/` | workflow and code | Covers browser traffic, OCTO Drone Shop, Enterprise CRM Portal, OCI APM tracing, RUM, synthetic monitoring, `traceparent`, `oracleApmTraceId`, `oracleApmSpanId`, and service identity. |
| Lab 4 | `end-to-end-observability.md`; `site/workshop/lab-09-chaos-drill.md`; `site/workshop/lab-17-root-cause-apm-logan.md`; `site/workshop/lab-18-payment-failure-rca-apm.md`; `crm/deploy/observability/log-analytics-saved-searches.json`; `site/architecture/correlation-contract.md` | workflow and query | Covers correlated troubleshooting across APM tracing, Log Analytics application logs, Log Analytics security monitoring, WAF logs, Monitoring, Operations Insights, Database Management, Stack Monitoring, invoice persistence, and database SQL IDs. |
| Lab 5 | `services/genai-studio/README.md`; `services/genai-studio/app/main.py`; `site/workshop/lab-12-genai-agent-trace.md`; `site/workshop/lab-13-apm-langfuse-grafana-pivot.md`; `site/observability-v2/ai-studio-genai-monitoring.md`; `deploy/oci/monitoring-dashboards/genai-token-cost.json` | design and runbook | Covers AI Studio, Langfuse, OpenTelemetry GenAI attributes, `studio.run_id`, agent/tool spans, token and cost metrics, behavior-change evidence, and anomaly-detection checkpoints. |
| Source coverage validation | `end-to-end-observability.md`; `end-to-end-observability-livelab/SOURCE-COVERAGE-VALIDATION.md`; OCTO APM Demo workshop source under `site/workshop/` | cross-validation | Maps source article and OCTO repository topics to the consolidated five-lab LiveLabs flow and records the screenshot asset gap. |
| OCI documentation expansion | OCI documentation for APM, OpenTelemetry, RUM, Logging, Log Analytics, Monitoring, Connector Hub, WAF, OKE, Stack Monitoring, Operations Insights, Database Management, Management Agent, Cloud Guard, Data Safe, Notifications, and Generative AI Agents | product documentation | Expands Labs 2-5 with deeper service checkpoints, evidence fields, and Learn More references while preserving the five-lab structure. |

## Notes

- The source anchor is `https://github.com/adibirzu/octo-observability-demo`.
- This workshop now follows OCTO APM Demo repository commands, services, DNS names, and correlation contracts.
- Local screenshot assets referenced by the source article, such as `screenshots/01-apm-trace-waterfall.png`, were not present under the current workshop source folder during authoring. The workshop therefore uses textual checkpoints and leaves screenshot capture as a future asset task.
- `SOURCE-COVERAGE-VALIDATION.md` records the source-to-lab mapping after the five-lab consolidation.
- Labs 2 through 5 include OCI documentation-backed Learn More links and additional validation checkpoints.

## Acknowledgements

* **Traceability Compiled By** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 19, 2026
