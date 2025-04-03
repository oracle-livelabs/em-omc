# Introduction

## About this Workshop

This workshop consists of four lab exercises organized to familiarize you with key capabilities of Oracle Cloud services, including Database Management, Ops Insights, Logging Analytics and Application Performance Management. We have simulated an External MySQL DB system, so you don't need to set up or use one from your cloud account.

Estimated Time: 1 hour 20 minutes

### Objectives

* Use Oracle Cloud Infrastructure (OCI) Database Management to monitor the External MySQL DB systems
* Use Ops Insights for capacity planning and Database Insights
* Use Logging Analytics to collect and analyze database logs, such as the General Query log, Audit log, and others
* Use APM Trace Explorer to view traces, spans, and span dimensions

## Task 1: Observability and Management Services

Oracle Cloud **Observability and Management Platform** provides full-stack visibility, prebuilt analytics, and automation to monitor, analyze, and manage multicloud applications and infrastructure environments.

* Database Management

    Database management provides a unified console for managing both cloud and on-premises databases. It includes lifecycle database management capabilities for monitoring, performance tuning, and administration. With Performance Hub, developers can optimize SQL code during active development and continuously monitor and tune queries in production.

    *For more information on External MySQL Database Management > **[Use Database Management for External MySQL](https://docs.oracle.com/en-us/iaas/database-management/doc/database-management-mysql-heatwave.html)***

* Ops Insights

    OCI Ops Insights (OPSI) is a cloud-native solution that gathers and analyzes telemetry data to help enterprises plan for growth. It enables data-driven capacity planning and performance management, reducing capital expenditures and improving application throughput. It supports ML-based resource usage trending, capacity planning, and Data Explorer-based performance analysis, all within an intuitive dashboard.

    *For more information on Ops Insights for External MySQL please refer to Ops Insights > **[Use Ops Insights for External MySQL ](https://docs.oracle.com/en-us/iaas/operations-insights/home.htm)***

* Logging Analytics

    Oracle Cloud Infrastructure (OCI) Logging Analytics is a cloud solution that lets you index, enrich, aggregate, explore, search, analyze, correlate, visualize and monitor log data from applications and system infrastructure-both in the cloud and on-premises. It can extract database instance records based on SQL queries provided in the log source configuration. In this lab, you'll learn how to use the Oracle Cloud Logging Analytics to enrich log data collected from the world's most popular open source database-MySQL.

    *For more information on Logging Analytics and log Explorer please refer to Logging Analytics > **[Use Logging Analytics for External MySQL](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-defined-sources.html)***

* Application Performance Management

    OCI Application Performance Monitoring includes an implementation of a Distributed Tracing system. It collects and processes transaction trace data (spans) from the monitored application and makes it available for viewing, dashboarding, exploration, alerts, etc. You can use Trace Explorer to view traces and spans and identify performance issues and bottlenecks in your monitored application, from browser to database.

    *For more information on APM and Trace Explorer please refer to Application Performance Monitoring > **[Use Trace Explorer for External MySQL](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/use-trace-explorer.html)***

## Acknowledgements

* **Author** - Sindhuja Banka, HeatWave MySQL Product Manager
* **Contributors** - Sindhuja Banka, Anand Prabhu
* **Last Updated By/Date** - Sindhuja Banka, March 2025
