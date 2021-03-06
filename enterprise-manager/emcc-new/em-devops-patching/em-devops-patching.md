# EM DevOps Patching

## Introduction

In this workshop you will get hands-on experience with the database patching capabilities of the Database as A Service offering in Oracle Enterprise Manager 13c with DevOps tools like Ansible.

*Estimated Time:* 130 minutes


### Objectives

In this lab you will learn:


| **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1**  | Install and Configure Ansible                               | 10 minutes       | Prepare the Live Labs environment in order to use Ansible as a DevOps automation/orchestration tool.                                                                                         | DevOps tools or toolchains help customers to automate tasks in their datacenter. This Lab makes use of Ansible as an orchestration tool.                                                                                                                                                                                                                                                                      |
| **2**  |  Setup DBaaS Pools and verify integration with Ansible             | 20 minutes       | EM's DBaaS extends the Oracle Private Cloud Management solution by automating the lifecycle of a database and allowing users to request database services through self-service portal or REST API's.                                                                                             | With this solution, IT Managers no longer have to perform mundane administrative tasks for provisioning databases. Database users can get instantaneous access to new database services through the Self Service Portal or REST API's.                                                                                                                                                                                                                                                                     |
| **3**  | Provision a PDB using DBaaS and Ansible             | 10 minutes       | DevOps orchestration tools like Ansible, Chef, Terraform, etc., can easily integrate with EM 13c in order to provision Oracle databases.                                                                                            | EM 13c implements pre-checks, best practices and processes to provision all these configurations in a secure, automated and controlled fashion.                                                                                                                                                                                                                                                      |
| **4**  | Configure Fleet Maintenance (Gold Image, Container and Pool)        | 80 minutes       | Once provisioned, Oracle databases need to be well maintained and secured. All these database lifecycle activity tasks can be automated by integrating EM 13c with orchestration DevOps tools.                                                | DB lifecycle activities can be easily scheduled using DevOps tools and Oracle Enterprise Manager 13c. There's no need to login directly to the DB as EM provides a secure framework for all these activities.                                                                                                                                                                                                                                                                                                                                                                                          |
| **5**  | Patch a PDB using DBaaS and Ansible       | 10 minutes       | In this activity you'll see how a pluggable database is terminated and deleted from EM's DBaaS framework using Ansible playbooks.                                                                                                                                        | This last Lab provides information on how to decommission a PDB from EM's DBaaS setup as well as a glance on all the requests submitted to EM through Ansible. |


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- SSH Private Key to access the host via SSH
- You have completed:
    - Lab: Generate SSH Keys (*Free-tier* and *Paid Tenants* only)
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository.

## Task 1: Install and Configure Ansible

1. From your remote desktop session, open a terminal window. Type and execute the command below in order to install Ansible in the environment.

    ```
    <copy>sudo yum install -y ansible</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch1step1.png " ")

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

    ![](../em-devops-patching/images/emdevpatch1step2.png " ")

    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

3. Verify that Ansible can properly ping the configured **emserver**.

    ```
    <copy>ansible emserver -m ping -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    Type **yes** and hit **Enter** on your keyboard.

    ```
    Are you sure you want to continue connecting (yes/no)? yes
    ```

    ![](../em-devops-patching/images/emdevpatch1step3.png " ")

    Verify that you receive the **pong** response from Ansible.

4. Create a directory where Ansible's YAML files will be placed. Then **cd** into the new directory.

    ```
    <copy>mkdir -p /home/oracle/ansible/yml
    cd /home/oracle/ansible/yml</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch1step4.png " ")


## Task 2: Setup DBaaS Pools and verify integration with Ansible

1. Using the terminal window execute below EMCLI command in order to make the "ROOT" named credential global.

    ```
    <copy>emcli modify_named_credential -cred_name=root -cred_scope=global</copy>
    ```


2. Open the Oracle Enterprise Manager console window and login as "SYSMAN".

    ![](../em-devops-patching/images/emdevpatch2step2.png " ")


3. Navigate to Setup -> Security and click on **Preferred Credentials**.

    ![](../em-devops-patching/images/emdevpatch2step3.png " ")    

4. In the Preferred Credentials window you will find a table containing information about Target Types. Select **Database Instance** and then click on **Manage Preferred Credentials**.

    ![](../em-devops-patching/images/emdevpatch2step4.png " ")

5. Under Database Instance Preferred Credentials make sure to select the **My Preferences** tab. Then using the Credentials table select **SYSDBA Database Credentials** and click the **Set** button. Choose the **SYS_SALES** named credential.
   Do the same for the **Database Host Credentials** and select the **ORACLE** named credential from the list.

    ![](../em-devops-patching/images/emdevpatch2step5a.png " ")

    ![](../em-devops-patching/images/emdevpatch2step5b.png " ")

6. Go back to the Preferred Credentials page.

    ![](../em-devops-patching/images/emdevpatch2step6.png " ")

7. Select the **Host** Target Type from the table and click on the **Manage Preferred Credentials** button.

    ![](../em-devops-patching/images/emdevpatch2step7.png " ")

8. Under Host Preferred Credentials make sure to select the **My Preferences** tab. Then using the Credentials table select **Normal Host Credentials** and click the **Set** button. Choose the **ORACLE** named credential.
   Do the same for the **Privileged Host Credentials** and select the **ROOT** named credential from the list.   

    ![](../em-devops-patching/images/emdevpatch2step8a.png " ")

    ![](../em-devops-patching/images/emdevpatch2step8b.png " ")

9. Go back to the Preferred Credentials page.

    ![](../em-devops-patching/images/emdevpatch2step9.png " ")

10. Select the **Oracle Home** Target Type from the table and click on the **Manage Preferred Credentials** button.

    ![](../em-devops-patching/images/emdevpatch2step10.png " ")

11. Under Oracle Home Preferred Credentials make sure to select the **My Preferences** tab. Then using the Credentials table select **Normal Host Credentials** and click the **Set** button. Choose the **ORACLE** named credential.
    Do the same for the **Privileged Host Credentials** and select the **ROOT** named credential from the list.

    ![](../em-devops-patching/images/emdevpatch2step11a.png " ")

    ![](../em-devops-patching/images/emdevpatch2step11b.png " ")

12. Startup the "db19c.subnet.vcn.oraclevcn.com" database. Go to **Targets** -> **Databases**.

    ![](../em-devops-patching/images/emdevpatch2step12.png " ")

13. Click on the "db19c.subnet.vcn.oraclevcn.com" database.

    ![](../em-devops-patching/images/emdevpatch2step13.png " ")

14. Navigate to **Control** and click on **Startup/Shutdown** menu.

    ![](../em-devops-patching/images/emdevpatch2step14.png " ")

15. Select both **Preferred** credentials for "Host" and "Database" and click **Ok**.

    ![](../em-devops-patching/images/emdevpatch2step15.png " ")

16. On the "Startup/Shutdown: Confirmation" page click **Yes**. Wait until the database is up and running.

    ![](../em-devops-patching/images/emdevpatch2step16a.png " ")

    ![](../em-devops-patching/images/emdevpatch2step16b.png " ")

17. Setup a new Pluggable Database (PDB) Pool in the DBaaS setup. Navigate to Setup -> Cloud and click on **Database**.

    ![](../em-devops-patching/images/emdevpatch2step17.png " ")

18. Select the **Pluggable Database** option from the "Getting Started" page.

    ![](../em-devops-patching/images/emdevpatch2step18.png " ")

19. Click on **Pluggable Database Pool** menu and then click on the **Create** button.

    ![](../em-devops-patching/images/emdevpatch2step19.png " ")

20. On the "Setup" page type the following entries:

    Pool Details:
      - Name: **PDB_POOL**

    Credentials:
      - Database Named Credential: **Preferred**
      - Root Credentials: **Preferred**
      - Database: **Preferred**

      **Note**: Leave the Grid Infrastructure Home Credentials empty (Default)

    Container Databases:
      - PaaS Infrastructure Zone: **Sales Infra Zone**
      - Platform: **Linux x86-64**
      - Target Type: **Database Instance**
      - Version: **19.0.0.0.0**

    Validate and compare these inputs with the image below.

    ![](../em-devops-patching/images/emdevpatch2step20.png " ")

21. Click on the **Add** button.

    ![](../em-devops-patching/images/emdevpatch2step21.png " ")

22. Select the "db19c.subnet.vcn.oracle.com" and click **Select**.

    ![](../em-devops-patching/images/emdevpatch2step22a.png " ")

23. Click on the **Next** button.

    ![](../em-devops-patching/images/emdevpatch2step23.png " ")

24. Leave the defaults and click on **Submit**. Wait until the new "PDB_POOL" is created.

    ![](../em-devops-patching/images/emdevpatch2step24.png " ")

25. Click on **Service Templates** menu and select the "Provision New Empty Pluggable Database" offering. Then click on **Edit**.

    ![](../em-devops-patching/images/emdevpatch2step25.png " ")

26. Notice that the "Sales Infra Zone" is currently assigned to the "pdbpool" that already existed. We want to assign the newly created "PDB_POOL". Click on **Assign Pool** button.

    ![](../em-devops-patching/images/emdevpatch2step26.png " ")

27. Select the "PDB_POOL" and then click the **Select** button.

    ![](../em-devops-patching/images/emdevpatch2step27.png " ")

28. Click **Next**.

    ![](../em-devops-patching/images/emdevpatch2step28.png " ")

29. On the next set of pages **don't** modify anything. Just click **Next** until you are in the final "Review" page.
    In the "Review" page click **Edit**.

    ![](../em-devops-patching/images/emdevpatch2step29.png " ")

## Task 3: Provision a PDB using DBaaS and Ansible

1. In this step, we are going to make use of both **uri** parameters below. These **uri** parameters are part of the "Service Template" configuration. You can get these parameters by executing the get PaaS Zone REST API.

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

    ![](../em-devops-patching/images/emdevpatch3step3.png " ")


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

    ![](../em-devops-patching/images/emdevpatch3step4.png " ")

5. Go back to the Oracle Enterprise Manager web console and logout from the "SYSMAN" account. After this login using "CYRUS".
    Cyrus is a user that has access and all the required privileges to use the DBaaS "Self Service Portal".

    ```
    CYRUS/welcome1
    ```

    ![](../em-devops-patching/images/emdevpatch3step5a.png " ")

    ![](../em-devops-patching/images/emdevpatch3step5b.png " ")

6. Verify that the new PDB shows up in the portal.

    ![](../em-devops-patching/images/emdevpatch3step6.png " ")

## Task 4: Configure Fleet Maintenance (Gold Image, Container and Pool)

1. Download a new Enterprise Manager Fleet Maintenance Gold Image version. This Gold Image will be imported into the our Fleet Maintenance setup.

    ```
    <copy>cd ~
    wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/oRaI83p8c3Iak4hcqzVmCewOi_NmBXfwNkCWD6Mm8aNXlWMMjyEaOnRgWr3rtLfy/n/natdsecurity/b/labs-files/o/19.14ExportGoldImage.zip</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step1.png " ")

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

    ![](../em-devops-patching/images/emdevpatch4step2.png " ")


3. Go back to the Oracle Enterprise Manager console and logout from the "CYRUS" account.

    ![](../em-devops-patching/images/emdevpatch4step3.png " ")


4. Login using the "SYSMAN" account.

    ![](../em-devops-patching/images/emdevpatch4step4.png " ")

5. Navigate to Enterprise -> Provisioning and Patching and click on **Procedure Activity**.

    ![](../em-devops-patching/images/emdevpatch4step5.png " ")

6. Click on the **ImportSoftwareImage_SYSMAN** task that was just created and refresh the screen until the task successfully completes.

    ![](../em-devops-patching/images/emdevpatch4step6a.png " ")

    ![](../em-devops-patching/images/emdevpatch4step6b.png " ")

7. Go back to the SSH terminal and execute below EMCLI command to verify the Gold Image details.

    ```
    <copy>emcli db_software_maintenance -getImages</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step7.png " ")

8. Notice the **IMAGE ID** column. Using the value of this column get the Gold Image version.

    ```
    <copy>emcli db_software_maintenance -getVersions -image_id=<paste the image id here></copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step8.png " ")

9. Subscribe the recently created **PDB_POOL** in the DBaaS setup with this Gold Image. Use the **IMAGE ID** used in the previous step.

    ```
    <copy>emcli db_cloud_maintenance -subscribeTarget -pool_name=PDB_POOL -pool_type=pdbaas_pool -image_id=<paste the image id here></copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step9.png " ")

10. Verify the subscription for that specific 19c container using the **IMAGE ID** from the previous step.

    ```
    <copy>emcli db_software_maintenance -getSubscriptionsForContainer -target_name="PDB_POOL" -target_type=pdbaas_pool -image_id=<paste the image id here></copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step10.png " ")

11. Deploy a new Oracle Home that will host a new 19c container using the 19.14 Gold Image.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="DEPLOY_DB_SOFTWARE" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Deploy Patch OH for Pool" -target_type=oracle_home -description="Deploys the Patched Oracle home on target nodes" -input_file="data:/home/oracle/fleet/deploy197_hr.inp"</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step11.png " ")

12. Go back to the Oracle Enterprise Manager console. Navigate to Enterprise -> Provisioning and Patching and click on **Procedure Activity**. Monitor the deployment procedure.

    ![](../em-devops-patching/images/emdevpatch4step12a.png " ")

    ![](../em-devops-patching/images/emdevpatch4step12b.png " ")

13. There's a local listener on the current 19c Oracle Home. This listener needs to be migrated to the 19.14 Oracle Home before we can create the new 19.14 container database.
    Go back to the SSH terminal and execute below EMCLI command.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="MIGRATE_LISTENER" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Migrate Listeners" -description="Migrate the listeners to the new Oracle Home, if any"</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step13.png " ")

14. Monitor the deployment procedure execution using the Enterprise Manager console.

    ![](../em-devops-patching/images/emdevpatch4step14a.png " ")

    ![](../em-devops-patching/images/emdevpatch4step14b.png " ")

15. Create a new container database (CDB) using the Oracle Home that was just deployed from the 19.14 Gold Image. Go back to the SSH terminal and execute.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="DEPLOY_CDB" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Deploy CDB" -target_type=oracle_database -description="Deploy a new CDB on the new OH for every CDB on the Pool using the prefix" -db_prefix="ssa"</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step15.png " ")

16. Monitor the deployment procedure execution using the Enterprise Manager console.

    ![](../em-devops-patching/images/emdevpatch4step16a.png " ")

    ![](../em-devops-patching/images/emdevpatch4step16b.png " ")

17. Activate the newly created container database (CDB). This means that the PDB_POOL now knows that a new version of the CDB exists and is ready for use.

    ```
    <copy>emcli db_cloud_maintenance -performOperation -purpose="ACTIVATE_CDB" -pool_name="PDB_POOL" -pool_type="pdbaas_pool" -name="Activate the CDBs" -target_type=oracle_database -description="Activates the newly created CDBs"</copy>
    ```

    ![](../em-devops-patching/images/emdevpatch4step17.png " ")


## Task 5: Patch a PDB using DBaaS and Ansible

1.  In this step we are going to patch the recently created PDB. Remember that this PDB was created using Ansible and by making use of the existing db19c.subnet.vcn.oraclevcn.com CDB. This CDB is currently running on 19.12 Oracle Home and we want to patch this PDB to 19.14 RU.
    In order to automate this process we are going to use an Ansible YAML file to update the PDB to the CDB deployed by EM running on the 19.14 Oracle Home.

2.  Login to the Enterprise Manager console using SYSMAN.

    ![](../em-devops-patching/images/emdevpatch5step2.png " ")

3.  Navigate to Setup -> Cloud and click on **Database**.

    ![](../em-devops-patching/images/emdevpatch5step3.png " ")

4.  Select the Pluggable Database option and click on **Pluggable Database Pool**.

    ![](../em-devops-patching/images/emdevpatch5step4.png " ")

5.  Select the **PDB_POOL** and then click **Edit**.

    ![](../em-devops-patching/images/emdevpatch5step5.png " ")

6.  Select the **Named Credential** option and choose the credentials as shown on the image below. Then click **Next**.

    ![](../em-devops-patching/images/emdevpatch5step6.png " ")

7.  Click **Submit**.

    ![](../em-devops-patching/images/emdevpatch5step7.png " ")

8.  Execute below.

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

    ![](../em-devops-patching/images/emdevpatch5step8.png " ")


9.  Go back to the Oracle Enterprise Manager web console. Navigate to Enterprise -> Provisioning and Patching -> **Procedure Activity**.

    ![](../em-devops-patching/images/emdevpatch5step9.png " ")

10. Monitor the **UPDATE** procedure.

    ![](../em-devops-patching/images/emdevpatch5step10a.png " ")

    ![](../em-devops-patching/images/emdevpatch5step10b.png " ")

11. Logout from the SYSMAN account and login with CYRUS user.

    ![](../em-devops-patching/images/emdevpatch5step11a.png " ")

    ![](../em-devops-patching/images/emdevpatch5step11b.png " ")

12. Click on the SSAPDB_PDB1 database.

    ![](../em-devops-patching/images/emdevpatch5step12.png " ")

13. Confirm the version is now 19.14 RU for the PDB.

    ![](../em-devops-patching/images/emdevpatch5step13.png " ")

    From this point any new PDB request using the PDB_POOL will be serviced by the recently activated 19.14 CDB.

This completes the Lab!

You may [proceed to the next lab](#next).

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements
- **Author** - Alfredo Krieg, NA Technology, June 2022
* **Contributors** - Andrew Hong, NA Technology
* **Last Updated By/Date** -
