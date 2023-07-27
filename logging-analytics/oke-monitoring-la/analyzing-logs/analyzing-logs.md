# Analyzing Logs

## Introduction

  In this lab, you'll explore the logs collected by Kubernetes Monitoring Solution you deployed in [previous lab](#prev). You'll also do basic analysis of the logs collected and learn types of logs are collected.

### Objectives

- Understand the data model of telemetry collected by kubernetes monitoring solution
- Gather information about the monitored OKE Cluster interactively in Log Explorer


Estimated Time: 30 minutes

## Task 1: View the Logs in Log Explorer
1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Log Explorer**.
    > Note : For a quick refresher on Log Explorer GUI [review Lab 1](?lab=log-explorer-gui).

2. Once you land on the **Log Explorer** page if the scope has pre-selected **Log Group Compartment**, then you can reset it by clicking on the `x` icon.
   ![close-icon-for-scope-filter](images/close-icon-for-scope-filter.png)
    
    > Note: If you have followed this step you can skip the below step.
   
   **OR**

   In the following steps we will select the **emdemo(root)** **Compartment** to view the various logs.
   
    - Click on the **Scope** filter, select the **emdemo(root)** **Compartment** into **Log Group Compartment** dropdown textbox and click **Apply** button.
    ![select-root-compartment](images/select-root-compartment.png)

    - Click on **Close** button

3. Clear the **Query** bar if it has any query present in it by clicking on the `x` icon and click on **Run** button.
    ![close-icon-query-bar-run-button](images/close-icon-query-bar-run-button.png)


4. Add Log Group Field to Group By. 


    - In the Fields panel, in the Search Fields textbox, search for the field **Log Group**.
    - In the resultant field, click on the three vertical dots menu icon.
    - Click on the **Add to Group By** menu option.
       ![log-group-add-to-groupby](images/log-group-add-to-groupby.png)
    - The **Log Group** field will be added in the **Group by** textbox under Visualization Panel. Click **Apply** button to apply the changes.
       ![drag-drop-log-group-field](images/drag-drop-log-group-field.png)   


5. The **Pie** chart view in the context of **Log Group** will be displayed along with logrecords count for each **Log Group**.
      > Note : The **Log Group** <em>kubernetes_logs</em> is precreated and it has VCN, LBaaS logs and it also has a copy of Kubernetes Logs ingested through Kubernetes Cluster **oke-cw23-II**.
   
   ![pie-chart-view-log-count](images/pie-chart-view-log-count.png) 

**OR**

5. (Optional) You can also use the following query in the **Query Bar** to get the **Pie Chart** view in the context of **Log Group**.

     ```
      <copy>
        * | stats count as logrecords by 'Log Group' | sort -logrecords
      </copy>
     ```

6. **End Notes** : Keep the same set up and perform the following actions.

  - Select the Visualization **Sunburst** from the Visualization drop-down.
      ![sunburst-visualization](images/sunburst-visualization.png)

  - Add the field **Log Source** to the **Group by** by following the instructions in step 4.
      
      > **Note :** Do Not Remove **Log Group** field from the **Group by**.

  - The **Sunburst** chart view in the context of **Log Group** and **Log Source** along with log record **Count** for each **Log Source** is displayed.
      ![sunburst-data-lg-ls](images/sunburst-data-lg-ls.png)

  - You can also hover over different colors of **Sunburst** chart to view the stats of the **Log Source**.
         



## Task 2 (To Be Removed as Task 1 End Notes Cover This): Review Logs in Log Groups

1. Select the visualization **Horizontal Bar**. This will take you to the **Horizontal Bar** view in context of **Log Group** along with logrecords count for each **Log Group**.
    ![horizontal-bar-view](images/horizontal-bar-view.png)
    ![log-records-horizontal-bar-view](images/log-records-horizontal-bar-view.png)
    

2. In the Fields panel, in the Search Fields textbox, search for the field **Log Source**.
    ![log-source-field-search](images/log-source-field-search.png)


3. Drag and Drop the **Log Source** field in the **Group by** textbox under Visualization Panel and click **Apply**.
    ![group-by-logsource-loggroup](images/group-by-logsource-loggroup.png)  

4. The results will be grouped by **Log Source** and **Log Group**.
    ![horizontal-bar-view-for-loggroup-logsource](images/horizontal-bar-view-for-loggroup-logsource.png)  


5. You can also use the following query in the **Query Bar** to get the view the results.
    > **Note:** Run this query only after step 1 is finished.

      ```
         <copy>
           * | stats count as logrecords by 'Log Group', 'Log Source' | sort -logrecords
          </copy>
       ``` 

6. (Optional) You can select any other visualization (e.g Sunburst, TreeMap etc) from the  **Visualizations** panel to view the data.  


## Task 3 (To Be Updated and Task 5 will be removed): Get inventory of namespace, pods, services, nodes for your cluster

### **Review Cluster**

1. Select the visualization **Distinct**.
    ![distinct-visualization](images/distinct-visualization.png)  

2. In the Fields panel, in the Search Fields textbox, search for the field **Kubernetes Cluster Name**. Click on the resultant field **Kubernetes Cluster Name**.
    ![k8s-cluster-name](images/k8s-cluster-name.png)  

3. **Filter Kubernetes Cluster Name** pop-window will be displayed. All the Kubernetes Cluster Names will be displayed.

    ![filter-k8s-cluster-name](images/filter-k8s-cluster-name.png)

4. Click on **Cancel** Button.

5. Clear the field **Kubernetes Cluster Name** in the Fields panel's Search Fields textbox by clicking `x` button.


### **Review Namespace**

1. In the Fields panel, in the Search Fields textbox, search for the field **Namespace**. Click on the resultant field **Namespace**.
   ![k8s-namespace](images/k8s-namespace.png) 

2. **Filter Namespace** pop-window will be displayed. All the Kubernetes Namespaces will be displayed. 
   ![k8s-namespace](images/filter-k8s-namespace.png) 

3. Click on **Cancel** Button.

4. Clear the text **Namespace** in the Fields panel's Search Fields textbox by clicking `x` button.    


### **Review Pods**

1. In the Fields panel, in the Search Fields textbox, search for the field **Pod**. Click on the resultant field **Pod**.
   ![k8s-pod](images/k8s-pod.png) 

2. **Filter Pod** pop-window will be displayed. All the Pods will be displayed. 
   ![k8s-pod](images/filter-k8s-pod.png) 

3. Click on **Cancel** Button.

4. Clear the field **Pod** in the Fields panel's Search Fields textbox by clicking `x` button.   
  

### **Review Nodes**

1. In the Fields panel, in the Search Fields textbox, search for the field **Node**. Click on the resultant field **Node**.
   ![k8s-pod](images/k8s-node.png) 

2. **Filter Node** pop-window will be displayed. All the Nodes will be displayed. Click on the checkbox of `Show Trend Chart`.
   ![k8s-pod](images/filter-k8s-node.png) 

3. Click on **Cancel** Button.

4. Clear the field **Node** in the Fields panel's Search Fields textbox by clicking `x` button.


## Task 4 : Building Interactive Visualization for Deployments

 In this task we will find what type of workloads are running in different namespaces and the names of those workloads.

1. Select the visualization **Distinct**.
  ![distinct-visualization](images/distinct-visualization.png)

2. Add Namespace Field to Group By. 


    - In the Fields panel, in the Search Fields textbox, search for the field **Namespace**.
    - In the resultant field, click on the three vertical dots menu icon.
    - Click on the **Add to Group By** menu option.
       ![ namespace-to-group-by.png](images/namespace-to-group-by.png)
    - The **Namespace** field will be added in the **Group by** textbox under Visualization Panel. 
       ![namespace-added-to-group-by](images/namespace-added-to-group-by.png) 
      > **Note :** The Group By textbox allows a maximum of 4 fields in the Distinct Visualization. Hence remove all the other fields apart from **Namespace**   

       

3. Repeat the instructions in the step 2 to add fields **Controller** and  **Controller Kind**.
     > **Note :** Remove all the other fields apart from **Namespace** , **Controller** and  **Controller Kind** from the Group by textbox. 

4. The **Group by** section should look like the following. Click on the **Apply** button to apply the changes. 
   ![group-by-controller-namespace-controllerkind](images/group-by-controller-namespace-controllerkind.png)   

5. The results will be grouped by **Namespace** , **Controller** and **Controller Kind**. 
   ![distinct-view-namespace-controller-controllerkind](images/distinct-view-namespace-controller-controllerkind.png) 

6. In the results look for your user's **Namespace** by scrolling in the **Field Value** column . The **Namespace** can be found from the **View Login Info** page with the field name **Kubernetes Namespace**.
         
      > **Note :** The **Namespace** will  be in the format **resrReservationId**.  



    i. Click on expand icon to view the different resources (Controller) created in your user's Namespace. 
     ![expand-icon-for-k8s-namespace](images/expand-icon-for-k8s-namespace.png) 


   ii. Click on expand icon of **oci-onm-logan** resource to see kind (Controller Kind) of the resource. It displays Daemonset & Deployment created as part of Kubernetes Solution installation performed in the [previous lab](#prev). 
     ![expand-icon-for-controller](images/expand-icon-for-controller.png) 


   iii. Repeat the step ii to view the Controller Kind of other resources which are created as part of the Kubernetes Solution installation.

   > Note : Upon expanding the Namespace icon we can also see No Value, need to check with Santhosh.
     

## Task 5 (To Be Removed) : Find number of total pods, running pods in a namespace

  > **Note** : Before moving on to the next steps. Clear the query bar and click on **Run**.

1. Select the visualization **Pie Chart**.
  ![distinct-visualization](images/distinct-visualization.png)

2. In the Fields panel, in the Search Fields textbox, search for the field **Namespace**. Click on the resultant field **Namespace**.
   ![k8s-namespace](images/k8s-namespace.png) 

3. **Filter Namespace** pop-window will be displayed. All the Kubernetes Namespaces will be displayed. 
   ![k8s-namespace](images/filter-k8s-namespace.png)

4. You can select any namespace value from the list - for e.g **default**. Click on the **Apply**.
   ![select-default-namespace](images/select-default-namespace.png)

5. Clear the field **Namespace** in the Fields panel's Search Fields textbox by clicking `x` button.   

6. In the Fields panel, in the Search Fields textbox, search for the field **Status**. Click on the resultant field **Status**.
   ![k8s-pods-status](images/k8s-pods-status.png) 

7. **Filter Status** pop-window will be displayed. All the pods status' will be displayed. 
   ![filter-k8s-pods-status](images/filter-k8s-pods-status.png) 

8. Select the status value **running** . Click on the **Apply**.
   ![select-running-pod-status](images/select-running-pod-status.png)

9. Clear the field **Status** in the Fields panel's Search Fields textbox by clicking `x` button.   

10. In the Fields panel, in the Search Fields textbox, search for the field **Namespace**.
   ![k8s-namespace](images/k8s-namespace.png) 

11. Drag and Drop the **Namespace** field in the **Group by** textbox under Visualization Panel and click **Apply**.
    ![group-by-namespace](images/group-by-namespace.png)

12. Clear the field **Namespace** in the Fields panel's Search Fields textbox by clicking `x` button. 

13. In the Fields panel, in the Search Fields textbox, search for the field **Pod**.
   ![k8s-pod](images/k8s-pod.png) 

14. Drag and Drop the **Pod** field in the **Value** textbox under Visualization Panel.
    ![pod-field-in-value](images/pod-field-in-value.png)   

15. Click on the Drop Down icon in the **Value** textbox. Select the **Distinct Count** menu item.
    ![distinct-value-menu-item](images/distinct-value-menu-item.png)   

16. Click on the **Apply** button.

17. The count of all the distinct running Pods in the selected Namespace will be displayed.
    ![distinct-running-pods-namespace](images/distinct-running-pods-namespace.png) 

18. The query in the query bar will be following.
    ```
      <copy>
        Namespace = default and Status = running | stats distinctcount(Pod) by Namespace
      </copy>

    ```  

19. Edit the query and provide the Name to the `distinctcount(Pod)` using the **as** operator. 
     - In the following query we used as operator and provided the Name `'Running Pods'` to the `distinctcount(Pod)`. 
     - You can copy and paste the following query in the **Query Bar**.

        ```
          <copy>
             Namespace = default and Status = running | stats distinctcount(Pod) as 'Running Pods' by Namespace
          </copy>

        ``` 
      - The column name will be changed to **Running Pods**.
      ![running-pods-as-operator](images/running-pods-as-operator.png) 

   > **Note** : Click the **x** icon in the query bar and click on the **Run** button before  moving to next Task.   

      

    


## Task 6 : Viewing Kubernetes Events

1. Run the following query in the Query Bar.
        ```  
            <copy>
                'Log Source' = 'Kubernetes Event Object Logs' | timestats count as logrecords by 'Log Source'
            </copy>
        ``` 
        ![query-bar-with-k8s-event-objects.png](images/query-bar-with-k8s-event-objects.png) 

2. Select the visualization **Table**.
  ![table-visualization](images/table-visualization.png)

3. Add fields to the Display Fields.
    - In the Fields panel, in the Search Fields textbox, search for the field  **Involved Object Kind**.
         > **Note** : Kubernetes objects are persistent entities in the Kubernetes system and are used to represent the state of your cluster.  Read more about Kubernetes Objects [here](https://kubernetes.io/docs/concepts/overview/working-with-objects/).  

    - In the resultant field, click on the three vertical dots menu icon. 
    - Click on **Add to Display Fields** menu icon.
       ![add-to-display-fields.png](images/add-to-display-fields.png)

4. Repeat the step 3 for the fields **Involved Object Name** & **Event Type**.
      > **Note** : Remove all the other fields apart from **Involved Object Kind** , **Involved Object Name** & **Event Type**  from the **Display Fields** textbox.

5. The Display fields textbox will look like the following after adding the fields **Involved Object Kind** , **Involved Object Name** & **Event Type**. 

      Click on the **Apply** button.
      ![k8s-event-obj-display-fields](images/k8s-event-obj-display-fields.png )

6. The **Table** view in context of **Kubernetes Event Object Logs** Log Source will be displayed.
   ![k8s-event-object-table-view](images/k8s-event-object-table-view.png)

7. Click on the expand field button to view all the extracted fields of a log entry. You can now see that various important information from the log entry has been extracted into different fields which can be further used for filtering and various analytics. 

    ![expand-icon-log-entry](images/expand-icon-log-entry.png)

> **Note** : We will use this set up to create the Dashboard in the next step.      



## Task 7 : Add Visualization to the Dashboard

1. Select the visualization **Bar**.
   ![bar-chart-visualization](images/bar-chart-visualization.png)

2. The **Bar** chart view in context of **Kubernetes Event Object Logs** Log Source will be displayed.
   ![bar-chart-view-k8s-event-object](images/bar-chart-view-k8s-event-object.png)

3. Click on the **Actions** button.
   ![actions-button.png](images/actions-button.png)

4. Click on the **Save as** option.
   ![save-as-button](images/save-as-button.png)

5. A **Save search** pop up will be displayed. By default your user's **Compartment** in selected in **Save Search Compartment** dropdown.
   ![save-search-popup](images/save-search-popup.png)
    > Note : You will see the Authorization error if any other **Compartment** is selected in **Save Search Compartment** dropdown.

6. In the  **Save search** pop up perform the following actions.
   
    - (Optional) Type the **Compartment** name in the **Saved Search Compartment** for your user the **Compartment** name will be **LLresrvationid-COMPARTMENT**.  You can always find the **Compartment** name from the View Login Info page.
        > Note : This step is optional if you have not changed the **Compartment** in step 5.
        

    - Enter the **Search Name**.
    - Check the **Add to dashboard** checkbox.
    - Select the **New Dashboard** radio button.
    - Select the **Dashboard Compartment** name. Make sure that you select the same **Compartment** for Dashboard and Save Search.
    - Enter the **Dashboard Name**. 
    - Click on **Save** button.
    ![create-dashboard](images/create-dashboard.png)
    - A saved search will be created and added to the Dashboard.
    ![save-search-and-dashboard-confirmation](images/save-search-and-dashboard-confirmation.png)  

7. Click on the drop-down on top left side of the Log Explorer Page and select **Dashboards**.
    ![dashboard-navigation](images/dashboard-navigation.png)

    **OR**

   Copy-paste the following link in your browser's address bar to navigate to the **Dashboards**.
      ```
         <copy>
           https://cloud.oracle.com/loganalytics/dashboards?region=us-phoenix-1
         </copy>
     
      ```

8. A Dashboards Page will be displayed. Click on the Dashboard Name that you have created in the Step 5.
    ![dashboards-page](images/dashboards-page.png)

9. A widget showing the saved search data will be displayed.
    ![dashboard-with-widget](images/dashboard-with-widget.png)


## Task 8 : Collecting Application Logs (Custom Log Sources)

1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Log Explorer**.

   **OR**

  You can also copy-paste the following link in your browser's address bar to navigate to the Log Explorer.
    ```
         <copy>
            https://cloud.oracle.com/loganalytics/explorer?region=us-phoenix-1
         </copy>   
    ```

2. Run the following query in the **Query Bar**.

    ```  
      <copy>
       'Log Source' = 'mushop-orders-app' | timestats sum('Sales Amount') as Revenue
      </copy>
    ``` 

3. The previous step takes you to the **Records with Histogram** view in context of **mushop-orders-app** Log Source.
   ![mushop-orders-app-data](images/mushop-orders-app-data.png)

4. Click on the expand field button to view all the extracted fields of a log entry of **mushop-orders-app** Log Source.
    ![expand-icon-mushop-orders-app](images/expand-icon-mushop-orders-app.png)

5. Select the visualization **Line**.
  ![line-chart-visualization](images/line-chart-visualization.png)

6. The previous step takes you to the **Line** chart view in context of **mushop-orders-app** Log Source displaying the **Time** in the X-axis and **Revenue** in the Y-axis for last 60 Minutes.
  ![line-chart-view-mushop-orders-log-source](images/line-chart-view-mushop-orders-log-source.png)

7. End Note : Change the values in the Time Picker to **Last 24 Hours**, **Last 14 Days** etc and check whether the line chart changes.  


## Task 9 : Find average daily  sales amount

   We looked at the trend of revenue in previous task. In this task we want to find out average **Sales Amount** that is processed.    

1. Select the visualization **Pie Chart**.
   ![pie-chart-visualization](images/pie-chart-visualization.png)


2. Run the following query in the **Query Bar**.

    ```  
      <copy>
        'Log Source' = 'mushop-orders-app' | stats count as logrecords by 'Log Source'
      </copy>
    ```

3. Add the field **Sales Amount** to the Value textbox.
      - In the Fields panel, in the Search Fields textbox, search for the field  **Sales Amount**.
      - In the resultant field, click on the three vertical dots menu icon. 
      - Click on **Add to Value** menu icon.
         ![sales-amount-add-to-value](images/sales-amount-add-to-value.png)
      - The **Value** textbox will look like the following.
         ![value-field-with-count-sales-amount](images/value-field-with-count-sales-amount.png)



4. Click on the Drop Down icon in the **Value** textbox. Select the **Average** menu item. Click **Apply** button.
     ![avg-sales-amount](images/avg-sales-amount.png)    

5. The daily average sales values will be dispalyed.
     ![daily-avg-sales-amount](images/daily-avg-sales-amount.png)

 6. Food For Thought - Do you think this value is correct? 
    
    
      > **Hint** : In the begining of this Lab we selected root compartment which has two **Log Group** and we learnt that the **Log Group** <em>kubernetes_logs</em> has the copy of the Kubernetes Logs ingested through Kubernetes Cluster **oke-cw23-II**. Refer **Task 1** > **Step 5** > **Note** to ascertain this.

7. Retrieveing the correct value of the daily average sales.
  - Clear the field **Sales Amount** in the Fields panel's Search Fields textbox by clicking `x` button.
  - Click on the field **Log Group**  in the Fields panel.
     ![field-log-group](images/field-log-group.png)
  -  **Filter Log Group** pop-window will be displayed.
  - Select your user's **Log Group**. 
  - Click on **Apply** button.
  - Now you will be able to see the correct value of the daily average sales.

         
                 
## Task 10 : Workshop Show and Tell

You'll get the opportunity to showcase your dashboard at the end of the lab. You can add any visualization that you like to your dashboard - here are few examples.
  - Find average number of orders per day, per hour ?
  - Which day had maximum number of orders ?
  - Which product was ordered most ?
  - Which city or region is at the top from total orders ?
  - What about sales amount perspective ?

**Congratulations!** In this lab, you have successfuly completed the following tasks:
- TO BE UPDATED

  You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Jul, 2023
