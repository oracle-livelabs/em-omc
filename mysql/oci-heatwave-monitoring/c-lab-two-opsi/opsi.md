# Ops Insights

## Introduction

In this lab, you will go through the steps to explore Ops Insights for HeatWave MySQL DB system which includes ML based resource usage trending, Capacity Planning, and Database Insights.

Estimated time: 20 minutes

### Objectives

* Enable Ops Insights Demo Mode
* Explore Capacity Planning and Database Insights

## Task 1: Enable Demo Mode

1. To access Ops Insights, click on the Oracle Cloud Console **Navigation menu** (aka hamburger menu) located in the upper left. Under **Observability & Management**, go to **Ops Insights** and click **Overview**.

      ![Selecting Ops Insights](./images/opsi-main.png " ")

2. Click on **Enable Demo Mode** to enable Demo Mode.

      ![Enable Demo Mode](./images/opsi-enable-demo.png " ")

3. Once the demo mode is enabled the overview page will now show resource information for the OperationsInsights compartment, notice the upper-right hand corner will show Demo Mode is now ON for your session.  When you would like to exit demo mode you can either click the disable link in the corner or click the **Disable Demo Mode** button where you initially enabled it on the overview page.

      ![Demo Mode ON](./images/opsi-demo-mode-on.png " ")

4. On the left-hand pane you will find links to quickly navigate to Ops Insights offerings for HeatWave MySQL which includes Capacity Planning, SQL Insights and Dashboards.

      ![Left Pane](./images/opsi-left-pane.png " ")

## Task 2: Capacity Planning - Databases

1. On the **Ops Insights Overview** page, from the left pane click on **Capacity Planning**.

      ![Capacity Planning](./images/capacity-planning.png " ")

2. On the **Database Capacity Planning** page, you will obtain a fleet-wide overview of your resource consumption and trends.  CPU insights, storage insights, and memory insights give a quick view into top resource consumers now and forecast potential resource bottlenecks over the selected period.

      ![Database Capacity Planning](./images/database-capacity-planning.png " ")

    From this page you can perform the following tasks in support of the Capacity Planning use case goals:

    * View total allocation and utilization of CPU, Storage, Memory, and I/O resources for all (enabled) databases in the compartment
    * Identify top-5 databases of CPU, Storage, and Memory by absolute usage or utilization percentage
    * Identify top-5 databases by CPU, Storage, and Memory growth over the period
    * See aggregated historical usage trends for CPU, Storage, and Memory over the period

3. From **Database type** on the left pane select **HeatWave MySQL**.

      ![Database Type as MySQL](./images/database-capacity-planning-mysql.png " ")

4. From **Time Range** on the left pane select **Last 90 days**.

      ![Time range selection](./images/time-range.png " ")

      You can filter based on **Time range**, **Database type** or **Tags**. This let’s you customize the fleet of database of your choice by using combination of one of these.

      ![Filter view](./images/filter.png " ")

5. Review the **Inventory** section. The **Inventory** section displays the total number of databases enabled for Ops Insights along with the database types. In addition, the CPU, Storage, Memory, and I/O usage charts display overall resource consumption (Top Consumers and Usage Trend) by these database targets.

      ![Inventory](./images/inventory.png " ")

6. **CPU Insights** - Database utilization percentage for the 90th percentile value of the daily average CPU Usage over the selected time period. These sections show the number of databases running with low (0–25%) and high (75–100%) utilization of CPU.

      ![CPU Insights](./images/cpu-insights.png " ")

7. **Storage Insights** - Database utilization percentage for the 90th percentile value of the daily average Storage Usage over the selected time period.  These sections show the number of databases running with low (0–25%) and high (75–100%) utilization of storage.

      ![Storage Insights](./images/storage-insights.png " ")

8. **Memory Insights** - Database utilization percentage for the 90th percentile value of the daily average Memory Usage over the selected time period.  These sections show the number of databases running with low (0–25%) and high (75–100%) utilization of memory.

      ![Memory Insights](./images/memory-insights.png " ")

## Task 3: Capacity Planning - CPU

1. On the **Database Capacity Planning** page, from the left pane click on **CPU**.

      ![Database CPU Planning](./images/database-cpu.png " ")

2. **Database CPU** page has a master-detail design with three primary components:

    * Insights – table of databases flagged for CPU utilization insights
    * Aggregate – treemap of CPU utilization over all databases in the compartment
    * Trend & Forecast – time series charts of CPU usage trends and forecasts for individual or groups of databases

      ![Left Pane](./images/database-cpu2.png " ")

3. On the **Database CPU** page, under **Insights** tab, select **30 Day Low Utilization Forecast** against **Databases**, to view database CPU utilization forecast for next 30 days.

      ![30 Day Low Utilization Forecast](./images/utilization-low-forecast.png " ")

4. Under the **Database Display Name** column, select the row corresponding to the **employeesdb** database.

      ![Employees Database](./images/employees-database.png " ")

5. Check the **Utilization (%)** and **Usage Change (%)** for database **employeesdb**.

    * Utilization (%) -  Utilization percentage for the 90th percentile value of the daily average storage usage over the selected time period
    * Usage Change (%): Percentage change in the linear trend of storage usage over the selected time

    ![Percentage Change in Employees Database](./images/employeesdb-database.png " ")

6. The **Trend and Forecast** chart displays historical time series plots related to CPU allocation and usage for the selected database **employeesdb**.

      ![Trend and Forecast](./images/trend-and-forecast.png " ")

      * Historical CPU Usage (dark solid green line) is the Avg Usage - average value of daily (hourly) CPU usage data.

      * Avg Usage Forecast - forecast of Avg Usage data using linear forecast model (dashed green line) and the Max Allocation - maximum allocation of CPU for the database.

      * The value **0.08** AVG ACTIVE CPU USAGE is forecasted for after 15 days for Avg usage of CPU.

      * The red line is **Max Usage** - maximum value of daily (hourly) CPU usage data for database **employeesdb**.

      * The value **1.1** AVG ACTIVE CPU USAGE is forecasted for after 15 days for Max usage Forecast of CPU.

    You can see the difference in average forecasted value v/s Max forecasted value. If the workload is critical and cannot tolerate any performance issues then the database must be allocated the max forecasted value. If the workload is not so critical and can tolerate deviations in performance then it is ok to allocate CPU based on average forecasted value and save money.

7. The trending and forecast chart facilitates:

     * Forecast future maximum and average demand for CPU resources
     * Compare current usage to allocation to detect over-provisioning
     * Compare maximum to average usage and trends to assess demand volatility
     * Forecast difference between the maximum and average daily CPU usage to estimate potential savings from workload smoothing

8. The following models can be selected for display on the upper right of the Trend and Forecast chart:

     * **Linear regression**: The linear regression model assumes a linear relationship across variables to predict the future resource usage.

      ![Linear Forecast](./images/forecast-linear.png " ")

     * **Seasonality aware**: The seasonal option combines a simple model that detects basic seasonality with dynamic, user-selectable data.

      ![Seasonality Forecast](./images/forecast-seasonality.png " ")

     * **AutoML forecasting**: The AutoML forecasting option selects the best fit from multiple machine learning models trained on fixed data window. AutoML (Machine Learning) forecasting leverages Oracle Data Science, employing metalearning to quickly identify the most relevant features, model and hyperparameters for a given training dataset. Forecast and model are precomputed and the forecasts are periodically retrained. The forecast uses up to 13 months of data, or the highest amount of data available for a resource if the resource has less than 13 months since onboarding.

     Within the **Trend & Forecast** chart, click **AutoML forecasting**

      ![Auto ML Forecasting](./images/auto-ml.png " ")

      A new pop up will appear with the AutoML forecasting charts loaded. It will state the training period and the selected forecast algorithms for maximum usage and average usage. The maximum and average confidence channels are also displayed within the chart. The confidence interval for these are 95%, meaning that 95% of future points are expected to fall within this radius from the forecast.

      ![Auto ML View](./images/automl-database.png " ")

      Click **Close** to close the **AutoML forecasting** pop-up and return to **Database CPU** page.

9. Click **Aggregate** on the top and from **Grouping** select **Database Type**.

      ![Aggregate View](./images/aggregate-database.png " ")

     The page displays a Treemap of all databases breaking it down by Database Type. This lets you compare how your different, individual databases are using their resources as well as between various database types.

## Task 4: Capacity Planning - Memory

1. Click on the **Memory** menu on the left panel.

      ![Select Memory Menu](./images/memory-menu.png " ")

2. You get a complete view of memory usage across all Ops Insights enabled databases.

      ![Memory Usage](./images/database-memory.png " ")

    From here we can identify servers with underused or overused memory and also compare memory utilization between databases.

3. From the drop-down on the top select **30 Days High Utilization Forecast**.

      ![30 Day High Utilization](./images/utilization-forecast.png " ")

4. Under the **Database Display Name** column, select the row corresponding to the **departmentsdb** database.

      ![Departments Database](./images/departments-db.png " ")

5. In the **Trend & Forecast** chart view the memory trend and usage forecast for the selected database. View **Max usage** and **Max usage forecast** from the right panel.

      ![Trend and Forecast](./images/memory-trend-max.png " ")

      You can compare the average forecasted memory usage with the maximum forecasted value. In this case, **Max Usage Forecast** is 27.33 GB, while the database has only 16 GB **allocated**. Since the forecasted usage exceeds the allocated memory, it is important to increase the allocation to avoid any potential issues.

6. In the **Trend & Forecast** chart view, the **AutoML forecasting** option selects the best fit from multiple machine learning models trained on fixed data window. AutoML (Machine Learning) forecasting leverages Oracle Data Science, employing metalearning to quickly identify the most relevant features, model and hyperparameters for a given training dataset. Forecast and model are precomputed and the forecasts are periodically retrained. The forecast uses up to 13 months of data, or the highest amount of data available for a resource if the resource has less than 13 months since onboarding.

      ![Auto ML Forecast](./images/memory-trend-forecast-ml.png " ")
      ![Auto ML](./images/memory-trend-forecast-auto-ml.png " ")

      Click **Close** to go back to the **Database Memory** page.

7. You can similarly check the **Storage utilization forecast** for all Ops Insights enabled databases. The **Trend & Forecast** chart lets you compare allocated storage with forecasted storage, helping you plan ahead and prevent potential storage issues.

## Task 5: Database Insights

1. On the **Ops Insights Overview** page, from the left pane click **Database Insights**. On the **SQL Insights - Fleet analysis** page and filter by database type as **MySQL**. Now you can view insights and analysis for HeatWave and External MySQL DB system enabled in the compartment.

      ![SQL Insights](./images/sql-insights.png " ")

2. Click the database **departmentsdb** to view **SQL Insights - Database Analysis**

      ![Database Analysis](./images/sql-departments-db.png " ")

3. HeatWave MySQL DB system dashboard provides a broad overview of the SQL workload executing in the database. This includes basic properties of the database and the SQL collected from it. SQL activity is shown by day broken down by command type and database, exposing changes in the workload over time. Average Active Session (AAS) by database schemas, latency type and Top SQLs additionally provide workload characteristics over time.

      ![DB Insights for Department Database](./images/departments-db-insights.png " ")

      ![Top SQLs](./images/top-sqls.png " ")

4. Click on **SQL activity by latency type**.

      ![SQL activity by latency type](./images/sql-latency-insights.png " ")

      The Database analysis dashboard is designed to give a broad overview of the SQL workload executing in the database.

## Task 6: SQL Explorer

1. SQL Explorer provides an easy-to-use interface that lets you interactively explore and visualize detailed performance statistics stored in Ops Insights SQL Warehouse.

2. With SQL Explorer, you can explore performance statistics via a SQL query to extract the data with which to create an intuitive visualization. This provides interactive data exploration and visualization for deep exploration of application SQL performance statistics. The user interface is designed to simplify and streamline query development.

3. In this lab create visualizations using pre-existing performance statistics via a SQL query.

4. In this example we will calculate the average latency per execution to analyze the performance of operations over time.

5. On the **Ops Insights Overview** page, from the left pane click **SQL Insights** and then click **SQL Explorer**.

      ![SQL Explorer](./images/sql-explorer.png " ")

6. This will take you to the **SQL Explorer** page.

      ![SQL Explorer View](./images/sql-explorer-main.png " ")

7. Select **Resource type** as **MySQL**.

      ![SQL Explorer](./images/sql-explorer-database.png " ")

8. Remove default **\*** from SELECT statement line.

      ![SQL Explorer](./images/sql-explorer-remove-select.png " ")

9. Enter the following SQL in the SQL query section (copy & paste the statement line by line)

      ```
            SELECT <copy> ROLLUP_TIME_UTC, AVG(TOTAL_LATENCY/EXEC_COUNT)/1000000000 as AVG_LATENCY_SEC
            </copy>
      ```

      ```
            <copy>WHERE</copy>
      ```

      ```
            GROUP BY <copy> ROLLUP_TIME_UTC
            </copy>
      ```

      ```
            <copy>HAVING</copy>
      ```

      ```
            ORDER BY <copy>ROLLUP_TIME_UTC ASC</copy>
      ```

      ![SQL Query](./images/sql-query.png " ")

10. Click **Run** to execute the query.

11. This will display the query result in a tabular format.

      ![SQL Output](./images/sql-query-table.png " ")

12. Under the **Visualization** tab on the right pane, select the following -

      **Chart type** : **Area Chart**

      **Y axis** : **AVG\_LATENCY\_SEC**

      **X axis** : **ROLLUP\_TIME\_UTC**

      Check mark **Correlated tooltips**

      ![SQL Visualization](./images/sql-query-visual.png " ")

13. This will display the visualization as an **Area Chart**.

14. Click on **Clear** to clear the query section.

      ![SQL Visualization](./images/sql-explorer-clear.png " ")

15. Click on **Advanced** Mode to view **SQL Explorer** in advanced mode. The advanced mode give you more control over the SQL queries that you are running against your database to view database performance.

      ![SQL Visualization](./images/sql-explorer-advanced.png " ")

16. This will take you to the **SQL Explorer Advanced** Mode page. Advanced mode can be used to execute your own custom queries and obtain more information above the SQLs running in the database.

      ![SQL Visualization](./images/sql-explorer-advanced-main.png " ")

## Acknowledgements

* **Author** - Sindhuja Banka, HeatWave MySQL Product Manager
* **Contributors** - Sindhuja Banka, Anand Prabhu, Sriram Vrinda
* **Last Updated By/Date** - Sindhuja Banka, March 2025
