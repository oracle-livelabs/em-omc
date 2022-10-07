# Log Exploration using Logging Analytics Dashboard.

## Introduction

This lab will walk you through the steps to visualize the data collected from the OKE Cluster through Dashboards.

### About
In this lab we will be exploring
* Dashboards: A data visualization tool that gathers real-time data from the various tiers of Kubernetes Cluster.
* Widgets: A component that displays the real-time data.


### Objectives

In this lab, you will:
* Visualize the data collected from the OKE Cluster through Dashboards.

### Prerequisites

* **Ingestion Flow Setup** and **Custom Log Collection** labs should be completed

Estimated Time: 30 minutes

## Task 1: Visualization with Dashboards and Widgets

1. Copy-paste the following link in your browser's address bar to navigate to the Dashboard. **Kubernetes Cluster Overview** page will be displayed.
    
      ```
        <copy>
          https://cloud.oracle.com/loganalytics/dashboards?id=ocid1.managementdashboard.oc1..aaaaaaaaad24nv2zeottsuszcmklnoegmh3kqeelnvja6tp7gso4rmo6ze5a
        </copy>
      ```
    ![kubernetes-cluster-overview](images/kubernetes-cluster-overview.png)

  >**Note:** The logs ingested from your **Kubernetes Cluster** as part of [Lab 2](?lab=ingestion) and [Lab 3](?lab=custom-log-collection) will exists in your **Log Group Compartment**. Thus few widgets will be empty till we set these fields, which will be performed in the next steps. 

2. Click on the **Scope Filter** panel.
    ![filter-panel](images/filter-panel.png)
    ![scope-panel](images/scope-panel.png)

3. Key in the **Compartment** value in the **Log Group Compartment** field and **Kubernetes Cluster Name** value in the **Kubernetes Cluster** field.
    ![compartment-cluster](images/compartment-cluster.png)

   > **Note:** Refer to the **Kubernetes Cluster Name** field in [Lab2 Task1](?lab=ingestion#Task1:GatheringRequiredInformation) for **Kubernetes Cluster** value.
    
4. You should be able to see the all the widgets displaying the data specific to your OKE Cluster.
     ![cloud-oracle-loganalytics-dashboard](images/cloud-oracle-loganalytics-dashboard.png)
    

## Task 2: Overview of Widgets

1. **OKE Component Inventory**

     - This widget displays the summary of components for your Kubernetes cluster. You can click on each link to get details for that component. 
      ![oke-component-inventory.png](images/oke-component-inventory.png)  

    -  Click on **Cluster** link. This would open a new tab with the cluster details page. On this page you can view the details of your cluster.
      ![cluster-details](images/cluster-details.png)  

      >**Note:** The cluster name you see in this page can be different from the one you had in the dashboard page. This is because we are using a single physical cluster in the backend for the purposes of this workshop.

    - Switch back to the Dashboard tab and click on the number of **Nodes** link. This would open a new tab with the node details page.

    - Click on the Scope filter icon and select the **Log Group Compartment** as your **Compartment**, and click **Apply**.
      ![log-group-compartment-select](images/log-group-compartment-select.png)

     - Click on **Close** button  

    - Node specific details will be displayed.  
      ![node-specific-details](images/node-specific-details.png)

    - Switch back to the Dashboard tab.


2. **Logs**
    - This widget displays all the total number of logs ingested from the selected OKE Cluster in the specified time range.
    - OCI Logging Analytics can collect and manage millions of records.
      ![widget-logs](images/widget-logs.png) 
    - Click on the View Query Icon to view the query used to populate the data in widget.   
      ![view-query-icon](images/view-query-icon.png)  
    - The query used to populate the data will be displayed.
      ![view-query](images/view-query.png) 
    - Click on the **Close** button.  
    - The detailed explaination of this widget is discussed in [Task 3](#Task3:DeepDiveintoLogsWidget). 

3. **Log Types**

    - This widget displays different log types from the cluster.

    - We collect 20+ types of logs from the cluster, and this covers all the tiers of the cluster such as Node, Pods, Container etc.

    - All the tiers of the cluster are shown in the chart legends. 
      ![widget-log-types-legends](images/widget-log-types-legends.png)    

    - Click on the each legend to view the trends of the corresponding log. 


4. **Events From Pods**
    - This widget displays the events from all the pods of the selected cluster.  
      ![widget-events-from-pods](images/widget-events-from-pods-1.png)   


5. **CPU Utilization**
    - This metric widget displays the details about CPU and memory utilization for each Node in your Kubernetes cluster.  
      ![cpu-utilization](images/cpu-utilization.png)  

6. **Network Transmit and Receive**
    - This metric widget displays the details about count of bytes received and transmitted by containers in the **mushop** application namespace.    
      ![network-transmit-receive](images/network-transmit-receive.png)

7. **Container Status**   
 
    - This widget displays the overview of all the nodes in your cluster for the selected time period. 

      The x-axis represents Start Time and y-axis represents the Nodes. 

      The summary of each Node at each time interval is displayed as bubble.
      ![container-status](images/container-status.png)  

    - Hover on any bubble to get the details. The following image shows at a given **Start Time** on **Node** 10.20.10.226 there are 31 **Containers** with **Status** running.
      ![hover-over-container-status-bubble](images/hover-over-container-status-bubble.png)  
      
    - Click on any one of the status e.g terminated, the results will be filtered with running and waiting state.
      ![filter-by-running-waiting](images/filter-by-running-waiting.png)  

    - Change the color to **Node** from the dropdown
      ![select-color-node](images/select-color-node.png) 

    - One unique color will be assigned to each node.
      ![unique-color-each-node](images/unique-color-each-node.png) 
          
       

8. **Programs with Outbound Connections**
    - This widget displays the network connection trends in the selected OKE Cluster.
    - Hover over any point to view the network connections in the cluster, the chart will be displayed.
      ![programs-with-outbound-connections](images/programs-with-outbound-connections.png)  
    - The chart aggregates and groups the connections initiated by a **Node** or a **Pod**.  

9. **Pods Error Analysis**           
    - This widget automatically anlyzes all the errors in the cluster logs and summarizes the results.
      The x-axis represents Node and y-axis represents the Pod.
      The summary of each Pod at each time interval is displayed as bubble.
      ![pods-error-analysis](images/pods-error-analysis.png)  

    - Hover on any bubble to get the details. 

      The following image shows that on **Node** 10.20.10.226 for **pod** mushop-edge in the **Namespace** mushop there are two **Issues** for the composite key Groups 2 (Pod and Node). 

      And these two issues constitues the 28.57% of the total issues. 

      For every identified issue, we perform natural language processing (NLP) and extract the relevant keywords.
      ![pods-analysis-hover](images/pods-analysis-hover.png)  
  
    - Change the color to **Node** from the dropdown
      ![select-color-node-pods-error](images/select-color-node-pods-error.png) 

    - One unique color will be assigned to each node.
      ![unique-color-each-pods](images/unique-color-each-pods.png) 

10. **Threads and Processes**
    - This metric widget displays the count of container processes and threads in the **mushop** application namespace.         
      ![threads-and-processes](images/threads-and-processes.png)         

## Task 3: Deep Dive into Logs Widget


1.  Click on the Punch Out Icon on the Logs widget.
    ![punch-out-icon](images/logs-punch-out-icon.png)  

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
    ![group-by-node-pod](images/group-by-node-pod.png)


**Congratulations!**, you have successfully visualized the data from the OKE Cluster through Dashboards. You may now proceed to the [next lab](#next).
## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** - Sreeji Das,  Santhosh Kumar Vuda, Vikram Reddy , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022
