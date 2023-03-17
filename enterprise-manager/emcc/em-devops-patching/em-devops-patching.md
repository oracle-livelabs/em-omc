# Patch Oracle databases with Ansible and Enterprise Manager

## Introduction

In this workshop you will get hands-on experience with the database patching capabilities of the Database as A Service offering in Oracle Enterprise Manager 13c with DevOps tools like Ansible.

*Estimated Time:* 120 minutes


### Objectives

In this lab you will learn:


| **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1**  | Install and Configure Ansible                               | 10 minutes       | Prepare the Live Labs environment in order to use Ansible as a DevOps automation/orchestration tool.                                                                                         | DevOps tools or toolchains help customers to automate tasks in their datacenter. This Lab makes use of Ansible as an orchestration tool.                                                                                                                                                                                                                                                                      |
| **2**  |  Setup DBaaS Pools and verify integration with Ansible             | 10 minutes       | EM's DBaaS extends the Oracle Private Cloud Management solution by automating the lifecycle of a database and allowing users to request database services through self-service portal or REST API's. This step covers how to setup a DBaaS pool in Enterprise Manager.                                                                                            | With this solution, IT Managers no longer have to perform mundane administrative tasks for provisioning databases. Database users can get instantaneous access to new database services through the Self Service Portal or REST API's.                                                                                                                                                                                                                                                                     |
| **3**  | Provision a PDB using DBaaS and Ansible             | 10 minutes       | DevOps orchestration tools like Ansible, Chef, Terraform, etc., can easily integrate with EM 13c in order to provision Oracle databases.                                                                                            | EM 13c implements pre-checks, best practices and processes to provision all these configurations in a secure, automated and controlled fashion.                                                                                                                                                                                                                                                      |
| **4**  | Configure Fleet Maintenance (Gold Image, Container and Pool)        | 80 minutes       | Once provisioned, Oracle databases need to be well maintained and secured. All these database lifecycle activity tasks can be automated by integrating EM 13c with orchestration DevOps tools. This step highlights the configuration needed to integrate DBaaS with Fleet Maintenance for patching databases.                                               | DB lifecycle activities can be easily scheduled using DevOps tools and Oracle Enterprise Manager 13c. There's no need to login directly to the DB as EM provides a secure framework for all these activities.                                                                                                                                                                                                                                                                                                                                                                                          |
| **5**  | Patch a PDB using DBaaS and Ansible       | 10 minutes       | In this activity you'll patch a PDB using an ansible YAML file and the previously configured DBaaS and Fleet Maintenance integration.                                                                                                                                        | The automation achieved by integrating DevOps tools with DBaaS enables administrators to focus in other activities rather than spending time on patching databases.  |


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- SSH Private Key to access the host via SSH
- You have completed:
    - Lab: Generate SSH Keys (*Free-tier* and *Paid Tenants* only)
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository. It's highly recommended to first execute the "Deploy and Manage Oracle Databases with Ansible and Enterprise Manager" LiveLabs workshop in order to explore the database management basics.

## Task 1: Install and Configure Ansible

1. From your remote desktop session, open a terminal window. Type and execute the command below in order to install Ansible in the environment.

    ```
    <copy>sudo yum install -y ansible</copy>
    ```

    ![Install Ansible](../em-devops-patching/images/install-ansible.png " ")

    Then hit the **Enter** key on your keyboard.

2. Ansible is now installed in the Lab environment. Modify the Ansible inventory file. Using the same SSH terminal, execute below command.

    ```
    <copy>sudo vi /etc/ansible/hosts</copy>
    ```

    Then hit **Enter** on your keyboard. Scroll down to the bottom of the file and hit the **i** letter on your keyboard. Now add below lines.

    ```
    <copy>[emserver]
    emcc.marketplace.com</copy>
    ```

    ![Edit Ansible Configuration](../em-devops-patching/images/edit-ansible-config.png " ")

    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

3. Verify that Ansible can properly ping the configured **emserver**. Execute below command:

    ```
    <copy>ansible emserver -m ping -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    Once prompted, type **yes** and hit **Enter** on your keyboard.

    ```
    Are you sure you want to continue connecting (yes/no)? yes
    ```

    ![Test Ansible Connectivity](../em-devops-patching/images/test-ansible-connect.png " ")

    Verify that you receive the **pong** response from Ansible.

4. Create a directory where Ansible's YAML files will be placed. Then **cd** into the new directory.

    ```
    <copy>mkdir -p /home/oracle/ansible/yml
    cd /home/oracle/ansible/yml</copy>
    ```

    ![Create Ansible Directories](../em-devops-patching/images/create-ansible-dirs.png " ")


## Task 2: Setup DBaaS Pools and verify integration with Ansible

1. Using the terminal window execute below EMCLI command in order to make the "ROOT" named credential global.

    ```
    <copy>emcli modify_named_credential -cred_name=root -cred_scope=global</copy>
    ```

    ![EMCLI Command To Make ROOT Global](../em-devops-patching/images/emcli-root-global-cred.png " ")

2. Open the Oracle Enterprise Manager console window and login as "SYSMAN".

    ![EM SYSMAN Login](../em-devops-patching/images/em-sysman-login.png " ")

3. Startup the "db19c.subnet.vcn.oraclevcn.com" database. In the Enterprise Manager console navigate to **Targets** -> **Databases**.

    ![EM Navigation](../em-devops-patching/images/em-targets-databases.png " ")

4. Click on the "db19c.subnet.vcn.oraclevcn.com" database.

    ![db19c Select](../em-devops-patching/images/em-select-db19c.png " ")

5. Navigate to **Oracle Database** then **Control** and click on **Startup/Shutdown** menu.

    ![EM db19c Start DB](../em-devops-patching/images/em-db19c-start.png " ")

6. Select both **Named** credentials for "Host" and "Database" and click **Ok**.

   Host credential: **ORACLE**

   Database credential: **OEM_SYS**

    ![EM db19c Set Credentials](../em-devops-patching/images/em-start-db19c-creds.png " ")

7. On the "Startup/Shutdown: Confirmation" page click **Yes**. Wait until the database is up and running.

    ![EM db19c Start DB](../em-devops-patching/images/em-db19c-start-confirm.png " ")

    ![EM db19c Start Progress](../em-devops-patching/images/em-db19c-start-progress.png " ")

8. Setup a new Pluggable Database (PDB) Pool in the DBaaS setup. Navigate to Setup -> Cloud and click on **Database**.

    ![EM Navigation](../em-devops-patching/images/em-cloud-database.png " ")

9. Select the **Pluggable Database** option from the "Getting Started" page.

    ![EM Cloud Dashboard](../em-devops-patching/images/em-cloud-pdb.png " ")

10. Click on **Pluggable Database Pool** menu and then click on the **Create** button.

    ![EM Create Pool](../em-devops-patching/images/em-cloud-pdbpool-create.png " ")

11. On the "Setup" page type the following entries:

    Pool Details:
      - Name: **PDB_POOL**

    Credentials:
      - Database Named Credential: **Named** -> **ORACLE(SYSMAN)**
      - Root Credentials: **Named** -> **ROOT(SYSMAN)**
      - Database: **Named** -> **SYS_SALES(SYSMAN)**

      **Note**: Leave the Grid Infrastructure Home Credentials empty (Default)

    Container Databases:
      - PaaS Infrastructure Zone: **Sales Infra Zone**
      - Platform: **Linux x86-64**
      - Target Type: **Database Instance**
      - Version: **19.0.0.0.0**

    Validate and compare these inputs with the image below.

    ![EM Setup Details](../em-devops-patching/images/em-cloud-pool-setup-details.png " ")

12. Click on the **Add** button.

    ![EM Add Database](../em-devops-patching/images/em-cloud-pool-add-database.png " ")

13. Select the "db19c.subnet.vcn.oracle.com" and click **Select**.

    ![EM Select db19c](../em-devops-patching/images/em-cloud-pool-select-db19c.png " ")

14. Click on the **Next** button.

    ![EM Next Button](../em-devops-patching/images/em-cloud-pool-next.png " ")

15. Leave the defaults and click on **Submit**. Wait until the new "PDB_POOL" is created.

    ![EM Submit Button](../em-devops-patching/images/em-cloud-pdbpool-submit.png " ")

16. Click on **Service Templates** menu and select the "Provision New Empty Pluggable Database" offering. Then click on **Edit**.

    ![EM Cloud Templates](../em-devops-patching/images/em-cloud-template-edit.png " ")

17. Notice that the "Sales Infra Zone" is currently assigned to the "pdbpool" that already existed. We want to assign the newly created "PDB_POOL". Click on **Assign Pool** button.

    ![EM Assign Pool](../em-devops-patching/images/em-cloud-template-assign-pool.png " ")

18. Select the "PDB_POOL" and then click the **Select** button.

    ![EM PDBPOOL](../em-devops-patching/images/em-cloud-template-pdbpool.png " ")

19. Click **Next**.

    ![EM Template Review](../em-devops-patching/images/em-cloud-template-review.png " ")

20. On the next set of pages **don't** modify anything. Just click **Next** until you are in the final "Review" page.
    In the "Review" page click **Edit**.

    ![EM Submit Button](../em-devops-patching/images/em-cloud-template-submit.png " ")

## Task 3: Provision a PDB using DBaaS and Ansible

1. In this step, we are going to make use of both **uri** parameters below. These **uri** parameters are part of the "Service Template" configuration. You can get these parameters by executing the get PaaS Zone REST API. This step won't cover how to get those parameters. We are just going to review them and make use of them in the next steps.

    ```
    zone:
    "uri": "/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3"

    service_template:
    "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/1"
    ```

2. Go back to the SSH terminal and create a new YAML (.yml) file.

    ```
    <copy>vi /home/oracle/ansible/yml/request_pdb.yml</copy>
    ```

    **NOTE:**

    a) The main url is made with the zone's uri reviewed in the previous step.

    b) We are passing the service_template uri in the body of the json file.

    Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

    ```
    <copy>---
    - name: Using a REST API
      become: false
      hosts: emserver
      gather_facts: false
      vars:
         nextdate: "{{ lookup('pipe', 'date --date=\"next day\" \"+%Y-%m-%dT%k:%M:%SZ%z\"') }}"
      tasks:

        - name: Request PDB
          uri:
            url: https://emcc.marketplace.com:7803/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3
            method: POST
            return_content: yes
            force_basic_auth: yes
            validate_certs: no
            body_format: json
            headers:
               Authorization: basic Q1lSVVM6d2VsY29tZTE=
               Content-Type: application/oracle.com.cloud.common.PluggableDbPlatformInstance+json
               Accept: application/oracle.com.cloud.common.PluggableDbPlatformInstance+json
            body:
              {
                 "based_on": "/em/cloud/dbaas/pluggabledbplatformtemplate/1",
                 "name": "API_Request_PDB",
                 "end_date": "{{ nextdate }}",
                 "params":
                 {
                     "username": "PDBADMIN",
                     "password": "welcome1" ,
                     "pdb_name" : "pdb_api1" ,
                     "workload_name" : "Small" ,
                     "service_name" : "SRVPDBA1",
                     "tablespaces" :
                     [
                       "pdb_tbs1"
                     ]
                 }
              }
          register: results

        - name: Print returned json dictionary
          debug:
            var: results.json</copy>
    ```

    Then hit the **Esc** key on your keyboard and type **:wq**, then hit the **Enter** key on your keyboard to save the file.

    Take a moment to review the parameters passed to Oracle Enterprise Manager in the JSON file. We are passing the PDB Admin username and password, the name of the new PDB, the workload settings, the PDB's service name and the PDB's tablespace.

    ```
    "params":
               {
                   "username": "PDBADMIN",
                   "password": "welcome1" ,
                   "pdb_name" : "pdb_api1" ,
                   "workload_name" : "Small" ,
                   "service_name" : "SRVPDBA1",
                   "tablespaces" :
                   [
                     "pdb_tbs1"
                   ]
               }
    ```


3. Execute the Ansible Playbook with the YAML file we just created.

    ```
    <copy>ansible-playbook /home/oracle/ansible/yml/request_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    ![Ansible Request PDB](../em-devops-patching/images/ansible-request-pdb.png " ")


4. Review the status of the provisioning request. Review the output of the previous request and find the **uri**.
    In this case, the uri of the provisioning request is.

    ```
    /em/cloud/dbaas/pluggabledbplatforminstance/byrequest/61
    ```

    Create a new YAML (.yml) file as below.

    ```
    <copy>vi /home/oracle/ansible/yml/get_pdb_status.yml</copy>
    ```

    Use the entries below, update the **uri** accordingly with the one we just reviewed and paste those entries in the new YAML file.

    Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

    ```
    <copy>---
    - name: Using a REST API
      become: false
      hosts: emserver
      gather_facts: false
      tasks:

        - name: Get PDB Creation Details
          uri:
            url: https://emcc.marketplace.com:7803/em/cloud/dbaas/pluggabledbplatforminstance/byrequest/61
            method: GET
            return_content: yes
            force_basic_auth: yes
            validate_certs: no
            headers:
              Authorization: basic Q1lSVVM6d2VsY29tZTE=
          register: results

        - name: Print returned json dictionary
          debug:
            var: results.json</copy>
    ```

    Then hit the **Esc** key on your keyboard and type **:wq**, then hit the **Enter** key on your keyboard to save the file.

    Execute the YAML file.

    ```
    <copy>ansible-playbook /home/oracle/ansible/yml/get_pdb_status.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    ![Ansible Get Status](../em-devops-patching/images/ansible-get-request-status.png " ")

    Re-execute the get_pdb_status.yml command until you see that the PDB was successfully created. STATUS should be set as RUNNING.

5. Go back to the Oracle Enterprise Manager web console and logout from the "SYSMAN" account. After this, login using "CYRUS" user.
    Cyrus is a user that has access and all the required privileges to use the DBaaS "Self Service Portal".

    ```
    CYRUS/welcome1
    ```

    ![EM SYSMAN Logout](../em-devops-patching/images/em-sysman-logout.png " ")

    ![EM Login CYRUS](../em-devops-patching/images/em-login-cyrus.png " ")

6. Verify that the new PDB shows up in the portal.

    ![EM Verify PDB Status](../em-devops-patching/images/em-verify-pdb.png " ")

7. Click on the new SSAPDB_API1 name and verify the current PDB software version is 19.12 RU.

    ![EM Verify DB Version](../em-devops-patching/images/em-verify-pdb-version.png " ")

## Task 4: Configure Fleet Maintenance (Gold Image, Container and Pool)

1. Download a new Enterprise Manager Fleet Maintenance Gold Image version. This Gold Image will be imported into Fleet Maintenance.

    ```
    <copy>cd ~
    wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/oRaI83p8c3Iak4hcqzVmCewOi_NmBXfwNkCWD6Mm8aNXlWMMjyEaOnRgWr3rtLfy/n/natdsecurity/b/labs-files/o/19.14ExportGoldImage.zip</copy>
    ```

    ![Fleet Get Image](../em-devops-patching/images/fleet-get-image.png " ")

2. Create a script with all the required parameters to import the downloaded Gold Image.

    ```
    <copy>cd /home/oracle/fleet
    vi sidb19c_tier3.inp
    </copy>
    ```

    Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

    ```
    <copy>IMAGE_NAME=Tier #3 SI DB Linux64
    IMAGE_DESCRIPTION=Tier #3 Gold Image for  Single Instance Oracle  DB on Linux x86_64
    HOST_NAME=emcc.marketplace.com
    HOST_CREDENTIAL=ORACLE:SYSMAN
    GOLD_IMAGE_BUNDLE_LOCATION=/home/oracle/
    GOLD_IMAGE_BUNDLE_NAME=19.14ExportGoldImage.zip
    IMAGE_SWLIB_LOC=Fleet Maintenance/
    STORAGE_TYPE_FOR_SWLIB=OmsShared
    STORAGE_NAME_FOR_SWLIB=default_loc
    WORKING_DIRECTORY=/tmp
    VERSION_NAME=19.14</copy>
    ```

    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

    Execute below EMCLI command in order to import the Gold Image.

    ```
    <copy>emcli db_software_maintenance -importSoftwareImage -input_file="data:/home/oracle/fleet/sidb19c_tier3.inp"</copy>
    ```

    ![Fleet Import Image](../em-devops-patching/images/fleet-import-image.png " ")

3. Go back to the Oracle Enterprise Manager console and logout from the "CYRUS" account.

    ![EM CYRUS Logout](../em-devops-patching/images/em-cyrus-logout.png " ")

4. Login using the "SYSMAN" account.

    ![EM SYSMAN Logout](../em-devops-patching/images/em-sysman-login-4.png " ")

5. Navigate to Enterprise -> Provisioning and Patching and click on **Procedure Activity**.

    ![EM Procedure Activity](../em-devops-patching/images/em-procedure-activity.png " ")

6. Click on the **ImportSoftwareImage_SYSMAN** task that was just created and refresh the screen until the task successfully completes.

    ![EM Procedure Import Image](../em-devops-patching/images/em-procedure-import-image.png " ")

    ![EM Procedure Import Image Status](../em-devops-patching/images/em-procedure-import-image-status.png " ")

    Then remove the downloaded .zip file used to create the Gold Image:

    ```
    <copy>cd ~
    rm 19.14ExportGoldImage.zip</copy>
    ```

7. Go back to the SSH terminal and execute below EMCLI command to verify the Gold Image details.

    ```
    <copy>emcli db_software_maintenance -getImages</copy>
    ```

    ![Fleet Get Image](../em-devops-patching/images/fleet-get-image-list.png " ")

8. Notice the **IMAGE ID** column. Using the value of this column get the Gold Image version.

    ```
    <copy>emcli db_software_maintenance -getVersions -image_id=<paste the image id here></copy>
    ```

    ![Fleet Get Version](../em-devops-patching/images/fleet-get-version.png " ")

9. Subscribe the recently created **PDB_POOL** in the DBaaS setup with this Gold Image. Use the **IMAGE ID** used in the previous step.

    ```
    <copy>emcli db_cloud_maintenance -subscribeTarget -pool_name=PDB_POOL -pool_type=pdbaas_pool -image_id=<paste the image id here></copy>
    ```

    ![Fleet Subscribe Pool](../em-devops-patching/images/fleet-subscribe-pool.png " ")

10. Deploy a new Oracle Home that will host a new 19c container using the 19.14 Gold Image.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="DEPLOY_DB_SOFTWARE" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Deploy Patch OH for Pool" -target_type=oracle_home -description="Deploys the Patched Oracle home on target nodes" -input_file="data:/home/oracle/fleet/deploy197_hr.inp"</copy>
    ```

    ![Fleet Deploy Software](../em-devops-patching/images/fleet-deploy-software.png " ")

11. Go back to the Oracle Enterprise Manager console. Navigate to Enterprise -> Provisioning and Patching and click on **Procedure Activity**. Monitor the deployment procedure.

    ![EM Procedure Deploy Software](../em-devops-patching/images/em-procedure-deploy-software.png " ")

    ![EM Procedure Deploy Software Status](../em-devops-patching/images/em-procedure-deploy-software-status.png " ")

12. There's a local listener on the current 19c Oracle Home. This listener needs to be migrated to the 19.14 Oracle Home before we can create the new 19.14 container database.
    Go back to the SSH terminal and execute below EMCLI command.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="MIGRATE_LISTENER" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Migrate Listeners" -description="Migrate the listeners to the new Oracle Home, if any"</copy>
    ```

    ![Fleet Migrate Listener](../em-devops-patching/images/fleet-migrate-listener.png " ")

13. Monitor the deployment procedure execution using the Enterprise Manager console.

    ![EM Procedure Migrate Listener](../em-devops-patching/images/em-procedure-migrate-listener.png " ")

    ![EM Procedure Migrate Listener Status](../em-devops-patching/images/em-procedure-migrate-listener-status.png " ")

14. Create a new container database (CDB) using the Oracle Home that was just deployed from the 19.14 Gold Image. Go back to the SSH terminal and execute.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="DEPLOY_CDB" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Deploy CDB" -target_type=oracle_database -description="Deploy a new CDB on the new OH for every CDB on the Pool using the prefix" -db_prefix="ssa"</copy>
    ```

    ![Fleet Deploy CDB](../em-devops-patching/images/fleet-deploy-cdb.png " ")

15. Monitor the deployment procedure execution using the Enterprise Manager console.

    ![EM Procedure Deploy CDB](../em-devops-patching/images/em-procedure-deploy-cdb.png " ")

    ![EM Procedure Deploy CDB Status](../em-devops-patching/images/em-procedure-deploy-cdb-status.png " ")

16. Activate the newly created container database (CDB). This means that the PDB_POOL now knows that a new version of the CDB exists and is ready for use.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="ACTIVATE_CDB" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Activate the CDBs" -target_type=oracle_database -description="Activates the newly created CDBs"</copy>
    ```

    ![Fleet Activate Container](../em-devops-patching/images/fleet-activate-container.png " ")


## Task 5: Patch a PDB using DBaaS and Ansible

1.  In this step we are going to patch the recently created PDB. Remember that this PDB was created using Ansible and by making use of the existing db19c.subnet.vcn.oraclevcn.com CDB. This CDB is currently running on 19.12 Oracle Home and we want to patch this PDB to 19.14 RU.
    In order to automate this process we are going to use an Ansible YAML file to update the PDB to the CDB deployed by EM running on the 19.14 Oracle Home.

2.  Execute below.

    ```
    <copy>cd ~/ansible/yml/
    vi /home/oracle/ansible/yml/update_pdb.yml</copy>
    ```

    Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

    ```
    <copy>---
    - name: Using a REST API
      become: false
      hosts: emserver
      gather_facts: false
      tasks:

        - name: Resize PDB
          uri:
            url: https://emcc.marketplace.com:7803/em/cloud/dbaas/pluggabledbplatforminstance/byrequest/61
            method: POST
            return_content: yes
            force_basic_auth: yes
            validate_certs: no
            body_format: json
            headers:
               Authorization: basic Q1lSVVM6d2VsY29tZTE=
               Content-Type: application/oracle.com.cloud.common.PluggableDbPlatformInstance+json
               Accept: application/oracle.com.cloud.common.PluggableDbPlatformInstance+json
            body:
              {
                 "operation":"UPDATE_DATABASE",
                 "update_schedule":"",
              }
          register: results

        - name: Print returned json dictionary
          debug:
            var: results.json</copy>
    ```

    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

    Execute the YAML file.

    ```
    <copy>ansible-playbook /home/oracle/ansible/yml/update_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    ![Ansible Update PDB](../em-devops-patching/images/ansible-update-pdb.png " ")


9.  Go back to the Oracle Enterprise Manager web console. Navigate to Enterprise -> Provisioning and Patching -> **Procedure Activity**.

    ![EM Provisioning Activity](../em-devops-patching/images/em-provisioning-activity.png " ")

10. Monitor the **UPDATE** procedure.

    ![EM Procedure Update PDB](../em-devops-patching/images/em-procedure-update-pdb.png " ")

    ![EM Procedure Update PDB Status](../em-devops-patching/images/em-procedure-update-pdb-status.png " ")

11. Logout from the SYSMAN account and login with CYRUS user.

    ![EM SYSMAN Logout](../em-devops-patching/images/em-sysman-logout.png " ")

    ![EM CYRUS Login](../em-devops-patching/images/em-login-cyrus.png " ")

12. Click on the SSAPDB_API1 database.

    ![EM Select PDB](../em-devops-patching/images/em-cyrus-pdb1-select.png " ")

13. Confirm the version is now 19.14 RU for the PDB.

    ![EM PDB Version](../em-devops-patching/images/em-cyrus-pdb1-version.png " ")

    At this stage any new PDB request using the PDB_POOL will be serviced by the recently activated 19.14 CDB.

This completes the Lab!

You may [proceed to the next lab](#next).

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements
- **Author** - Alfredo Krieg, NA Technology, August 2022
* **Contributors** - 
* **Last Updated By/Date** - March 2023
