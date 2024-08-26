# Provision the infrastructure

## Introduction

This workshop uses Spring Boot-based Java microservices connecting to a MySQL HeatWave database as a target application to illustrate the capabilities for end-to-end monitoring using OCI Observability and Management Services. In this lab, you will provision an Oracle Container Engine for Kubernetes (OKE) cluster and a MySQL HeatWave DB System through the OCI Console.

Estimated time: 35 minutes

### Objectives

* Create a compartment
* Provision Oracle Container Engine for Kubernetes (OKE) cluster & MySQL HeatWave DB System

### Prerequisites

* This lab requires an [Oracle Cloud account](https://www.oracle.com/cloud/free/). You may use your cloud account, or a Free tier account, a cloud account that you obtained through a trial.


## Task 1: Create an OCI compartment

1. Open the navigation menu from the top-left corner (aka. hamburger menu) of the Oracle Cloud console and select **Identity & Security** > **Compartments**.
	![Oracle Cloud console Menu](images/1-1-compartments.png " ")
2. Click **Create Compartment**
	![Oracle Cloud console, Create Compartment](images/1-2-compartments.png " ")
3. Enter the following parameters:
*	Compartment name: **devlive24**
*	Description: **Compartment for 2024 DevLive Hands-on lab**
*	Accept the default values for the other fields, and click, **Create Compartment**
	![Oracle Cloud console, Create Compartment](images/1-3-compartments.png " ")
*	Verify that your **devlive24** compartment is created in the table
	![Oracle Cloud console, Create Compartment](images/1-4-compartments.png " ")

## Task 2: Create a policy for the volume management 

1. Open the navigation menu from the top-left corner (aka. hamburger menu) of the Oracle Cloud console and select **Identity & Security** > **Policies**.
      ![Oracle Cloud console Menu](images/1-5-policy.png " ")

2. Select **root** tenancy from the compartment drop down and then click on **Create Policy**
      ![Oracle Cloud console Menu](images/1-6-policy.png " ")

3. Enter the following parameters:
    - Policy name: **OCIVolumeMgmt**
    - Description: **OCI Volume Mgmt**
    - Compartment: select root compartment 
    - Click on **Show manual editor** in Policy Builder
    - Copy the below policies and paste in the editor
     
      ```bash
      <copy>
      ALLOW any-user to manage volumes in TENANCY where request.principal.type = 'cluster'
      ALLOW any-user to manage volume-attachments in TENANCY where request.principal.type = 'cluster'
      </copy>
      ```
    - click, **Create**
    ![Oracle Cloud console Menu](images/1-7-policy.png " ")
    ![Oracle Cloud console Menu](images/1-8-policy.png " ")

## Task 3: Setup up cloud shell and code editor

1. Click on the below link to open OCI Code Editor and clone the repository 

    [Open Code Editor and Clone the repository](https://cloud.oracle.com/?region=home&cs_repo_url=https://github.com/oracle-devrel/oci-devlive-2024.git&cs_branch=main&cs_readme_path=README.md&cs_open_ce=true)

2. Retrieve the sample code and supporting scripts that will be used in this section
    - Click on the **I have reviewed and accepted the Oracle Terms of Use.** checkbox 
    - Click on **Clone**

    ![Code Editor](images/3-2-1-clone.png " ")

    Repository is successfully cloned and its shown in the code editor 
    ![Code Editor](images/3-2-2-clone.png " ")

3. Change orientation of the Cloud Shell and Code Editor 
    - Click on the **Actions** and then **Tabs** 
    ![Code Editor](images/3-2-3-codeeditor.png " ")

    - Now Cloud Shell and Code Editors are shown as tabs 
    ![Code Editor](images/3-2-4-codeeditor.png " ")

    - Now the cloud shell and code editor are set. Proceed to **Task 4**

## Task 4: Create a Kubernetes Cluster 

1. From the OCI menu, select **Developer Services**, then **Containers & Artifacts > Kubernetes Clusters (OKE)**.
	![Oracle Cloud console Menu](images/3-1-1-nodepool.png " ")

2. Select the compartment **devlive24** and then click on **Create cluster**
	![Oracle Cloud console Menu](images/3-1-2-nodepool.png " ")

3. Quick Create pane is pre-selected. Keep the default selection and click **Submit**.
	![Oracle Cloud console Menu](images/3-1-3-nodepool.png " ") 

4. Enter the following parameters:
    * Name the cluster: **devlive24-oke**
    * Kubernetes API endpoint : Select **Public endpoint**
    * Node type : Select **Managed**
    ![Oracle Cloud console Menu](images/3-1-4-nodepool.png " ") 
    * Kubernetes worker nodes : Select **Private workers**
    * Shape and image: **Keep default**
    ![Oracle Cloud console Menu](images/3-1-5-nodepool.png " ") 
    * Node count: **1**
    * Click **Next**
    ![Oracle Cloud console Menu](images/3-1-6-nodepool.png " ") 
    * Review the configuration, and click **Create cluster**.
    ![Oracle Cloud console Menu](images/3-1-7-nodepool.png " ") 
    * Make sure all verification steps are cleared. Click **Close**
    ![Oracle Cloud console Menu](images/3-1-8-nodepool.png " ") 

> **Note:** This will start to create a cluster, and takes 7 to 10 minutes to complete. While waiting for the creation of the cluster, you can proceed to the next task to provision the **MySQL HeatWave Database**


## Task 5: Deploy the MySQL Database System

1.	From the OCI menu, select **Databases**, then **MySQL HeatWave > DB Systems**.
	![Oracle Cloud console Menu](images/3-1-mysqlheatwave.png " ")

2. Select the **devlive24** compartment from the pulldown menu and Click **Create DB System**
	![Oracle Cloud console, DB Systems](images/3-2-mysqlheatwave.png " ")

3.	Choose **Production** and select the **devlive24** compartment and provide name **mysql-appdev**  for the MySQL HeatWave Database
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-3-mysqlheatwave.png " ")

4. Provide MySQL database administrator credentials (store these credentials for the later use) & choose **Standalone**
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-4-mysqlheatwave.png " ")

5. Choose the VCN **`oke-vcn-quick-devlive24-oke-#########`** and private subnet for the MySQL DB System **`oke-nodesubnet-quick-devlive24-oke-#########-regional`** to allow access to MySQL HeatWave database from Kubernetes nodes and keep placement settings default.  
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-5-mysqlheatwave.png " ")
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-6-mysqlheatwave.png " ")

6. Uncheck **Enable HeatWave** checkbox and keep hardware settings default.
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-6-2-mysqlheatwave.png " ")

7. Uncheck **Enable automatic backups**, then click _`Show advanced options`_. Uncheck **Delete protected** under **Deletion Plan** Tab and verify if **Database Management** under  **Management** Tab is checked and then click on **Create**
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-7-mysqlheatwave.png " ")
  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-8-mysqlheatwave.png " ")

8. This will start to create a MySQL HeatWave Database, and takes 10-15 minutes to complete. While waiting for the creation of the MySQL HeatWave Database, learn more about MySQL HeatWave Database Management through the recorded demos mentioned below. In Lab 2, we will resume the steps to deploy the application connecting to the MySQL HeatWave Database.

  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-9-mysqlheatwave.png " ")

   Watch a video demonstration of monitoring and managing MySQL HeatWave Database 
   [](youtube:4VlRypYXJ48?si=k68OnLN9XI4KXo9B)

   Watch a video demonstration of tuning MySQL HeatWave DB System queries using  Performance Hub
   [](youtube:vXqA8nkcF4c?si=B314cImffyHCfk1b)

9. Once the MySQL HeatWave Database created successfully,then go to **Connections** tab to copy and save the **Private IP Address** of MySQL HeatWave Database and also database credentails to a text file to use in lab 2 and 3. 

  ![Oracle Cloud console, Create MySQL HeatWave Database](images/3-10-mysqlheatwave.png " ")


[You may now **proceed to the next lab**.](#next)


## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
* **Last Updated By/Date** - Anand Prabhu, January 2024