# Deploy the Application

## Introduction

Now that the infrastructure is up and running, it's time to deploy the app and see it all come together. This workshop uses Spring Boot-based Java microservices as a target application and in this lab, you will deploy the application to the Kubernetes cluster created in Lab 1.

Estimated time: 15 minutes

### Objectives

* Connect to the OKE Cluster
* Prepare the MySQL Database
* Deploy the application

### Prerequisites

* Completion of the preceding labs in this workshop.

## Task 1: Connect to Kubernetes

1. Export the `kubeconfig` variable to enable communication to your new OKE cluster. **Note**: During the Terraform execution process, the `kubeconfig` file was automatically retrieved and stored in a project subfolder. 

      ```bash
      <copy>
      cd ~/oci-devlive-2024
      export KUBECONFIG=~/oci-devlive-2024/deployment/terraform/generated/kubeconfig
      </copy>
      ```

      > If the console closes, remember to rerun this command.
   
2. Check that Kubernetes is up and running and you can talk to the Control Plane API endpoint by listing the nodes.

      ```bash
      <copy>
      kubectl get nodes
      </copy>
      ```

      ```bash
      $ kubectl get nodes
      NAME          STATUS   ROLES   AGE   VERSION
      10.0.156.59   Ready    node    3d    v1.28.2
      ```

## Task 2: Prepare Database for the application

1. Deploy an OKE Pod containing the MySQL client that will be used to connect to the DB System.

      ```bash
      <copy>
      kubectl run mysql-client --image=iad.ocir.io/axfo51x8x2ap/load-mysql-data:latest -it --rm --restart=Never -- /bin/bash
      </copy>
      ```

      ![Kubectl command](images/2-2-1-buildapp.png " ")

2. Execute the command below to connect to the MySQL HeatWave Database using the Private IP address of the database and the credentials provided when the DB System was created.

      ```bash
      <copy>
      mysql -h <mds-private-ip-address> -u <mds-admin-user> -p
      </copy>
      ```

      ![Kubectl command](images/2-2-2-buildapp.png " ")

3. Execute the command below to create a **`WINE`** application database with required tables.

      ```bash
      <copy>
      source insert_100_mysql.sql
      </copy>
      ```

      ![Kubectl command](images/2-2-3-buildapp.png " ")

4. Type **exit** to leave the MySQL client, then **exit** once more to leave and terminate the MySQL Client pod.

      ![Kubectl command](images/2-2-4-buildapp.png " ")


## Task 3: Deploy the application

1. Navigate to the app deployment folder.

      ```bash
      <copy>
      cd ~/oci-devlive-2024/sb-hol
      </copy>
      ```

2. Verify the contents of the **sb-hol** directory.

      ```bash
      <copy>
      ls
      </copy>
      ```

      ![Oracle Cloud console, Cloud Shell](images/2-3-1-buildapp.png " ")

      >**Note:** Verify the follwoing files are present in the folder
      * admessage.yaml
      * apmnamespace.yaml
      * customapmresource.yaml
      * wstore.yaml

3. Modify the file **wstore.yaml** to update the MySQL HeatWave Database Private IP

      ```bash
      <copy>
      vi wstore.yaml
      </copy>
      ```

    - Update field **<mds-private-ip-address>** with MySQL HeatWave Database Private IP (line 88) 

    ![Oracle Cloud console, Cloud Shell](images/2-3-2-buildapp.png " ")

    - Press the Esc key to ensure you are in command mode.
    - Type :wq (colon followed by wq) in the vi editor.
    - Press Enter to execute the command to save the file 

    ![Oracle Cloud console, Cloud Shell](images/2-3-3-buildapp.png " ")

4. Execute the command below to deploy to the application cluster.

      ```bash
      <copy>
      kubectl apply -f wstore.yaml --validate=false
      </copy>
      ```

## Task 4: Launch the application

1. Verify the 2 services and 2 statefule sets are created successfully

      ![Oracle Cloud console, Cloud Shell](images/2-4-1-buildapp.png " ")

2. Run the `kubectl` command below to display the status of the pod creation. Wait until all pods are in the 'Running' state. This might take a minute or two.

      ```bash
      <copy>
      kubectl get pods
      </copy>
      ```

      ```bash
      $ kubectl get pods
      NAME             READY   STATUS    RESTARTS   AGE
      wstore-back-0    1/1     Running   0          2d23h
      wstore-back-1    1/1     Running   0          2d23h
      wstore-front-0   1/1     Running   0          2d23h
      ```

3. Retrieve the public IP address for the application service endpoint. Copy it into a text file for future use.

      ```bash
      <copy>
      kubectl get svc
      </copy>
      ```

      ![OCI Console, Cloud Shell, kubectl results](images/2-4-2-buildapp.png " ")

4. Refer to the example below and construct a URL, then paste it into the address bar of a new browser tab. If you see the WineCellar content as illustrated in the screenshot below, deployment was successfull.

      ```bash
      <copy>
      http://<IP of the wstore-frontend service>/winestore/
      </copy>
      ```

      ![Wine cellar demo app](images/2-4-3-buildapp.png " ")

      >**Note:** It may take a few minutes to complete the deployment and start loading the page content on the screen for the first time.

You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
* **Last Updated By/Date** - Anand Prabhu, January 2024