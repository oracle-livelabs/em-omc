# Analyzing Logs

## Introduction

```
  TO BE UPDATED
```

Watch the video below for a quick walk-through of the lab.

### Objectives

```
  TO BE UPDATED
```


Estimated Time: 30 minutes

## Task 1: View the Logs in Log Explorer
1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Log Explorer**.

2. In the following steps we will select the **Compartment** to view the various logs.
    > **Note:** By default root **Compartmemnt** (in this case emdemo(root)) will always be selected. Do not change the **Compartment** throughout this livelab session.

    - Click on the **Scope** filter, select the **emdemo(root)** **Compartment** into **Log Group Compartment** dropdown textbox and click **Apply** button.
    ![select-root-compartment](images/select-root-compartment.png)

    - Click on **Close** button

3. In the Fields panel, in the Search Fields textbox, search for the field **Log Group**.
    ![log-group-field-search](images/log-group-field-search.png)
    

4. Drag and Drop the **Log Group** field in the **Group by** textbox under Visualization Panel and click **Apply**.
    ![drag-drop-log-group-field](images/drag-drop-log-group-field.png)

5. The **Pie** chart view in context of **Log Group** will be displayed along with logrecords count for each **Log Group**.
     ![pie-chart-view-log-count](images/pie-chart-view-log-count.png) 

6. You can also use the following query in the **Query Bar** to get the **Pie Chart** view.

     ```
      <copy>
        * | stats count as logrecords by 'Log Group' | sort -logrecords
      </copy>
     ```


## Task 2: Review Logs in Log Groups

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

## Task 3: Get inventory of namespace, pods, services, nodes for your cluster

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

 

1. Select the visualization **Distinct**.
  ![distinct-visualization](images/distinct-visualization.png)

2. In the Fields panel, in the Search Fields textbox, search for the field **Namespace**. Drag and Drop the **Namespace** field in the **Group by** textbox under Visualization Panel.  

    > **Note** : Remove **Log Source** and **Log Group** field from Group by section.
  
3. In the Fields panel, in the Search Fields textbox, search for the field **Controller**. Drag and Drop the **Controller** field in the **Group by** textbox under Visualization Panel.     

4. In the Fields panel, in the Search Fields textbox, search for the field **Controller Kind**. Drag and Drop the **Controller Kind** field in the **Group by** textbox under Visualization Panel.  

5. The **Group by** section should look like the following. Click on the **Apply** button. 
   ![group-by-controller-namespace-controllerkind](images/group-by-controller-namespace-controllerkind.png)

6.  The results will be grouped by **Namespace** , **Controller** and **Controller Kind**. 
   ![distinct-view-namespace-controller-controllerkind](images/distinct-view-namespace-controller-controllerkind.png)

7. Screenshot to be updated with user namespace and controllers. The below screenshot is not final
   ![expand-user-namespace.png](images/expand-user-namespace.png)


## Task 5 : Find number of total pods, running pods in a namespace

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

      

    


## Task 6 : Viewing Events 

1. Select the visualization **Table**.
  ![distinct-visualization](images/table-visualization.png)

2. Run the following query in the Query Bar.
        ```  
            <copy>
                'Log Source' = 'Kubernetes Event Object Logs' | timestats count as logrecords by 'Log Source'
            </copy>
        ```  

3. In the Fields panel, in the Search Fields textbox, search for the field **Involved Object Kind**.
   ![involved-object-kind](images/involved-object-kind.png) 


4. Drag and Drop the **Involved Object Kind** field in the **Display Fields** textbox under Visualization Panel.
   ![drag-drop-involved-object-kind](images/drag-drop-involved-object-kind.png)   

5. In the Fields panel, in the Search Fields textbox, search for the field **Involved Object Name**.
   ![involved-object-name](images/involved-object-name.png) 


6. Drag and Drop the **Involved Object Name** field in the **Display Fields** textbox under Visualization Panel.
   ![drag-drop-involved-object-name](images/drag-drop-involved-object-name.png)


7. In the Fields panel, in the Search Fields textbox, search for the field **Event Type**.
   ![event-type](images/event-type.png) 


8. Drag and Drop the **Event Type** field in the **Display Fields** textbox under Visualization Panel.
   ![drag-drop-event-type](images/drag-drop-event-type.png)

  > **Note** : Remove the fields **Entity** , **Entity Type** , **Host Name (Server)**, **Problem Priority**, **Label** from the **Display Fields** textbox.

9. Click on the **Apply** button.
   ![apply-button-display-fields](images/apply-button-display-fields.png)


10. The **Table** view in context of **Kubernetes Event Object Logs** Log Source will be displayed.
   ![table-view-k8s-event-log-source](images/table-view-k8s-event-log-source.png)

11. Click on the expand field button to view all the extracted fields of a log entry. You can now see that various important information from the log entry has been extracted into different fields which can be further used for filtering and various analytics. 

    ![expand-icon-log-entry](images/expand-icon-log-entry.png)

> **Note** : We will use this set up to create the Dashboard in the next step.    



## Task 7 : Add Visualization to the Dashboard

1. Click on the **Actions** button.
   ![actions-button.png](images/actions-button.png)

2. Click on the **Save as** option.
   ![save-as-button](images/save-as-button.png)

3. A **Save search** pop up will be displayed.
   ![save-search-popup](images/save-search-popup.png)
    > Note : Getting AuthZ error, needs the fix.

4. In the  **Save search** pop up perform the following actions.
    - Type the **Compartment** name in the **Saved Search Compartment** for your user the **Compartment** name will be **LLresrvationid**
        > Note : You can always find the **Compartment** name from the View Login Info page.

    - Enter the **Search Name**.
    - Check the **Add to dashboard** checkbox.
    - Select the **New Dashboard** radio button.
    - Select the **Dashboard Compartment** name same as step 1.
    - Enter the **Dashboard Name**.
    - Click on **Save** button.
    ![create-dashboard](images/create-dashboard.png)
    - A saved search will be created and added to the Dashboard.
    ![save-search-and-dashboard-confirmation](images/save-search-and-dashboard-confirmation.png)  

5. Click on the drop-down of top left side of the Log Explorer Page and select **Dashboards** 
    ![dashboard-navigation](images/dashboard-navigation.png)

    **OR**

   Copy-paste the following link in your browser's address bar to navigate to the Dashboards.
      ```
         <copy>
           https://cloud.oracle.com/loganalytics/dashboards?region=us-phoenix-1
         </copy>
     
      ```

6. A Dashboards Page will be displayed. Click on the Dashboard Name that you have created in the Step 5.
    ![dashboards-page](images/dashboards-page.png)

7. A widget showing the saved search data will be displayed.
    ![dashboard-with-widget](images/dashboard-with-widget.png)




 


    
 



## Task 8 : Review Custom Log Source

1. Run the following query in the **Query Bar**.

    ```  
      <copy>
        'Log Source' = 'mushop-orders-app' and 'ReceivedCustomer' | timestats count as logrecords by 'Log Source'
      </copy>
    ``` 

2. The previous step takes you to the **Records with Histogram** view in context of **mushop-orders-app** Log Source.

3. Select the visualization **Cluster**.
  ![cluster-visualization](images/cluster-visualization.png)

4. The previous step takes you to the **Cluster** view in context of **mushop-orders-app** Log Source.
  ![cluster-view-mushop-orders-log-source](images/cluster-view-mushop-orders-log-source.png)

5. Next Steps to be updated.  


## Task 9 : Find average daily  sales amount

1. Select the visualization **Pie Chart**.

2. Run the following query in the **Query Bar**.

    ```  
      <copy>
        'Log Source' = 'mushop-orders-app' | timestats count as logrecords by 'Log Source'
      </copy>
    ```



3. In the Fields panel, in the Search Fields textbox, search for the field **Sales Amount**.
   ![mushop-sales-amount](images/mushop-sales-amount.png) 


4. Drag and Drop the **Sales Amount** field in the **Value** textbox under Visualization Panel.
   ![sales-amount-in-value-field](images/sales-amount-in-value-field.png) 

5. Click on the Drop Down icon in the **Value** textbox. Select the **Average Count** menu item. Click **Apply** button.
    

6. The daily average sales values will be dispalyed.
   ![daily-average-sales](images/daily-average-sales.png)
                 
## Task 10 : Workshop Show and Tell

You'll get the opportunity to showcase your dashboard at the end of the lab. You can add any visualization that you like to your dashboard - here are few examples.
  - Find average number of orders per day, per hour ?
  - Which day had maximum number of orders ?
  - Which product was ordered most ?
  - Which city or region is at the top from total orders ?
  - What about sales amount perspective ?



## Task 2: Get list of events for cluster, namespace, pods, services
    
    

## Task 3: Find number of pods by namespace

  

## Task 4: Get different type of events → Group-by different objects → Remove informational events



## Task 5: Get health status of pods, services 



## Task 6: Find pods running on a node



## Task 7: Review fields extracted by custom parser for Mishap Orders App Logs



## Task 8: Find trend of orders



## Task 9: Find total order value 



**Congratulations!** In this lab, you have successfuly completed the following tasks:
- TO BE UPDATED

  You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics, Madhavan Arnisethangaraj, OCI Management Agent
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022
