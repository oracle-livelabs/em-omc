# End-to-End Observability on OCI for Applications Running Anywhere

## Introduction

Modern applications need more than a healthy endpoint. A customer action can cross a browser, an edge service, several Kubernetes services, Oracle Autonomous Database, and an AI agent workflow. Each layer emits a different signal. OCI Observability and Management services help operators connect those signals into one investigation.

In this workshop, you deploy [OCTO APM Demo](https://github.com/adibirzu/octo-observability-demo), enable the supporting OCI Observability and Management services, and investigate the OCTO Drone Shop, Enterprise CRM Portal, Oracle ATP database, Java payment sidecar, and AI Studio workflows. You will use OCI Application Performance Monitoring, Real User Monitoring, Synthetic Monitoring, OCI Logging, Log Analytics, Monitoring, Operations Insights, Database Management, WAF, OCI GenAI observability, Langfuse, and the platform correlation contract.

The application monitoring path highlights three use cases: OCI Log Analytics OKE Monitoring, OCI Log Analytics for Security Monitoring, and OCI Application Performance Monitoring tracing. The labs also validate the three collection paths from the source article: direct OpenTelemetry SDK instrumentation, the OCI APM Java agent, and OCI Management Agent or native OCI collection.

### Prerequisites

- Access to an OCI tenancy with permission to deploy OCTO APM Demo resources.
- OCI CLI profile, instance principal, or resource principal authentication configured for the deployment host.
- A workstation, bastion, or Cloud Shell session that can run `git`, `bash`, `make`, `oci`, `kubectl`, `jq`, and `curl`.
- A configured `.env` file for OCTO APM Demo deployment values.
- OCI Console access to Application Performance Monitoring, Logging, Log Analytics, Monitoring, Operations Insights, Database Management, WAF, OKE, Autonomous Database, Generative AI, and agent-related resources.
- Public or internal access to the deployed application URLs:
  - `https://drones.${DNS_DOMAIN}`
  - `https://admin.${DNS_DOMAIN}`

### Objectives

- Deploy the OCTO APM Demo stack with Resource Manager or the `make` quickstart.
- Enable OCI Observability and Management services for the application, Kubernetes, WAF, and database layers.
- Validate OCI Log Analytics OKE Monitoring and OCI Log Analytics Security Monitoring use cases.
- Generate e-commerce traffic and inspect the end-to-end request path in OCI APM.
- Validate OCI Application Performance Monitoring tracing for the application flow.
- Pivot from traces to Log Analytics, Monitoring, Operations Insights, and Database Management evidence.
- Confirm that database, invoice, WAF, JVM, and security evidence share the same correlation contract.
- Monitor agent behavior changes and detect anomalies from trace, log, metric, tool, and token signals.

Estimated Workshop Time: 6.5 hours

## Learn More

- [OCTO APM Demo repository](https://github.com/adibirzu/octo-observability-demo)
- [OCTO APM Demo Quickstart](https://github.com/adibirzu/octo-observability-demo/blob/main/docs/QUICKSTART.md)
- [OCTO APM Demo Correlation Contract](https://github.com/adibirzu/octo-observability-demo/blob/main/site/architecture/correlation-contract.md)
- [OCI Application Performance Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/)
- [APM Real User Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/use-real-user-monitoring.html)
- [OCI Logging Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Stack Monitoring](https://docs.oracle.com/en-us/iaas/stack-monitoring/)
- [OCI Operations Insights](https://docs.oracle.com/en-us/iaas/operations-insights/)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)
- [OCI Management Agent](https://docs.oracle.com/en-us/iaas/management-agents/)
- [OCI Service Connector Hub](https://docs.oracle.com/en-us/iaas/Content/connector-hub/home.htm)
- [OCI Cloud Guard](https://docs.oracle.com/en-us/iaas/cloud-guard/)
- [OCI Data Safe](https://docs.oracle.com/en-us/iaas/data-safe/)
- [OCI Web Application Firewall](https://docs.oracle.com/en-us/iaas/Content/WAF/Concepts/overview.htm)
- [OCI Container Engine for Kubernetes](https://docs.oracle.com/en-us/iaas/Content/ContEng/home.htm)
- [OCI Resource Manager](https://docs.oracle.com/en-us/iaas/Content/ResourceManager/home.htm)
- [OpenTelemetry](https://opentelemetry.io/)
- [W3C Trace Context](https://www.w3.org/TR/trace-context/)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 19, 2026
