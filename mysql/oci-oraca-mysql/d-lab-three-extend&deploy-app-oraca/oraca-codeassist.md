# Build a microservices application using Oracle AI Code Assist 

## Introduction

In this workshop you'll enhance the existing microservices application with a brand new component. Currently, we have a static ad message **2023 Thanks Giving Promotion: Buy 1 get 1!!!!** shown in the storefront. Watch as we use Oracle AI Code Assist to generate all the code for a Spring Boot-based Java app. That code has been provided as part of the workshop resources so now it's time to package and deploy it.

For this portion of the workshop, you have three different options to pick from when you reach **Task 2** - choose only one option:
1. [ ~20 minutes ] Build, package, and deploy the code entirely on your own.
2. [ ~10 minutes ] Run the pre-built script provided to automatically build and package the new app component. Then deploy to kubernetes.
3. [ ~5 minutes ] Deploy the new app component with the container image provided

Estimated time: Up to 20 minutes

### Objectives

* Update the MySQL HeatWave Database with a new table
* Choose how you want to deploy the new component


## Task 1: Create table **admessage** in the MySQL HeatWave Database

1. Deploy an OKE Pod containing the MySQL client that will be used to connect to the DB System.

      ```bash
      <copy>
      kubectl run mysql-client --image=iad.ocir.io/axfo51x8x2ap/load-mysql-data:latest -it --rm --restart=Never -- /bin/bash
      </copy>
      ```

      ![Kubectl command](images/3-1-1-admessage.png " ")

2. Execute the command below to connect to the MySQL HeatWave Database using the Private IP address of the database and the credentials provided when the DB System was created.

      ```bash
      <copy>
      mysql -h <mds-private-ip-address> -u <mds-admin-user> -p
      </copy>
      ```

      ![Kubectl command](images/3-1-2-admessage.png " ")

3. Execute the command below to connect to the **wine** database

    ```bash
    <copy>
    use wine;
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/3-1-3-admessage.png " ")

4. Execute below sql statement to create the table **admessage**, then insert a new record

    ```bash
    <copy>
    CREATE TABLE admessage (ID INT AUTO_INCREMENT PRIMARY KEY, message VARCHAR(255));
    INSERT INTO admessage (ID, MESSAGE) VALUES (1,'Welcome to MySQL DevLive Event');
    COMMIT;
    SELECT * FROM admessage;
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/3-1-4-admessage.png " ")


## Task 2 - Deployment Option 1: Full DIY Approach

The full do it yourself (DIY) approach involves building the app with the new code, using the output to create a new container image, pushing that image to the OCI Container Registry (OCIR), and deploying the app to Kubernetes. If you choose this path, you can then skip the remaining deployment options. This will take about 20 minutes.

1. Build an artifact from the source code.

    ```bash
    <copy>
    cd ~/oci-devlive-2024/src/admessage
    mvn clean install
    </copy>
    ```

    ![Cloud Shell - Maven build process](images/3-2-1-1-admessage.png " ")

2. Prepare the container image

    ```bash
    <copy>
    docker build -f Dockerfile -t admessage:latest .
    </copy>
    ```

    ```bash
    $ docker build -f Dockerfile -t admessage:latest .
    Sending build context to Docker daemon  85.02MB
    Step 1/5 : FROM openjdk:17-oracle
    ---> 5e28ba2b4cdb
    Step 2/5 : WORKDIR /spring
    ---> Using cache
    ---> 15a38db6ecb3
    Step 3/5 : COPY target/AdMessage-1.0.0.jar ./AdMessage.jar
    ---> 38102ba43ae6
    Step 4/5 : COPY src/main/resources/application.properties application.properties
    ---> 893058f7d71b
    Step 5/5 : ENTRYPOINT ["java","-jar","./AdMessage.jar","--spring.config.location=file:/spring/application.properties"]
    ---> Running in 2cc7d9c84d19
    Removing intermediate container 2cc7d9c84d19
    ---> 5640fc1e1362
    Successfully built 5640fc1e1362
    Successfully tagged admessage:latest
    ```

3. Retrieve the user credentials for connecting to the OCI Container Registry

    ```bash
    <copy>
    cd ~/oci-devlive-2024/deployment/terraform/
    terraform output -json
    </copy>
    ```

    ```bash
    {
        "deploy_id": {
            "sensitive": false,
            "type": "string",
            "value": "nj"
        },
        "repository_name": {
            "sensitive": false,
            "type": "string",
            "value": "devlive-nj-repository/admessage"
        },
        "user_auth_token": {
            "sensitive": true,
            "type": "string",
            "value": "z---redacted---t"
        },
        "user_email": {
            "sensitive": false,
            "type": "string",
            "value": "devlive-nj-ocir-user@example.com"
        },
        "user_name": {
            "sensitive": false,
            "type": "string",
            "value": "devlive-nj-ocir-user"
        }
    }
    ```

4. Copy the **value** for repository_name, user_auth_token, and user_name and store them for later use.

5. Retrieve the Object Storage Namespace for the tenancy and store it for later use.

    ```bash
    <copy>
    oci os ns get
    </copy>
    ```

    ```bash
    {
    "data": "a---redacted---2"
    }
    ```

6. Authenticate to OCIR. This will require the `user_name` and `user_auth_token` values copied earlier.

    ```bash
    <copy>
    echo "<replace with auth token value>" | docker login -u <os namespace>/user_name --password-stdin phx.ocir.io
    </copy>
    ```

    >**Note**: Once again, be sure to replace `phx` with the abbreviation for your selected region.

    ```bash
    $ echo "---redacted---" | docker login -u a---redacted---2/devlive-nj-ocir-user --password-stdin phx.ocir.io

    Login Succeeded
    ```
    
7. Tag the container image

    ```bash
    <copy>
    docker tag admessage phx.ocir.io/{object storage namespace}/devlive-##-repository/admessage:1.0.0
    </copy>
    ```

    >**Note**: `phx.ocir.io` is the endpoint for your selected region. If you are not using Phoenix, replace `phx` with the 3-letter abbreviation for your region.

    ```bash
    $ docker tag admessage phx.ocir.io/a---redacted---2/devlive-nj-repository/admessage:v1.0.0
    ```

8. Push the container image to OCIR

    ```bash
    <copy>
    docker push phx.ocir.io/a---redacted---2/devlive-##-repository/admessage:latest
    <copy>
    ```

    ```bash
    $ docker push phx.ocir.io/a---redacted---2/devlive-nj-repository/admessage:latest
    The push refers to repository [phx.ocir.io/a---redacted---2/devlive-nj-repository/admessage]
    68c651c86e51: Pushed 
    9d8f57404a71: Pushed 
    0bf5a6521e69: Pushed 
    dc9fa3d8b576: Pushed 
    27ee19dc88f2: Pushed 
    c8dd97366670: Pushed 
    latest: digest: sha256:94570178a7149ca8dda2b921b2e04440d99cbb94d5d89a960fe31eb1898d8f6a size: 1579
    ```

9. Modify the file **admessage.yaml** to update hte MySQL HeatWave Database Private IP and container image location.

    - Update the field for the MySQL HeatWave Databae Private IP (line 38)

    ![Oracle Cloud console, Cloud Shell](images/3-2-3-2-admessage.png " ")

    - Update the field for **image** (line 32). Use the full path from the previous `docker push` command.

    ![Oracle Cloud console, Cloud Shell](images/3-2-3-3-admessage.png " ")
    

    - Press the Esc key to ensure you are in command mode.
    - Type `:wq` (colon followed by wq) in the editor.
    - Press Enter to execute a save and exit.

10. Execute the command below to deploy the **AdMessage** application to the cluster.

    ```bash
    <copy>
    kubectl apply -f admessage.yaml --validate=false
    </copy>
    ```

    Verify the service and stateful set are both created:

    ![Oracle Cloud console, Cloud Shell](images/3-2-3-4-admessage.png)

11. Verify that the new **admessage** pod is running successfully

    ```bash
    <copy>
    kubectl get pods
    </copy>
    ```


    **Result**:

    ```bash
    $ kubectl get pods
    NAME             READY   STATUS    RESTARTS   AGE
    admessage-0      1/1     Running   0          31s
    wstore-back-0    1/1     Running   0          48m
    wstore-back-1    1/1     Running   0          48m
    wstore-front-0   1/1     Running   0          48m
    ```

## Task 2 - Deployment Option 2: Take the automated path

1. Run the super awesome script (TODO: expand further)

    ```bash
    <copy>
    cd ~/oci-devlive-2024
    npx zx scripts/artifacts.mjs
    </copy>
    ```

## Task 2 - Deployment Option 3: Just Deploy

1. Go back to the cloud shell and inside **~/sb-hol** directory, find **admessage.yaml**

   ![Oracle Cloud console, Cluster details](images/3-2-3-1-admessage.png " ")

   Admessage.yaml contains reference to the containerized image with packaged Admessage application built through Oracle AI Code assist.

2. Modify the file **admessage.yaml** to update the MySQL HeatWave Database Private IP 

    ``` bash
    <copy>
    vi admessage.yaml
    </copy>
    ```
    - Update field **<mds-private-ip-address>** with MySQL HeatWave Database Private IP (line 38) 

    ![Oracle Cloud console, Cloud Shell](images/3-2-3-2-admessage.png " ")

    - Press the Esc key to ensure you are in command mode.
    - Type :wq (colon followed by wq) in the vi editor.
    - Press Enter to execute the command to save the file 

    ![Oracle Cloud console, Cloud Shell](images/3-2-3-3-admessage.png " ")

3. Execute the command below to deploy the **AdMessage** application to the cluster.

    ``` bash
    <copy>
    kubectl apply -f ~/sb-hol/admessage.yaml --validate=false
    </copy>
    ```

    Verify the 2 services and 2 stateful sets are created

    ![Oracle Cloud console, Cluster details](images/3-2-3-4-admessage.png " ")

3. Run the kubectl command below to display the status of the pod creation. Wait until the statuses become 'Running'. This may take a few minutes.

    ``` bash
    <copy>
    kubectl get pods
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/3-2-3-5-admessage.png " ")

4. Run the kubectl command below to display the deployed services.

    ``` bash
    <copy>
    kubectl get svc
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/3-2-3-6-admessage.png " ")

## Task 3: Integrate the AdMessage API with the main Wine App

1. Modify the file **wstore.yaml** to update the endpoint of the **Admessage**

    ``` bash
    <copy>
    vi wstore.yaml
    </copy>
    ```
    - Update value of parameter  **winStore.services.adservice** with **AdMessage Endpoint** mentioned below. New endpoint is `adapi/admessage` (line 59)

    ``` bash
    <copy>
    http://${ADMESSAGE_SERVICE_HOST}:${ADMESSAGE_SERVICE_PORT}/adapi/admessage/
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/3-3-1-admessage.png " ")

    - Press the Esc key to ensure you are in command mode.
    - Type :wq (colon followed by wq) in the vi editor.
    - Press Enter to execute the command to save the file 

    ![Oracle Cloud console, Cloud Shell](images/3-3-2-admessage.png " ")
  
2. Execute the command below to deploy the application to the cluster.

    ``` bash
    <copy>
    kubectl apply -f ~/sb-hol/wstore.yaml --validate=false
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/3-3-3-admessage.png " ")

3. Run the kubectl command below to display the status of the pod creation. Wait until the statuses become 'Running'. This may take a few minutes.

    ``` bash
    <copy>
    kubectl get pods
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/3-3-4-admessage.png " ")

4. Run the kubectl command below to display the deployed services.

    ``` bash
    <copy>
    kubectl get svc
    </copy>
    ```
    ![Oracle Cloud console, Cloud Shell](images/3-3-5-admessage.png " ")

4. Launch the application to see new **ad message** 

    ``` bash
    <copy>
    http://<IP of the wstore-frontend service>/winestore/
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/3-3-6-admessage.png " ")

5. Additional task: Update table **admessage** to see how the admessage changes on update of table and refreshing the winestore url in the browser. 

    ``` bash
    <copy>
    UPDATE admessage SET message="Oracle AI Code Assistant HOL" WHERE ID=1;
    COMMIT;
    SELECT * FROM admessage;

    </copy>
    ```

You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Wojciech Pluta, Principal Staff Developer
- **Contributors** -
Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
Victor Martin, Product Strategy Directory 
Eli Schilling, Developer Advocate
* **Last Updated By/Date** - Eli Schilling, February 2024