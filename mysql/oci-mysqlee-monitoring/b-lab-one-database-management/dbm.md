# Database Management

## Introduction

In this lab, you will explore Database Management for External MySQL DB System. Database Management provides a single-pane-of-glass view of your cloud and on-premises databases in OCI, helping you monitor and detect issues efficiently.

Estimated time: 20 minutes

### Objectives

* Use Oracle Cloud Infrastructure Database Management to manage a fleet of MySQL Databases and drill down to a single database for further investigation
* Explore Database Management Summary
* Analyze all Metrics of an External MySQL DB system
* Review Configuration variables of an External MySQL DB system
* Explore Alarm definitions of an External MySQL DB system
* Diagnose database performance issues quickly with Performance Hub

## Task 1: Getting Started with Database Management

1. Login to the Oracle Cloud Console and change the selected region to **US East (Ashburn)** region as shown.

     ![Selecting Cloud Region](./images/mysql-ee-region.png " ")

2. Click on the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Database Management**.

     ![Selecting Database Management](./images/dbmgmt.png " ")

3. The error appears due to the default root compartment, but it can be ignored as we only enabled policies for the **dbmgmt** compartment.

     ![Policy Error](./images/navigation-error.png " ")

4. The **root** compartment is selected by default in the Compartment field. Set the **Compartment** to **dbmgmt** following the navigation.

     ![Compartment Navigation](./images/navigation.png " ")

     ![Compartment Selection](./images/navigation-compartment.png " ")

5. The **MySQL databases** tile (on the **Overview** page) displays the total number of External MySQL DB systems and HeatWave MySQL Databases in the compartment and region for which Database Management is enabled.

     ![Database Management Overview](./images/overview.png " ")

## Task 2: Monitoring a Fleet of MySQL Databases

1. On the left pane, click on **Diagnostics & Management**.

     ![Navigation to Diagnostics & Management](./images/nav.png " ")

2. Navigate to the **HeatWave & MySQL fleet summary** page.

     ![Navigation to HeatWave and MySQL](./images/nav-mysql.png " ")

3. The following tiles are available on the **Fleet Summary** page:

    * **Inventory**: Displays the number of MySQL Databases in the compartment.
    * **Monitoring Status**: Displays the availability status of the managed MySQL Databases in the compartment.
    * **Resource Usage**: Displays a summary of the overall CPU utilization, Storage and Memory allocation for the selected time period on the top-left corner of the page.
    * **Alarms**: Displays the total number of open database alarms in the compartment and the number of alarms by severity.

     ![Fleet Summary](./images/fleet-summary.png " ")

4. Below the tiles, the list of HeatWave and External MySQL DB systems for which Database Management is enabled is displayed along with the following information:
    * **DB system name**: Name of the DB system.
    * **Monitoring status**: Monitoring status of the DB system.
    * **HeatWave**: HeatWave enablement status. Indicates whether a HeatWave cluster is attached to the HeatWave DB system. This information is only displayed for HeatWave DB systems.
    * **HeatWave nodes**: Number of HeatWave nodes in the HeatWave cluster. This information is only displayed for HeatWave DB systems.
    * **Average statements**: Displays the Average number of SQL statements executed per minute.
    * **Average statement latency**: Displays the Average latency (in milliseconds) for the executed SQL statements.
    * **CPU utilization**: Displays the Percentage of CPU utilized by the DB system.
    * **Storage utilization**: Displays the Percentage of storage utilized by the DB system.
    * **Memory utilization**: Displays the Percentage of memory utilized by the DB system.

    ![Fleet Summary of MySQL DB systems](./images/fleet-summary-db-systems.png " ")

## Task 3: Monitor a Single External MySQL DB system - Summary

1. In the **Fleet Summary** page, click on the **sales-database** database.

     ![DB system selection](./images/fleet-summary-selection.png " ")

2. In the **Resources** page you will get to the **Summary** section. We can monitor database performance attributes in the **Summary** section, for the time period selected in the **Time Period** menu on the top of this page. Last 60 min is the default time period, and the visual representations or charts provide a quick insight into the health of the database during the selected time period.

     ![Selecting single DB system](./images/single-mysql-summary.png " ")

3. **Monitoring status timeline** displays the availability of the database during the selected period of time. The color of the blocks denotes the status and the number of blocks denotes the time slots within the selected time period over which availability is checked. For example, if the default time period, Last 60 min, is selected, then each block represents a period of two minutes.

     ![Monitoring Status Timeline](./images/timeline.png " ")

4. **Metric charts such as Average statement latency (seconds) and CPU (%)** monitor the visual representation of DB system metrics or metric charts in the Summary section to obtain a quick insight into the performance and core resource utilization of your DB system. These charts enable you to analyze data better by monitoring different parameters such as active connections, disk operations and throughput. You can hover the mouse on the charts to view additional details such as the metric name (Series), date and time, and value; filter the data in the charts by clicking the options displayed in the legend. For descriptions of the metric charts, see [HeatWave and External MySQL DB System Metric Charts](https://docs.oracle.com/en-us/iaas/database-management/doc/mysql-heatwave-metric-charts.html#GUID-758BB559-01FF-4EEC-9CF9-266B94A2604F).

     ![Metric charts](./images/single-mysql-summary-metrics.png " ")

5. The Summary section is displayed by default on the MySQL database details page, however, you can click one of the other options on the left pane under Resources.

## Task 4: Monitor a Single External MySQL DB system - Metrics

1. In the **Resources** page, click on the **Metrics** section. The **Summary** page shows only a couple of metrics. To view all metrics, go to the **Metrics** page.

     ![Metric page](./images/single-mysql-metrics.png " ")

2. You can **select** or **deselect** specific metrics on the Metrics page.

     ![Select more charts](./images/select-more-charts.png " ")

3. You can also choose a time period from the last **60 minutes, 24 hours, or 7 days** to view the metrics.

     ![Time Selection](./images/select-more-time.png " ")

## Task 5: Monitor a Single External MySQL DB system - Configuration variables

1. In the **Resources** page, click on the **Configuration variables** section. You can monitor the configuration variables that are currently used by running instances.

     *Configuration variables are the user, system, initialization, or service-specific variables that define the operation of the DB system.*

     ![Configuration variables](./images/configuration-variables-home.png " ")

2. In the Configuration variables section, you can use filters on the left pane to filter the configuration variables.

     ![Unmodified Variables](./images/config-variables-filters.png " ")

3. Deselect the Hide unmodified variables check box to view the variables that were not modified. This check box is selected by default.

     ![View Configuration Variables](./images/configuration.png " ")

4. View the following configuration variable information:

    * **Name**: Name of the configuration variable.
     Click the Arrow icon adjacent to the name of the configuration variable to view the default and current value.

    * **Value**: Value of the configuration variable.
    * **Modified**: Check mark to indicate if the configuration variable was modified.
    * **Dynamic**: Check mark to indicate if the configuration variable is a dynamic variable, which means changing the variable does not require restarting the DB system.
    * **Configurable**: Check mark to indicate if the configuration variable is configurable.
    * **Source**: Source from which the configuration variable was most recently set. For information on the various types of sources, see Performance Schema variables_info Table.
    * **Time set**: Date and time the configuration variable was most recently set.

    ![Configuration](./images/view-config-variables.png " ")

## Task 6: Set Up Alarm Definitions for External MySQL

1. In the **Resources** page, click on the **Alarm definitions** section. You can set up alarm definitions to simplify the process of creating and managing alarms for External MySQL DB systems in Database Management.

     ![Alarms Definitions](./images/alarms-home-view.png " ")

2. In the Alarm definitions section, you can create Oracle recommended alarms that are preconfigured for common operational scenarios for your External MySQL DB system. In this case, we have already set up and configured alarms.

3. Click the alarm to view the alarm details on the Alarm Definitions page in the Monitoring service.

     *For Oracle-recommended alarms, the provider: DBM free-form tag is added by default during the creation process and is displayed in the Tags section.*

     ![Alarms](./images/click-view-alarm.png " ")

4. It opens the alarm on a new page.

     ![View Alarms](./images/view-alarm.png " ")

5. Use the **Search** field and the filter drop-down lists above the list of alarms to filter the alarms:
     * **Severity filter**: View the alarms of a particular severity type (Critical, Error, Warning, Information).
     * **Scope filter**: View the alarms specified for all the DB systems in a compartment or the alarms specified for the DB system. By default, all the alarms are displayed.
     * **Origin filter**: View the Oracle-recommended alarms or the custom alarms created in the Monitoring service, for the DB system. By default, all the alarms are displayed.

     ![Search for an Alarm](./images/search-alarm.png " ")

6. Optionally, you can click the Actions icon (Actions) available for each recommended alarm and click **Edit threshold** to edit the basic alarm values in Database Management or click **Edit alarm** to view and edit the complete set of values specified for the alarm in the Monitoring service. For information on the fields displayed in the Edit alarm panel, see [Edit Alarms](https://docs.oracle.com/en-us/iaas/database-management/doc/set-alarm-definitions_mysql.html#GUID-E8FF0501-4B5C-4508-A9D2-17692591B4B2).

     ![Edit Alarm](./images/edit-alarm.png " ")

     ![Edit Alarm Panel](./images/edit-alarm-window.png " ")

7. Select alarms and click **Clone** to clone the alarms. You can clone existing Oracle-recommended or custom alarms and apply them to specific DB systems or all the DB systems in a compartment. The cloning capability reduces the effort required to create multiple alarms, and allows you to standardize alarm settings across multiple DB systems. For information, see [Clone Alarms](https://docs.oracle.com/en-us/iaas/database-management/doc/set-alarm-definitions_mysql.html#GUID-682C254A-EB5F-424B-B713-7D90737F9DDA).

     ![Clone Alarm](./images/clone-alarm.png " ")

8. Select alarms and click Delete to delete the alarms.

     ![Delete Alarm](./images/delete-alarm.png " ")

## Task 7: Performance Hub

1. Click on **Performance Hub** tab on the top of the page under DB system name.

     ![Performance Hub](./images/performance-hub.png " ")

2. Using Performance Hub, you can improve the performance of your database applications by monitoring query performance. It enables you to accurately pinpoint SQL code that is the root cause of a slow down; and improve SQL code during active development as well as continuously monitor and tune queries running on production systems.

     ![Home View of Performance Hub](./images/perf-hub-home.png " ")

3. In Performance Hub, select an option in the **Last seen** drop-down list to specify the duration for which you want to monitor SQL activity and view the last seen SQL statements. If you select the Custom option in the Last seen drop-down list, you can specify a custom duration within the last seven-day period. The Time range field displays the time period depending on the selected Last seen option. You can also click the Time range field to specify a custom duration within the last seven-day period. To refresh the data in Performance Hub, click **Refresh** in the upper-right corner.

     ![Performance Hub Duration](./images/perf-hub-duration.png " ")

4. Based on the selected time period, relevant information is displayed in the following charts and section:

     * **Average statement latency (seconds)**: Displays the average latency (in seconds) for the SQL statements executed against the DB system.

     * Click **Select charts** in the upper-right corner and select Statement count to view the Statement count chart. This chart displays the total number of SQL statements executed against the DB system, during the selected time period. For an External DB system, the Statement count chart also displays the number of SQL statements executed.

     ![Performance Hub Charts](./images/perf-hub-selected-charts.png " ")

5. Top 100 by **indicator** section displays the aggregated summary information for the top SQL statements based on a selected indicator such as **average statement latency, total execution count, or execution status**. You can filter and monitor SQL statements to quickly identify expensive statements, customize the displayed information using the **Columns** dropdown.

     ![Top Queries](./images/top-100-queries.png " ")

6. The listed SQL statements in the Top 100 by **indicator** section are normalized statement digests with aggregated data from the time each statement was first seen, helping you pinpoint performance issues and click the link in the Query column to examine the SQL statement in the SQL details panel. In the SQL details panel, you can:

     * Use the statement digest ID to write a query and obtain additional information from the DB system.
     * View the normalized SQL.
     * Monitor detailed information about the execution time, number of rows, and temporary tables. For example, you can monitor the number of rows that were examined or returned and the number of temporary tables that were created.
     * For information on statement digests, see [Performance Schema Statement Digests and Sampling](https://dev.mysql.com/doc/refman/8.0/en/performance-schema-statement-digests.html#statement-digests-general).

     ![Statement Digest](./images/statement-digest.png " ")

7. Click **Close** to exit the SQL details panel.

8. Click **Close** on Performance Hub to return to the main Database Management page for the HeatWave MySQL DB system.

## Acknowledgements

* **Author** - Sindhuja Banka, HeatWave MySQL Product Manager
* **Contributors** - Sindhuja Banka, Anand Prabhu, Sriram Vrinda
* **Last Updated By/Date** - Sindhuja Banka, March 2025
