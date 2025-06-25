# Capacity Planning of Oracle Exadata

## Introduction

In this lab, you will go through the steps to explore the Capacity Planning of Oracle Exadata.

Estimated Time: 10 minutes

### Objectives

-   Explore Capacity Planning Oracle Exadata.

### Prerequisites

This lab assumes you have completed the following labs:
* Lab: Enable Demo Mode

## Task 1: Enable Demo Mode

1.  Skip this task and proceed to *Task 2: Exadata Insights* if you have already enabled Demo Mode in Ops Insights.
    
    To access Ops Insights, click on the Oracle Cloud Console **Navigation menu** (aka hamburger menu) located in the upper left. Under **Observability & Management**, go to **Ops Insights** and click **Overview**.

      ![Ops Insights](./images/opsi-main-ocw.png " ")

2.  Click on **Enable Demo Mode** to enable Demo Mode.

      ![Enable Demo Mode](./images/opsi-enable-demo.png " ")

3.  Once the mode is enabled the overview page will now show resource information for the OperationsInsights compartment, notice the upper-right hand corner will show Demo Mode is now ON for your session.  When you would like to exit demo mode you can either click the disable link in the corner or click the now present **Disable Demo Mode** button where you initially enabled it on the overview page.

      ![Demo Mode ON](./images/opsi-demo-mode-on-ocw.png " ")

4.  On the left-hand pane you will find links to quickly navigate to OPSI offerings including Capacity Planning, Exadata Insights, Oracle SQL Warehouse, AWR Hub, and Dashboards.  

      ![Left Pane](./images/opsi-left-pane-new.png " ")


## Task 2: Exadata Insights

1.  On the **Overview** page, click on **Exadata Insights** from the left pane.

      ![Left Pane](./images/exadata-insights-ocw.png " ")

2.  This will show the Exadata systems registered for Ops Insights.

      ![Left Pane](./images/exadata-systems-ocw.png " ")

3.  On this page, the aggregate view of all the discovered Exadata systems will be shown.

      ![Left Pane](./images/aggregate-view-ocw.png " ")

4.  Also, the current and forecast utilization of the Exadata system will be shown in the bottom section. Click on an Exadata system to evaluate more insights. Click on the Full Rack **X8-2\_Full_DBM08.us.oracle.com**.

      ![Left Pane](./images/current-forecast-ocw.png " ")

5.  On the **Exadata System Details** page, you can view **Rack and Key Metrics**. The page displays Software and Hardware Summary.

      ![Left Pane](./images/rack-and-key-metrics-ocw.png " ")

6.  Navigate to **Metrics by Database** on the left pane.

      ![Left Pane](./images/metrics-by-database-ocw.png " ")

7.  Select the **CPU** tab and choose **Host** under Grouping.

      ![Left Pane](./images/metrics-by-database-host-ocw.png " ")

8.  Now choose **Allocation (CPU)** under **Size** and **Usage Change (%)** under **Color**.

      ![Left Pane](./images/max-allocation-usage-change-ocw-before.png " ")

    Heatmap gets updated based on the selection as shown below

      ![Left Pane](./images/max-allocation-usage-change-ocw-after.png " ")

9.  To show the trend & forecast of CPU for Host and Database, click on the hostname **DBM08adm04.us.oracle.com** and highlight the trend graph.

      ![Left Pane](./images/trend-host-cpu-ocw.png " ")

      We see the aggregate CPU demand of the 3 databases is very stable at the host-level. At the database-level, 2 have growing demand and one is shrinking.

10.  Select the database and highlight the trend and forecast graph.

      ![Left Pane](./images/trend-host-database-ocw.png " ")

11.  To view **Unused CPU capacity** within your database resources navigate to **Metrics by database**. Under **Grouping** select **Host**. Choose **Usage (avg. active CPU)** under **Size** and **Utilization (%)** under **Color**.

      Selecting one of these will allow you to checkmark the **Show Unused Capacity** check.
      Once the **Show Unused Capacity** has been checked, a gray bar will appear on the treemap showing the unused space. 
      
      You can additionally expand the treemap for a better visualization, as well as view the treemap squarified, vertical, or horiziontal. Unused capacity will be grouped by vertically default.

      ![Left Pane](./images/exa-unused-host.png " ")

      Under **Grouping** select **VM cluster**.

      ![Left Pane](./images/exa-unused-vmcluster.png " ")

12.  Click **Metrics by Host** on the left pane.

      ![Left Pane](./images/metrics-by-host-ocw.png " ")

13.  On the **Metrics by Host** page, click on the **CPU** tab, select **All hosts** to see the aggregate trend & forecast. 

      ![Left Pane](./images/cpu-all-hosts-ocw.png " ")

14.  Click the **Exadata Storage Server** option on the left pane.

      ![Left Pane](./images/exadata-storage-server-ocw.png " ")

15. Select **Individual data series** on the top right pane to show the individual storage utilization.

      ![Left Pane](./images/exadata-storage-server1-ocw.png " ")

16. Select **Aggregate data series and forecast** on the top right pane to show total individual storage utilization.

      ![Left Pane](./images/exadata-storage-server2.png " ")

In Conclusion, OPSI Exadata Insights provides comprehensive capacity analysis to give administrators the ability to view, analyze, proactively forecast, and detect potential constraints in Exadata resources. As a system administrator they want to be able to make critical decisions to optimize their Exadata stacks; plan for growth, compare resource usage and perform what-if analysis for various scenarios.


## Acknowledgements

- **Author** - Vivek Verma, Master Principal Cloud Architect, North America Cloud Engineering
- **Contributors** - Vivek Verma, Sriram Vrinda, Derik Harlow, Murtaza Husain
- **Last Updated By/Date** - Vivek Verma, Feb 2025