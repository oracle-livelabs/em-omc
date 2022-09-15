# OKE Monitoring with Logging Analytics

## Introduction

This lab will walk you through the steps to configure an open source log collector fluentd to collect OKE System and Service log using package manager Helm.

Estimated Time: 30 minutes

### About <Product/Technology> 
In this lab we will be using the following tools:
* oci cli -  tool that enables user to work with Oracle Cloud Infrastructure objects and services at a command line 
* helm - package manager for Kubernetes
* kubectl - Kubernetes command line tool

And, below are the ingestion methods that would be implemented 
* fluentd - an open source data collector
* management-agent - Pending with Agent Team
### Objectives

In this lab, you will:
* Set up fluentd to collect OKE System logs and Object logs


### Prerequisites

* Basic Understanding of Kubernetes


## Task 1: Generating the Prerequisite Values

1. On the **Kubernetes and OKE Monitoring and Troubleshooting** home page click on the View Login Info link. 

2. A Reservation Information page will be displayed.

3. Keep the below fields handy from the Terraform Values frame of the Reservation Information page.

    i. **Kubernetes Cluster Id:** The OCID of the Kubernetes Cluster created for this live lab session

   ii. **Kubernetes Cluster Name:** The name of the Kubernetes Cluster created for this live lab session

  iii. **Kubernetes Namespace:** Namespace of Kubernetes in which the helm chart needs to be installed

   iv. **Kubernetes Service Account:** Kubernetes service accounts are Kubernetes resources, created and managed using the Kubernetes API, meant to be used by in-cluster Kubernetes-created entities, such as Pods, to authenticate to the Kubernetes API server or external services.

    v. **Container Image URL:** URL of the docker image which needs to be pulled that contains all the necessary plugins and dependencies for log collection to work seamlessly.

   vi. **Logging Analytics Namespace:** OCI Tenancy Namespace to which the collected log data to be uploaded
  
  vii. **Logging Analytics LogGroup Id:** The OCID of the Logging Analytics Log Group where the logs must be stored.


## Task 2: Launching Cloud Shell
  
1. On Oracle Cloud Home Page click the **Cloud Shell**  ![cloud-shell-button](images/cloud-shell-button.png)  button. 

  ![cloud-shell](images/cloud-shell.png)

2. A Cloud Shell Instance will be created and the text area will be displayed as below. 
  ![cloud-shell-textarea](images/cloud-shell-textarea.png)

 

## Task 3: Setting Up Kube Config In Cloud Shell

1. To Set up kubeconfig for the OKE Cluster replace the Cluster ID value in the below command.
    ```
     <copy>
       oci ce cluster create-kubeconfig --cluster-id <Kubernetes Cluster Id> --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
     </copy>

    ```

2. If the Cluster Id `ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx` then the command will look like below.
     
     ```
     <copy>
        oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
     </copy>

     ```

3. Copy the modified command in step II and paste it into the Cloud Shell and hit Enter. A new config file will be created.

    ```
     oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.abcxyzxxxxxxxxxxxxx --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
    
New config written to the Kubeconfig file /home/livelab/.kube/config
    ```
## Task 4: Accessing OKE Cluster In Cloud Shell
1. Run the following command to verify if the kubeconfig is configured properly and you can access the OKE Cluster.

     ```
       <copy>
          kubectl get nodes
       </copy>
     ```
   
     ```
       $ kubectl get nodes
       NAME          STATUS   ROLES   AGE   VERSION
       10.0.10.xxx   Ready    node    91d   v1.21.5
       10.0.10.xxx   Ready    node    77d   v1.21.5
       10.0.10.xxx   Ready    node    77d   v1.21.5
     ```
  > **Note:** Node ip's will differ for every cluster.


## Task 5: Download Helm Charts from GitHub
1. In the present working directory create the directory oke-livelab and navigate into it. 
    ```
      <copy>
          mkdir oke-livelab && cd $_
      </copy>
    ```

2. Download the helm chart configuration tar from the [github] (https://github.com/oracle-quickstart/oci-kubernetes-monitoring/releases/tag/v.2.0.0) using the following command.
    ```
      <copy>
          wget https://github.com/oracle-quickstart/oci-kubernetes-monitoring/releases/download/v.2.0.0/helm-chart-v2.0.0.tgz 
     </copy>
    ```  
 The output of the above step would be in line with the below.
    ```
    Length: 10750 (10K) [application/octet-stream]
    Saving to: ‘helm-chart-v2.0.0.tgz’
    100%[============================================================>] 10,750      --.-K/s   in 0.001s  
    2022-09-07 10:06:21 (17.0 MB/s) - ‘helm-chart-v2.0.0.tgz’ saved [10750/10750]
    ```
   

4. Unpack the tar file by using the below command.
    ```
        <copy>
          tar zxvf helm-chart-v2.0.0.tgz
        </copy>
    ```
 Validate the helm-chart directory and its contents are extracted.   
    ![helm-chart-extraction](images/helm-chart-extraction.png)

## Task 6: Create Custom values yaml file
1. In the **oke-livelab** directory created in the above task, create a directory external-values, using following command.
      ```
        <copy>
          mkdir external-values && cd $_
        </copy>
      ```


2. Create a file values.yaml in the external-values directory using the following command.
      ```
        <copy>
          touch values.yaml
        </copy>
      ```
3. In the values.yaml file created above, paste the following content and update the values of the respective fields.

      ```
      <copy>
namespace: <Value of Kubernetes Namespace obtained from Terraform Values Frame>
image:
   url: <Value of Container Image URL obtained from Terraform Values Frame>
   imagePullPolicy: Always

ociLANamespace: <Value of Logging Analytics Namespace obtained from Terraform Values Frame>
ociLALogGroupID: <Value of Logging Analytics LogGroup Id obtained from Terraform Values Frame>
kubernetesClusterID: <Value of Kubernetes Cluster Id obtained from Terraform Values Frame>
kubernetesClusterName:  <Value of Kubernetes Cluster Name obtained from Terraform Values Frame>
createServiceAccount:  false
serviceAccount: <Value of Kubernetes Service Account obtained from Terraform Values Frame>
fluentd:
   baseDir: /var/log/<Value of namespace specified above>
   tailPlugin:
            readFromHead:  false
      </copy>
      ```

  > **Note:** In the subsequent steps, replace <namespace\> with the value of namespace specified in the values.yaml above.

 4. The above **values.yaml** contains the minimal values that need to be changed for log collection to work. The detailed **values.yaml** could be found using the below command.

      ```
        <copy>
          cat ~/oke-livelab/helm-chart/values.yaml
        </copy>
      ```


## Task 7: Verifying Helm Configuration
1. (Optional) Once the values.yaml is updated, it is important to perform the dry run to validate the configuration is correct. To perform this check, 
  run the following command.
      ```
        <copy>
          helm template --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/helm-chart/
        </copy>
      ```
 2. Validate that the above command returns no errors or failures.     
 
## Task 8: Install Helm Chart
1. Once the dry-run is completed without any errors. Install the helm-chart to apply the configuration for log collection.
      ```
        <copy>
         helm install <namespace> --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/helm-chart/ -n=<namespace>
        </copy>
      ```
  > **Note:** Value of namespace specified after install is release name. Please keep it handy for subsequent labs.

2. Once the helm-install is completed sucessfully, it will create three resources - Daemonset, Deployment and Config Map.

   i. **Daemonset**

    - A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. In this case we are running logs collection daemon on each and every node. 
    - We have used Daemonset to collect the Kubernetes System Logs.
    - Run the below command to check the list of fluentd-daemonset's running
      ```
        <copy>
          kubectl get pods -n=<namespace> |grep fluentd-daemonset
        </copy>
      ```
      ```
      NAME                                         READY   STATUS    RESTARTS   AGE
      oci-la-fluentd-daemonset-dltzv               1/1     Running   0          3h21m
      oci-la-fluentd-daemonset-r6ntn               1/1     Running   0          3h22m
      oci-la-fluentd-daemonset-xpv6t               1/1     Running   0          3h21m
      oci-la-fluentd-daemonset-xqjnp               1/1     Running   0          3h22m
      ```
    > **Note:** Keep the pod names handy and in subsequent steps replace <daemonset-pod-name\> value with any one of the pod-name above.

   ii. **Deployment** 

    - A Kubernetes deployment is a resource object in Kubernetes that provides declarative updates to applications.
    - We have used deployment to collect the Kubernetes Object Logs.
    - Run the below command to check fluentd-deployment.
      ```
        <copy>
          kubectl get pods -n=<namespace> |grep fluentd-deployment
        </copy>
      ```
      ```
      NAME                                         READY   STATUS    RESTARTS   AGE
      oci-la-fluentd-deployment-69bd489c65-2v26s   1/1     Running   0          3h22m
      ```

    > **Note:** Keep the pod names handy and in subsequent steps replace <deployment-pod-name\> value with the above pod-name.

   iii. **Config Map** 
    - A config map contains the necessary fluentd configuration to collect all the telemetry information on the OKE Cluster.
    - Run the following command to view Kubernetes System log config map.
      ```
        <copy>
            kubectl get configmaps oci-la-fluentd-logs-configmap -n=resr47160
        </copy>
      ```

      ```
        NAME                            DATA   AGE
        oci-la-fluentd-logs-configmap   2      6h40m
      ```
    - Run the following command to view Kubernetes Objects log config map.
      ```
        <copy>
            kubectl get configmaps oci-la-fluentd-logs-configmap -n=resr47160
        </copy>
      ```  

      ```
        NAME                              DATA   AGE
        oci-la-fluentd-objects-configmap   2     6h41m
      ```

    - (Optional) To view the detailed config map, following command can be used.

      ```
        <copy>
            kubectl get configmaps <config-map-name> -o yaml -n=<namespace>
        </copy>
      ```  


## Task 9: Verify fluentd is Running 

1. To verify fluentd is up and running
    - For Kubernetes System, provide any one pod name in the daemonset-pod-name
     ```
     <copy>
        kubectl logs <daemonset-pod-name> -n=<namespace> |grep 'fluentd worker'
     </copy>
     ```
     - You should see the below message
     ```
        2022-08-18 10:34:31 +0000 [info]: #0 starting fluentd worker pid=14 ppid=7 worker=0
        2022-08-18 10:35:06 +0000 [info]: #0 fluentd worker is now running worker=0
     ```
     - For Kubernetes Objects
     ```
     <copy>
        kubectl logs <deployment-pod-name> -n=<namespace> |grep 'fluentd worker'
     </copy>
     ```
     - Output will be the same as above.
     
2. (Optional) Verify logs are sent to Logging Analytics 
     - To verify logs are sent to the Logging Analytics, execute the following command. 
     
    ```
    <copy>
        kubectl exec -n=<namespace> --stdin --tty <daemonset-pod-name> -- tail -f /var/log/oci-logging-analytics.log
    </copy>
    ```
    
     - Check for a similar message in the logs
     ```
     I, [2022-08-16T12:31:32.234958 #11]  INFO -- : Generating payload with 95  records for oci_la_log_group_id: ocid1.loganalyticsloggroup.oc1.abc.abcxxxxxxxxyx543xxxxxx
     I, [2022-08-16T12:31:32.402328 #11]  INFO -- : The payload has been successfully uploaded to logAnalytics -
                         oci_la_log_group_id: ocid1.loganalyticsloggroup.oc1.abc.abcxxxxxxxxyx543xxxxxx,
                         ConsumedRecords: 95,
                         Date: Tue, 16 Aug 2022 12:31:32 GMT,
                         Time: 2022-08-16T12:31:32.000Z,
                         opc-request-id: D61380FCECC84BD8A84349A766CF59FE/DD09F19E0CDBCDFCC5A4741CB178C3DF/897B96A83E503277C0B2287E2D4B2221,
                         opc-object-id: c9959334-65ef-403f-9224-7e7c28e44587
     ```


**Congratulations!**, you have successfully set up fluentd to collect OKE System logs and Object logs. Please, proceed to next lab.
## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022