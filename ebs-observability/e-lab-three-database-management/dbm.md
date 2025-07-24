# Managing SQL and Database Performance

## Introduction
* In this lab, you will explore OCI Database Management for Oracle E-Business Suite (EBS) databases. Database Management offers a unified, cloud-native console for managing EBS databases (cloud and on-prem), delivering real-time diagnostics, workload insights, and automated tuning for optimal query performance.

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

5. Click on **SQL Text** to reveal the SQL statement.

    ![SQL Text](./images/performance-hub/perfhub-sql-text.png " ")

## Task 3: Viewing SQL Performance from Application Transactions

## Task 4: Insights into Database Performance

1. Click the **Close** button at the bottom of Performance Hub to return to the database details. 

    ![Exit Performance Hub](./images/performance-hub/perfhub-exit.png " ")

2. In the Database Details page, click on the **ADDM Spotlight** button to view findings provided by the OCI Ops Insights service.

    ![ADDM Spotlight Navigation](./images/database-performance/addm-spotlight-nav.png " ")

5. Adjust the time window to **7 days** and review any findings. You can also view recommendations by clicking the **Recommendations** tab on top.

    ![ADDM Spotlight Findings](./images/database-performance/addm-spotlight-findings.png " ")
    ![ADDM Spotlight Recommendations](./images/database-performance/addm-spotlight-recommendations.png " ")

6. Click the **Managed database details** breadcrum link on top to return to the database overview page. 
    ![Database Details Navigation](./images/database-performance/addm-spotlight-exit.png " ")

## Task 5: Analyzing Database Performance Trends

## Acknowledgements

* **Author** - Zyaad Khader, Principal Member of Technical Staff
* **Contributors** - Zyaad Khader
* **Last Updated By/Date** - Zyaad Khader, July 2025