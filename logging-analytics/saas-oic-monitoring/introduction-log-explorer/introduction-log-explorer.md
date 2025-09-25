# Lab 1 -  Introduction to Log Explorer 

## Introduction

This lab walks you through Log Explorer in OCI Console and various sections within it.
OCI Log Explorer is a visual interface in OCI Log Analytics used to:
    - Search and analyze log data.
    - Apply filters and queries.
    - Use visualizations like timelines, bar charts, and tables.
    
   To understand more about Log Explorer refer  [documentation](https://docs.oracle.com/en-us/iaas/log-analytics/doc/visualize-data-using-charts-and-controls.html#GUID-93988D5B-9717-4F63-8362-16B08BC3E020__SECTION_OL5_STR_V5B).

Estimated Time: 5 minutes

### Objectives
In this lab, you will learn to 
   -  Navigate to Log Explorer in OCI Console
   -  Learn about different UI sections of Log Explorer
   -  Understand key features of Log Explorer


## Task 1: Navigate to Log Explorer in OCI Console

  1. The Log Analytics service is available from the top level OCI console menu.
   ![top-level](images/top-level-hamburger-menu.jpg) 
 
 2.  Navigate to Observability & Management and click Log Explorer within Log Analytics.  
    ![log-explorer](images/log-explorer.jpg)


## Task 2: Learn different section of Log Explorer

- The different sections of Log Explorer are 
 ![log-explorer-section](images/log-explorer-section.jpg)
 
      1. Query bar, with Clear, Search Help, and Run buttons at the right end of the bar.
      2. Time range menu, and Actions menu where you can find actions such as, Open, Save, and Save as.
      3. Fields panel, where you can select sources and fields to filter your data.
      4. Visualization panel, where you can select the way to present search data in a form that helps you.
      5. Main panel, where the visualization outputs appear above the results of the query.
      6. Compass, which can be used to add data,videos ,sample data.


## Task 3: Understand key features of Log Explorer

1. Click on **Compass** icon  present on the  right hand side of the page. ![compass](images/compass.jpg)  This will open the compass section that comprises of -
      - Add Data
      - Videos
      - Tips
      - What's New
      - Sample Log Data

   **Enable** the **Sample Log Data**  in order to populate the Log Explorer with predefined sample logs.
    ![enable-log-data](images/enable-log-data.jpg)

    After enabling log data close the **Compass Section**.

2. In **Main Panel**  the results of the query is displayed along with visualization.The interactive data visualizations in OCI Log Analytics enable you to get deeper insights into your log data. Depending on the data you want to filter, group, and compare, you can choose various visualization types, from a rich set of options within **Visualization Panel**  ![main-panel](images/main-panel.jpg)
**Pie Chart** is one of the visulaization available in log explorer that shows the overall composition of a data set by encoding the percentage values in angles. It is a circular representation of the count of the log records that are grouped using the input parameter.
   ![pie-chart](images/pie-chart.jpg)

3. **Fields Panel**  - The Fields panel of Oracle Log Analytics lists the field attributes based on which you can filter log data. The fields can be searched or can be put into different buckets as per usage. The different sections of fields panel are -
![field-panel](images/field-panel.jpg)
      1. Search Field 
      2. Pinned
      3. Computed
      4. Other 
    

4. Set **Time range**  to **Last 24 Hours**. ![time-range](images/time-range.jpg)

5. Search for **Label** in **Search Field**.  ![field-search](images/field-search.jpg)

6. Click on Label and Select **Log Writer Switch** and **Checkpoint Wait** and click on Apply. 
![label-view](images/label-view.jpg)

7. Accordingly the query within the query bar changes and label selected is added to it and hence log records and pie chart gets updated. ![query-pie-chart](images/query-pie-chart.jpg)

8. Within **Vizualization Panel** , change visualization to **Records with Histogram** ![histogram](images/histogram.jpg)

9. The visualization changes from Pie Chart to Records with Histogram. Browse to second log entry and Click on Message field and right click on it. One can see various menu option available there like 'Add to Search', 'Exclude from search', 'Enrich source' etc.
![message-menu](images/message-menu.jpg)

**Congratulations!** In this lab, you have successfuly completed the following tasks:
- Understanding Log Explorer

You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Supriya Joshi, OCI Log Analytics
* **Contributors** -  Supriya Joshi, Jolly Kundu, Kumar Varun, Royce Fu
* **Last Updated By/Date** - Supriya Joshi, Jul, 2025
