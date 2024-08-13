# Connect the existing Kubernetes Cluster for Monitoring

## Introduction

In this lab, you'll use OCI Logging Analytics Solutions offering to get familiar with Kubernetes Monitoring on the existing Kubernetes cluster which has monitoring enabled. (To Be Updated)

Estimated Time: 30 minutes

### Objectives

In this lab, you will see step-by-step instructions to:

  - Navigate to the existing Kubernetes cluster on which monitoring is enabled
  - Understanding the current state of the Kubernetes Cluster
  - Visualizing the data in different views Cluster, Workload, Node & Pod 


## Task 1: Navigating to Cluster

1. To navigate to Solutions page, follow one of the below two methods.

    - Open url : https://cloud.oracle.com/loganalytics/solutions?region=us-phoenix-1&tenant=emdemo

    - From Navigation Menu > **Observability & Management** > **Logging Analytics** > **Solutions**.
    ![final-navigation-solutions.](images/final-navigation-solutions.gif)

2. Click on the Kubernetes tile.
![K8s-tile](images/K8s-tile.png)

3. Kubernetes Monitoring Solution page is displayed. You will see three clusters. 
    
    The clusters of interest for this Live Lab are  :
    - ***education-eks-rQNmdNI7*** : An AWS EKS cluster. We support multi-cloud Kubernetes clusters to monitor their logs.
    - ***oke-cw24*** : An OCI OKE Cluster.

    ![solutions-table](images/solutions-table.png)

4. In the Kubernetes Monitoring Solution page, click the ***oke-cw24*** cluster.

5. The Cluster view of the ***oke-cw24*** cluster will be displayed.

6. The cluster view has the following important sections :

    ![cluster-full-view](images/cluster-full-view.png)

    1. ***Namespaces*** Filter to filter the cluster view by Kubernetes namespaces.
    2. ***Time selector***  has two time range options, Last 60 Minutes (default) and Last 24 Hours. Any changes you make in the time range will impact the Events and Metrics Widget.
    3. ***Summary Panel***  shows the current state of the Kubernetes Objects (namespace, workloads, nodes, pods) & topology summary.
    4. ***Topology*** the objects data collected from the Kubernetes cluster is displayed in this section. The color of each object in the topology indicates its status derived from active warning events associated with the object or its children.
    5. ***Pods by namespace*** all the pods available in the Kubernetes cluster. 
    6. ***Events Panel*** displays the State changes occurring in Kubernetes Cluster in the form of Events.
    7. ***Telemetry Panel***  help you to monitor the health of the system.



## Task 2: Understanding the Cluster View

### **Task 2.1 : Understand the data presented in Summary panel** ###

1. **Prerequisite** : Change time range to 24 hours in time selector at top right corner.

2. Understand when was the topology updated. 
   
    - In Cluster view, observe the first tile in left panel, hover over info icon to see the time when topology was last updated.
    ![topology-lastupdated](images/topology-lastupdated.png)

3. Understand how many namespaces, workloads, nodes, and pods are in the cluster.
  
    - Observe second tile in left summary panel, it displays the number of namespaces in kubernetes cluster. You can check all namespaces in cluster by reviewing the topology view Namespace tier.
    ![namespace-tile](images/namespace-tile.png)
    - Third tile shows total number of workloads with the overall percentage of workloads which needs attention. Objects with associated warning events are flagged as Needs Attention. You can also see the breakdown of workload types & percentage of workload type that needs attention.
    ![workload-tile](images/workload-tile.png)
    - Fourth tile shows the number of Nodes along with percentage of nodes that needs attention due to warning events.
    ![nodes-tile](images/nodes-tile.png)
    - Last tile in left panel shows number of Pods along with percentage of problem pods which needs attention. All pods grouped by namespace are displayed in ***Pods by namespace*** section.
    ![pods-tile](images/pods-tile.png)

4. Understand how many objects need attention in cluster.
    
    - Topology Summary tile displays count of kubernetes objects in blue which are healthy and red for those objects which needs attention due to any active warning event.
    ![topology-summary-needs-attention](images/topology-summary-needs-attention.png)
    - Topology chart shows nodes in red which Needs Attention. The red colour of each object in the topology indicates its status derived from warning events associated with the object or it's children.
    ![topology-needs-attention](images/topology-needs-attention.png)
    - In Pods by namespace section, review all the red coloured polygons representing problem pods grouped by namespace.
    ![podsByNamesapce-needs-attention](images/podsByNamesapce-needs-attention.png)


### **Task 2.2:  View and compare metrics** ###

1. Review metrics for the entire cluster (Ensure no filter selection).

    - Observe the right panel telemetry widgets, these widgets help you to monitor the overall health of the system.
    
    - View ***CPU cores (used/allocatable)*** widget. This widget displays chart for Total CPU cores used by selected pods divided by total allocatable CPU in the cluster.
    ![cpucore-metrics](images/cpucore-metrics.png)
    - There are total 17 metrics widgets available in cluster view. For details of each metrics widget refer [here](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/queries-used-kubernetes-solution.html#GUID-E02C7B04-98A2-48A7-B7B1-97DFC0DE5197).**REVIEW**

2.  Use scroll up and down to see different telemetry widgets.

    - To view all metrics widgets available in cluster, use arrow above first widget to move up and arrow below fourth widget to move down.
    ![metrics-scrolling](images/metrics-scrolling.gif)
    - **Exercise** : Scroll up/down telemetry widgets panel and view all metrics widgets in cluster view.

3. Expand ***CPU cores (used/allocatable)*** metric widget.

    - You can expand each widget to view a larger visualization. Hover the over first widget - 
    ***CPU core (used/allocatable)*** and click on expand icon on top right corner.
    ![expand-cpucoreua](images/expand-cpucoreua.png)
    - In expanded widget, hover over the chart to see metrics details.
    ![expand-cpucoreua-chart](images/expand-cpucoreua-chart.png)

4. Add two metric widgets to compare.

    - In expanded widget, hit Metrics to analyze to open list of all metrics available for comparison with current metrics widget chart.
    ![metrics-to-analyze](images/metrics-to-analyze.png)
    - Select any widget for analysis. e.g. - ***CPU cores used***
    ![metrics-to-analyze-selected](images/metrics-to-analyze-selected.png)
    **Note** - Maximum three metrics can be used for comparison at a time.

    - Hit Close button to close the widget.

    - **Exercise**  - Try selecting different metrics and compare.


### **Task 2.3: View Kubernetes system logs** ###

This widget helps you to monitor the trend and distribution of potential issues in Kubernetes component logs (API Server, Controller Manager, CSI Node Driver).

1. **Prerequisite** :  Change time range to 60 min in time selector at top right corner.

2. Expand ***Kubernetes system*** widget.

    - In right panel widget scroll down to view ***Kubernetes system*** widget, expand this widget.
    ![kubesys-expand](images/kubesys-expand.png)

3. Review Issue trend and potential issues charts.

    - Observe All Issues section showing Issue trend chart. This time series chart gives count of Issues detected over given time interval. Hover over data points for details.
    ![kubesys-all-issues](images/kubesys-all-issues.png)
    - Check Potential Issues chart to view Issues count grouped by kubernetes components & error. Hover over different colored data points to view details of components with corresponding error.
    ![kubesys-potential-issues](images/kubesys-potential-issues.png)

4. Review issues table to see kubernetes component logs. 

    - Move down to view logs table. Check the log records for Error samples and Issue count for different components.
    ![kubesys-component-logs](images/kubesys-component-logs.gif)
    - Collapse widget by clicking collapse icon on top right corner.


### **Task 2.4: View OS health logs** ###

This widget helps you to monitor the trend and distribution of potential issues identified in compute OS logs.

1. Expand ***OS health*** widget.

    - In right telemetry widget panel scroll down to view ***OS health*** widget, expand it.
    ![oshealth-expand](images/oshealth-expand.png)

2. Review trend of issues and specific issues.

    - Observe All Issues section showing Issue trend chart. This time series chart gives count of Issues detected over given time interval. Hover over data points for details.
    ![oshealth-all-issues](images/oshealth-all-issues.png)
    - Check Issues chart to view Issues count grouped by kubernetes component, Node, Issues count, Label & Error. Hover over the data points to get potential issue details.
    ![oshealth-potential-issues](images/oshealth-potential-issues.png)
    - Move down to view logs table. Check the Cluster sample column records for list of issues and see related details about node, count etc in different columns.
    ![oshealth-issues-logs](images/oshealth-issues-logs.gif)
    - Collapse OS health expanded widget.


### **Task 2.5: Review latest kubernetes events** ###

Events section displays the State changes occurring in Kubernetes Cluster in the form of Events.

1. Expand Events panel.

    - Hover over top right corner of Events panel to view Expand icon. Click on it, widget will expand.
    ![events-expand](images/events-expand.png)
    - Events grouped by namespace are listed.
    ![events-panel](images/events-panel.png)

2. "Expand All" in Events.

    - Check the Expand All checkbox to expand all event entries grouped by namespace.
    - View details of each event entry shown in columns. Move through pages in table to view all entries.
    ![events-expand-all](images/events-expand-all.png)

3. Filter Warning events only.

    - Check the Warnings Only checkbox to filter out all warning events.
    - Warning events entries are listed.Type column shows warning. Review more details of this event in other columns.
    ![events-warnings-only](images/events-warnings-only.png)

4. Close the Events panel by clicking collapse icon on top right corner of panel.


### **Task 2.6: Understand kubernetes cluster namespace and pods topology** ###

1. Filter ***wpexapp*** namespace from topology to see workloads, nodes and pods for this namespace.

    - In Topology diagram, in Namespace tier search for node with name -*** wpexapp*** and right click on it.
    ![add-ns-filter](images/add-ns-filter.png)
    - Hit Add to filters option, ***wpexapp*** will be added to Namespace filter in top right corner. Observe the topology view reflecting changes in objects in the namespace which includes workloads and nodes.
    ![ns-filtered-topology](images/ns-filtered-topology.png)
    - Notice Left panel tiles showing object counts corresponding to filtered namespace.
    Also, Pods by workload section gets updated to show pods grouped by workloads under filtered namespace - ***wpexapp***.
    ![ns-filtered-summary-pods](images/ns-filtered-summary-pods.png)

2. Observe changes in telemetry panel and compare metrics.

    - Move to ***CPU cores used*** widget in telemetry panel, after applying namespace filter observe the changes in metrics chart.
    ![ns-filter](images/ns-filter.gif)
    - **Exercise** : Observe metrics charts changes on applying namespace filter for CPU, Memory & Network widgets. → **REVIEW** CPU cores used,Memory used, Network: bytes rx,  Network: bytes tx,  Network: Packet Rx Rate, Network: Packet Tx Rate,  Network Packet Rx Dropped Rate,  Network Packet Tx Dropped Rate. 

3. View logs for different topology nodes including pods.

    - **Prerequisite** : Update time range to 24 hours.

    - View logs for cluster node in topology.
        
        - In topology right click on main cluster node and hit View logs on context menu.
        ![cluster-viewlogs](images/cluster-viewlogs.png)
        - A Visualization pops up which helps identifying new issues in logs in the selected time range, at cluster level.Review errors in table records and corresponding details of log sources, issue counts and others in different columns.
        ![cluster-viewlogs-panel](images/cluster-viewlogs-panel.png)
        - These are the issues found in the selected time range but are not present in the baseline time range specified for the analysis(last 12 hours).Hover info icon for more details.
        ![cluster-viewlogs-panel-info](images/cluster-viewlogs-panel-info.png)
        - Collapse this logs panel using collapse icon at top right corner.
            

    - View logs for ***wpexapp*** namespace node in topology.

        - In topology view Namespace tier right click on ***wpexapp*** and hit View logs on context menu.
        ![ns-viewlogs](images/ns-viewlogs.png)
        - A panel pops up which helps identifying new issues under ***wpexapp*** namespace in the selected time range. Review errors in records and corresponding details of log sources, issue counts and others in different columns.
        ![ns-viewlogs-panel](images/ns-viewlogs-panel.png)
        - Collapse this logs panel using collapse icon at top right corner.


    - View logs for ***wordpress*** workload in ***wpexapp*** namespace.

        -  In topology in Workloads tier right click on  ***wordpress*** and hit View logs on context menu.
        ![workload-viewlogs](images/workload-viewlogs.png)
        - A panel pops up which helps identifying new issues for ***wordpress*** workload under ***wpexapp*** namespace in the selected time range. Review issues in Cluster Sample column and other columns to view details of error log sources, issue counts, etc.
        ![workload-viewlogs-panel](images/workload-viewlogs-panel.png)
        - Collapse this panel.
        

    - View logs for ***10.0.10.211*** Node in ***wpexapp*** namespace.

        - In topology in Node tier right click on ***10.0.10.211*** and hit View logs on context menu.
        ![node-viewlogs](images/node-viewlogs.png)
        - A panel pops up which helps identifying new issues for ***10.0.10.211*** node under ***wpexapp*** namespace in the selected time range. Review table records for issue details.
        ![node-viewlogs-panel](images/node-viewlogs-panel.png)
        - Collapse this panel.


    - View logs for pods from Pods by namespace section.

        - Pods by namespace section right click on ***wordpress-5ff998994b-85hh4*** pod and hit View logs on context menu.
        ![pods-viewlogs](images/pods-viewlogs.png)
        - A panel pops up which helps identifying new issues for ***wordpress-5ff998994b-85hh4*** pod in ***wpexapp*** namespace in the selected time range. Review table records for issue details.
        ![pods-viewlogs-panel](images/pods-viewlogs-panel.png)
        - Collapse this panel.


    - **Exercise** : View logs all other workloads, nodes and pods.



## Task 3: Understand Workload, Node, Pod View - which workload types, applications are running in "wpexapp"

### **Task 3.1: Understand Workload View** ###

1. Understand Workload tab details with ***wpexapp*** Namespace filter only.
    
    - Click on the Workload tab.
    ![workload-tab](images/workload-tab.png)

    - The workload view in the context of all the Namespaces available in the Kubernetes cluster will be displayed.

    - **Note** : In the workload view Topology section is replaced by Workload Details table, Pods by namespaces by Pods by workload & Topology summary by Workload summary.

    - Click on the Namespaces filter & select the namespace ***wpexapp***. Observe Workloads details panel, all the workloads running in the namespace ***wpexapp*** are listed grouped by workload types.

    - The other sections Pods by workloads , Summary panel, Events and Telemetry Panel are updated in the context of namespace ***wpexapp***.

    - Pods by workloads will show all the pods in the namespace ***wpexapp***.

    - Summary panel is updated and each tile will show details specific to the namespace ***wpexapp***.

    -  Telemetry Panel will show the data now in the context of the namespace ***wpexapp***. Use the arrows above first & below the fourth widget to view all the widget.

    - Events section will not show any events as there are no warning events logged in the ***wpexapp***. **REVIEW - need some events**


### **Task 3.2: Incrementally add workloads (running in "wpexapp") to workload filter and nodes to nodes filter (in workload tab).** ###
    
1.  Add a workload running in ***wpexapp*** to Workload filter.

    - Click on the Workloads filter. All the workloads running in the namespace ***wpexapp*** namespace will be shown.
    Select the item ***wordpress-mysql***.

2.  Add a node running in ***wpexapp*** to Node filter.

    - Click on the Node filter and select the Node IP from the list - ***10.0.10.114***


### **Task 3.3: Check Workload details and status in Workload Tab** ###

1. Observe the changes in the Workload summary tiles, Metric Widgets & Events section.

2. View changes in the Workload details section. Click on the Expand all checkbox, to view important details of filtered workload such as Namespace, Name, Status and Age.



### **Task 3.4: Understand Node View - Check Node health and status in Node Tab** ###

1. Understand Node details table and Review changes in Events panel.

    - Click on the Node tab. 
    ![node-tab](images/node-tab.png)

    - The node view in the context of the Namespace ***wpexapp***, Workload ***wordpress-mysql*** & Node IP selected in above step i.e ***10.0.10.114***. in the Kubernetes cluster will be displayed.
    - **Note** : In the node view Topology section is replaced by Node Status section, Pods by namespaces section is replaced by Pods by node & & Topology summary by Node summary.

    - The Node status section shows all the nodes in which the workload ***wordpress-mysql*** is running.

    - Pods by node section shows the pods running in the node for the workload ***wordpress-mysql***.

    - The Node summary tile shows node health.
   
    - **Note** : Events section,Telemetry Panel section & all other tiles in Summary panel remains same.

    - In the Node status section click on the expand icon of the Node IP to view The important details of filtered node such as Status, OS details, CPU, Memory details etc.



### **Task 3.5: Understand Pod View - Check Pod details and health in Pod Tab** ###

1. Understand Pod details table & Review changes in Events panel

    - Click on the Pod tab.
    ![pod-tab](images/pod-tab.png)

    - The Pod view in the context of the workload ***wordpress-mysql*** & Node IP i.e ***10.0.10.114*** is displayed
    
    - **Note** : In the node view Topology section is replaced by Pods status table, Pods by namespaces section is replaced by Pods & Topology summary by Pods summary.

    - Once you land on the Pod page, in the Pods status tab failed status would have been selected by default. 

    - Change the status to Show All. All the pods in the Namespace wpexapp & node ***10.0.10.114*** in the Kubernetes cluster will be displayed.

    - Pods section displays all the pods in the namespace ***wpexapp*** & node ***10.0.10.114***.

    - The Pod summary tile shows number of pods that needs attention & pods which are normal.
    **Note** : Events section,Telemetry Panel section & all other tiles in Summary panel remains same.

    - In the Pods status section click on the expand icon of one of pods to view the important details such as Status,Node, Pod IP, Controller etc  of the filtered pod will be displayed.

    - **Exercise** : View the details of the pods based on their current status like running, failed, succeeded, and pending in Pods status table.


**Congratulations!** In this lab, you have successfuly completed the following tasks:
  - Navigated to the existing Kubernetes cluster on which monitoring is enabled
  - Understood the current state of the Kubernetes Cluster
  - Visualized the data in different views Cluster, Workload,  Node & Pod

  You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Heena Rahangdale, OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Heena Rahangdale , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Jul, 2024