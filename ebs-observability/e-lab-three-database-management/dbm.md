# Managing SQL and Database Performance

## Introduction
* In this lab, you will explore OCI Database Management and OCI Ops Insights for Oracle E-Business Suite (EBS) databases. These services offer a offers a unified, cloud-native console for managing EBS databases (cloud and on-prem), delivering real-time diagnostics, workload insights, and automated tuning for optimal query performance.

### Objectives

* Analyze database sessions and SQL performance 
* Reveal database ineffeciencies and remediation recommendations
* Drill down from application traces to SQL performance

## Task 1: Database Overview

1. Click on the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Diagnostics & Management**. 

    ![Selecting Diagnostics and Management](./images/setup/dbm-nav.png " ")

2. The **root** compartment is selected by default in the Compartment field. Set the compartment to **EBS Demo** (emdemo -> eStore -> EBS_Demo).

    ![Compartment Navigation](./images/setup/dbm-compartment-selection.png " ")

3. This is the Fleet Summary page, which provides an overview of the database fleet being monitored. Click on **CDB EBS Demo** to open the database details for the Container Database. 

    ![Database Details Navigation](./images/database-performance/diagnostics-and-management.png " ")

4. The Database Details page provides a summary of the monitored database in addition to links for additional insights.

    ![Database Details](./images/database-performance/cdb-details.png " ")

## Task 2: Analyzing SQL Performance

1. In the Database Details page, click on the **Performance Hub** button to analyze SQL performance.

    ![Performance Hub Navigation](./images/performance-hub/perfhub-nav.png " ")

2. The Performance Hub provides details on long-running SQL queries, database sessions and blocking sessions. Click on an SQL ID hyperlink to view more information.

    ![Performance Hub](./images/performance-hub/perfhub.png " ")

3. An SQL Summary page is opened, which provides metrics and statistics for that specific SQL.

    ![SQL Summary](./images/performance-hub/perfhub-sql-summary.png " ")

4. Navigate to the **Execution Statistics** tab to view a detailed breakdown of the SQL performance.

    ![SQL Statistics](./images/performance-hub/perfhub-execution-statistics.png " ")

5. Click on the **SQL Text** tab to reveal the SQL statement.

    ![SQL Text](./images/performance-hub/perfhub-sql-text.png " ")

6. Click the **Close** button at the bottom of Performance Hub to return to the database details. 

    ![Exit Performance Hub](./images/performance-hub/perfhub-exit.png " ")

## Task 3: Viewing SQL Performance from Application Transactions

1. Use the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Trace Explorer**. For more information on Trace Explorer, please refer to the *Application Performance Management* lab.

    ![Selecting APM Trace Explorer](./images/setup/apm-nav.png " ")

2. Click the **SQLs** tab at the top of the Trace Explorer, then click on count hyperlink for the row item with the **1tgrzyv00tyy2** SQL ID. 

    ![Selecting a Database Span](./images/apm-drilldown/apm-sql-spans.png " ")

3. Click on the hyperlink of any of the spans, then click the button **SQL ID in DBM**. This will link to Performance Hub and filter by that specific SQL ID. 

    ![APM Drilldown to Performance Hub](./images/apm-drilldown/apm-drilldown-to-perfhub.png " ")

4. To view a user session that used this SQL ID, click on the hyperlink of any of the user sessions.

    ![Performance Hub](./images/apm-drilldown/perfhub-sqlid.png " ")

5. Click on ASH Analytics to select the SQL ID that you would like to further analyze.

    ![ASH Analytics](./images/apm-drilldown/perfhub-ash-analytics.png " ")

6. We follow the same flow here as we did in *Task 2*, starting with the SQL summary.

    ![SQL Summary](./images/apm-drilldown/perfhub-sql-summary.png " ")

7. Navigate to the **Execution Statistics** tab to view a detailed breakdown of the SQL performance.

    ![SQL Statistics](./images/apm-drilldown/perfhub-execution-statistics.png " ")

8. Click on the **SQL Text** tab to reveal the SQL statement.

    ![SQL Text](./images/apm-drilldown/perfhub-sql-text.png " ")

9. Click the **Close** button at the bottom of Performance Hub to return to the database details. 

    ![Exit Performance Hub](./images/apm-drilldown/perfhub-exit.png " ")

## Task 4: Insights into Database Performance

1. In the Database Details page, click on the **ADDM Spotlight** button to view findings provided by the OCI Ops Insights service.

    ![ADDM Spotlight Navigation](./images/database-performance/addm-spotlight-nav.png " ")

2. Adjust the time window to **7 days** and review any findings. You can also view recommendations by clicking the **Recommendations** tab on top.

    ![ADDM Spotlight Findings](./images/database-performance/addm-spotlight-findings.png " ")
    ![ADDM Spotlight Recommendations](./images/database-performance/addm-spotlight-recommendations.png " ")

3. Click the **Managed database details** breadcrum link on top to return to the database overview page. 
    ![Database Details Navigation](./images/database-performance/addm-spotlight-exit.png " ")

## Task 5: Analyzing Database Performance Trends

1. In the Database Details page, click on the **AWR Explorer** button to view database performance trends.

    ![AWR Explorer Navigation](./images/database-performance/awr-explorer-nav.png " ")

2. View the various sections of AWR Explorer:
    * ### Load Profile
    ![AWR Explorer Load Profile](./images/database-performance/awr-explorer-load-profile.png " ")

    * ### Metrics
    ![AWR Explorer Metrics](./images/database-performance/awr-explorer-metrics.png " ")

    * ### Wait Events
    ![AWR Explorer Wait Events](./images/database-performance/awr-explorer-wait-events.png " ")

    * ### Activity
    ![AWR Explorer Activity](./images/database-performance/awr-explorer-activity.png " ")


## Acknowledgements

* **Author** - Zyaad Khader, Principal Member of Technical Staff
* **Contributors** - Zyaad Khader
* **Last Updated By/Date** - Zyaad Khader, July 2025