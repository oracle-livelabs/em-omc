# Lab 2: Enable OCI Operations and Management Services

## Introduction

In this lab, you enable the OCI Observability and Management services that make the e-commerce stack operationally visible. You will verify APM, RUM, synthetic checks, OCI Log Analytics OKE Monitoring, OCI Log Analytics Security Monitoring, Monitoring, database observability, WAF logging, and database log routing.

Estimated Time: 95 minutes

### Objectives

In this lab, you will:

- Verify the OCTO APM Demo observability bootstrap.
- Validate the OCI Log Analytics OKE Monitoring solution.
- Validate OCI Log Analytics for Security Monitoring.
- Enable Autonomous Database observability through Database Management and Operations Insights.
- Confirm that application, WAF, and database signals are visible in OCI services.
- Confirm the full OCI Observability and Management surface used by OCTO APM Demo.
- Tie each enablement checkpoint to the relevant OCI documentation surface.

## Task 1: Verify the Observability Baseline

1. From the OCTO APM Demo repository, confirm that the observability bootstrap assets exist.

    ```bash
    ls deploy/oci/ensure_apm.sh \
       deploy/oci/ensure_log_analytics_connectors.sh \
       deploy/oci/ensure_monitoring.sh \
       deploy/oci/ensure_stack_monitoring.sh \
       deploy/oci/ensure_waf.sh
    ```

2. If the observability resources are not deployed, run the bootstrap path for your environment before continuing.

    ```bash
    ./deploy/bootstrap.sh
    ```

3. Run the smoke test after bootstrap or deployment.

    ```bash
    make smoke
    ```

4. In the OCI Console, open **Observability & Management**.

5. Confirm that these resources exist:

    - Log Analytics namespace.
    - OCI APM domain.
    - APM private and public data keys.
    - APM dashboards or saved queries.
    - Log Analytics parsers, sources, dashboards, and detection searches.
    - Monitoring alarms or alarm definitions for platform signals.

6. Open the APM domain and confirm that Trace Explorer is available.

7. Open **Monitoring** and confirm that you can query metrics and inspect alarm status for the compartment that contains the demo resources.

8. Open **Connector Hub** and confirm that service connectors exist for the log routes that feed Log Analytics.

9. Record the OCI documentation concept each resource validates.

    | Resource | OCI documentation concept |
    | --- | --- |
    | APM domain | APM traces, spans, RUM, synthetic monitoring, and OpenTelemetry data sources. |
    | Log Analytics namespace | Search, correlate, dashboard, and alert across logs. |
    | OCI Logging log group | Fully managed log collection and search in the tenancy. |
    | Connector Hub connector | Managed routing of data between OCI services. |
    | Monitoring metrics and alarms | Health, capacity, performance, and alarm evaluation. |

## Task 2: Validate the OCI Log Analytics OKE Monitoring Solution

1. Verify whether this deployment uses OKE.

    ```bash
    kubectl config current-context
    kubectl get nodes
    ```

2. If your environment uses the OCTO Helm path, confirm the installed release.

    ```bash
    helm list --all-namespaces | grep octo-apm-demo
    ```

3. Confirm the core namespaces and deployments.

    ```bash
    kubectl get deploy -n octo-drone-shop
    kubectl get deploy -n enterprise-crm
    kubectl get deploy -n octo-drone-shop | grep octo-apm-java-demo
    ```

4. In Log Analytics, confirm that the Kubernetes entity for the demo cluster shows active status.

5. Confirm that recent pod, container, node, or namespace records appear for the OKE cluster.

6. If you have `kubectl` access, confirm that the monitoring pods run in the cluster.

    ```bash
    kubectl get pods --all-namespaces | grep -E 'oci-onm|logan|mgmt-agent'
    ```

7. In Log Analytics, run a recent search for Kubernetes records. Adjust field names to match your tenancy.

    ```text
    'Entity Type' contains 'Kubernetes' or 'Log Source' contains 'Kubernetes' | timestats count as Records by 'Entity Name'
    ```

8. Record one evidence item for the OKE Monitoring use case:

    - Kubernetes entity name.
    - Log Analytics source or parser.
    - recent pod or container log row.
    - dashboard or saved search URL.

9. In APM, confirm that the CRM and Drone Shop services appear after you generate traffic.

10. Cross-check the OKE service surface in the OCI Console.

    - Open **Developer Services**.
    - Open **Kubernetes Clusters**.
    - Select the `octo-apm-demo-oke` cluster or your equivalent cluster.
    - Review cluster health, node pools, work requests, audit logs, application logs, and metrics.

11. Record whether OKE evidence comes from Log Analytics, OCI Logging, Monitoring metrics, or all three.

## Task 3: Enable Database Observability

1. From the OCTO APM Demo repository, enable or verify database observability for the ATP target.

    ```bash
    bash deploy/oci/ensure_db_observability.sh
    bash deploy/oci/ensure_stack_monitoring.sh
    ```

2. In the OCI Console, open the Autonomous Database used by the demo.

3. Confirm that Database Management shows enabled status.

4. Confirm that Operations Insights shows enabled status for the database.

5. Confirm that OCI Logging and Log Analytics receive database audit or diagnostic events when available in your tenancy.

6. Confirm that Stack Monitoring shows the ATP target or related host resource when your deployment enables Stack Monitoring.

7. Confirm that the database target name lines up with the trace resource attribute used by the application.

    ```text
    db.target = octo-atp
    ```

8. In the Enterprise CRM Portal, open the observability or operations pages if they are available.

    ```text
    https://admin.${DNS_DOMAIN}
    ```

9. In **Operations Insights**, record the database name, SQL activity window, and any capacity trend that appears for the ATP target.

10. In **Database Management**, record current sessions, wait events, SQL activity, and execution-plan visibility for the ATP target.

11. In **Stack Monitoring**, record ATP or host health if your tenancy enables Stack Monitoring. If it is not enabled, record the gap and continue with Operations Insights and Database Management.

## Task 4: Verify Edge, Browser, and Synthetic Monitoring

1. Open the Drone Shop and CRM public URLs.

    ```text
    https://drones.${DNS_DOMAIN}
    https://admin.${DNS_DOMAIN}
    ```

2. In OCI APM, open **Real User Monitoring** and confirm browser activity for the application hostnames after you browse the applications.

3. In OCI APM, open **Synthetic Monitoring** and confirm that REST monitors exist for the deployed application endpoints.

4. In OCI Logging, confirm that WAF logs or load balancer logs route public application traffic when your deployment enables those resources.

5. In Log Analytics, run a recent search for the application services. Use your actual log source names when they differ.

    ```text
    'Log Source' in ('OCTO Drone Shop', 'Enterprise CRM Portal') | timestats count as Records by 'Log Source'
    ```

6. Save the APM domain, Log Analytics namespace, and database display name. You will use them in the remaining labs.

7. In **Monitoring**, inspect metrics for at least two layers:

    - load balancer or public endpoint metrics.
    - OKE node or pod metrics.
    - database metrics.
    - application custom metrics such as `octo_apm_demo` when available.

8. Confirm whether any alarms exist for availability, latency, error rate, or database health. Record the alarm name, metric namespace, query, and destination topic.

## Task 5: Validate OCI Log Analytics for Security Monitoring

1. In Log Analytics, open **Dashboards** or **Saved Searches**.

2. Find the security monitoring content deployed by the observability baseline. Look for dashboards, searches, or detection rules related to:

    - WAF events.
    - OWASP application security events.
    - MITRE or Sigma-style detections.
    - edge-fuzz, container-lab, VM-lab, or Cloud Guard records when your deployment enables those security labs.

3. Search WAF and application security records for the e-commerce hostnames.

    ```text
    ('Log Source' contains 'WAF' or Message contains 'OWASP' or Message contains 'MITRE' or Message contains 'x-oci-waf')
    and (ClientRequestHost in ('drones.${DNS_DOMAIN}', 'admin.${DNS_DOMAIN}') or Message contains 'octo')
    ```

4. If you have a safe test URL from your instructor, send one detection-mode request to the application and confirm that Log Analytics receives the event.

    ```bash
    curl -I "https://drones.${DNS_DOMAIN}/?q=%3Cscript%3Ealert(1)%3C/script%3E"
    ```

5. Open the matching Log Analytics row and record:

    - source name.
    - rule, parser, or dashboard name.
    - WAF action or score when present.
    - client hostname.
    - trace ID or request ID when present.

6. Confirm that this evidence answers the Security Monitoring use case: detect suspicious application or edge activity and keep the event available for investigation in Log Analytics.

7. Open the WAF policy or firewall for the application when your deployment exposes it.

8. Confirm how the WAF policy handles detection-mode traffic. Map the observed behavior to WAF concepts:

    - request protection rules inspect HTTP requests.
    - protection rules can log, allow, or block traffic.
    - actions such as check, allow, or return HTTP response determine the outcome.
    - rate limiting and request control protect the public application endpoint.

9. Open **Cloud Guard** when your tenancy enables it. Look for problems, detector recipes, responder recipes, or security posture findings related to the demo compartment.

10. Open **Data Safe** when your tenancy enables it. Confirm whether ATP audit or assessment evidence exists for the demo database.

## Task 6: Inventory the Full OCI Observability Surface

1. Confirm how each service contributes to the investigation workflow.

    | Service | Evidence to confirm |
    | --- | --- |
    | APM and RUM | Trace Explorer, topology, RUM pages, and Synthetic checks. |
    | OCI Logging | Structured application, WAF, database, or service logs. |
    | Log Analytics | Parsers, saved searches, dashboards, detections, and trace pivots. |
    | Monitoring | Business or runtime metrics, including `octo_apm_demo` or `octo_genai` when present. |
    | Stack Monitoring | ATP or host health tied to `db.target=octo-atp`. |
    | Operations Insights | SQL and capacity trend for the ATP target. |
    | Database Management | Live sessions, waits, execution plans, and SQL activity. |
    | Cloud Guard | Security posture, detector recipes, responder recipes, or related findings. |
    | Data Safe | Audit or sensitive-data evidence for the ATP target when enabled. |
    | Service Connector Hub | OCI Logging routes into Log Analytics. |
    | WAF | Detection-mode edge events such as `octo-waf`. |

2. Record any service that your lab tenancy does not enable. Mark it as an environment gap, not a workshop gap.

3. Confirm that at least one service in each layer has evidence:

    - application and browser layer.
    - Kubernetes or compute runtime layer.
    - edge and security layer.
    - database layer.
    - AI or agent layer when you reach Lab 5.

## Learn More

- [OCTO APM Demo repository](https://github.com/adibirzu/octo-observability-demo)
- [OCTO APM Demo observability surface map](https://github.com/adibirzu/octo-observability-demo#oci-observability-surface-map)
- [OCTO APM Demo Log Analytics assets](https://github.com/adibirzu/octo-observability-demo/tree/main/deploy/oci/log_analytics)
- [OCTO APM Demo OKE deployment](https://github.com/adibirzu/octo-observability-demo/blob/main/deploy/oke/README.md)
- [OCI Logging](https://docs.oracle.com/en-us/iaas/Content/Logging/home.htm)
- [OCI Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/)
- [OCI Kubernetes Engine](https://docs.oracle.com/en-us/iaas/Content/ContEng/home.htm)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Service Connector Hub](https://docs.oracle.com/en-us/iaas/Content/connector-hub/home.htm)
- [OCI Web Application Firewall](https://docs.oracle.com/en-us/iaas/Content/WAF/Concepts/overview.htm)
- [OCI Stack Monitoring](https://docs.oracle.com/en-us/iaas/stack-monitoring/)
- [OCI Operations Insights](https://docs.oracle.com/en-us/iaas/operations-insights/)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)
- [OCI Management Agent](https://docs.oracle.com/en-us/iaas/management-agents/)
- [OCI Cloud Guard](https://docs.oracle.com/en-us/iaas/cloud-guard/)
- [OCI Data Safe](https://docs.oracle.com/en-us/iaas/data-safe/)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 19, 2026
