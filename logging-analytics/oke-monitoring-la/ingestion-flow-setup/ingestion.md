# OKE Monitoring with Logging Analytics

## Introduction

This lab will walk you through the steps to configure open source log collector fluentd to collect OKE System and Service log using package manager Helm.

Estimated Time: 30 minutes

### About <Product/Technology> 
In this lab we will be using following tools:
* fluentd - open source data collector
* helm - package manager for Kubernetes

### Objectives

In this lab, you will:
* Set up fluentd to collect system/service logs as well custom container logs
* Visualize the data in the OCI Logging Analytics Log Explorer 


### Prerequisites

This lab assumes you have following details handy that were displayed upon the succesful completion of setup:
* Kubernetes Namespace 
* LA Namespace
* Log Group 
* Cluster ID
* Cluster Name

## Task 1: Launching Cloud Shell

1. Click the **Cloud Shell**  ![Image alt text](images/cloud-shell-button.png)  button. 

	![Image alt text](images/cloud-shell.png)

	> **Note:** Use this format for notes, hints, tips. Only use one "Note" at a time in a step.


2. A Cloud Shell Instance will be created and text area will be displayed as below. 

  ![Image alt text](images/cloud-shell-textarea.png)


## Task 2: Setting Up Kube Config In Cloud Shell

1. To Set up kubeconfig for the OKE Cluster replace the Cluster ID value in the below command.
    ```
     <copy>
    $ oci ce cluster create-kubeconfig --cluster-id <CLUSTER_ID> --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
     </copy>

    ```

2. If the Cluster Id `ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx` then the command will look like below.
     
     ```
     <copy>
       $ oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
     </copy>

     ```

3. Copy the modified command in the step II and paste it in the Cloud Shell and hit Enter. A new config file will be created.

    ```
    logan_test@cloudshell:~ (us-phoenix-1)$ oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
    
    New config written to the Kubeconfig file /home/logan_test/.kube/config
    ```

## Task 3: Accessing OKE Cluster In Cloud Shell
1. To verify whether the kubeconfig is correctly set up and you are able to access the OKE Cluster run the following command.

     ```
       <copy>
          kubectl get nodes
       </copy>
     ```
   
     ```
      logan_test@cloudshell:~ (us-phoenix-1)$ kubectl get nodes
       NAME          STATUS   ROLES   AGE   VERSION
       10.0.10.116   Ready    node    91d   v1.21.5
       10.0.10.136   Ready    node    77d   v1.21.5
       10.0.10.146   Ready    node    77d   v1.21.5
     ```
  > **Note:** Node ip's will differ for every cluster.

## Task 4: Download Helm Charts from GitHub
1. In the present working directory create the directory oke-livelab and navigate into it. 
  > **Note:** You can use the command - `mkdir oke-livelab && cd $_`

2. Download the helm chart configuration from the [github] (https://github.com/oracle-quickstart/oci-kubernetes-monitoring) using the following command.
    ```
    <copy>
       git clone https://github.com/oracle-quickstart/oci-kubernetes-monitoring.git
    </copy>
    ```  
3. The content will be downloaded.
    ![Image alt text](images/git-clone-command.png)

4. Check the `oci-kubernetes-monitoring` is cloned and validate it has logan directory by running the command **cd oci-kubernetes-monitoring/ && ls**.
     ![Image alt text](images/oke-monitoring-dir.png)

## Task 5: Create Custom values yaml file
1. In the **oke-livelab** directory created in the above task, create a directory external-values , using following command.
      ```
        <copy>
          mkdir external-values
        </copy>
      ```


2. Create a file values.yaml in the external-values directory using following command.
      ```
        <copy>
          touch values.yaml
        </copy>
      ```
3. In the values.yaml file created above, paste the following content and update the values of the respective fields.
      ```
      <copy>
      namespace: <Kubernetes Namespace Generated Upon Clicking Green Button>
      image:  
        imagePullSecrets: <image-pull-secret>
        url: <docker-image-pull-url>
   
      # Logging Analytics Namespace
      ociLANamespace: <LA Namespace Generated Upon Clicking Green Button>
      # Logging Analytics Default Log Group ID
      ociLALogGroupID: <LA Log Group Id Generated Upon Clicking Green Button>
      # Kubernetes Cluster ID
      kubernetesClusterID: <Kubernetes Cluster Id Generated Upon Clicking Green Button>
      # Kubernetes Cluster NAME  
      kubernetesClusterName: <Kubernetes Cluster Name Generated Upon Clicking Green Button>

      </copy>
      ```
## Task 6: Verifying Helm Configuration
1. Once the values.yaml is updated, it is important to perform the dry-run to validate the configuration is correct. To perform this check, 
  run the following command.
      ```
        <copy>
          helm template --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/oci-kubernetes-monitoring/logan/helm-chart/
        </copy>
      ```
 2. Validate the above command return  no errors or failures.     
 
## Task 7: Install Helm Chart
1. Once the dry-run is completed without any errors. Install the helm-chart to apply the configuration for log-collection.
      ```
        <copy>
         helm install <release-name-of-choice> --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/oci-kubernetes-monitoring/logan/helm-chart/
        </copy>
      ```
  > **Note:** Provide the release-name-of-choice and keep it handy.

2. To verify the pods are created in the OKE, execute the following command and check the output. Keep the pod names handy for next steps.

    ```
      <copy>
      kubectl get pods --namespace=Live-Lab-Generated-Kubernetes-Namespace |grep fluentd
      </copy>
    ```
    ![Image alt text](images/get-fluentd-pods.png)
   > **Note:** Provide the correct kubernetes namespace. 


## Task 8: Verify All Resources Are Created
  As part of this deployment following resources are created - 
  - daemonset
  - deployment
  - configMap
  
1. Daemonset
    - A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. In this case we are running logs collection daemon on each node. 
    - We have used Daemonset to collect the Kubernetes System Logs.  
    - To validate the fluentd daemonset is running, execute the command - 
      ```
        <copy>
          kubectl get daemonset oci-la-fluentd-daemonset --namespace=Live-Lab-Generated-Kubernetes-Namespace
        </copy>
      ```  
    - Output will be in-line with the below snapshot.    
    ![Image alt text](images/daemonset.png)
  

2. Deployment 
    - A Kubernetes deployment is a resource object in Kubernetes that provides declarative updates to applications.
    - We have used deployment to collect the Kubernetes Object Logs
    - To validate the fluentd deployment is running, execute the command -
      ```
        <copy>
          kubectl get deployments oci-la-fluentd-deployment --namespace=Live-Lab-Generated-Kubernetes-Namespace
        </copy>
      ```  
    - Output will be in-line with the below snapshot.  
    ![Image alt text](images/deployment.png)

3. Service Account, Cluster Role and Cluster Role Binding
    - **Service Account** gives identity to the pods which can be used to authenticate Pods with API server and fetch the metadata details.    
        ```
          <copy>
            kubectl describe serviceaccount/oci-la-fluentd-serviceaccount --namespace=Live-Lab-Generated-Kubernetes-Namespace
          </copy>
         ```  
    - **Cluster Role** defines the permission to the user on cluster-scoped resources.
        ```
          <copy>
            kubectl describe clusterrole/oci-la-fluentd-logs-clusterrole
          </copy>
         ```  
    - **Cluster Role Binding** grants the permission defined in the Cluster Role to the user.
         ```
          <copy>
            kubectl describe clusterrolebinding/oci-la-fluentd-logs-clusterrolebinding
          </copy>
         ```  
   
4. ConfigMap
    - A ConfigMap is an API object used to store non-confidential data in key-value pairs.
    - To check the config map of fluentd daemonset, execute the command -
      ```
        <copy>
          kubectl describe configmaps oci-la-fluentd-logs-configmap --namespace=Live-Lab-Generated-Kubernetes-Namespace
        </copy>
      ```  
    - To check the config map of fluentd daemonset, execute the command -
      ```
        <copy>
         kubectl describe configmaps oci-la-fluentd-objects-configmap --namespace=Live-Lab-Generated-Kubernetes-Namespace
        </copy>
      ```  
 

5. To view the logs of the fluent plugin
    - For Kubernetes System 
     ```
     <copy>
     kubectl logs --tail=100 <fluentd-daemonset-pod-name-from-task-7.2> --namespace=Live-Lab-Generated-Kubernetes-Namespace
     </copy>
     ```
     - For Kubernetes Objects
     ```
     <copy>
     kubectl logs --tail=100 <fluentd-deployment-pod-name-from-task-7.2> --namespace=Live-Lab-Generated-Kubernetes-Namespace
     </copy>
     ```
6. Verify logs are sent to Logging Analytics 
     - To verify logs are sent to the Logging Analytics execute the following command. 
    ```
    <copy>
    command to be updated once the feature is ready
    </copy>
    ```
     - Check for the below message in the logs
     ```
     I, [2022-08-16T12:31:32.234958 #11]  INFO -- : Generating payload with 95  records for oci_la_log_group_id: <LA Log Group Id Generated Upon Clicking Green Button>
     I, [2022-08-16T12:31:32.402328 #11]  INFO -- : The payload has been successfully uploaded to logAnalytics -
                         oci_la_log_group_id: <LA Log Group Id Generated Upon Clicking Green Button>,
                         ConsumedRecords: 95,
                         Date: Tue, 16 Aug 2022 12:31:32 GMT,
                         Time: 2022-08-16T12:31:32.000Z,
                         opc-request-id: D61380FCECC84BD8A84349A766CF59FE/DD09F19E0CDBCDFCC5A4741CB178C3DF/897B96A83E503277C0B2287E2D4B2221,
                         opc-object-id: c9959334-65ef-403f-9224-7e7c28e44587
     ```
   
## Task 9: Validate in the Log Explorer

1. Log In to the console with the user. (Would we be providing link directly to Log Explorer ??)

2. From the Logging Analytics Home Page, select Log Explorer from the drop down menu.
   ![Image alt text](images/select-log-explorer.png) 

3. By default, the Log Explorer will show the Pie-Chart view of all the logs received from the OKE. 
    ![Image alt text](images/log-explorer-pie-chart-view.png)

4. Drill Down to any log source for e.g Kubernetes Kubelet Logs
    ![Image alt text](images/drill-down.png) 

5. The view would be like below.
    ![Image alt text](images/kubelet-logsource-logs.png) 

6. Click on the expand field button, all the captured fields are displayed.
    ![Image alt text](images/expand-fields.png)    

## Learn More

*(optional - include links to docs, white papers, blogs, etc)*

* [URL text 1](http://docs.oracle.com)
* [URL text 2](http://docs.oracle.com)

## Acknowledgements
* **Author** - Vikram Reddy , Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Aug, 2022


