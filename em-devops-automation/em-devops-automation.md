# EM Extensibility and Interoperability for DevOps

## Introduction

In this workshop you will get hands-on experience with the Extensibility and Interoperability capabilities of the Database as A Service offering in Oracle Enterprise Manager 13c with DevOps tools like Ansible.

*Estimated Time:* 50 minutes


### Objectives

In this lab you will learn:


| **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1**  | Install and Configure Ansible                               | 10 minutes       | Prepare the Live Labs environment in order to use Ansible as a DevOps automation/orchestration tool.                                                                                         | DevOps tools or toolchains help customers to automate tasks in their datacenter. This Lab makes use of Ansible as an orchestration tool.                                                                                                                                                                                                                                                                      |
| **2**  | Verify DBaaS Setup and Integration with Ansible             | 10 minutes       | EM's DBaaS extends the Oracle Private Cloud Management solution by automating the lifecycle of a database and allowing users to request database services through self-service portal or REST API's.                                                                                             | With this solution, IT Managers no longer have to perform mundane administrative tasks for provisioning databases. Database users can get instantaneous access to new database services through the Self Service Portal or REST API's.                                                                                                                                                                                                                                                                     |
| **3**  | Provision a PDB using DBaaS and Ansible             | 10 minutes       | DevOps orchestration tools like Ansible, Chef, Terraform, etc., can easily integrate with EM 13c in order to provision Oracle databases.                                                                                            | EM 13c implements pre-checks, best practices and processes to provision all these configurations in a secure, automated and controlled fashion.                                                                                                                                                                                                                                                      |
| **4**  | PDB Lifecycle Management using DBaaS and Ansible       | 10 minutes       | Once provisioned, Oracle databases need to be well maintained and secured. All these database lifecycle activity tasks can be automated by integrating EM 13c with orchestration DevOps tools.                                                | DB lifecycle activities can be easily scheduled using DevOps tools and Oracle Enterprise Manager 13c. There's no need to login directly to the DB as EM provides a secure framework for all these activities.                                                                                                                                                                                                                                                                                                                                                                                          |
| **5**  | Delete a PDB using DBaaS and Ansible       | 10 minutes       | In this activity you'll see how a pluggable database is terminated and deleted from EM's DBaaS framework using Ansible playbooks.                                                                                                                                        | This last Lab provides information on how to decommission a PDB from EM's DBaaS setup as well as a glance on all the requests submitted to EM through Ansible. |


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

    ![](../em-devops-automation/images/emdevau1step1.png " ")

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

    ![](../em-devops-automation/images/emdevau1step2.png " ")

    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

3. Verify that Ansible can properly ping the configured **emserver**.

    ```
    <copy>ansible emserver -m ping -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    Type **yes** and hit **Enter** on your keyboard.

    ```
    Are you sure you want to continue connecting (yes/no)? yes
    ```

    ![](../em-devops-automation/images/emdevau1step3.png " ")

    Verify that you receive the **pong** response from Ansible.

4. Create a directory where Ansible's YAML files will be placed. Then **cd** into the new directory.

    ```
    <copy>mkdir -p /home/oracle/ansible/yml
    cd /home/oracle/ansible/yml</copy>
    ```

    ![](../em-devops-automation/images/ansible-new-dir.png " ")


## Task 2: Verify DBaaS Setup and Integration with Ansible

1. Go back to the Oracle Enterprise Manager (EM) Web console. Login to the console using below credentials.

    **cyrus/welcome1**

    ![](../em-devops-automation/images/emdevau2step1.png " ")

2. Oracle EM will then show the DBaaS Self Service Portal. Click the **Create Instance** button and verify the offerings from the catalog.

    ![](../em-devops-automation/images/emdevau2step2.png " ")

    ![](../em-devops-automation/images/emdevau2step3.png " ")

3.  From the catalog, we can see that we have two offerings to request a Pluggable Database (PDB). We are going to use the first offering **Provision New Empty Pluggable Database** with Ansible.

4.  Go back to the previous terminal session. Create a new YAML (.yml) file that includes the instructions so that Ansible can request the current DBaaS configuration from EM.

    ```
    <copy>vi /home/oracle/ansible/yml/get_dbaas_resources.yml</copy>
    ```

    Hit the **i** letter on your keyboard in order to enable "insert" mode. Then copy and paste below lines.

    ```
    <copy>---
    - name: Using a REST API
      become: false
      hosts: emserver
      gather_facts: false
      tasks:

       - name: Get DBaaS Resources
         uri:
           url: https://emcc.marketplace.com:7803/em/cloud
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
    Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

5.  Execute the Ansible Playbook with the YAML (.yml) just created.

    ```
    <copy>ansible-playbook /home/oracle/ansible/yml/get_dbaas_resources.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
    ```

    The output will be an JSON type content as below.

    ```
    PLAY [Using a REST API] ********************************************************
    TASK [Get DBaaS Resources] *****************************************************
    [WARNING]: Platform linux on host emcc.marketplace.com is using the discovered
    Python interpreter at /usr/bin/python, but future installation of another
    Python interpreter could change this. See https://docs.ansible.com/ansible/2.9/
    reference_appendices/interpreter_discovery.html for more information.
    ok: [emcc.marketplace.com]

    TASK [Print returned json dictionary] ******************************************
    ok: [emcc.marketplace.com] => {
    "results.json": {
        "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud",
        "description": "This represents the Cloud resource of the Oracle Enterprise Manager Cloud Management solution",
        "media_type": "application/oracle.com.cloud.common.Cloud+json",
        "name": "Oracle Cloud by Enterprise Manager",
        "resource_state": {
             "state": "READY"
        },
        "service_family_types": {
             "elements": [
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/service_family_type/opc",
                    "media_type": "application/oracle.com.cloud.common.ServiceFamilyType+json",
                    "name": "opc",
                    "type": "opc",
                    "uri": "/em/cloud/service_family_type/opc"
                },
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/service_family_type/dbaas",
                    "media_type": "application/oracle.com.cloud.common.ServiceFamilyType+json",
                    "name": "dbaas",
                    "type": "dbaas",
                    "uri": "/em/cloud/service_family_type/dbaas"
                },
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/service_family_type/iaas",
                    "media_type": "application/oracle.com.cloud.iaas.IaasServiceFamilyType+json",
                    "name": "iaas",
                    "type": "iaas",
                    "uri": "/em/cloud/service_family_type/iaas"
                }
            ],
            "media_type": "application/oracle.com.cloud.common.ServiceFamilyType+json",
            "total": "3"
        },
        "service_requests": {
            "elements": [],
            "media_type": "application/oracle.com.cloud.common.Request+json",
            "total": "0"
        },
        "service_templates": {
            "elements": [
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/pluggabledbplatformtemplate/1",
                    "description": "Create a new enterprise Pluggable Database",
                    "media_type": "application/oracle.com.cloud.common.PluggableDbPlatformTemplate+json",
                    "name": "Provision New Empty Pluggable Database",
                    "service_family_type": "dbaas",
                    "type": "dbaas",
                    "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/1"
                },
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/pluggabledbplatformtemplate/21",
                    "description": "Creates a new PDB with data from non-container database",
                    "media_type": "application/oracle.com.cloud.common.PluggableDbPlatformTemplate+json",
                    "name": "Provision Pluggable Database with Data",
                    "service_family_type": "dbaas",
                    "type": "dbaas",
                    "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/21"
                }
            ],
            "media_type": "application/oracle.com.cloud.common.ServiceTemplate+json",
            "total": "2"
        },
        "uri": "/em/cloud",
        "zones": {
            "elements": [
                {
                    "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3",
                    "description": "",
                    "media_type": "application/oracle.com.cloud.common.DbZone+json",
                    "name": "Sales Infra  Z one",
                    "service_family_type": "dbaas",
                    "type": "self_service_zone",
                    "uri": "/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3"
                }
            ],
            "media_type": "application/oracle.com.cloud.common.Zone+json",
            "total": "1"
        }
      }
    }
    PLAY RECAP *********************************************************************
    emcc.marketplace.com       : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    ```

6. Using the output above, review two important sections. The first one is **service_templates**. Service templates are basically the service catalog in our DBaaS setup.
   In this output there are two elements in our service catalog.

   ```
   "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/pluggabledbplatformtemplate/1",
   "description": "Create a new enterprise Pluggable Database",
   "media_type": "application/oracle.com.cloud.common.PluggableDbPlatformTemplate+json",
   "name": "Provision New Empty Pluggable Database",
   "service_family_type": "dbaas",
   "type": "dbaas",
   "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/1"
   ```

   ```
   "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/pluggabledbplatformtemplate/21",
   "description": "Creates a new PDB with data from non-container database",
   "media_type": "application/oracle.com.cloud.common.PluggableDbPlatformTemplate+json",
   "name": "Provision Pluggable Database with Data",
   "service_family_type": "dbaas",
   "type": "dbaas",
   "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/21"
   ```

   These 2 elements represent the same service offerings from the Web console.

   ![](../em-devops-automation/images/emdevau2step3.png " ")

   In order to request an empty Pluggable database (PDB) we need the **uri** of that specific offering. In this case is.

   ```
   "uri": "/em/cloud/dbaas/pluggabledbplatformtemplate/1"
   ```

   Now take a look at the **zones** section and review the elements of the zone.

   ```
   "canonicalLink": "/em/websvcs/restful/extws/cloudservices/service/v0/ssa/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3",
   "description": "",
   "media_type": "application/oracle.com.cloud.common.DbZone+json",
   "name": "Sales Infra  Z one",
   "service_family_type": "dbaas",
   "type": "self_service_zone",
   "uri": "/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3"
   ```

   In order to request the PDB we need the **uri** of the zone where the PDB will be created into. In this case will be.

   ```
   "uri": "/em/cloud/dbaas/zone/BE3E75753F97FDB6976A229AA7C1D2E3"
   ```


## Task 3: Provision a PDB using DBaaS and Ansible

1. In this step, we are going to make use of both **uri** parameters reviewed on step 2.

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

   ![](../em-devops-automation/images/emdevau3step3.png " ")


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

   ![](../em-devops-automation/images/emdevau3step4.png " ")

5. Go back to the Oracle Enterprise Manager web console and refresh the screen. Verify that you can see the newly created PDB in the Self Service Portal.

   ![](../em-devops-automation/images/emdevau3step5.png " ")


## Task 4: PDB Life Cycle Management using DBaaS and Ansible

1. In the previous step, we requested a new PDB using the "Small" workload type. Depending on how you configure your DBaaS service catalog, you may have different types of workload offerings. In this Lab, we have 2 different workload types available. Small and Large.

2. Let's resize the newly provisioned PDB from the Small workload type to the Large workload type. For this, go back to the SSH terminal and create a new YAML (.yml) file.

   ```
   <copy>vi /home/oracle/ansible/yml/resize_pdb.yml</copy>
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
                "operation":"RESIZE_PDB",
                "WORKLOAD_NAME":"large",
             }
         register: results

       - name: Print returned json dictionary
         debug:
           var: results.json</copy>
   ```

   Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

   Execute the YAML file.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/resize_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step2.png " ")

   Execute the previously created YAML file to get the status of the PDB.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/get_pdb_status.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step21.png " ")

3. In this step, we are going to shutdown the recently created PDB. Go back to the SSH terminal and create a new YAML (.yml) file.

   ```
   <copy>vi /home/oracle/ansible/yml/shutdown_pdb.yml</copy>
   ```

   Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

   ```
   <copy>---
   - name: Using a REST API
     become: false
     hosts: emserver
     gather_facts: false
     tasks:

       - name: Shutdown PDB
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
                "operation":"SHUTDOWN"
             }
         register: results

       - name: Print returned json dictionary
         debug:
           var: results.json</copy>
   ```

   Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

   Execute the YAML file.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/shutdown_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step3.png " ")

   Execute the previously created YAML file to get the status of the PDB.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/get_pdb_status.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step31.png " ")

4. Start the recently created PDB. Go back to the SSH terminal and create a new YAML (.yml) file.

   ```
   <copy>vi /home/oracle/ansible/yml/start_pdb.yml</copy>
   ```

   Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

   ```
   <copy>---
   - name: Using a REST API
     become: false
     hosts: emserver
     gather_facts: false
     tasks:

       - name: Start PDB
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
                "operation":"STARTUP"
             }
         register: results

       - name: Print returned json dictionary
         debug:
           var: results.json</copy>
   ```

   Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

   Execute the YAML file.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/start_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step4.png " ")

   Execute the previously created YAML file to get the status of the PDB.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/get_pdb_status.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau4step41.png " ")


## Task 5: Delete a PDB using DBaaS and Ansible

1. In this step we are going to delete the recently provisioned PDB using Ansible. Go back to the SSH terminal and create a new YAML (.yml) file.

   ```
   <copy>vi /home/oracle/ansible/yml/delete_pdb.yml</copy>
   ```

   Hit the **i** letter on your keyboard in order to enable insert mode. Then copy the lines below.

   ```
   <copy>---
   - name: Using a REST API
     become: false
     hosts: emserver
     gather_facts: false
     tasks:

       - name: Delete PDB
         uri:
           url: https://emcc.marketplace.com:7803/em/cloud/dbaas/pluggabledbplatforminstance/byrequest/61
           method: DELETE
           return_content: yes
           force_basic_auth: yes
           validate_certs: no
           body_format: json
           headers:
              Authorization: basic Q1lSVVM6d2VsY29tZTE=
              Accept: application/oracle.com.cloud.common.PluggableDbPlatformInstance+json
         register: results

       - name: Print returned json dictionary
         debug:
           var: results.json</copy>
   ```

   Save the changes by hitting the **Esc** key on your keyboard, type **:wq** then hit **Enter**.

   Execute the YAML file.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/delete_pdb.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images//emdevau5step1.png " ")

   Execute the previously created YAML file to get the status of the PDB.

   ```
   <copy>ansible-playbook /home/oracle/ansible/yml/get_pdb_status.yml -u oracle --private-key=~/.ssh/rsa_id</copy>
   ```

   ![](../em-devops-automation/images/emdevau5step11.png " ")

2. Go back to the Oracle Enterprise Manager web console. Click on Requests (located on the left panel) and verify all the requests submitted through Ansible.

   ![](../em-devops-automation/images/emdevau5step2.png " ")

This completes the Lab!

You may [proceed to the next lab](#next).

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements
- **Author** - Alfredo Krieg, NA Technology, January 2022
* **Contributors** -  
* **Last Updated By/Date** -
