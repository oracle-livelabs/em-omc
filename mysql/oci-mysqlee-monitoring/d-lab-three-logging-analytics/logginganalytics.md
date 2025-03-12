## Introduction

In this lab, you will learn how to use the Oracle Cloud Logging Analytics service to enrich the log data collected based on the SQL query provided in the log configuration from the world's most popular open source database - MySQL.

Estimated Lab Time: 20 minutes

### Objectives

- Learn OCI Logging Analytics fundamentals in the context of log collection from an Application architecture hosted on top of MySQL Database
- Learn to analyse, monitor, troubleshoot, and derive knowledge from the collected log data using Logging Analytics' Machine Learning features such as Cluster and Link
- Learn to create and use monitoring dashboards

## Task 1: Getting Familiar with Log Explorer

1. To access Logging Analytics, click on the Oracle Cloud Console **Navigation menu** (aka hamburger menu) located in the upper left corner. Under **Observability & Management**, navigate to **Logging Analytics**.

     ![Database Management](./images/navigation.png " ")

2. Click on **Administration** from the tab on the top beside Home.

     ![Database Management](./images/home-view.png " ")

3. From the Resources Menu, click on **Sources** to navigate to the Source that I have already created for visualization purposes.

      ![Database Management](./images/resources.png " ")

      ![Database Management](./images/mysource.png " ")

      ![Database Management](./images/view-log-explorer.png " ")

4. Here are the main parts of the user interface that will be used throughout this lab.

      ![Database Management](./images/log-explorer.png " ")

      - **Scope Filter** - for setting Entity and Log Group Compartment scope for exploration.

      - **Time range** picker, and **Actions** menu - where you can find actions such as, *Open*, *Save*, and *Save as*.

      - **Query bar**, with **Clear**, **Search Help** and **Run** buttons at the right end of the bar.

      - **Fields panel** - where you can select sources and fields to filter your data.

      - **Visualization panel** - where you can select the way to present search data in a form that helps you.

      - **Main panel** - where the visualization outputs appear above the results of the query.

*Note: You are working with live logs so it may take a few minutes for logs to show up in your Log Explorer view. Click the **Run** button to re-run the query.*

## Task 2: Visualize Data Using Charts and Controls

1. In the Visualizations panel, click the **Visualizations** options.

     ![Compartment](./images/visualizations.png " ")

2. Select any simple visualization like **Heat Map** (table with histogram icon). The data is represented in the form of a Heat Map.

      ![Compartment](./images/visualizations-heatmap.png " ")

      ![Compartment](./images/visualizations-heatmap-view.png " ")

2. Select any other visualization like **Line** (table with histogram icon). The data is represented in the form of a Line.

      ![Compartment](./images/visualizations-line.png " ")

      ![Compartment](./images/visualizations-line-view.png " ")

## Task 3: Explore Logs Using Cluster Visualization

1. Click on the **Cluster** Visualization to invoke Machine Learning Algorithm.

     ![Fleet Summary](./images/cluster.png " ")

     ![Fleet Summary](./images/cluster-analysis.png " ")

2. You can drill down into different Clusters, Potential Issues, Outliers and Trends. Logging Analytics uses unsupervised ML to find related clusters in data. This reduces the approximately 500,000 log records to 500 cluster patterns, in real time.

      *Note: The numbers you see might be slightly different than the ones shown in the workshop. You can use the START time **Feb 7, 2025 04:54 PM UTC(-08:00)** and END time **Feb 14, 2025 04:54 PM UTC(-08:00)** in the time picker to replicate these in your lab environment.*

3. Click on the **Potential Issues** tab.

   In this screenshot, we see that out of the 53 clusters, 2 were automatically identified as Potential Issues.

   *Note: The actual numbers on your screen may be different because you are using live log data.*

   **Potential Issues** are a subset of total clusters that have potential issues based on log records containing words such as error, fatal, exception, and so on.

      ![Fleet Summary](./images/potential-issues.png " ")

4. Click on the **Outliers** tab.

   These issues occurred only once, and indicate an anomaly in the system.

   **Outliers:** Number of clusters that have occurred only once during a given time period

      ![Fleet Summary](./images/outliers.png " ")

5. Correlate logs based on **Trends** tab.

   **Trend**: Number of unique trends during the time period. Many clusters may have the same trend. These are log cluster patterns that are correlated in time.

   Click on the **Trends** tab in the Cluster Visualization,

      ![Fleet Summary](./images/trends.png " ")

   Scroll down to find the cluster shown in the screenshot below.

      ![Fleet Summary](./images/similar-trends.png " ")

   Next, click on "2 similar trends" to see a set of related logs from the Concurrent Manager and Linux OS.

   *Note that the exact number of displayed trends may vary based on the selected time window.*

   ![Fleet Summary](./images/similar-trends-view.png " ")

   These are the clusters that had the same shape (i.e. occuring at the same time) to as the selected cluster pattern in time. In this case these are the messages issued by Concurrent Manager for a failing job.

## Task 4: Explore examples of Tile Layout in Link

1. Click on the **Link** Visualization from the Visualizations panel.

      ![Fleet Summary](./images/link.png " ")

2. Presented here is an example implementation of query in link that you can customize for your requirement. Enter the following SQL in the query section (copy & paste the statement)

      ```
            <copy> * | eval 'Raw Size (bytes)' = unit('Raw Size', byte) | link includenulls = true 'Log Source', Entity, cluster() | stats sum('Raw Size (bytes)') as R | addfields [ * | where 'Potential Issue' = '1' | eventstats count as I ], [ * | where Count = 1 | eventstats count as O ] | eval 'Query Duration' = 'Query End Time' - 'Query Start Time' | eventstats distinctcount('Log Source') as L, distinctcount(Entity) as E, sum(Count) as Logs, sum(R) as Size, max(I) as I1, max(O)
      as O1 | eval QS = formatDate('Query Start Time') | eval QE = formatDate('Query End Time') | eval URL_LS = replace(replace('https://cloud.oracle.com/loganalytics/explorer?viz=hbar&amp;query=Time%20between%20%27STARTTIME%27%20and%20%27ENDTIME%27%20%7C%20stats%20count%20by%20%27Log%20Source%27', literal(STARTTIME), QS), ENDTIME, QE) | eval URL_E = replace(replace('https://cloud.oracle.com/loganalytics/explorer?viz=pie&amp;query=Time%20between%20%27STARTTIME%27%20and%20%27ENDTIME%27%20%7C%20stats%20count%20by%20%27Entity%27', literal(STARTTIME), QS), ENDTIME, QE) | eval URL_I = replace(replace('https://cloud.oracle.com/loganalytics/explorer?viz=cluster&amp;query=Time%20between%20%27STARTTIME%27%20and%20%27ENDTIME%27%20%7C%20cluster', literal(STARTTIME), QS), ENDTIME, QE) | eval URL_O = replace(replace('https://cloud.oracle.com/loganalytics/explorer?viz=cluster&amp;query=Time%20between%20%27STARTTIME%27%20and%20%27ENDTIME%27%20%7C%20cluster', literal(STARTTIME), QS), ENDTIME, QE) | eval 'Log Sources' = url(URL_LS, toString(L)) | eval E1 = if(E != null, E, 0) | eval Entities = url(URL_E, toString(E)) | eval I2 = if(I1 != null, I1, 0) | eval Issues = url(URL_I, toString(I2)) | eval Outliers = url(URL_O, toString(O1)) |
      fields -L, -E, -I, -I1, -I2, -E1, -O, -O1, -QS, -QE, -URL_LS, -URL_I, -URL_O, -URL_E,
      -'Potential Issue', -R, -'Log Source', -'Start Time', -'End Time', -'Query Duration' | head limit = 3
            </copy>
      ```

3. Click **Run** to execute the query.

      ![Fleet Summary](./images/query.png " ")

4. Use **Tiles** in link visualization to show summary data.

     ![Fleet Summary](./images/tile.png " ")

5. Click on **New** to create a link visualization to show summary data.

     ![Fleet Summary](./images/new.png " ")

6. Modify the XML custom template by copying the below.

      ```
      <copy>
      <summary>
            <container background-color="#80DEEA">
                  <title>
                  <title-text color="#212121" font-size="medium">Summary</title-text>
                  </title>
                  <table>
                        <row>
                              <column>
                              <tiles background-color="#E1F5FE">
                              <tile field="Log Sources"><title><title-text font-size="medium">Log Sources</title-text></title></tile>
                              <tile field="Entities"><title><title-text font-size="medium">Entities</title-text></title></tile>
                              <tile type="separator"/>
                              <tile field="Size"><title><title-text font-size="medium">Size</title-text></title></tile>
                              <tile type="separator"/>
                              <tile field="Issues"><title><title-text font-size="medium">Issues</title-text></title></tile>
                              <tile field="Outliers"><title><title-text font-size="medium">Outliers</title-text></title></tile>
                              </tiles>
                              </column>
                        </row>
                  </table>
            </container>
      </summary>
            </copy>
      ```

7. Click on Save Changes.

      ![Fleet Summary](./images/save-changes.png " ")

8. This shows the **Summary of Issues: Compact Layout**. The following example has one row, one column, packed cards, and vertical separators.

      ![Fleet Summary](./images/final-summary.png " ")

## Task 5: Explore Logs using Issues Visualization

1. Click on the **Issues** Visualization from the Visualizations panel.

      ![Fleet Summary](./images/issues.png " ")

2. This dashboard shows the **Cluster Compare by Time Shift**. To generate useful analytics by reducing the number of clusters to only the clusters that are unique in the current time period, then use the **Time Shift** option.

      ![Fleet Summary](./images/cluster-comparison.png " ")

3. This is the default option available with the cluster compare utility. You can modify the baseline time range upto maximum of 7 days.

      ![Fleet Summary](./images/cluster-default.png " ")

4. Using this data, you can identify the unique potential issue in the current week, and find a root-cause. Narrow down your selection of log records to those are the cause for the potential issue.

*Note: The time shift value is subtracted from the start and end of the current time. If the time shift is less than the duration of the current time, there will be an overlap. This will show all the common (duplicate) clusters from that overlap period. A message will be shown when this is detected. In such a case, the baseline query is the same as the current query.*

## Acknowledgements

- **Author** - Sindhuja Banka, HeatWave MySQL Product Manager
- **Contributors** - Sindhuja Banka, Anand Prabhu, Sriram Vrinda
- **Last Updated By/Date** - Sindhuja Banka, March 2025
