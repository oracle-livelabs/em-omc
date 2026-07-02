# Lab 5: Operationalize Monitoring, Events, and Resource Analytics

## Introduction

In this lab, you turn the investigation workflow into repeatable operations. You will validate an OCTO Monitoring alarm, route a Resource Manager job event through OCI Events and Notifications, and query Resource Analytics for the OCI resources that support the application.

Estimated Time: 65 minutes

### Objectives

In this lab, you will:

- Validate an application latency alarm and its Notifications destination.
- Create or inspect an OCI Events rule for OCTO Resource Manager jobs.
- Trigger a non-mutating Resource Manager Plan job.
- Verify Events rule matching and delivery metrics.
- Query Resource Analytics for APM, OKE, Database Management, and Ops Insights inventory.
- Separate live telemetry from resource inventory and configuration context.
- Complete the workshop evidence matrix.

## Task 1: Validate the OCI Monitoring Alarm

1. In **Monitoring**, open **Alarm Definitions** and select the OCTO compartment.

2. Open `octo-shop-db-latency`.

3. Confirm the alarm definition matches the OCTO deployment:

    ```text
    Namespace: octo_apm_demo
    Metric: app.db.latency_ms
    Statistic: percentile(0.95)
    Threshold: greater than 2000 ms
    Severity: WARNING
    Pending duration: 5 minutes
    Destination: octo-drone-shop-alarms
    ```

4. Review the metric chart and alarm history for the Lab 4 time window.

5. Record whether the N+1 workload changed this metric. A high execution count can create database work without breaching a per-call latency threshold.

6. Verify the other OCTO alarm definitions.

    ```text
    octo-shop-high-error-rate
    octo-shop-health-down
    octo-shop-crm-sync-stale
    octo-shop-low-stock
    ```

7. Open the destination topic in **Notifications**. Confirm that at least one subscriber has confirmed the subscription.

8. Record the alarm evidence.

    ```text
    Alarm OCID:
    Query:
    Current state:
    Last transition:
    Destination topic:
    Confirmed subscription:
    ```

## Task 2: Create an OCI Events Rule

1. Open **Observability & Management**, **Events Service**, and **Rules**.

2. Select **Create Rule**.

3. Enter:

    ```text
    Display name: octo-resource-manager-job-end
    Description: Notify the workshop topic when an OCTO Resource Manager job completes.
    Compartment: <OCTO compartment>
    ```

4. Under **Rule Conditions**, select **Event Type**.

5. Select:

    ```text
    Service Name: Resource Manager
    Event Type: Create Job End
    ```

6. Add a compartment or resource filter that limits the rule to the OCTO environment when the Console offers the field.

7. Under **Actions**, select **Notifications** and choose `octo-drone-shop-alarms`.

8. Create the rule.

9. If your workshop role cannot create rules, open the instructor-provided rule and verify the same condition and action.

10. Record the rule OCID, event type, action type, and destination.

11. OCI Events rules deliver only to Notifications, Streaming, or Functions. Monitoring alarms are separate resources even when they use the same Notifications topic.

## Task 3: Trigger and Verify the Event

1. Open **Developer Services**, **Resource Manager**, **Stacks**, and the OCTO stack.

2. Select **Plan**. A Plan job evaluates Terraform without applying infrastructure changes.

3. Wait for the job to reach a terminal state.

4. Confirm that the Notifications subscriber receives a Resource Manager event message.

5. Return to the Events rule and open its **Metrics** tab.

6. Set the time range to include the Plan job and inspect:

    | Metric | Expected use |
    | --- | --- |
    | `PublishedEvents` | Resource events emitted in the compartment |
    | `MatchedEvents` | events that matched this rule |
    | `DeliverySucceedEvents` | successful deliveries to the action |
    | `DeliveryFailedEvents` | failed action deliveries |

7. Confirm that `MatchedEvents` and `DeliverySucceedEvents` increased for the rule.

8. If the workshop does not use Resource Manager, choose an event producer that the instructor approves. An Autonomous Database automatic-backup completion event provides one supported alternative.

9. Record the event evidence.

    ```text
    Resource Manager job OCID:
    Job state:
    Event type:
    Matched events:
    Successful deliveries:
    Failed deliveries:
    Notification received:
    ```

## Task 4: Query OCI Resource Analytics

1. Open the Resource Analytics Autonomous AI Database through Database Actions or your approved SQL client.

2. Discover the available views for the workshop services. This guards against data-model changes between Resource Analytics releases.

    ```sql
    SELECT view_name
    FROM all_views
    WHERE owner = 'OCIRA'
      AND (
        view_name LIKE 'APPLICATION_PERFORMANCE_MONITORING%'
        OR view_name LIKE 'CONTAINER_ENGINE%'
        OR view_name LIKE 'DATABASE_MANAGEMENT%'
        OR view_name LIKE 'OPS_INSIGHTS%'
        OR view_name LIKE 'EVENTS%'
      )
    ORDER BY view_name;
    ```

3. Find the OCTO APM domain.

    ```sql
    SELECT apm_domain_id,
           display_name,
           is_free_tier
    FROM ocira.application_performance_monitoring_domain_fact_v
    WHERE UPPER(display_name) LIKE '%OCTO%';
    ```

4. Review OKE lifecycle state and node count.

    ```sql
    SELECT cluster_id,
           lifecycle_state,
           node_count
    FROM ocira.container_engine_cluster_fact_v;
    ```

5. Review active Ops Insights resources and their latest inventory metrics.

    ```sql
    SELECT rsf.resource_id,
           rsf.resource_type,
           rsf.latest_cpu_used,
           rsf.latest_storage_used_gb,
           rsf.awr_import_lag_hours,
           rd.lifecycle_state,
           rd.resource_name
    FROM ocira.ops_insights_resource_state_fact_v rsf
    JOIN ocira.ops_insights_resource_dim_v rd
      ON rsf.ocira_resource_key = rd.ocira_resource_key
    WHERE rd.lifecycle_state = 'ACTIVE'
    ORDER BY rd.resource_name;
    ```

6. Confirm that Resource Analytics has Database Management inventory.

    ```sql
    SELECT COUNT(*) AS managed_database_count
    FROM ocira.database_management_managed_database_dim_v;
    ```

7. From the discovery query, note the Events views available in this Resource Analytics release. Do not invent a fixed Events view name when the schema does not expose one.

8. Record the inventory evidence.

    ```text
    OCTO APM domain:
    OKE cluster ID, state, and node count:
    Active Ops Insights resource:
    Managed database count:
    Events views discovered:
    Resource Analytics data timestamp:
    ```

## Task 5: Map Resource Relationships

1. Open the Resource Analytics OAC dashboards when the instance includes Oracle Analytics Cloud.

2. Review the OKE and APM subject areas. Filter to the OCTO compartment and region.

3. If the instance includes Graph Studio, inspect the OKE graph or a resource relationship notebook.

4. Build the OCTO relationship map from your query results:

    | Resource | Relationship to the application |
    | --- | --- |
    | APM domain | stores application traces and spans |
    | OKE cluster | runs the Drone Shop, CRM, Java, and support workloads |
    | Autonomous Database | stores the shared OCTO business data |
    | Database Management target | provides database performance and SQL detail |
    | Ops Insights resource | provides historical database and SQL trends |
    | Events rule | responds to OCI resource state changes |
    | Notifications topic | delivers alarm and event messages |

5. State the boundary clearly:

    - APM, Log Analytics, and Monitoring hold live operational telemetry.
    - Database Management and Ops Insights diagnose current and historical database behavior.
    - Events reacts to OCI resource state changes.
    - Resource Analytics holds near-real-time resource inventory, relationships, and configuration metadata.

## Task 6: Complete the Workshop Evidence Matrix

1. Complete one row for every focused service.

    | Service | Evidence captured | Join key or resource ID |
    | --- | --- | --- |
    | OCI Monitoring | alarm definition and history | alarm OCID, metric dimensions |
    | OCI Log Analytics | Kubernetes, Security, and trace-correlated records | trace ID, pod, source IP, request ID |
    | OCI Events | matched Resource Manager event and delivery metrics | rule OCID, job OCID, event type |
    | OCI APM | distributed trace and database spans | trace ID, span ID, SQL ID |
    | OCI Database Management | SQL, wait, and plan evidence | managed database OCID, SQL ID |
    | OCI Ops Insights | database and SQL trend | Ops Insights resource, SQL ID |
    | OCI Resource Analytics | inventory and relationship queries | OCI resource OCIDs |

2. Write the final operational statement.

    ```text
    Detection:
    Application scope:
    Runtime evidence:
    Security context:
    Database diagnosis:
    Automated notification:
    Resource relationship context:
    Recommended owner and next action:
    ```

3. Disable or delete `octo-resource-manager-job-end` if you created it only for this workshop. Keep it only when the tenancy owner approves ongoing notifications.

4. Keep the OCTO Monitoring alarms and Resource Analytics instance unchanged unless the instructor directs otherwise.

## Learn More

- [OCTO Monitoring bootstrap](https://github.com/adibirzu/octo-observability-demo/blob/main/deploy/oci/ensure_monitoring.sh)
- [OCTO correlation contract](https://github.com/adibirzu/octo-observability-demo/blob/main/site/architecture/correlation-contract.md)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Events overview](https://docs.oracle.com/en-us/iaas/Content/Events/Concepts/eventsoverview.htm)
- [OCI Events metrics](https://docs.oracle.com/en-us/iaas/Content/Events/Reference/eventsmetrics.htm)
- [Resource Manager event types](https://docs.oracle.com/en-us/iaas/Content/Events/Reference/eventsproducers.htm)
- [OCI Resource Analytics](https://docs.oracle.com/en-us/iaas/Content/resource-analytics/home.htm)
- [Resource Analytics data model reference](https://docs.oracle.com/en-us/iaas/Content/resource-analytics/reference-resources.htm)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
