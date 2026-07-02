# Lab 2: Connect OCI Observability Services

## Introduction

In this lab, you connect the OCI services used by the remaining investigations. You will onboard the OCTO OKE cluster to the Log Analytics Kubernetes Monitoring Solution, prepare the Security Monitoring Solution, and verify APM, Monitoring, database observability, Events, and Resource Analytics.

Estimated Time: 90 minutes

### Objectives

In this lab, you will:

- Verify the OCTO observability resources and shared identifiers.
- Connect OKE to the Log Analytics Kubernetes Monitoring Solution.
- Prepare the VCN, Compute, and OCI Audit inputs used by the Security Monitoring Solution.
- Verify OCI APM, Monitoring, Database Management, and Ops Insights.
- Confirm that OCI Events and Resource Analytics are ready for Lab 5.
- Record a baseline for all seven focused services.

## Task 1: Verify the OCTO Observability Baseline

1. From the OCTO repository root, confirm that the deployment assets used by this workshop exist.

    ```bash
    ls deploy/oci/ensure_apm.sh \
       deploy/oci/ensure_log_analytics_connectors.sh \
       deploy/oci/ensure_monitoring.sh \
       deploy/oci/ensure_db_observability.sh \
       deploy/oci/log_analytics/deploy_octo_apm_workshop.sh
    ```

2. Verify the application and OKE runtime.

    ```bash
    make smoke
    kubectl get nodes
    kubectl get deploy -n octo-drone-shop
    kubectl get deploy -n enterprise-crm
    ```

3. Record the resource identifiers that you will reuse.

    ```text
    Compartment OCID:
    OKE cluster name and OCID:
    APM domain name and OCID:
    Log Analytics namespace:
    Autonomous Database name and OCID:
    Resource Manager stack name and OCID:
    Notifications topic name and OCID:
    Resource Analytics instance:
    ```

4. In the OCI Console, open **Observability & Management** and confirm access to:

    - Application Performance Monitoring
    - Log Analytics
    - Monitoring
    - Events Service
    - Database Management
    - Ops Insights
    - Resource Analytics

5. Open **Connector Hub** and confirm that the OCTO log connectors are active. These connectors route OCI Logging records to Log Analytics.

6. Record any missing permission or resource. Resolve required gaps before Lab 4.

## Task 2: Connect the Log Analytics Kubernetes Monitoring Solution

1. In the OCI Console, open **Observability & Management**, **Log Analytics**, **Solutions**, and then **Kubernetes**.

2. Select **Connect clusters**. In the Add Data wizard, expand **Monitor Kubernetes** and select **Oracle OKE**.

3. Select the OCTO OKE cluster. Use the cluster name and OCID recorded in Task 1.

4. Select the compartment that will store the telemetry and monitoring resources.

5. Review the policies and dynamic groups proposed by the wizard. Let an administrator create them when your workshop user cannot manage tenancy-level policy.

6. Choose the deployment mode:

    - Use automatic deployment when the OKE API endpoint is public and your policies allow it.
    - Use manual deployment for a private OKE API endpoint. Follow the generated Helm or Kubernetes instructions from a host that can reach the cluster.

7. Keep metrics-server installation enabled unless the cluster already has a compatible metrics server.

8. Select **Configure log collection**. Wait until **Latest Telemetry** no longer shows **Unknown**.

9. Open the monitored cluster and inspect all four solution views:

    - **Cluster**: topology, namespace counts, CPU, memory, network, and Kubernetes events.
    - **Workload**: deployments and workload status.
    - **Node**: node health, capacity, and runtime details.
    - **Pod**: pod state, restarts, resource use, and failure events.

10. Filter to the `octo-drone-shop` and `enterprise-crm` namespaces.

11. In the Pod view, right-click an OCTO pod and select **View logs**. Confirm these enrichment fields:

    ```text
    Kubernetes Cluster Name
    Namespace
    Pod
    Container
    Container Image Name
    ```

12. Run the OCTO ingestion-health and trace-correlation searches when the deployment imported them:

    ```text
    oke-onm-ingestion-health
    oke-kubernetes-trace-correlation
    ```

13. Record the solution evidence.

    ```text
    Cluster:
    Latest telemetry time:
    Workload:
    Pod:
    Log source:
    Kubernetes event or issue:
    ```

## Task 3: Prepare the Log Analytics Security Monitoring Solution

1. In Log Analytics, open **Administration** and select **Add Data**.

2. Configure the VCN input:

    - Expand **Monitor OCI resources**.
    - Select **Virtual Cloud Network - Flowlogs**.
    - Select the OCTO VCN and the target Log Analytics compartment.
    - Confirm or create the Service Connector requested by the wizard.

3. Configure OCI Audit input:

    - Expand **Security and Compliance**.
    - Select **OCI Audit Logs**.
    - Select the compartment and Log Analytics log group.
    - Confirm or create the Service Connector.

4. Configure Compute security logs only when the OCTO environment includes Compute hosts:

    - Expand **Monitor with management agent**.
    - Configure the Management Agent and Logging Analytics plugin.
    - Select **Linux Core Logs**.

5. Return to **Solutions** and open **Security**.

6. Inspect the three Oracle-defined views:

    | View | Evidence to inspect |
    | --- | --- |
    | Virtual Cloud Network | denied connections, target ports, source IPs, traffic volume, and threat-IP context |
    | Compute | failed SSH or RDP logins, failed sudo commands, and access-control changes |
    | OCI Audit | failed logins, API methods, resource paths, users, and activity |

7. Generate a harmless control-plane Audit record from Cloud Shell or your deployment host.

    ```bash
    oci iam region list --all >/dev/null
    ```

8. Wait for ingestion, then use the OCI Audit view to locate activity from your user and time window.

9. Open one widget in Log Explorer and inspect its query. Save the query URL if the tenancy permits sharing.

10. Record the security baseline.

    ```text
    VCN view evidence:
    Compute view evidence or not applicable:
    OCI Audit view evidence:
    Source and time range:
    Query URL:
    ```

## Task 4: Verify APM, Monitoring, and Database Observability

1. Print the APM outputs from the existing OCTO Terraform state.

    ```bash
    COMPARTMENT_ID="${OCI_COMPARTMENT_ID}" \
      ./deploy/oci/ensure_apm.sh --print
    ```

2. In APM, open the OCTO domain and confirm that Trace Explorer is available.

3. Open **Saved Queries** and look for:

    ```text
    OCTO APM - DB slow spans
    checkout-end-to-end
    trace-drilldown
    ```

4. Verify the OCTO Monitoring resources. The script is idempotent and creates the topic, health check, and alarm definitions when they are absent.

    ```bash
    COMPARTMENT_ID="${OCI_COMPARTMENT_ID}" \
    SHOP_PUBLIC_URL="https://drones.${DNS_DOMAIN}" \
      ./deploy/oci/ensure_monitoring.sh
    ```

5. In Monitoring, confirm the `octo_apm_demo` namespace and these alarm definitions:

    ```text
    octo-shop-high-error-rate
    octo-shop-db-latency
    octo-shop-health-down
    octo-shop-crm-sync-stale
    octo-shop-low-stock
    ```

6. Enable Database Management and Ops Insights if the stack did not enable them.

    ```bash
    AUTONOMOUS_DATABASE_ID="${AUTONOMOUS_DATABASE_ID}" \
      ./deploy/oci/ensure_db_observability.sh
    ```

7. Open the OCTO Autonomous Database and confirm:

    - The database shows Database Management status **Enabled**.
    - The database shows Ops Insights status **Enabled**.
    - The database is visible as a managed target.

8. In **Database Management**, open **Performance Hub**. Confirm access to Top Activity, Top SQL, SQL Monitoring, and wait information available for this database.

9. In **Ops Insights**, open **Database Insights** and **DB Performance**. Confirm that the OCTO database appears in the selected time range.

10. Do not enable a paid management-pack feature outside the entitlement for your workshop tenancy. If a chart or SQL detail is unavailable, record the limitation and continue with the available Database Management and Ops Insights views.

## Task 5: Verify Events and Resource Analytics Readiness

1. Open **Events Service**, then **Rules**. Confirm that you can list rules in the OCTO compartment.

2. Open the Notifications topic used by `ensure_monitoring.sh`. Confirm that at least one subscription is in the **Confirmed** state.

3. Record whether your user can create an Events rule and select Notifications as its action. You will create or verify the rule in Lab 5.

4. Open **Resource Analytics** and select the instructor-provided instance.

5. Confirm that the monitored tenancy and region show successful data population.

6. Open the Resource Analytics Autonomous AI Database through Database Actions or another approved SQL client.

7. Confirm that the `OCIRA` schema is visible.

    ```sql
    SELECT COUNT(*) AS ocira_views
    FROM all_views
    WHERE owner = 'OCIRA';
    ```

8. Do not provision a new Resource Analytics instance during the lab unless the instructor approved the cost. Resource Analytics requires an Autonomous AI Database and can also use Oracle Analytics Cloud.

## Task 6: Record the Seven-Service Baseline

1. Complete the baseline before continuing.

    | Focused service | Required evidence |
    | --- | --- |
    | OCI Monitoring | `octo_apm_demo` metrics and OCTO alarm definitions |
    | OCI Log Analytics | Kubernetes and Security solution data |
    | OCI Events | rule access and confirmed Notifications destination |
    | OCI APM | OCTO domain, Trace Explorer, and saved queries |
    | OCI Database Management | managed OCTO database and Performance Hub |
    | OCI Ops Insights | OCTO database in DB Performance |
    | OCI Resource Analytics | populated instance and accessible `OCIRA` views |

2. Mark each item as **Ready**, **Blocked**, or **Not entitled**.

3. Resolve every **Blocked** item required by Labs 3 and 4.

## Learn More

- [OCTO APM Demo repository](https://github.com/adibirzu/octo-observability-demo)
- [OCTO Log Analytics assets](https://github.com/adibirzu/octo-observability-demo/tree/main/deploy/oci/log_analytics)
- [Log Analytics Kubernetes Monitoring Solution](https://docs.oracle.com/en-us/iaas/log-analytics/doc/kubernetes-solution.html)
- [Log Analytics Security Monitoring Solution](https://docs.oracle.com/en-us/iaas/log-analytics/doc/security-monitoring-solution.html)
- [OCI Application Performance Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Events](https://docs.oracle.com/en-us/iaas/Content/Events/)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)
- [OCI Ops Insights](https://docs.oracle.com/en-us/iaas/operations-insights/)
- [OCI Resource Analytics](https://docs.oracle.com/en-us/iaas/Content/resource-analytics/home.htm)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
