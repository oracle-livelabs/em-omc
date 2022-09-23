# OKE Monitoring with Logging Analytics

## Introduction

This lab will walk you through the steps to configure an open source log collector Fluentd and Oracle Management Agent to collect various logs, objects and metrics from OKE cluster using package manager Helm.

In this lab we will be using the following tools
* oci cli :  Tool that enables user to work with Oracle Cloud Infrastructure objects and services at a command line 
* helm : Package manager for Kubernetes
* kubectl : Kubernetes command line tool

And below are the ingestion mechanisms that would be used 
* fluentd : An open source data collector
* management-agent : Oracle provided data collector and Prometheus scraper.


### Objectives

In this lab, you will install a helm chart that deploys various Kubernetes manifests and configuration files that in turn will

* Set up Fluentd to collect Kubernetes & Linux System logs, application/container logs and Kubernetes Objects logs.
* Set up Management Agent to collect Kubernetes metrics and reporting them to OCI Monitoring. 

Estimated Time: 30 minutes

## Task 1: Gathering Required Information

Gather the following information that will be used in this and subsequent labs.

1. Click on the **View Login Info** link on the top left of this workshop page. 
    ![view-login-info](images/view-login-info.png)

2. Keep the below fields handy obtained from the **Terraform Values** frame of the Reservation Information page in a **notepad**.

    - **Kubernetes Cluster OCID:** The OCID of the Kubernetes(OKE) cluster. 

    - **Kubernetes Cluster Name:** The name of the Kubernetes(OKE) cluster.

    - **Kubernetes Namespace:** Kubernetes Namespace in which the Kubernetes manifests and configuration files to be deployed.

    - **Kubernetes Service Account:** The name of the Kubernetes service account to be used for the deployment.

    - **Container Image URL:** URL of the container image that contains Fluentd, Logging Analytics Fluentd output plugin and other plugins for the logs and objects collection.

    - **Logging Analytics Namespace:** OCI Logging Analytics Namespace to which the logs to be ingested. 

    - **Logging Analytics LogGroup OCID:** The OCID of the Logging Analytics Log Group where the logs to be stored.
  
    - **Management Agent Install Key:** Base64 encoded string representation of input.rsp required for Management Agent registration.
  
    - **Management Agent Container Image URL:**  URL of the Management Agent container image. 
  
    - **Compartment OCID:** The OCID of the Compartment in which the metrics to be ingested. 


## Task 2: Launching Cloud Shell
  
1. On Oracle Cloud Home Page, click the **Cloud Shell**  ![cloud-shell-button](images/cloud-shell-button.png)  button. 

  ![cloud-shell](images/cloud-shell.png)

2. A Cloud Shell Instance will be launched and displayed. 
  ![cloud-shell-textarea](images/cloud-shell-textarea.png)

 

## Task 3: Setting up Kube Config in Cloud Shell

1. To set up kubeconfig for the OKE Cluster execute the following command in the cloud shell after replacing **Kubernetes Cluster OCID**.

    ```
     <copy>
       oci ce cluster create-kubeconfig --cluster-id <Kubernetes Cluster OCID> --file $HOME/.kube/config --region us-phoenix-1 --token-version 2.0.0  --kube-endpoint PUBLIC_ENDPOINT
     </copy>
    ```   
  
    ```
    New config written to the Kubeconfig file /home/llxxxxx_us/.kube/config
    ```


## Task 4: Verify OKE Cluster's Access 
1. Run the following command in the cloud shell to verify that you can access the OKE Cluster.

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
  > **Note:** Node IPs may differ for your cluster.


## Task 5: Download Helm Chart
1. In the home directory of the cloud shell, create a directory **oke-livelab** and navigate into it. 
    ```
      <copy>
          mkdir ~/oke-livelab && cd $_
      </copy>
    ```


2. Download the helm chart using the following command.
    ```
      <copy>
          wget https://objectstorage.us-phoenix-1.oraclecloud.com/p/YQy-JQa0RPGxI-pGKmnmA_PJArpo8ZjMdYXCJQM7yXXf6bSCyzI7X_YYmfTDxGbw/n/axfo51x8x2ap/b/oci-kubernetes-monitoring/o/helm-chart/v2.0.0.alpha.1.tgz
      </copy>      
    ```  
 
    ```
    Length: 10750 (10K) [application/octet-stream]
    Saving to: ‘v2.0.0.alpha.1.tgz’
    100%[============================================================>] 10,750      --.-K/s   in 0.001s  
    2022-09-22 05:01:55 (121 MB/s) - ‘v2.0.0.alpha.1.tgz’ saved [11505/11505]
    ```
 

3. Unpack the downloaded tar file by using the below command.
    
    ```
      <copy>
        tar zxvf v2.0.0.alpha.1.tgz
      </copy>
    ``` 

   ![helm-chart-extraction](images/helm-chart-extraction.png) 
   
## Task 6: Create Custom values.yaml 

1. In the **oke-livelab** directory created in the task #5 , create a directory **external-values**, using the following command.
      ```
        <copy>
          mkdir ~/oke-livelab/external-values && cd $_
        </copy>
      ```


2. Open a file named values.yaml using **vi**.
      ```
        <copy>
             vi values.yaml
        </copy>
      ```
3.  Paste the following content and update the values of the respective variables by using the information gathered in task #1.
    

      ```
      <copy>

      # custom values
        namespace: <Kubernetes Namespace>
        image:
            url: <Container Image URL>
            imagePullPolicy: Always

        ociLANamespace: <Logging Analytics Namespace>
        ociLALogGroupID: <Logging Analytics LogGroup OCID>
        kubernetesClusterID: <Kubernetes Cluster OCID>
        kubernetesClusterName:  <Kubernetes Cluster Name>
        createServiceAccount:  false
        serviceAccount: <Kubernetes Service Account>
        mgmtagent: 
            installKey: <Management Agent Install Key>
            imageUrl: <Management Agent Container Image URL>
        ociCompartmentID: <Compartment OCID>
        fluentd:
            baseDir: /var/log/<Kubernetes Namespace>
            tailPlugin:
                readFromHead:  false
      </copy>
      ```
 4. (Optional) The above created **values.yaml** contains the minimalistic values that need to be changed for telemetry collection to work. The full **values.yaml** could be found using the below command.


      ```
        <copy>
          cat ~/oke-livelab/helm-chart/values.yaml
        </copy>
      ```


## Task 7: (Optional) Verifying Helm Configuration
1. The following command helps performing a dry run of helm install to validate the exact manifests and configurations that are going to be deployed.

      ```
        <copy>
          helm template --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/helm-chart/
        </copy>
      ```    
 
## Task 8: Install Helm Chart
1. Install the helm-chart using the following command.
      ```
        <copy>
         helm install <Kubernetes Namespace> --values ~/oke-livelab/external-values/values.yaml ~/oke-livelab/helm-chart/ -n=<Kubernetes Namespace>
        </copy>
      ```
      
      ```
        NAME: resr31821
        LAST DEPLOYED: Fri Sep 23 05:18:11 2022
        NAMESPACE: resr31821
        STATUS: deployed
        REVISION: 1
        TEST SUITE: None
      ```

## Task 9:(Optional) Verify the Installation

1. Upon the successful installation of helm chart, following resources are created.

   i. **DaemonSet**

    - The DaemonSet deployed as part of this installation is responsible for logs collection.


      ```
        <copy>
          kubectl get daemonset -n=<Kubernetes Namespace>
        </copy>
      ```
      ```
 NAME                       DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
 oci-la-fluentd-daemonset   4         4         4       4            4           <none>         5m35s           
      ```
     
      ```
            <copy>
                kubectl get pods -n=<Kubernetes Namespace> | grep daemonset
            </copy>
      ```
     
      ```
      NAME                                         READY   STATUS    RESTARTS   AGE
      oci-la-fluentd-daemonset-c2pfc               1/1     Running   0          4m22s
      oci-la-fluentd-daemonset-rnq6x               1/1     Running   0          4m22s
      oci-la-fluentd-daemonset-wmpf9               1/1     Running   0          4m22s
      oci-la-fluentd-daemonset-zztlx               1/1     Running   0          4m22s
      ```
   ii. **StatefulSet**
   
    - The StatefulSet deployed as part of this installation is responsible for metrics collection.
      ```
      <copy>
        kubectl get statefulset -n <Kubernetes Namespace>
      </copy>
      ```
      ```
        NAME                  READY   AGE
        mgmtagent-bv          1/1     13d
      ```

      ```
      <copy>
        kubectl get pods -l app=mgmtagent-bv -n <Kubernetes Namespace>
      </copy>
      ```
      ```
        NAME             READY   STATUS    RESTARTS   AGE
        mgmtagent-bv-0   1/1     Running   0          7d4h
      ```
   
   iii. **Deployment** 


    - The Deployment created as part of this installation is responsible for objects collection.

      ```
        <copy>
          kubectl get deployment -n=<Kubernetes Namespace>
        </copy>
      ```

       ```
       NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
       oci-la-fluentd-deployment   1/1     1            1           10m
       ```



       ```
          <copy>
              kubectl get pods -n=<Kubernetes Namespace> |grep deployment
          </copy>
       ```
      
      ```
      NAME                                         READY   STATUS    RESTARTS   AGE
      oci-la-fluentd-deployment-69bd489c65-2v26s   1/1     Running   0          3h22m
      ```

   iv. **Config Map** 


    - The config maps created as part of this installation contains the fluentd configuration for logs & objects collection and management agent configuration for metrics collection.

      ```
        <copy>
            kubectl get configmaps -n=<Kubernetes Namespace>
        </copy>
      ```
      ```
        NAME                               DATA   AGE
        kube-root-ca.crt                   1      49m
        mgmtagent-monitoring-config        1      13m
        oci-la-fluentd-logs-configmap      2      13m
        oci-la-fluentd-objects-configmap   2      13m
      ```


## Task 9: Verify fluentd is Running 

1. To verify fluentd is up and running
    - For logs collection, provide any one pod name from the Task #9 DaemonSet step.
     ```
     <copy>
        kubectl logs <daemonset-pod-name> -n=<Kubernetes Namespace> |grep 'fluentd worker'
     </copy>
     ```
     - You should see the below message
     ```
        2022-08-18 10:34:31 +0000 [info]: #0 starting fluentd worker pid=14 ppid=7 worker=0
        2022-08-18 10:35:06 +0000 [info]: #0 fluentd worker is now running worker=0
     ```
     - For objects collection, provide the pod name from the Task #9 Deployment step.
     ```
     <copy>
        kubectl logs <deployment-pod-name> -n=<Kubernetes Namespace> |grep 'fluentd worker'
     </copy>
     ```
     - Output will be the same as above.
     
2. (Optional) Verify logs are sent to Logging Analytics. 

     - To verify logs are sent to the Logging Analytics, execute the following command. 
     
        ```
        <copy>
            kubectl exec -n=<Kubernetes Namespace> --stdin --tty <daemonset-pod-name> -- tail -f /var/log/oci-logging-analytics.log
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


**Congratulations!**, you have successfully set up fluentd to collect OKE System logs and Object logs. You have also successfully setup Management Agent to ingest Kubernetes metrics. Please, proceed to next lab.
## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics, Madhavan Arnisethangaraj, OCI Management Agent
* **Last Updated By/Date** - Vikram Reddy, Sep, 2022
