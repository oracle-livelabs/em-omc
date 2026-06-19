# Lab 4: Investigate Application, Log, and Database Signals

## Introduction

In this lab, you investigate a slow or failed application path by combining APM traces, Log Analytics application rows, Log Analytics security monitoring rows, Monitoring charts, WAF evidence, Operations Insights, and Database Management.

Estimated Time: 75 minutes

### Objectives

In this lab, you will:

- Trigger or select an application symptom.
- Build an evidence chain from APM to Log Analytics.
- Add Log Analytics security monitoring evidence when the symptom touches WAF, OWASP, or suspicious requests.
- Use SQL identifiers to continue the investigation in Operations Insights and Database Management.
- Validate database persistence evidence, including orders, audit logs, and invoice BLOB spans.
- Classify whether the issue is application, edge, database, infrastructure, or expected business behavior.
- Use OCI documentation concepts to separate trace, log, metric, SQL, security, and alarm evidence.

## Task 1: Select a Symptom to Investigate

1. Open the control-plane stress page if it is available.

    ```text
    https://cp.octodemo.cloud/stress-test
    ```

2. Generate a short, controlled application load or select a recent slow checkout, failed checkout, paid order, payment decline, invoice generation, or CRM synchronization event.

3. Record the symptom details:

    - affected URL or route
    - approximate timestamp
    - user-visible error or latency
    - order or customer identifier when available
    - payment result when available
    - service name

4. Keep the test short. The goal is observability validation, not load testing.

## Task 2: Build the APM Evidence

1. Open the APM Trace Explorer for the same time range.

2. Filter for traces with high duration, error status, or the affected service.

3. Open the strongest candidate trace.

4. Identify the span where latency or failure first appears.

5. Record these fields from the span:

    - service name
    - operation name
    - duration
    - status code or error type
    - trace ID
    - span ID
    - SQL ID when present
    - payment or fraud decision when present

6. If the span shows a declined payment with no fault, classify it as a business outcome before treating it as an incident.

7. Decide whether the trace points first to application code, a downstream service, WAF or edge routing, database activity, or an external dependency.

8. Create the first RCA hypothesis.

    ```text
    Hypothesis:
    Supporting span:
    Missing evidence:
    Next service to inspect:
    ```

## Task 3: Add Log Analytics Application and Security Monitoring Evidence

1. Open Log Analytics for the same time range.

2. Search by the trace ID or `oracleApmTraceId`.

    ```text
    oracleApmTraceId = '<trace-id>'
    ```

3. Expand the matching rows and compare the log timestamps to the APM waterfall.

4. Search for warnings and errors for the affected services.

    ```text
    ('Log Source' in ('OCTO Drone Shop', 'Enterprise CRM Portal')) and (Severity in ('ERROR', 'WARN') or Message contains 'error')
    ```

5. Search WAF or edge logs when the trace suggests request validation, status code changes, or blocked traffic.

    ```text
    'Log Source' contains 'WAF' and ClientRequestHost in ('shop.octodemo.cloud', 'crm.octodemo.cloud')
    ```

6. Search security monitoring records when the symptom looks suspicious or policy-driven.

    ```text
    Message contains 'OWASP' or Message contains 'MITRE' or Message contains 'x-oci-waf' or Message contains 'blocked'
    ```

7. Open a related Log Analytics dashboard or saved search for security monitoring. Confirm whether a detection, WAF event, or security row exists for the same time window.

8. Record whether the logs support, contradict, or narrow the APM hypothesis.

9. Record the security monitoring result separately.

    ```text
    Security source:
    Detection or dashboard:
    WAF action or score:
    Related trace ID:
    Interpretation:
    ```

10. Confirm the log-routing path for the related records.

    ```text
    OCI Logging log group:
    Service Connector Hub connector:
    Log Analytics source:
    Parser:
    Saved search or dashboard:
    ```

## Task 4: Investigate Database Impact and Invoice Persistence

1. If the APM trace includes a SQL ID, copy it.

2. Open **Operations Insights** for the Autonomous Database.

3. Use the SQL ID or time range to inspect SQL activity, CPU, waits, and execution trend.

4. Open **Database Management** for the same database.

5. Review sessions, waits, SQL activity, and active performance data around the symptom timestamp.

6. If no SQL ID appears in the trace, use the application timestamp and database service name to search by time range instead.

7. Decide whether the database evidence indicates:

    - a slow SQL statement
    - a blocking or waiting session
    - resource pressure
    - no database contribution

8. Confirm that the main application tables carry correlation evidence when your environment exposes them.

    | Table | Evidence to check |
    | --- | --- |
    | `products` | catalog item details such as SKU, category, price, and stock. |
    | `orders` | `payment_status`, `payment_gateway_request_id`, idempotency key, and `correlation_id`. |
    | `order_items` | line items for the order. |
    | `customers`, `support_tickets`, `campaigns`, `leads`, `shipments` | CRM-side records tied to the user or order. |
    | `audit_logs` | `trace_id` for privileged or security-relevant activity. |
    | `invoices` | PDF metadata and BLOB storage when the order reaches paid status. |

9. If the order generated an invoice, search the APM trace for the invoice persistence span.

    ```text
    db.write.invoice_pdf
    ```

10. Confirm that the invoice path proves user-to-database coverage:

    - a browser or API action caused the order state change.
    - CRM generated a PDF with application code.
    - Oracle ATP stored the PDF bytes in the `invoices.pdf_data` SecureFile BLOB column.
    - the BLOB write appears on the same trace or same correlated investigation timeline.

11. If your environment has historical invoice backlog handling enabled, verify that the scheduled job or manual reconcile endpoint also emits trace or log evidence.

    ```text
    invoice reconcile
    invoice backlog
    db.write.invoice_pdf
    ```

12. Record the database service conclusion.

    ```text
    SQL ID:
    Operations Insights trend:
    Database Management session or wait:
    Stack Monitoring status:
    Invoice evidence:
    ```

## Task 5: Add Metrics, Alarms, and Notification Context

1. Open **Monitoring** for the same compartment and time range.

2. Query metrics that match the symptom. Start with these categories:

    - OKE node or pod CPU and memory.
    - load balancer response time and backend health.
    - database CPU, storage, sessions, or waits.
    - application custom metrics such as payment success rate or login failures.
    - GenAI or agent metrics if the symptom involves Lab 5 activity.

3. Record the metric namespace, metric name, dimensions, statistic, interval, and time range.

4. Check whether an alarm fired during the symptom.

5. If an alarm exists, record:

    ```text
    Alarm name:
    Metric namespace:
    MQL expression:
    Severity:
    Destination topic:
    Current state:
    ```

6. If no alarm exists, draft the alarm that would have detected the symptom. Do not create it unless your instructor asks you to.

## Task 6: Write the RCA Summary

1. Write a short RCA summary with the evidence you collected.

    ```text
    Symptom:
    Time range:
    Affected service or route:
    APM evidence:
    Log Analytics evidence:
    WAF or edge evidence:
    Database evidence:
    Invoice or BLOB evidence:
    Metric and alarm evidence:
    Most likely cause:
    Next action:
    ```

2. Include links to the APM trace, Log Analytics query, Operations Insights page, and Database Management page when your tenancy allows shareable URLs.

3. Classify the issue as one of these categories:

    - application defect
    - database performance
    - edge or WAF behavior
    - infrastructure or Kubernetes capacity
    - expected business decline
    - inconclusive

4. Review the summary with your instructor or team before moving to the agent monitoring lab.

## Learn More

- [OCI Application Performance Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/)
- [OCI Logging](https://docs.oracle.com/en-us/iaas/Content/Logging/home.htm)
- [OCI Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Service Connector Hub](https://docs.oracle.com/en-us/iaas/Content/connector-hub/home.htm)
- [OCI Web Application Firewall](https://docs.oracle.com/en-us/iaas/Content/WAF/Concepts/overview.htm)
- [OCI Operations Insights](https://docs.oracle.com/en-us/iaas/operations-insights/)
- [OCI Database Management](https://docs.oracle.com/en-us/iaas/database-management/)
- [OCI Stack Monitoring](https://docs.oracle.com/en-us/iaas/stack-monitoring/)
- [OCI Notifications](https://docs.oracle.com/en-us/iaas/Content/Notification/home.htm)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
