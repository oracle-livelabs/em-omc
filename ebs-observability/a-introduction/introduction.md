# Introduction

## About this Workshop

This workshop consists of 6 lab exercises organized to familiarize you with Oracle E-Business Suite (EBS) observability on Oracle Cloud Infrastructure (OCI). The covered OCI observability services include Stack Monitoring, Application Performance Monitoring (APM), Database Management, Log Analytics, and Ops Insights. We have a demo EBS environment, so you don't need to set up or use one from your cloud account. The lab exercises are designed to be independent of one another, allowing you to pick the exercises that interest you the most.

Estimated Time: 60 minutes

### Objectives

* Use OCI Stack Monitoring to monitor the health of EBS stack components such as Concurrent Processing, WebLogic, EBS Forms, OA-Core, and more.
* Use OCI Application Performance Monitoring (APM) to monitor application transactions, gain insights into the user experience, and proactively monitor EBS service availability.
* Use OCI Database Management to monitor the performance of databases and SQLs in an EBS environment.
* Use OCI Log Analytics to analyze EBS and WebLogic logs, such as Concurrent Manager logs, WebLogic Server logs, and more.
* Use OCI Ops Insights for host and database Capacity Planning, as well as Database Insights.


## Task 1: Oracle E-Business Suite (EBS)

Oracle E-Business Suite (EBS) is a comprehensive suite of integrated business applications that helps organizations manage core business processes such as finance, supply chain, human resources, and customer relationship management. It offers extensive functionality with deep industry-specific capabilities and can be deployed on-premises or in Oracle Cloud Infrastructure (OCI). EBS is known for its flexibility, scalability, and strong support for global operations.

## Task 2: Observability and Management Services

Oracle Cloud **Observability and Management Platform** provides full-stack visibility, prebuilt analytics, and automation to monitor, analyze, and manage multicloud applications and infrastructure environments.

* Stack Monitoring
    Stack Monitoring provides a single-pane view into the full EBS stack. This includes Concurrent Managers, WebLogic Servers, Oracle DBs, and host infrastructure. After discovering the stack components, Stack Monitoring collects performance metrics, any user-defined custom metrics, and provides alarms via Monitoring Templates. It can also highlight anomalies with ML‑powered baseline, and offers topology-aware maintenance windows during patch cycles.

    *For more information on Stack Monitoring, please refer to the Stack Monitoring Documentation > **[Stack Monitoring Documentation](https://docs.oracle.com/en-us/iaas/stack-monitoring/home.htm)***

* Application Performance Monitoring (APM)
    APM Enables deep tracing of HTML, server, and Forms‑based EBS transactions by inserting Java agents into WebLogic and Browser agents into HTML pages. The agents capture end‑user experience, servlet spans, SQL calls, and EBS‑specific dimensions (e.g., function name, class package). APM also provides service availability monitoring via synthetic tests on the browser, REST calls, SQL, networking, and more.

    *For more information on APM, please refer to the APM Documentation > **[APM Documentation](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/home.htm)***

* Database Management

    Database management provides a unified console for managing both cloud and on-premises databases. It includes lifecycle database management capabilities for monitoring, performance tuning, and administration. With Performance Hub, developers can optimize SQL code during active development and continuously monitor and tune queries in production.

    *For more information on Database Management, please refer to the Database Management documentation > **[Database Management Documentation](https://docs.oracle.com/en-us/iaas/database-management/home.htm)***

* Log Analytics

    Log Analytics is a cloud solution that lets you index, enrich, aggregate, explore, search, analyze, correlate, visualize, and monitor log data from applications and system infrastructure-both in the cloud and on-premises. It can extract valuable information from EBS, WebLogic, host, and OCI logs. Log Analytics empowers users to correlate log data with events in the EBS stack, enhancing troubleshooting and root-cause analysis.

    *For more information on Log Analytics, please refer to the Log Analytics documentation > **[Log Analytics Documentation](https://docs.oracle.com/en-us/iaas/log-analytics/home.htm)***

* Ops Insights

    OCI Ops Insights (OPSI) is a cloud-native solution that gathers and analyzes telemetry data to help enterprises plan for growth. It enables data-driven capacity planning and performance management, reducing capital expenditures and improving application throughput. It supports ML-based resource usage trending, capacity planning, and SQL-based performance analysis, all within an intuitive dashboard.

    *For more information on Ops Insights, please refer to the Ops Insights Documentation > **[Ops Insights Documentation](https://docs.oracle.com/en-us/iaas/operations-insights/home.htm)***

## Acknowledgements

* **Author** - Zyaad Khader, Principal Member of Technical Staff
* **Contributors** - Zyaad Khader
* **Last Updated By/Date** - Zyaad Khader, July 2025
