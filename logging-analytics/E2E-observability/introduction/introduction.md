# End-to-End Observability on OCI for Applications Running Anywhere

## Introduction

A customer request can cross a browser, Kubernetes services, a Java payment component, and Oracle Database. Each layer emits different telemetry. Operators need one workflow that joins those signals and leads from a symptom to evidence.

In this workshop, you deploy [OCTO APM Demo](https://github.com/adibirzu/octo-observability-demo) and observe its Drone Shop, Enterprise CRM Portal, Java payment sidecar, OKE runtime, and Oracle Autonomous Database. The application uses W3C trace context and shared identifiers so traces, logs, metrics, events, and database evidence can describe the same request.

The workshop focuses on these OCI services:

- OCI Monitoring
- OCI Log Analytics
- OCI Events
- OCI Application Performance Monitoring
- OCI Database Management
- OCI Ops Insights
- OCI Resource Analytics

OCI Notifications and Connector Hub support the core flow. They deliver alarm and event messages and route OCI logs into Log Analytics.

The labs cover four application-monitoring use cases:

- Monitor OCTO on OKE with the Log Analytics Kubernetes Monitoring Solution.
- Investigate security posture with the Log Analytics Security Monitoring Solution.
- Trace a customer transaction from browser to Oracle Database with OCI APM.
- Find a database-bound application bottleneck in APM, then diagnose its SQL and database impact with Ops Insights and Database Management.

The OCTO instrumentation also demonstrates a portable operating model. APM and Log Analytics can collect from applications on OCI, other public clouds, private clouds, and on-premises. OCI Events and Resource Analytics add OCI resource state, inventory, and relationship context.

### Prerequisites

- Access to an OCI tenancy and a compartment for the OCTO resources.
- Permission to use the seven focused services.
- An OKE deployment of OCTO APM Demo for the complete workshop path.
- Administrator-assisted onboarding for the Log Analytics Kubernetes and Security solutions.
- A pre-provisioned Resource Analytics instance with populated regional data and access to its Autonomous AI Database.
- An OCI Notifications topic with a confirmed subscription for alarm and event delivery.
- A workshop user with the OCTO `chaos-operator` role for controlled fault scenarios.
- A workstation, bastion, or Cloud Shell session with `git`, `bash`, `make`, `oci`, `kubectl`, `helm`, `jq`, `curl`, and `openssl`.
- Access to the deployed application URLs:

    ```text
    https://drones.${DNS_DOMAIN}
    https://admin.${DNS_DOMAIN}
    ```

### Objectives

In this workshop, you will:

- Deploy and validate OCTO APM Demo on OKE.
- Connect the application, Kubernetes, security, and database telemetry paths.
- Use OCI APM to follow a distributed transaction and identify database spans.
- Pivot from a trace ID to matching Log Analytics records.
- Use the Log Analytics Kubernetes and Security solutions for operational investigations.
- Diagnose a database-bound bottleneck with APM, Ops Insights, and Database Management.
- Validate a Monitoring alarm and an OCI Events rule with a Notifications action.
- Query Resource Analytics for OCTO service inventory and relationship context.
- Produce a concise evidence chain for an application incident.

Estimated Workshop Time: 6.5 hours

## Workshop Flow

1. Deploy OCTO APM Demo.
2. Connect OCI Observability services.
3. Trace a customer transaction end to end.
4. Investigate Kubernetes, security, and database incidents.
5. Operationalize Monitoring, Events, and Resource Analytics.

## Learn More

- [OCTO APM Demo repository](https://github.com/adibirzu/octo-observability-demo)
- [OCTO APM Demo Quickstart](https://github.com/adibirzu/octo-observability-demo/blob/main/docs/QUICKSTART.md)
- [OCTO correlation contract](https://github.com/adibirzu/octo-observability-demo/blob/main/site/architecture/correlation-contract.md)
- [OCI Application Performance Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/)
- [OCI Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Events](https://docs.oracle.com/en-us/iaas/Content/Events/)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)
- [OCI Ops Insights](https://docs.oracle.com/en-us/iaas/operations-insights/)
- [OCI Resource Analytics](https://docs.oracle.com/en-us/iaas/Content/resource-analytics/home.htm)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
