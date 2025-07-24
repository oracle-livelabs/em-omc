# Application Performance Insights

## Introduction

In this lab, you will explore OCI Application Performance Monitoring (APM) for an Oracle E-Business Suite (EBS) environment. APM provides end-to-end tracing of EBS transactions, user experience, and EBS Forms, revealing performance bottlenecks and errors. It can also proactively test components of an EBS environment. 

Estimated time: 10 minutes

### Objectives

* View transactions for EBS services, user sessions, and SQL calls
* Visualize the end-user experience
* Monitor availability of EBS services and user flows

## Task 1: Viewing EBS Application Transactions

1. Click on the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Trace Explorer** (under the Application Performance Monitoring section). 

      ![Selecting APM Trace Explorer](./images/setup/apm-nav.png " ")

2. The **root** compartment is selected by default in the Compartment field. Set the compartment to **EBS Demo** (emdemo -> eStore -> EBS_Demo).

      ![Compartment Navigation](./images/setup/apm-compartment-selection.png " ")

3. APM displays a table of all the application transactions (called traces) that it has collected from EBS. 

      ![Selecting a Trace](./images/trace-explorer/trace-explorer.png " ")

4. Click on the three dots to the right of a row item to view the details for that trace, then click **Show trace details**. In this case, we chose an **Error** trace. If you don't see Error traces, you can proceed with any trace in the table.

      ![Selecting a Trace](./images/trace-explorer/trace-details-nav.png " ")

5. The Trace Details page provides a topology view of the calls made in that trace. Hover over the topology items and arrows to view metrics regarding services used and call duration.

      ![Trace Details 1](./images/trace-explorer/trace-details.png " ")

6. Below the topology view, is a waterfall view of all the calls made within the trace (called spans). Scroll through the spans until you find the one which errored. Error spans have a red exclamation icon which identifies them. Click on the hyperlink for the erroring span.

      ![Trace Details 2](./images/trace-explorer/trace-details-2.png " ")

7. This opens the Span Details page, highlighting important attributes for that specific span. Scroll down the table until you see the **ErrorMessage** attribute, which shows more details about that error. 

      ![Span Details](./images/trace-explorer/span-details.png " ")

8. Close the Span Details and Trace Details by clicking **Close** on the bottom-left. The Trace Explorer has multiple out-of-box queries that you can view at the top of the Trace Explorer. Click on the **Operations** query to see a view of traces grouped by the the operation performed in the EBS environment. Click on the count hyperlink to view all the spans for that specific operation.

      ![Operations View](./images/trace-explorer/span-details.png " ")
      ![Spans for a Specific Operation](./images/trace-explorer/operation-spans.png " ")

## Task 2: Understanding the End-User Experience

1. To view user session traces, click on the **User Sessions** query at the top of Trace Explorer. This will give a breakdown of traces, grouped by session.

      ![Sessions View](./images/real-user-monitoring/sessions.png " ")

2. To view a specific user session, click on **Traces** count hyperlink for any of the sessions row items. 

      ![Specific Session View](./images/real-user-monitoring/specific-session.png " ")

3. Navigate to the Real User Monitoring dashboard by clicking the navigation dropdown on the top-left of the screen, then select **Real User Monitoring**. 

      ![Real User Monitoring Navigation](./images/real-user-monitoring/rum-dashboard-nav.png " ")

4. This will display a dashboard of useful user session information. You can click on any of the hyperlinks in the widget to view relevant information in Trace Explorer. 

      ![Real User Monitoring Dashboard](./images/real-user-monitoring/rum-dashboard.png " ")


## Taks 3: Service Availability Monitoring

1. On the left pane, click on **Availability Monitoring** to navigate to the dashboard of synthetic tests (called monitors) in this EBS environment. 

      ![Availability Monitoring](./images/availability-monitoring/availability-monitoring-dashboard.png " ")

2. To view a specific monitor, click on the hyperlink in the Availability table. In this case, we will explore the **EBS-Login** monitor. 

      ![Availability Monitoring](./images/availability-monitoring/availability-monitor-nav.png " ")

3. The Monitor Details page provides an overview of the monitor setup along with a history of the test exetions that it ran. For each of the monitor executions in the history table, you can view important details such:

      * Traces for that specific execution
      * HTTP Archive (HAR) breakdown
      * Screenshots taken during the test
      * Network data

      ![Availability Monitor Details](./images/availability-monitoring/availability-monitor-details.png " ")

4. Click on **View Trace Details** to view the traces for the monitor execution.

      ![Monitor Traces Navigation](./images/availability-monitoring/traces-nav.png " ")
      ![Monitor Traces](./images/availability-monitoring/traces.png " ")

5. Click on **View HAR** to open the HTTP Archive viewer for the monitor execution.

      ![Monitor HAR Navigation](./images/availability-monitoring/har-nav.png " ")
      ![Monitor HAR](./images/availability-monitoring/har-viewer.png " ")

6. Click on **View Screenshots** to view the captured screenshots for the monitor execution.

      ![Monitor Screenshots Navigation](./images/availability-monitoring/screenshots-nav.png " ")
      ![Monitor Screenshots](./images/availability-monitoring/screenshots.png " ")

7. Click on **View Network Data** to view the network details for the monitor execution.

      ![Monitor Network Details Navigation](./images/availability-monitoring/network-nav.png " ")
      ![Monitor Network Details](./images/availability-monitoring/network-data.png " ")

8. To view metrics for the monitor, click on **Metrics** in the left pane.

      ![Monitor Metrics Navigation](./images/availability-monitoring/metrics-nav.png " ")

9. The metrics view provides important information such as availability, execution failures, latency, and more. Users are able to create alarms for those metrics to recieve proactive alerts and implement remediation steps.

      ![Monitor Metrics](./images/availability-monitoring/metrics.png " ")


## Acknowledgements

* **Author** - Zyaad Khader, Principal Member of Technical Staff
* **Contributors** - Zyaad Khader
* **Last Updated By/Date** - Zyaad Khader, July 2025