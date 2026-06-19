# Traceability Summary

Estimated Time: 5 minutes

| Workshop Area | Source | Evidence Type | Notes |
| --- | --- | --- | --- |
| Introduction | `end-to-end-observability.md`; `OCI-DEMO-1/README.md`; `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md` | mixed | Establishes the learner goal: deploy the OCI-DEMO e-commerce stack and enable OCI Observability and Management services for end-to-end monitoring. |
| Lab 1 | `OCI-DEMO-1/README.md`; `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md`; `https://github.com/adibirzu/OCI-DEMO#quick-start` | runbook | Uses the Quick Start deployment pattern: configure `.env.local`, dry-run/deploy with `deploy.py`, run the control-plane setup script, verify, and check status. |
| Lab 2 | `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md`; `OCI-DEMO-1/components.yaml`; `OCI-DEMO-1/docs/create_demo_steps.js` | runbook and component metadata | Covers C2 Observability, C10 OKE Native Monitoring, C15 DB Advanced, OCI Log Analytics OKE Monitoring, OCI Log Analytics Security Monitoring, application telemetry, WAF, APM/RUM, Monitoring, Operations Insights, and Database Management. |
| Lab 3 | `end-to-end-observability.md`; `OCI-DEMO-1/docs/create_demo_steps.js`; `OCI-DEMO-1/external/octo-drone-shop/docs/technical-architecture.md`; `OCI-DEMO-1/external/octo-drone-shop/server/observability/otel_setup.py`; `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md` | workflow and code | Covers browser traffic, OCTO Drone Shop, Enterprise CRM, OCI Application Performance Monitoring tracing, RUM, synthetic monitoring, `traceparent`, `oracleApmTraceId`, and service identity. |
| Lab 4 | `end-to-end-observability.md`; `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md`; `OCI-DEMO-1/external/EnterpriseCrmPortal/deploy/observability/log-analytics-saved-searches.json`; `OCI-DEMO-1/external/oci-coordinator/src/agents/database/troubleshoot.py`; `OCI-DEMO-1/docs/create_demo_steps.js` | workflow and query | Covers correlated troubleshooting across APM tracing, Log Analytics application logs, Log Analytics security monitoring, Monitoring, Operations Insights, Database Management, WAF logs, and database SQL IDs. |
| Lab 5 | `OCI-DEMO-1/docs/DEPLOYMENT_GUIDE.md`; `OCI-DEMO-1/docs/C12_GENAI_IMPLEMENTATION_PLAN_2026-02-27.md`; `OCI-DEMO-1/docs/LLMETRY_GENAI_EXPANSION.md`; `OCI-DEMO-1/components.yaml` | design and runbook | Covers C12 GenAI, C24 Agent Fabric, C34 Langfuse, OpenTelemetry GenAI attributes, agent/tool spans, behavior-change evidence, and anomaly-detection checkpoints. |
| Source coverage validation | `end-to-end-observability.md`; `end-to-end-observability-livelab/SOURCE-COVERAGE-VALIDATION.md` | cross-validation | Maps every source section to the consolidated five-lab LiveLabs flow and records the screenshot asset gap. |
| OCI documentation expansion | OCI documentation for APM, OpenTelemetry, RUM, Logging, Log Analytics, Monitoring, Connector Hub, WAF, OKE, Stack Monitoring, Operations Insights, Database Management, Management Agent, Cloud Guard, Data Safe, Notifications, and Generative AI Agents | product documentation | Expands Labs 2-5 with deeper service checkpoints, evidence fields, and Learn More references while preserving the five-lab structure. |

## Notes

- Local screenshot assets referenced by the source article, such as `screenshots/01-apm-trace-waterfall.png`, were not present under the current workshop source folder during authoring. The workshop therefore uses textual checkpoints and leaves screenshot capture as a future asset task.
- `SOURCE-COVERAGE-VALIDATION.md` records the source-to-lab mapping after the five-lab consolidation.
- Labs 2 through 5 include OCI documentation-backed Learn More links and additional validation checkpoints.
- The user provided the public GitHub URL as the Quick Start reference. Anonymous raw README fetch returned 404 in this environment. The local `OCI-DEMO-1` bundle supplied exact commands and component names.
- Local source and standard OCI service workflows support the Oracle database feature steps. The exact `oracle-db-skills` skill was not loaded in this session.

## Acknowledgements

* **Traceability Compiled By** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
