# Customizing Application Logs Configuration

## Introduction

The prebuilt OKE Cluster being used for this workshop already has MuShop (a cloud-native reference application of several Oracle Cloud services) deployed. Mushop has various services running on different containers generating their own application logs which goes to /var/log/containers. All these Mushop service logs are being processed using the generic source **Kubernetes Container Generic Logs** as explained in the previous lab.

This lab will walk you through the steps required to customize pre-defined fluentd configuration in specific to MuShop container logs.  
 
### Objectives

In this lab, you will:
* Modify configuration to collect and process some MuShop container logs using their specific Log Sources.
* Verify the log data of those MuShop logs in the Log Explorer.


### Prerequisites

* **Ingestion Flow Setup** lab should have been completed

Estimated Time: 15 minutes

## Task 1: Determining the Logs for Customization

1. Navigate to the Log Explorer.

2. Run the following query in the Query Bar.
        ```  
            <copy>
                'Log Source' = 'Kubernetes Container Generic Logs' | timestats count as logrecords by 'Log Source'
            </copy>
        ``` 
   
3. The previous step takes you to the "Records with Histogram view" in context of **Kubernetes Container Generic Logs** Log Source
    ![kubernetes-logs](images/kubernetes-container-generic-logs.png) 

4. Click on the **Log Origin** field from the Fields Panel.
    ![log-origin](images/log-origin.png) 

5. **Filter Log Origin** pop-window will be displayed. Filter the results with the keyword **mushop** and hit enter. All the logs pertaining to the mushop app will be displayed. We have highlighted two log files, whose logs will be rerouted to be processed with existing mushop Log Sources.
    ![mushop](images/mu-shop.png)    


## Task 2 (Optional): MuShop Log Sources
1. Click on the drop-down of top left side of the Log Explorer Page and select **Administration**
    ![administration](images/administration.png) 

   Administration Overview Page will be displayed.
    ![admin-overview](images/admin-overview.png) 

2. Click on Sources from the Resources Section.
    ![sources](images/sources.png) 

   Sources page will be displayed. Filter the results with the keyword **mushop** and hit enter. The list of all **mushop** sources will be displayed.
    ![all-mushop-sources](images/all-mushop-sources.png)

> **Note:** Refer [Learn More](#learn-more) section that has references for creating your own custom Log Parser and Log Source.


## Task 3: Inserting the mushop application specific configuration in values.yaml.

1. In the next few steps we will update the values.yaml to collect the logs for some of the **mushop application containers**.
    - Open the file values.yaml using **vi**.
      ```
        <copy>
             vi ~/oke-livelab/external-values/values.yaml
        </copy>
      ```
    - For the vi/vim to not auto-indent any text that you paste we will enable paste mode.
      
      ```
        <copy>
            :set paste
        </copy>
      ``` 

    - Switch to the insert mode and append the below **customLogs** configuration at the end of the file in the fluentd section.
     ```
     <copy>
    # Custom Configuration for mushop application logs 
        customLogs:
           mushop-orders:
                path: /var/log/containers/mushop-orders-*.log
                ociLALogSourceName: "mushop-orders-app"
                multilineStartRegExp: /^\d{4}-\d{2}-\d{2}\s*\d{2}:\d{2}:\d{2}.\d{3}/
                isContainerLog: true
           mushop-api:
                path: /var/log/containers/mushop-api-*.log
                ociLALogSourceName: "mushop api logs"
                multilineStartRegExp: /^::\w{4}:\d{2}.\d{3}.\d{1}.\d{1}\s*-\s*-\s*\[\d{2}\/\w{3}\/\d{4}:\d{2}:\d{2}:\d{2}\s*\+\d{4}\]/
                isContainerLog: true
           mushop-edge:
                path: /var/log/containers/mushop-edge-*.log
                ociLALogSourceName: "mushop-edge logs"
                isContainerLog: true  
           mushop-catalogue:
                path: /var/log/containers/mushop-catalogue-*.log
                ociLALogSourceName: "mushop-catalogue logs"
                isContainerLog: true
     </copy>
     ```
    
    - After appending the **customLogs** configuration, the final values.yaml file will look like below
      
      ```
        <copy>
        
             # custom values

                namespace: <Kubernetes Namespace>
                image:
                url: <Container Image URL>
                imagePullPolicy: Always

                ociLANamespace: <Logging Analytics Namespace>
                ociLALogGroupID: <Logging Analytics LogGroup Id>
                kubernetesClusterID: <Kubernetes Cluster Id>
                kubernetesClusterName:  <Kubernetes Cluster Name>
                createServiceAccount:  false
                serviceAccount: <Kubernetes Service Account>
                fluentd:
                baseDir: /var/log/<Kubernetes Namespace>
                tailPlugin:
                        readFromHead:  false
                    # Custom Configuration for mushop application logs 
                        customLogs:
                                mushop-orders:
                                        path: /var/log/containers/mushop-orders-*.log
                                        ociLALogSourceName: "mushop-orders-app"
                                        multilineStartRegExp: /^\d{4}-\d{2}-\d{2}\s*\d{2}:\d{2}:\d{2}.\d{3}/
                                        isContainerLog: true
                                mushop-api:
                                        path: /var/log/containers/mushop-api-*.log
                                        ociLALogSourceName: "mushop api logs"
                                        multilineStartRegExp: /^::\w{4}:\d{2}.\d{3}.\d{1}.\d{1}\s*-\s*-\s*\[\d{2}\/\w{3}\/\d{4}:\d{2}:\d{2}:\d{2}\s*\+\d{4}\]/
                                        isContainerLog: true
                                mushop-edge:
                                        path: /var/log/containers/mushop-edge-*.log
                                        ociLALogSourceName: "mushop-edge logs"
                                        isContainerLog: true  
                                mushop-catalogue:
                                        path: /var/log/containers/mushop-catalogue-*.log
                                        ociLALogSourceName: "mushop-catalogue logs"
                                        isContainerLog: true
        </copy>
     ```   

    - We have now added configuration to send logs for four mushop application to be processed by their specific Log Sources.
    
    - Each configuration has following important information.

         i. path - log origin path from which application logs needs to be read.

         ii. ociLALogSourceName - Logging Analytics Log Source to be used to process these logs 

         iii. multilineStartRegExp - When the individual log entry in the file spans across multiple lines, multilineStartRegExp is used to uniquely identify  the starting point of the log entry like **mushop-orders** and **mushop-api** in the above configuration . 

        
2. Upgrade the helm chart using the above values.yaml.

    ```
     <copy>
        helm upgrade --values ~/oke-livelab/external-values/values.yaml <Kubernetes Namespace> ~/oke-livelab/helm-chart/ -n=<Kubernetes Namespace>
     </copy>
       
     ```

## Task 4: Verification of mushop logs in Log Explorer

1. Navigate to the Log Explorer.

2. Run the following query in the Query Bar.

    ```
    <copy>
        'Log Source' in ('mushop api logs', 'mushop-catalogue logs', 'mushop-orders-app', 'mushop-edge logs') | stats count as logrecords by 'Log Source' | sort -logrecords
    </copy>
    ```
3. In the Pie Chart view now you should be able to see the Log Sources pertaining to the mushop applications along with the other OKE System and Objects logs.
    ![mushop-piechart](images/mushop-piechart.png)

4. Drill Down to the Log Source **mushop api logs**
    ![drill-down-mushop-api-logs](images/drill-down-mushop-api-logs.png)

5. Click on the expand field button to view all the extracted fields of a log entry. You can now see that various important information from the log entry has been extracted into different fields which can be further used for filtering and various analytics.
    ![mushop-api-logs](images/mushop-api-logs.png)


**Congratulations!**, you have successfully modified the helm configuration to collect custom application container logs. Please, proceed to next lab.

## Learn More
For further reading please refer to the resources.

[Configure Sources] (https://docs.oracle.com/en-us/iaas/logging-analytics/doc/configure-sources.html)

[Create Parser] (https://docs.oracle.com/en-us/iaas/logging-analytics/doc/create-parser.html)

[Custom Configuration] (https://github.com/oracle-quickstart/oci-kubernetes-monitoring#custom-configuration)

## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022