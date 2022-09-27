# Log Exploration using Logging Analytics Dashboard.

## Introduction

This lab will walk you through the steps to visualize the log from the OKE Cluster.

### About
In this lab we will be exploring
* Dashboards - 
* Widgets - 


### Objectives

In this lab, you will:
* Visualize the data from the OKE Cluster through Dashboards and Widgets.

### Prerequisites

* **Ingestion Flow Setup** and **Custom Log Collection** lab should be completed

Estimated Time: 30 minutes

## Task 1: Visualization with Dashboards and Widgets
// To Be Replaced with the Direct URL for Kubernetes Cluster Overview.

1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Dashboards**

2. A Dashboard page will be displayed. This page will list the pre-created Dashboards.

3. Click on the **Kubernetes Cluster Overview** Dashboard from the table.

4. **Kubernetes Cluster Overview** page will be displayed.
    ![kubernetes-cluster-overview](images/kubernetes-cluster-overview.png)

5. Select the time range as **Last 7 Days** from the Time Range Picker.
    ![last-7-days](images/last-7-days.png)    

6. Click on the Filter Panel button.
    ![filter-panel](images/filter-panel.png)



7. Key in the **Compartment** value obtained from the Terraform Values Frame in the Log Group Compartment textbox. The compartment value will be in the format **LL-12345** .
    ![log-group-compartment](images/log-group-compartment.png)
    
8. Key in the **Kubernetes Cluster Name** value obtained from the Terraform Values Frame.
    ![kubernetes-cluster-name](images/kubernetes-cluster-name.png)

9. You should be able to see the all the widgets displaying the data specific to your OKE Cluster.
     ![cluster-specific-view](images/cluster-specific-view.png)

## Task 2: Overview of Widgets

1. **Logs**
    - This widget displays all the total number of logs ingested from the selected OKE Cluster in the specified time range.
    - OCI Logging Analytics can collect and manage millions of records.
      ![widget-logs](images/widget-logs.png) 
    - Click on the View Query Icon to view the query used to populate the data in widget.   
      ![view-query-icon](images/view-query-icon.png)  
    - The query used to populate the data will be displayed.
      ![view-query](images/view-query.png) 
    - The detailed explaination of this widget is discussed in Task #3.     

2. **Namespaces**
    This widget displays total number of namespaces present in the selected OKE Cluster.
      ![widget-namespace](images/widget-namespace.png)  

3. **Log Types**

    - This widget displays different log types from the cluster.

    - We collect 20+ types of logs from the cluster, and this covers all the tiers of the cluster such as Node, Pods, Container etc.

    - All the tiers of the cluster are shown in the chart legends. 
      ![widget-log-types-legends](images/widget-log-types-legends.png)    

    - Click on the each legend to view the trends of the corresponding log.

4. **Cluster Components**
    - This widget displays the different components of the cluster such as Cluster Name, number of Nodes and number of Pods.
      ![widget-cluster-components](images/widget-cluster-components.png)  

5. **Events From Pods**
    - This widget displays the events from all the pods of the selected cluster  
      ![widget-events-from-pods](images/widget-events-from-pods.png)  

6. **Connections Trend**  
    - This widget displays the newtwork connection trends in the selected OKE Cluster.
    - Hover over any point to view the newtwork connections in the cluster, the chart will be displayed.
      ![widget-connections-trends](images/widget-connections-trends.png)  
    - The chart aggregates and groups the connections based on the direction (inbound or outbound), IPs involved and the number of connections.          

  // To Be Updated after the discussion - CPU and Memory Utilization, Network Transmit and Receive and Threads and Processes

## Task 3: Deep Dive into Logs Widget

1.  Click on the Punch Out Icon on the Logs widget.
    ![punch-out-icon](images/punch-out-icon.png)  

    This will take you to the "Tile view" of Log Explorer in context of **Kubernetes Cluster Name** .
    ![log-explorer-tile-view](images/log-explorer-tile-view.png)

2. Select the visualization "Records with Histogram". This will take you to the "Records with Histogram view" in context of **Kubernetes Cluster Name**.
   The bar chart  shows the trends of the logs.
    ![records-with-histogram-view](images/records-with-histogram-view.png)


3. Click on the Other icon in the Fields Panel to view all the other fields automatically parsed from the cluster logs. 
    ![other-icon](images/other-icon.png)
   
4. In the Fields panel, in the _Search Fields_ textbox, search for the field **Node**.
    ![node-field](images/node-field.png)   

5. Drag and Drop the **Node** field in the **Group by** textbox under **Visualization Panel** and click **Apply**.
    ![group-by-node](images/group-by-node.png)  
   The results will be grouped by Node.
    ![histogram-group-by-nodes](images/histogram-group-by-nodes.png)  

6. Select the "Pie Chart" visualization.  
    ![pie-chart-view](images/pie-chart-view.png)
   The query carries over the group by automatically and the data in step #4 will be represented in the "Pie Chart" view. 
    ![pie-chart-node-data](images/pie-chart-node-data.png)

7. Select the "Tree Map" visualization.  
    ![tree-map-view](images/tree-map-view.png)
   
   In the Fields panel, in the _Search Fields_ textbox, search for the field **Pod**.
     ![pod-field](images/pod-field.png)
   
   Drag and Drop the **Pod** field in the **Group by** textbox under **Visualization Panel** and click **Apply**.
     ![group-by-pod](images/group-by-pod.png)

   The results will be grouped by Node and Pod.
   // Screenshot To Be Updated once the fix is available.
    ![group-by-node-pod](images/group-by-node-pod.png)


**Congratulations!**, you have successfully visualized the data from the OKE Cluster through Dashboard and Widgets. Kindly proceed  to next lab.
## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics, Madhavan Arnisethangaraj, OCI Management Agent
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022
