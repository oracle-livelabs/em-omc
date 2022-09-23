# Log Exploration using Logging Analytics Dashboard.

## Introduction

This lab will walk you through the steps to visualize the log from the OKE Cluster.

Estimated Time: 30 minutes

### About <Product/Technology> 
In this lab we will be exploring
* Dashboards - 
* Widgets - 


### Objectives

In this lab, you will:
* Visualize the data from the OKE Cluster through Dashboards and Widgets.

### Prerequisites

* **Ingestion Flow Setup** and **Custom Log Collection** lab should be completed


## Task 1: Visualization with Dashboards and Widgets

1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Dashboards**

2. A Dashboard page will be displayed. This page will list the pre-created Dashboards.

3. Click on the **Kubernetes Cluster Overview** Dashboard from the table.

4. **Kubernetes Cluster Overview** page will be displayed.
    ![kubernetes-cluster-overview](images/kubernetes-cluster-overview.png)

5. Click on the Filter Panel button shown as below.
    ![filter-panel](images/filter-panel.png)

6. Select the time range as **Last 7 Days** from the Time Range Picker.
    ![last-7-days](images/last-7-days.png)

7. Key in the **Compartment** value obtained from the Terraform Values Frame in the Log Group Compartment textbox. The compartment value will be in the format **LL-12345** .
    ![log-group-compartment](images/log-group-compartment.png)
    
8. Key in the **Kubernetes Cluster Name** value obtained from the Terraform Values Frame.
    ![kubernetes-cluster-name](images/kubernetes-cluster-name.png)

9. You should be able to see the all the widgets displaying the data specific to your OKE Cluster.
     ![cluster-specific-view](images/cluster-specific-view.png)

## Task 2: Overview of Widgets

1. **Logs**
    - This widget displays all the total number of logs ingested from the selected OKE Cluster in the specified time range.
    - OCI Logging Analytics can collect and manage terabytes of data at a given point in time.
      ![widget-logs](images/widget-logs.png) 
    - Click on the View Query Icon to view the query used to populate the data in widget.   
      ![view-query-icon](images/view-query-icon.png)  
    - The query used to populate the data will be displayed.
      ![view-query](images/view-query.png)    

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


## Task 3: Deep Dive into Log Types Widget

1.  Click on the Punch Out Icon on the Log Types widget.
    ![punch-out-icon](images/punch-out-icon.png)  

    This will take to the "Tile view" of Log Explorer in context of **Kubernetes Cluster Name** .
    ![log-explorer-tile-view](images/log-explorer-tile-view.png)

2. Select the visualization "Records with Histogram".
    ![records-with-histogram-view](images/records-with-histogram-view.png)

3. In the Fields panel, click on the Other icon
    ![others-icon](images/others-icon.png)   




**Congratulations!**, this lab ends here, kindly proceed  to next lab.
## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics, Madhavan Arnisethangaraj, OCI Management Agent
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022
