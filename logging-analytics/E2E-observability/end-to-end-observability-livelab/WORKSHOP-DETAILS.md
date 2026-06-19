# Workshop Details

Estimated Time: 5 minutes

## Short Description

Deploy the OCI-DEMO e-commerce application and control plane, then enable OCI Observability and Management services for end-to-end monitoring. Learners validate OCI Log Analytics OKE Monitoring, OCI Log Analytics Security Monitoring, OCI Application Performance Monitoring tracing, database observability, and agent monitoring.

## Long Description

This workshop helps customers understand OCI Observability and Management offerings by deploying the OCI-DEMO e-commerce application stack, enabling the corresponding OCI services, and using those services to investigate real application activity. The learner starts with the Quick Start deployment path, brings up the control plane, and verifies the Enterprise CRM Portal and OCTO Drone Shop.

The workshop then turns on OCI Application Performance Monitoring, Real User Monitoring, Synthetic Monitoring, OCI Logging, Log Analytics, Monitoring, Operations Insights, Database Management, and database log routing. The application monitoring use cases are explicit: OKE logs and metrics in Log Analytics, security events and detections in Log Analytics, and distributed traces in OCI APM.

Each lab reinforces a common correlation contract: stable service identity, W3C trace context, `oracleApmTraceId` in logs, and SQL identifiers on database spans. The consolidated flow still covers the three collection paths from the source article: direct OpenTelemetry SDK instrumentation, the OCI APM Java agent, and OCI Management Agent or native OCI collection.

The final lab applies the same operating model to AI agents. Learners deploy and verify the GenAI and Agent Fabric components, inspect agent and tool spans in OCI APM and Langfuse, and identify behavior changes or anomalies from latency, error, token, tool, and trace patterns.

## Workshop Outline

1. Introduction
2. Lab 1 - QuickStart Deployment
3. Lab 2 - Enable OCI Operations and Management Services
4. Lab 3 - Observe the E-Commerce Flow End to End
5. Lab 4 - Investigate Application, Log, and Database Signals
6. Lab 5 - Monitor Agent Behavior and Detect Anomalies

## Workshop Prerequisites

- Access to an OCI tenancy with permission to deploy OCI-DEMO resources.
- OCI CLI profile, instance principal, or resource principal authentication configured for the deployment host.
- A local or bastion checkout of the OCI-DEMO repository with `.env.local` configured from `.env.example`.
- Permission to use OCI Application Performance Monitoring, Logging, Log Analytics, Monitoring, Operations Insights, Database Management, WAF, OKE, Autonomous Database, Generative AI, and agent-related resources.
- Access to the canonical application URLs after deployment, or equivalent values for your environment:
  - `https://shop.octodemo.cloud`
  - `https://crm.octodemo.cloud`
  - `https://cp.octodemo.cloud`

## Notes

- Mode used: `publish-ready`.
- Target duration: approximately 6.5 hours.
- FreeSQL is not used because the workshop is driven by OCI Console, application, observability, and database management workflows rather than standalone SQL exercises.
- The generated workshop does not embed screenshots because local screenshot assets were not present in the source folder during authoring.

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
