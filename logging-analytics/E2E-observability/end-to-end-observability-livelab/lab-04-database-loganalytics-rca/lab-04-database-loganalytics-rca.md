# Lab 4: Investigate Application and Database Incidents

## Introduction

In this lab, you run three investigations against OCTO APM Demo. You will connect an APM trace to its OKE pod, assess application security activity with the Log Analytics Security Monitoring Solution, and diagnose a database-bound N+1 query pattern with APM, Ops Insights, and Database Management.

Estimated Time: 100 minutes

### Objectives

In this lab, you will:

- Locate the OKE workload and pod that served an application request.
- Use Log Analytics Kubernetes views, events, metrics, and logs to assess pod health.
- Use the Security Monitoring Solution to add VCN, Compute, and OCI Audit context.
- Generate a controlled, read-only N+1 workload in OCTO.
- Identify repeated Oracle Database spans and SQL IDs in APM.
- Compare application evidence with Ops Insights and Database Management.
- Write one evidence-based root-cause summary.

## Task 1: Prepare the Investigation Window

1. Confirm that the seven-service baseline from Lab 2 remains ready.

2. Open the Drone Shop and generate one normal product request.

    ```bash
    curl -sS "https://drones.${DNS_DOMAIN}/api/products" | jq '.[0]'
    ```

3. Record a UTC start time for the investigations.

    ```bash
    date -u '+%Y-%m-%dT%H:%M:%SZ'
    ```

4. Set APM, Log Analytics, Monitoring, Ops Insights, and Database Management to the same time range.

5. Keep the trace ID and SQL ID captured in Lab 3 available.

## Task 2: Investigate the OKE Workload

1. In APM, open the Lab 3 checkout trace.

2. Select the root application span and copy these Kubernetes attributes when present:

    ```text
    k8s.cluster.name:
    k8s.namespace.name:
    k8s.pod.name:
    k8s.node.name:
    service.name:
    TraceId:
    ```

3. In Log Analytics, open **Solutions**, **Kubernetes**, and the OCTO cluster.

4. In the **Workload** view, filter to the namespace and application service from the APM span.

5. Confirm the workload status and inspect:

    - desired and available replicas
    - warning events
    - CPU and memory
    - network activity
    - pods grouped by workload

6. Open the **Pod** view and select the pod copied from APM.

7. Check pod status, restart count, node, container image, and recent Kubernetes events.

8. Select **View logs** for the pod. Search for the APM trace ID.

    ```text
    'Trace ID' = '<TRACE_ID>' or oracleApmTraceId = '<TRACE_ID>'
    ```

9. If the OCTO saved search exists, run it for the same trace.

    ```text
    oke-kubernetes-trace-correlation
    ```

10. Decide whether the pod evidence supports a runtime problem.

    ```text
    APM service and pod:
    Kubernetes workload status:
    Pod restarts or warnings:
    Resource pressure:
    Matching log record:
    Runtime problem found: Yes / No
    ```

## Task 3: Investigate Security Context

1. Send one harmless request that resembles an input-validation probe. Use only the workshop endpoint.

    ```bash
    curl -I "https://drones.${DNS_DOMAIN}/?q=%3Cscript%3Eworkshop-test%3C%2Fscript%3E"
    ```

2. Record the UTC time, response status, and any request identifier returned by the edge.

3. In Log Analytics, search OCTO WAF and application-security records for that time.

    ```text
    ('Log Source' contains 'WAF' or Message contains 'workshop-test')
    and (ClientRequestHost = 'drones.${DNS_DOMAIN}' or Message contains 'octo')
    ```

4. Open a matching row and record the WAF action, source IP, host, path, request ID, and trace ID when available.

5. Open **Solutions**, **Security**, and review the **Virtual Cloud Network** view for the same time range.

6. Inspect denied connections, target ports, source IPs, and threat-IP context. Determine whether the application request aligns with wider network activity.

7. Review the **Compute** view when the OCTO environment includes monitored Compute hosts. Check failed logins and privilege-escalation indicators.

8. Review the **OCI Audit** view. Check for unexpected API calls or resource changes around the incident.

9. Keep the evidence types separate:

    - OCTO WAF and application-security logs describe the application edge.
    - The Security Monitoring Solution adds VCN, host, and control-plane context.

10. Record the security conclusion.

    ```text
    Application-edge evidence:
    VCN evidence:
    Compute evidence or not applicable:
    OCI Audit evidence:
    Broader security incident found: Yes / No
    ```

## Task 4: Generate a Read-Only Database Workload

1. Confirm that this is a workshop deployment. Do not run the workload against a production endpoint.

2. Create a known trace ID for one N+1 request.

    ```bash
    DB_TRACEPARENT="00-$(openssl rand -hex 16)-$(openssl rand -hex 8)-01"
    DB_TRACE_ID="$(printf '%s' "${DB_TRACEPARENT}" | cut -d- -f2)"
    printf 'database trace id: %s\n' "${DB_TRACE_ID}"
    ```

3. Send one traced request to the OCTO N+1 demonstration endpoint.

    ```bash
    curl -sS \
      -H "traceparent: ${DB_TRACEPARENT}" \
      -H "X-Workflow-Id: livelab-db-bottleneck" \
      "https://drones.${DNS_DOMAIN}/api/dashboard/n-plus-one" \
      | jq '{pattern, orders, query_count}'
    ```

4. Generate a short read-only workload so the SQL pattern is visible in database activity. The endpoint performs one order query followed by one item query per order.

    ```bash
    for run in {1..12}; do
      curl -sS \
        -H "X-Workflow-Id: livelab-db-bottleneck" \
        "https://drones.${DNS_DOMAIN}/api/dashboard/n-plus-one" \
        >/dev/null
    done
    ```

5. Record the end time and the query count returned by the traced request.

    ```bash
    date -u '+%Y-%m-%dT%H:%M:%SZ'
    ```

6. The workload does not update application data. It creates repeated SELECT activity that exposes the N+1 access pattern.

## Task 5: Diagnose the Database-Bound Path in APM

1. Open APM Trace Explorer and search for the known database trace.

    ```text
    TraceId = '<DB_TRACE_ID>'
    ```

2. Open the trace and select the `dashboard.n_plus_one` span.

3. Count the database query spans beneath it. Compare the span count with `query_count` from Task 4.

4. Identify the repeated order-item query and copy:

    ```text
    OperationName:
    DbStatement:
    DbOracleSqlId:
    SpanDuration:
    Executions visible in trace:
    ```

5. Run the OCTO saved query when it is available.

    ```text
    OCTO APM - DB slow spans
    ```

6. If the saved query does not include short repeated spans, keep the exact-trace view. An N+1 problem can be expensive because of execution count even when each SQL call is individually fast.

7. Pivot to Log Analytics with the database trace ID.

    ```text
    'Trace ID' = '<DB_TRACE_ID>' or oracleApmTraceId = '<DB_TRACE_ID>'
    ```

8. Find the `N+1 query demo executed` log record and compare its query count with the trace.

9. State the application-level hypothesis:

    ```text
    One request loads the order list, then issues one item query per order.
    The repeated database round trips increase total request time and database work.
    ```

## Task 6: Confirm Database Impact

1. Open **Ops Insights**, **Database Insights**, and **DB Performance**.

2. Select the OCTO Autonomous Database and the Task 4 time range.

3. Review:

    - Top Activity and average active sessions
    - CPU insight
    - degrading SQL
    - high wait time
    - Top SQL by activity or elapsed time

4. Open SQL Insights or SQL Warehouse and filter by the Oracle SQL ID copied from APM.

5. Record whether the SQL pattern is new, recurrent, or too small to rise above the current database workload.

6. Open **Database Management**, select the OCTO managed database, and open **Performance Hub**.

7. Use Top Activity or Top SQL for the Task 4 window. Search for the same SQL ID.

8. Review the available execution evidence:

    ```text
    SQL ID:
    Executions:
    Elapsed time:
    CPU time:
    Buffer gets:
    Physical reads:
    Dominant wait class or event:
    Plan hash value:
    ```

9. Open the actual SQL detail or execution plan when available. Prefer runtime statistics over a standalone estimated plan.

10. Do not assume that a full table scan or high wait count is the root cause. Compare elapsed time, executions, waits, and actual rows before recommending a change.

11. Some historical, ASH, AWR, SQL Monitoring, or tuning views depend on database type, collection time, service entitlement, and management-pack access. Use only the capabilities enabled for the workshop tenancy.

12. Compare the services:

    | Service | Question answered |
    | --- | --- |
    | OCI APM | Which request and application operation generated the SQL calls? |
    | Log Analytics | What did the application report for that trace and workload? |
    | Ops Insights | Is the database or SQL trend new, degrading, or persistent? |
    | Database Management | What SQL, execution, wait, and plan evidence exists on the managed database? |

## Task 7: Verify Recovery and Write the RCA

1. The controlled workload ends when the loop completes. Wait two minutes.

2. Send one normal product request.

    ```bash
    curl -sS "https://drones.${DNS_DOMAIN}/api/products" >/dev/null
    ```

3. In APM, compare the normal request with the N+1 trace. Confirm that the normal route has fewer database spans.

4. Write the root-cause statement.

    ```text
    Symptom:
    Affected service and operation:
    APM trace and SQL evidence:
    OKE evidence:
    Security evidence:
    Ops Insights evidence:
    Database Management evidence:
    Root cause:
    Recommended application change:
    Recovery proof:
    ```

5. A suitable recommendation should address the query pattern, such as eager loading, batching, or one set-based query. Do not propose an index or database parameter change without plan and workload evidence.

6. Save links to the APM trace, Log Analytics query, Ops Insights page, and Database Management page.

## Learn More

- [OCTO slow SQL drill-down](https://github.com/adibirzu/octo-observability-demo/blob/main/site/workshop/lab-03-slow-sql-drill-down.md)
- [OCTO root-cause workflow](https://github.com/adibirzu/octo-observability-demo/blob/main/site/workshop/lab-17-root-cause-apm-logan.md)
- [OCTO N+1 endpoint implementation](https://github.com/adibirzu/octo-observability-demo/blob/main/shop/server/modules/dashboard.py)
- [OCI APM Trace Explorer](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/use-trace-explorer.html)
- [Log Analytics Kubernetes Monitoring Solution](https://docs.oracle.com/en-us/iaas/log-analytics/doc/kubernetes-solution.html)
- [Log Analytics Security Monitoring Solution](https://docs.oracle.com/en-us/iaas/log-analytics/doc/security-monitoring-solution.html)
- [Analyze database performance in Ops Insights](https://docs.oracle.com/en-us/iaas/operations-insights/doc/analyze-database-performance.html)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
