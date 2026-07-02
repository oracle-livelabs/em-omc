# Source Coverage Validation

## Introduction

This file maps the approved workshop scope to OCTO APM Demo, the original end-to-end observability narrative, and current Oracle documentation.

Estimated Time: 5 minutes

### Objectives

- Confirm that the workshop remains anchored to `adibirzu/octo-observability-demo`.
- Verify coverage of the four requested application-monitoring use cases.
- Verify hands-on coverage of the seven focused OCI services.
- Record intentional prerequisites and runtime gaps.

## Coverage Matrix

| Requirement | Workshop evidence | Status |
| --- | --- | --- |
| Applications running anywhere | Introduction explains portable APM and Log Analytics collection while using OCTO on OKE as the reference deployment. | Covered |
| OCTO source anchor | Lab 1 clones the OCTO repository; all labs use OCTO paths, endpoints, service names, and correlation fields. | Covered |
| Five-lab structure | Manifest contains deployment, service connection, tracing, incident investigation, and operationalization labs. | Covered |
| OCI Log Analytics OKE monitoring | Lab 2 connects OKE through the Kubernetes Monitoring Solution; Lab 4 pivots from an APM pod attribute to Workload, Pod, event, metric, and log evidence. | Covered |
| OCI Log Analytics Security Monitoring | Lab 2 configures VCN, Compute when applicable, and OCI Audit inputs; Lab 4 uses the three Security solution views to assess application context. | Covered |
| OCI APM tracing | Lab 3 creates a known W3C trace, follows a browser checkout across Python, Java, and Oracle Database, and pivots to Log Analytics. | Covered |
| Oracle Database bottleneck diagnosis | Lab 4 invokes the current read-only OCTO N+1 endpoint, identifies repeated database spans and SQL IDs in APM, and continues through Ops Insights and Database Management. | Covered |
| OCI Monitoring | Lab 2 verifies `octo_apm_demo` metrics and alarms; Lab 5 validates the database-latency alarm and Notifications destination. | Covered |
| OCI Log Analytics | Labs 2 through 4 use Kubernetes, Security, application, WAF, Audit, and trace-correlated log evidence. | Covered |
| OCI Events | Lab 5 creates or inspects a Resource Manager Create Job End rule, triggers a Plan job, and verifies match and delivery metrics. | Covered |
| OCI Application Performance Monitoring | Labs 2 through 4 use the OCTO domain, saved queries, flame charts, service spans, Kubernetes attributes, and database spans. | Covered |
| OCI Database Management | Labs 2 and 4 enable the target, open Performance Hub, and inspect SQL, execution, wait, and plan evidence. | Covered |
| OCI Ops Insights | Labs 2 and 4 verify DB Performance and SQL trend evidence for the OCTO database. | Covered |
| OCI Resource Analytics | Labs 2 and 5 verify a populated instance and query APM, OKE, Database Management, Ops Insights, and available Events views. | Covered |
| Correlation contract | Labs 1, 3, and 4 use `trace_id`, `span_id`, `oracleApmTraceId`, `oracleApmSpanId`, `request_id`, `workflow_id`, pod identity, and Oracle SQL ID. | Covered |
| Alert and automation path | Lab 5 distinguishes Monitoring alarms from Events rules while using one confirmed Notifications destination. | Covered |

## Source Corrections

1. The OKE Resource Manager stack is the primary full-workshop deployment. A Compute-only deployment cannot complete the OKE use case by itself.
2. The official Oracle product name is **Kubernetes Monitoring Solution**. OKE is the reference cluster in this workshop.
3. The Security Monitoring Solution uses the Virtual Cloud Network, Compute, and OCI Audit views. OCTO WAF records remain application-edge evidence.
4. The current OCTO code exposes `/api/dashboard/n-plus-one` for a read-only database workload. The workshop does not use the stale `?slow=true` source example.
5. APM identifies the request and SQL bridge. Ops Insights and Database Management perform the deeper database trend and execution diagnosis.
6. Resource Analytics supplies resource inventory and relationship context, not live application telemetry.

## Prepared-Tenancy Requirements

- OKE and OCTO workloads are running.
- The tenancy sends data to the Log Analytics Kubernetes and Security solutions.
- The tenancy enables APM, Monitoring, Database Management, and Ops Insights.
- At least one subscriber has confirmed the Notifications subscription.
- Resource Analytics has populated the selected regions, and learners can query its Autonomous AI Database.

## Result

The refocused five-lab workshop covers all four use cases and all seven focused services. Supporting services appear only where they enable routing or delivery.

## Acknowledgements

* **Coverage Reviewed By** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
