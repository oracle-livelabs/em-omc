# Lab 3: Trace a Customer Transaction End to End

## Introduction

In this lab, you create a trace with a known W3C trace ID, inspect it in OCI APM, and find the matching application logs. You will then follow a browser checkout across the Drone Shop, Java payment sidecar, and Oracle Database.

Estimated Time: 65 minutes

### Objectives

In this lab, you will:

- Inject a valid W3C `traceparent` header into an OCTO request.
- Find the exact trace in OCI APM Trace Explorer.
- Read service, Kubernetes, HTTP, Java, and database span attributes.
- Observe a customer checkout across multiple services.
- Pivot from APM to Log Analytics with `oracleApmTraceId`.
- Validate the OCTO correlation contract.

## Task 1: Generate a Request with a Known Trace ID

1. From the OCTO repository root, create a W3C trace header.

    ```bash
    TRACEPARENT="00-$(openssl rand -hex 16)-$(openssl rand -hex 8)-01"
    TRACE_ID="$(printf '%s' "${TRACEPARENT}" | cut -d- -f2)"
    printf 'traceparent=%s\ntrace_id=%s\n' "${TRACEPARENT}" "${TRACE_ID}"
    ```

2. Send the trace header to the Drone Shop.

    ```bash
    curl -sS \
      -H "traceparent: ${TRACEPARENT}" \
      -H "X-Workflow-Id: livelab-tracing" \
      "https://drones.${DNS_DOMAIN}/api/products" | jq '.[0]'
    ```

3. Confirm that the response contains a product and that `TRACE_ID` contains 32 hexadecimal characters.

4. Record the request time, trace ID, route, and response status.

    ```text
    Request time:
    Trace ID:
    Route: GET /api/products
    Status:
    ```

## Task 2: Inspect the Trace in OCI APM

1. Open **Observability & Management**, **Application Performance Monitoring**, and **Trace Explorer**.

2. Select the OCTO APM domain.

3. Search for the trace ID.

    ```text
    TraceId = '<TRACE_ID>'
    ```

4. Allow one to two minutes for first-time ingestion, then run the query again if needed.

5. Open the matched trace and inspect the flame chart.

6. Identify the root FastAPI span and its database children.

7. Record the root-span evidence:

    ```text
    ServiceName:
    OperationName:
    TraceDuration:
    StatusCode:
    service.namespace:
    k8s.namespace.name:
    k8s.pod.name:
    ```

8. Select a database child span and record the attributes that exist in your deployment:

    ```text
    db.system:
    db.statement or DbStatement:
    db.oracle.sql_id or DbOracleSqlId:
    db.target:
    SpanDuration:
    ```

9. Confirm that the trace shows where time was spent. A wide span contributes more wall-clock time than a narrow sibling.

## Task 3: Trace a Browser Checkout

1. Open the Drone Shop.

    ```text
    https://drones.${DNS_DOMAIN}
    ```

2. Sign in with the workshop account, open a product, add it to the cart, and complete a simulated checkout.

3. Record the checkout time, order identifier, and browser session details shown by the application.

4. In APM, open the OCTO saved query for the checkout flow when it is available.

    ```text
    checkout-end-to-end
    ```

5. Otherwise, search recent traces for the OKE service and checkout operation.

    ```text
    ServiceName = 'octo-drone-shop-oke' and OperationName = 'shop.checkout'
    ```

6. Open the checkout trace and find the stages available in your deployment:

    - browser or incoming HTTP request
    - `octo-drone-shop-oke` checkout logic
    - `octo-java-app-server-oke` payment verification or authorization
    - Enterprise CRM synchronization
    - Oracle Database spans for cart, order, payment, or invoice work

7. Select the Java payment span. Confirm the Java agent contributed it without changing the Python application instrumentation.

8. Select a database span and copy its Oracle SQL ID when present.

9. Record the checkout evidence.

    ```text
    Checkout trace ID:
    Root service:
    Java service:
    Database target:
    SQL ID:
    Slowest span:
    ```

## Task 4: Validate the Correlation Contract

1. Compare the trace and span attributes with the OCTO correlation contract.

2. Confirm the primary identity fields:

    | Field | Purpose |
    | --- | --- |
    | `trace_id` | W3C trace identifier shared across the request |
    | `span_id` | identifier for one operation |
    | `oracleApmTraceId` | log field that matches the APM trace ID |
    | `oracleApmSpanId` | log field that matches an APM span |
    | `request_id` | application request identifier |
    | `workflow_id` | business-flow identifier |
    | `DbOracleSqlId` | bridge from an APM database span to Oracle SQL diagnostics |

3. Confirm the service identity:

    ```text
    service.namespace = octo
    deployment.environment = production
    app.runtime = oke
    ```

4. Confirm that Kubernetes resource attributes identify the pod that served the request.

5. Keep the checkout trace ID and SQL ID for Lab 4.

## Task 5: Pivot from APM to Log Analytics

1. Copy the known trace ID from Task 1.

2. Open **Log Analytics** and set the same time range as APM.

3. Search the direct OKE application source.

    ```text
    'Log Source' = 'SOC Application Logs' and 'Trace ID' = '<TRACE_ID>'
    ```

4. If the application record arrived through OCI Logging and Connector Hub, use the unified source instead.

    ```text
    'Log Source' = 'OCI Unified Schema Logs' and oracleApmTraceId = '<TRACE_ID>'
    ```

5. Open a matching record and compare:

    - timestamp
    - service name
    - route or operation
    - log level
    - `oracleApmTraceId`
    - `oracleApmSpanId`
    - `workflow_id`
    - pod name

6. Use the configured drilldown to return to APM, or paste the trace ID into Trace Explorer.

7. Repeat the search with the checkout trace ID when checkout logs are available.

8. Save one APM trace URL and one Log Analytics query URL.

## Task 6: Verify the Tracing Use Case

1. Run the OCTO verifiers for the known trace when your environment provides the required OCI CLI variables.

    ```bash
    ./tools/workshop/verify-01.sh "${TRACE_ID}"
    ./tools/workshop/verify-02.sh "${TRACE_ID}"
    ```

2. Confirm the use-case result.

    ```text
    APM trace found:
    Database span found:
    Correlated Log Analytics rows:
    APM-to-log round trip:
    Checkout crossed Python, Java, and Oracle Database:
    ```

3. Explain which instrumentation path produced each signal:

    - OpenTelemetry SDK and auto-instrumentation for Python services.
    - OCI APM Java agent or Java OpenTelemetry instrumentation for the payment sidecar.
    - Native OCI services, Connector Hub, and Log Analytics collection for logs.

## Learn More

- [OCTO first-trace lab](https://github.com/adibirzu/octo-observability-demo/blob/main/site/workshop/lab-01-first-trace.md)
- [OCTO trace-to-log lab](https://github.com/adibirzu/octo-observability-demo/blob/main/site/workshop/lab-02-trace-log-correlation.md)
- [OCTO correlation contract](https://github.com/adibirzu/octo-observability-demo/blob/main/site/architecture/correlation-contract.md)
- [OCI APM Trace Explorer](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/use-trace-explorer.html)
- [Trace and span attributes](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/trace-and-span-attributes.html)
- [W3C Trace Context](https://www.w3.org/TR/trace-context/)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
