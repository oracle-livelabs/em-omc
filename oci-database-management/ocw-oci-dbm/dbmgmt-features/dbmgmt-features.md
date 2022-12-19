# Exploring Oracle Cloud Infrastructure Database Management

## Introduction

Database Management provides a single-pane-of-glass view of your fleet of on-premises and cloud databases in OCI, and enables you to detect issues across the fleet and respond to performance and configuration alerts. Here are some of the tasks you can perform using Database Management, which are categorized under database monitoring and management areas.

Fleet Monitoring and Management
-   Obtain an overview of your fleet of databases.
-   View the reports of the database fleet to obtain an insight into the overall health of the databases.
-   Automate database fleet management for enhanced operational efficiency.

Performance Diagnostics
-   Diagnose database performance issues quickly with Performance Hub.
-   Explore database performance statistics for advanced diagnostics with ADDM reports.
-   Use AWR Explorer to view customizable performance metrics from multiple sources of data in table form.

Database Administration
-   Enable SQL jobs to automate a scheduled database maintenance task across all databases in the fleet.
-   View, create, and perform basic administration tasks for tablespaces and their datafiles.
-   Perform SQL Tuning Advisor runs and implement recommendations for improvement.

Estimated Time: 1 hour

Watch the video below for a quick walk-through of the lab.
[Exploring Oracle Cloud Infrastructure Database Management](videohub:1_qpjm77l8)

### Objectives

-   Use Oracle Cloud Infrastructure Database Management to manage a fleet of Oracle Databases and drill down to a single database for additional investigation.

### Prerequisites

This lab assumes you have already completed the following:
- An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account

## Task 1: Getting Started with Database Management

1.  Login to the Oracle Cloud Console, click the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Database Management**.

     ![](./images/dbmgmt1.png " ")

     ![](./images/dbmgmt2.png " ")

2.  The **Databases** tile (on the **Overview** page) displays the total number of Oracle Databases in the compartment and the number of Oracle Databases for which Database Management is enabled.

## Task 2: Monitoring a Fleet of Databases

1.  On the left pane, click **Fleet Summary** to navigate to the **Fleet Summary** page. The dbmgmt compartment is selected by default in the Compartment field.

     ![](./images/fleet-summary.png " ")

2.  The following tiles are available on the **Fleet Summary** page:

    - Databases: Displays the number of Oracle Databases (PDB and Non-CDB) in the compartment. Note that this does not show the number of CDBs.
    - Status: Displays the availability status of the Oracle Databases. You can click the **Alarms** link to view the Alarm Status page of the Oracle Cloud Infrastructure Monitoring service.
    -  Resource Usage: Displays a summary of the overall CPU and Storage allocation and utilization and a change percentage that denotes the comparison of resource usage between the selected time and the comparison time period. *Note*: Use the menus at the top-right corner of the page to select two time periods to compare the performance and configuration metrics of the fleet of databases.
    -  Members: Displays a thumbnail view of your Oracle Databases with their name, status, and type. This view is useful if you have a smaller number of databases in your fleet. The **List** view is displayed by default on the Members tab, however, you can select the **Table** option to view the same information in a tabular format.

3.  On **Fleet Summary** page under **Members** tab, by default, you will see only PDBs and non-CDBs in the database fleet.

4.  On **Fleet Summary** page under **Databases** tile, select **CDB** option for **View by** to view the CDBs in the database fleet.

     ![](./images/showcdbs.png " ")

    For each database including the CDB, the following metrics are displayed along with the change percentage that denotes the comparison of database metrics between the selected period and the comparison time period:
    - Avg. Active Sessions: Displays the average active sessions broken down by CPU, User I/O, and Others, which includes different categories within wait time such as System I/O and Commit.
    - CPU: Displays the CPU allocation and usage.
    - Storage: Displays the storage allocation and usage.
    - I/O: Displays the I/O rate and throughput.

5.  On **Fleet Summary** page, click the **Performance** tab. The Performance view displays a tree map of the performance of your Oracle Databases against various database metrics as seen in the **Members** tab. This view is more useful when you have a large number of databases in the fleet. The databases are displayed as a collection of rectangles in different sizes and colors, in which the size of a rectangle indicates the value of the selected metric and the color indicates the change percentage for the selected metric over the selected time period.

     ![](./images/perf.png " ")

## Task 3: Working with Database Groups

1.  On **Fleet Summary** page, click **Database Groups** under **Database Management**.

     ![](./images/database-group.png " ")

2.  Click **dbmgmt\_pdbs\_group** under the list of Database Groups.

     ![](./images/dbmgmt-pdbs-group.png " ")

3.  On **Database group details** page, **Managed Databases** section has the list of all Managed Databases that are part of the group. You can also:

    - Click **Fleet Summary** to monitor all the Managed Databases in the Database Group on the Fleet Summary page.
    - Click **Edit Description** to add or edit the description of the Database Group.
    - Click **Move Resource** to move the Database Group to another compartment.
    - Click **Jobs** on the left pane under Resources to create a job for the Database Group and monitor job runs and executions.

4.  On the **Database Group Details** page, under **Resources** on the left pane, click **Jobs** to list jobs associated with the database group.

     ![](./images/jobs.png " ")

    - **Runs**: On this tab, you can monitor job runs and executions.
    - **Definitions**: On this tab, you can create a job and view the jobs that are in the Active state and were created within the time period selected in the **Time Period** field.

5.  Under **Runs** tab click on a particular job to view job executions.

     ![](./images/jobs-runs.png " ")

6.  Click on a particular Job Execution to view the **Job execution details** page, which contains the execution details of the job and **Job execution output**.

     ![](./images/job-exec-output.png " ")

7.  On **Database group details** page, click **Definitions** tab under **Jobs** to view the list of jobs.

     ![](./images/job-definition.png " ")

8.  Click a particular Job under **Job Name** to view Job details.

     ![](./images/job-details.png " ")

## Task 4: Monitoring Alert Log

1.  Go back to **Fleet Summary** page. Scroll down to the **Members** tab on the Fleet Summary page. Click **MFG** under **Members** tab to go to **Managed database details** page.

2.  On the left pane, under **Resources** click **Alert logs** to view alert and attention logs generated for the Managed Database in a selected time period. 

     ![](./images/mfg-alert-log.png " ")

    You can use the drop-down lists, fields, and links on this tab to reduce the number of log entries displayed, or search for specific log entries:

    - Use the **Filter by Level** and **Filter by Type** drop-down lists to filter the entries by level or type.
    - Enter a specific message in the Search field and click Search to search for the alert log entry that contains the message. If you select the Regular Expression check box, then you can enter a regular expression such as ^Errors in the Search field and search for the alert log entry whose message entirely or partially contains the regular expression.

## Task 5: Monitoring and Managing Individual Databases

1.  Go back to **Fleet Summary** page. Scroll down to the **Members** tab on the Fleet Summary page.

     ![](./images/fleet-summary.png " ")

2.  Click the **MFG** database in the **Members** tab. In the **Managed Database Details** page Scroll down to the **Summary** section.

     ![](./images/op-stats.png " ")

3.  We can monitor database performance attributes in the **Summary** section, for the time period selected in the **Time Period** menu on the top of this page. Last 60 min is the default time period, and the visual representations or charts provide a quick insight into the health of the database during the selected time period.

     **Activity Class (Avg. Active Sessions):** Displays the average active sessions in the selected time period, broken down by CPU, User I/O, and Wait. The total CPU count is denoted by a red line and enables you to monitor average active sessions compared to the CPU count.

     **DB Time (Avg. Active Sessions):** Displays a summary of the average active sessions data broken down by CPU, User I/O, and Wait. The total CPU count is denoted by a red line.

     **I/O:** Displays the I/O Throughput in MBPS and I/O Rate in IOPS broken down by Read and Write operations.

     **Memory:** Displays memory usage in GB, broken down by the memory usage in various components.

     **Storage Usage:** Displays system storage and user data storage in TB. System storage is broken down by usage in system tablespaces and user data, and User Data storage is broken down by usage in the top five user tablespaces. The total storage allocation for the database is denoted by a red line and enables you to monitor storage usage compared to the total allocation.

4.  You can click one of the other options on the left pane under Resources to perform the following tasks:

     - Monitor the alert and attention logs.
     - Use SQL Tuning Advisor to analyze SQL statements.
     - Monitor the tablespaces and data files.
     - View the users created in the Oracle Database.
     - View and edit database parameters.
     - Monitor the optimizer statistics for a Managed Database.
     - Create and manage Jobs and Job executions for the Managed Database.
     - View the Database Groups the Managed Database is a part of, if any.

5.  On **Managed database details** page, click **Tablespaces** from the left pane to monitor the tablespaces and datafiles stored in each tablespace in the Managed Database.

     ![](./images/tablespace.png " ")

6.  On **Managed database details** page, click **Users** from the left pane to view the users created in the Oracle Database.

     ![](./images/users.png " ")

7.  On **Managed database details** page, click **Database Parameters** from the left pane to view and edit the database parameters for the Managed Database.

     ![](./images/db-parameters.png " ")

## Task 6: Performing Database Performance Diagnostics

1.  Go back to the **Fleet Summary** page. Scroll down to the **Members** tab and click the **MFG** database. On the top of the **Managed Database Details** page, click the **Performance Hub** button.

     ![](./images/perf-hub.png " ")

2.  This will launch the **Performance Hub** page. Performance Hub provides a single view of the database’s performance and enables you to perform the rapid diagnosis of its issues.

     ![](./images/perf-hub1.png " ")

     Performance Hub provides holistic performance management capabilities providing a single view of the database performance using a varied set of features, such as Active Session History Analytics, Real-time SQL Monitoring, Automatic Database Diagnostics Monitoring (ADDM), Blocking sessions, and so on.

     **Active Session History Analytics (ASH) Analytics** allows you to analyze and resolve transient performance problems that can last for only a short period, such as why a particular job or session is not responding when the rest of the instance is performing as usual. It also allows you to perform scoped and targeted analysis by various dimensions and their combinations, such as time, session, module, action, or SQL identifier.

3.  Stay in **Performance Hub**, scroll down and click the **SQL Monitoring** tab.

     ![](./images/sql-monitoring.png " ")

     With Real-Time SQL Monitoring, you can perform complex run-time application SQL analysis, identity, and guide optimization of application calls in the data tier.

     Real-Time SQL Monitoring gives you the following capabilities:

     - Observe and analyze important SQL executions in progress (parallel and long-running queries)
     - Perform detailed and comprehensive execution analysis
     - Resource footprint per query plan step
     - Parallel plan skew across query workers
     - Visualize query plans interactively
     - Perform real-time and historical analysis

4.  Click on the SQL ID to view **Real-time SQL Monitoring for SQL**

     ![](./images/sql-monitoring1.png " ")

5.  Stay in **Performance Hub**, select the **Last 8 Hours** in the time select. Select the most recent snapshot interval to view the automatic report. Click on the **Top SQL Statements** link in the **Findings** section of the **ADDM** tab to view the recommendations

     ![](./images/addm1.png " ")
     ![](./images/addm2.png " ")

     The statistical data needed for the accurate diagnosis of a problem is saved in the Automatic Workload Repository (AWR) of the Oracle Database. The Automatic Database Diagnostic Monitor (ADDM) analyzes the AWR data regularly, locates the root causes of the performance problems, provides recommendations for correcting any problems, and identifies non-problem areas of the system. You can use ADDM to analyze performance issues after the event, often saving the time and resources needed to reproduce a problem.

     ADDM gives you the following capabilities:

     - Identify the root cause of a problem, not symptoms
     - Get recommendations for treating the root causes of problems
     - Identify non-problem areas of the system

5.  Stay in **Performance Hub**, scroll down and click the **Blocking Sessions** tab.

     ![](./images/blocking-session.png " ")

     The **Blocking Sessions** tab displays the current blocking and waiting sessions in a hierarchical display. You can view detailed information about each blocking session and view the sessions blocked by each blocking session. You can also use the tab to inspect or perform deeper analysis of the SQL involved to determine the cause of the blocking. You can perform several operations in the tab, including stopping one or more of the listed sessions to resolve a waiting session problem.

## Acknowledgements

- **Author** - Vivek Verma, Master Principal Cloud Architect, North America Cloud Engineering
- **Contributors** - Vivek Verma, Sriram Vrinda, Murtaza Husain and Derik Harlow
- **Last Updated By/Date** - Vivek Verma, Aug 2022