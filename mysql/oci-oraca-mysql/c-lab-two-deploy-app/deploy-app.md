# Deploy a microservices application

## Introduction

This workshop uses Spring Boot-based Java microservices as a target application and in this lab, you will deploy the application to the Kubernetes cluster created in Lab 1.

Estimated time: 15 minutes

### Objectives

* Deploy a microservices application to Kubernetes cluster 

### Prerequisites

* Completion of the preceding labs in this workshop

## Task 1: Verify OKE

1. Go back to the Kubernetes cluster page where you left Lab 1, and check the status of the cluster. Open the navigation menu from the top left corner (aka. hamburger menu) in the Oracle Cloud console, and select **Developer Services** > **Kubernetes Clusters (OKE)**.

   ![Oracle Cloud console, Cluster details](images/6-1-1-buildapp.png " ")

2. Click the **k8-appdev** link from the table.

   ![Oracle Cloud console, Navigation Menu](images/6-1-2-buildapp.png " ")

3. If the status of the cluster is **Active**, creation was successful. If it is still in a **Creating** status, it may take a few more minutes to complete. (Usually, it takes 7 to 10 minutes to finish the jobs to create a cluster).

   ![Oracle Cloud console, Cluster details](images/6-1-3-buildapp.png " ")

## Task 2: Access the OKE in the Oracle Cloud shell


1. Click **Access Cluster** on the cluster details page.

  ![Oracle Cloud console, Cluster details](images/6-1-3-buildapp.png " ")

2. Make sure the **Cloud Shell Access** is selected. Click the **Copy** link from the command to access kubeconfig for the cluster.

  ![Oracle Cloud console, Cluster details](images/6-1-4-buildapp.png " ")

3. Then click **Launch Cloud Shell**.

  ![Oracle Cloud console, Cluster details](images/6-1-5-buildapp.png " ")

4. Oracle Cloud Shell window opens at the lower side of the browser screen and paste the copied command to the command shell prompt. Then hit enter.   

  ![Oracle Cloud console, Cluster details](images/6-1-6-buildapp.png " ")

  >**Note:** Save the command to a text file on your laptop, and execute it whenever you start a new Cloud Shell session while working in the labs in this workshop.


## Task 3: Prepare Database for the application 

1. Install MySQL client to connect to the MySQL HeatWave Database from cloud shell 
    ```
    <copy>
    kubectl run mysql-client --image=iad.ocir.io/axfo51x8x2ap/load-mysql-data:latest -it --rm --restart=Never -- /bin/bash
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/6-2-1-buildapp.png)

2. Execute below command to connect to MySQL HeatWave Database using Private IP of the database and admin credentials provided during database creation. 
    ```
    <copy>
    mysql -h <mds-private-ip-address> -u <mds-admin-user> -p
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/6-2-2-buildapp.png)

3. Execute below command to create a "WINE" application database and tables required for the application 
    ```
    <copy>
    source insert_100_mysql.sql
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/6-2-3-buildapp.png)

4. Execute **exit** to exit from the mysql client and execute **exit** again to exit from mysql pod to kubectl session.

    ![Oracle Cloud console, Cloud Shell](images/6-2-4-buildapp.png)

  >**Note:** Now the database is prepared with necessary tables and records. Please proceed to the next task.

## Task 4: Download configuration files

1. Download the zip file to the home directory in the Cloud Shell.

    ``` bash
    <copy>
    cd ~; wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/nzVKfbkHfZ5xMIyz9xRJDbKz6awoBwha88WKF35mtyFsT5T52pO5UXzkZ_iHHIuJ/n/axfo51x8x2ap/b/DevLive-MySQL/o/sb-hol.zip 
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/6-3-1-buildapp.png " ")

3. Unzip the file. This will create a directory **sb-hol**.

    ``` bash
    <copy>
    unzip ~/sb-hol.zip
    </copy>
    ```

  ![Oracle Cloud console, Cloud Shell](images/6-3-2-buildapp.png " ")

## Task 5: Deploy the application

1. Execute the following command from the Cloud Shell.

    ``` bash
    <copy>
    cd ~/sb-hol;ls
    </copy>
    ```
  ![Oracle Cloud console, Cloud Shell](images/6-4-1-buildapp.png " ")

    >**Note:** Verify there are the following files in the folder.
    - admessage.yaml
    - apmnamespace.yaml
    - customapmresource.yaml
    - wstore.yaml

2. Modify the file **wstore.yaml** to update the MySQL HeatWave Database Private IP 

    ``` bash
    <copy>
    vi wstore.yaml
    </copy>
    ```
    - Update field **<mds-private-ip-address>** with MySQL HeatWave Database Private IP (line 88) 

    ![Oracle Cloud console, Cloud Shell](images/6-4-3-buildapp.png " ")

    - Press the Esc key to ensure you are in command mode.
    - Type :wq (colon followed by wq) in the vi editor.
    - Press Enter to execute the command to save the file 

    ![Oracle Cloud console, Cloud Shell](images/6-4-4-buildapp.png " ")
  
3. Execute the command below to deploy the application to the cluster.

    ``` bash
    <copy>
    kubectl apply -f ~/sb-hol/wstore.yaml --validate=false
    </copy>
    ```

## Task 6: Launch the application
1. Verify the 2 services and 2 stateful sets are created
  ![Oracle Cloud console, Cloud Shell](images/6-4-5-buildapp.png " ")
  
2. Run the kubectl command below to display the status of the pod creation. Wait until the statuses become 'Running'. This may take a few minutes.

    ``` bash
    <copy>
    kubectl get pods
    </copy>
    ```
  ![Oracle Cloud console, Cloud Shell](images/6-4-6-buildapp.png " ")

3. Run the kubectl command below to display the deployed services.

    ``` bash
    <copy>
    kubectl get svc
    </copy>
    ```

4. Copy the External IP of the wstore-frontend service
  ![Oracle Cloud console, Cloud Shell](images/6-4-7-buildapp.png " ")

5. Refer to the below example and construct a URL, and paste it into a browser's address bar. If you see the WineCellar content as in the below screenshot, the deployment was successful.

    ``` bash
    <copy>
    http://<IP of the wstore-frontend service>/winestore/
    </copy>
    ```
  ![WineCellar Demo app](images/6-4-8-buildapp.png " ")

    >**Note:** It may take a few minutes to complete the deployment and start loading the page content on the screen for the first time.  


You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
* **Last Updated By/Date** - Anand Prabhu, January 2024