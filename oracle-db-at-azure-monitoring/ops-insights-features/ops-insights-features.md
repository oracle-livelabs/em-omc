# Exploring Oracle Cloud Infrastructure Ops Insights for Oracle Database@Azure

## Introduction

Oracle Cloud Infrastructure Ops Insights is an Oracle Cloud Infrastructure (OCI) native service that provides holistic insight into database and host resource utilization and capacity. Ops Insights (OPSI) provides capacity planning, long-term SQL analysis, and historical performance reports for your Oracle databases. The service has a full offering of features to improve performance and reduce overhead for your resources. The ability to quickly and easily ingest valuable metric data allows administrators, engineers, and executives to make informed decisions on allocating resources to prevent major issues and reduce overhead for managing their infrastructure resources.

Estimated Time: 60 minutes

### Objectives

-   Utilize predictive insights to forecast database and host resource consumption for long-term capacity planning. 
-   Uncover database performance issues using SQL Insights and ADDM Spotlight.
-   Make data-driven decisions to optimize resource use, proactively avoid outages, and improve performance.

## Task 1: Getting Started with Oracle Database@Azure Ops Insights

*  Login to the Oracle Cloud Console, click the **Navigation Menu** in the upper left, navigate to **Oracle Database**, and select **Oracle Exadata Database Service on Dedicated Infrastructure**.

*  Navigate to the **Exadata VM Clusters** page and select the Oracle Database@Azure VM Cluster.

*  Navigate to the **Databases** page and select the Oracle Database@Azure cloud database.

*  On the **Database Information** page, navigate to **Associated services** section. 

*  Click **View** for Ops Insights.

     ![Ops Insights](./images/odaa-associated-service-dbm-opsi.png "Ops Insights")
     ![Ops Insights Overview](./images/odaa-exadatas-overview.png "Ops Insights")

## Task 2: Exadata Insights

*  On the **Ops Insights Overview** page, from the left pane select the **Exadata Insights**.

      ![Left Pane](./images/odaa-exadata-insights.png " ")

*  On the **Overview** page, click on **Exadata Insights** from the left pane.

      ![Left Pane](./images/odaa-exadata-insights.png " ")

*  This will show the Exadata systems registered for Ops Insights.

      ![Left Pane](./images/odaa-exadata-system.png " ")

*  On this page, the aggregate view of all the discovered Exadata systems will be shown.

      ![Left Pane](./images/odaa-aggregate-view.png " ")

*  Also, the current and forecast utilization of the Exadata system will be shown in the bottom section. Click on the Oracle Database@Azure Exadata system to evaluate more insights. 

      ![Left Pane](./images/odaa-current-forecast.png " ")

*  On the **Exadata System Details** page, you can view **Rack and Key Metrics**. The page displays Software and Hardware Summary.

      ![Left Pane](./images/odaa-rack-and-key-metrics.png " ")

*  Navigate to **Metrics by Database** on the left pane.

      ![Left Pane](./images/odaa-metrics-by-database.png " ")

*  Click **Metrics by Host** on the left pane.

*  On the **Metrics by Host** page, click on the **CPU** tab, select Grouping **None** to see the aggregate trend & forecast for All Hosts. 

      ![Left Pane](./images/odaa-metrics-by-host.png " ")


*  Now choose **Allocation(CPU)** under **Size** and **Usage Change (%)** under **Color**.Select the **Seasonality aware** radio button. 

      ![Left Pane](./images/odaa-metrics-by-host-seasonality.png " ")

*  Click the **Exadata Storage Server** option on the left pane.

      ![Left Pane](./images/odaa-exadata-storage-server.png " ")

* Select **Aggregate data series and forecast** on the top right pane to show total individual storage utilization.
      ![Left Pane](./images/odaa-exadata-storage-server1.png " ")


## Task 3: SQL Insights

*  On the **Ops Insights Overview** page, from the left pane select the **Database Insights**.

      ![Left Pane](./images/odaa-sql-insights.png " ")

*  On the **SQL Insights** page, from the left pane select the **Database Analysis** page.

      ![Left Pane](./images/odaa-database-insights-analysis.png " ")

*  On the **Insights** section, to look at the Degraded SQL due to the plan changes, click the number under **Degraded plan changes**.

      ![Left Pane](./images/odaa-degraded-sql.png " ")

*  It will bring up the page for the **Top 50 degraded plan changes**.

      ![Left Pane](./images/odaa-top-50-degraded-plan-changes.png " ")

*  Click on the **SQL ID: cu05sdu975cnh** to see the details of the SQL.

      ![Left Pane](./images/odaa-sql-plan-details.png " ")

## Conclusion

OCI Ops Insights enables administrators to uncover performance issues, forecast consumption, and plan capacity using machine-learning-based analytics on historical and SQL data. Organizations can use these capabilities to make data-driven decisions to optimize resource use, proactively avoid outages, and improve performance.

## Acknowledgements

- **Author** - Royce Fu, Master Principal Cloud Architect, North America Cloud Infrastructure Engineering
- **Contributors** - Royce Fu, Derik Harlow, Murtaza Husain,Sriram Vrinda
- **Last Updated By/Date** - Royce Fu, December 2024

