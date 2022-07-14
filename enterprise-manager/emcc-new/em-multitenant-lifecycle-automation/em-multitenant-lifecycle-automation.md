# Multitenant Database Lifecycle Management
## Introduction

This workshop will help you understand how one can utilize Enterprise Manager to make the best use of Oracle Database Multitenancy , and Lifecycle Management capabilities. We also have labs which will help you understand how organizations can utilize the Database Private Cloud which allows self-service users to request and manage Pluggable Databases (PDBs) with ease. 

*Estimated Lab Time: 60 minutes*

Watch the video below for a quick walk through of the lab.
[](youtube:N6840yjGnME)

### About Multitenant Database Lifecycle Management

Oracle Enterprise Manager's Database Lifecycle Management (DBLM) Pack  comes with out-of-box Deployment Procedures to provision, clone, and patch various configurations of the Oracle Database. The Management Pack offers new capabilities that simplify support for the entire lifecycle of pluggable databases, including migration, plugging and unplugging. The Management Pack features include pluggable database (PDB) provisioning and management from the self-service portal, PDB patching and upgrades, and PDB relocation to new platforms.

Cloud Management Pack (CMP) that resides on top of DBLM, provides  lifecycle management of PDBs in Database Private Cloud. This enables the Self Service Users to Provision, Plug-Unplug , Clone and Migrate PDBs in the Private Cloud.



### Objectives

The objective of this workshop is to highlight Oracle Enterprise Manager 13c Lifecycle Management capabilities for multitenant databases.

| **Step No.** | **Feature**                                                                | **Approx. Time** | **Details**                                                                                                                                                                      | **Value proposition**                                                                                                                                                                                                                   |
|--------|----------------------------------------------------------------------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | Create a Pluggable Database (PDB)                                      | 10min                     | Create Pluggable database (PDB) within a CDB and run a post-script to lock/unlock accounts.                                                                                  | Create multiple PDBs with few clicks while making sure they follow organization’s standards by using automated post-scripts.                                                                                                           |
| 2    | Un-plug/Plug an existing Pluggable Database | 10min                     | Un-plug a PDB and later Plug it back in a CDB when needed (Create from unplugged)                                                                                                                       | Unplug a PDB when not needed and plug it back as per need, hence maximizing resource utilization in your organization. Easily upgrade PDBs with few clicks by moving from one container to another.                                                                                                                  |
| 3    | Clone an existing Pluggable Database                                 | 5min                      | Create multiple copies (Clones) of a PDB for dev/test purpose                                                                                                                     | Create multiple PDBs clones for Dev/test with few clicks while making sure they follow organization’s standards by using automated post-scripts.                                                                                      |
| 4    | Compliance Management for Pluggable Database                                                         | 10min                     | Apply a compliance standard on PDB, generate report and validate the results.                                                                                                 | Make sure PDBs comply with compliance standards and explore options to fix in case of any anomalies.                                                                                                                   |
| 5    | Self- service to request a PDB using PDBaaS            | 10min                     | Request PDB (pluggable database) using Service Catalogue on Private Cloud. Resize the PDB and then Delete the PDB while preserving the contents.                                                      | Review self-service option to provision PDB, which only requires minimal inputs.                                                                                                                                                        |
| 6    | Administrative Setup for PDBaaS (Private Cloud)- Review only               | 10min                     | An overview of the administrative setup involved for PDBaaS (Private Cloud) which includes setting up a PaaS Infrastructure Zone, Pluggable Database Pool, Data Sources, Service Template, etc. | Setup private cloud using Enterprise Manager where admin can define resources and EM’s placement algorithm and make sure that resources are utilized to their best. It is complimented by metering, and show back/chargeback capabilities. |


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository. Workshop activities included in this lab will be executed both locally on the instance using Enterprise Manager Command Line Interface (EMCLI) or Rest APIs, and the Enterprise Manager console (browser)

## Task 1: Create Pluggable Database (PDB)

1. On the browser window on the right preloaded with *Enterprise Manager*, if not already logged in, click on the *Username* field and login with the credentials provided below.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![](../initialize-environment/images/em-login.png " ")


2.  Navigate to  ***Enterprise >> Provisioning and Patching >>
    Database provisioning***

   ![](images/DB_provisioning-flow-main.jpg " ")



3.  On the Database Provisioning page, in the *Related Links* section on the left menu pane, click **Provision Pluggable Databases**

    ![](images/PDB_provisioning-flow-main.jpg " ")



4.  On the Provision Pluggable Database Console, in the *Container   Database* section, click on the magnifier to select  **cdb186.subnet.vcn.oraclevcn.com** within which you want to create new PDBs.

    ![](images/Select-CDB-main-flow-helper.jpg " ")
    ![](images/Select-CDB-main-flow.jpg " ")



5.  In the PDB Operations section, select **Create New Pluggable Databases**.

    Click **Launch**

    ![](images/2248640eabc0efa2fb32293ec07fb389.jpg " ")



6.  In the PDB Creation Options section, choose **Create a New PDB**. 

    Use the Named credentials (*ORACLE*) for login.

    Click **Next**


    ![](images/9be6823423a692b7e1f0e240c10567c9.jpg " ")



7. In the Identification page, Enter a unique name for the PDB you are creating (*prov_pdb*). 


    *In your data center, if you want to create multiple pluggable databases on a container, you can select ‘Create Multiple Copies’ to optimize time required to create these multiple pluggable databases*



    In the PDB Administrator section, enter the credentials of the admin user account you need to create for administering the PDB.     


    ```
    Username: <copy>PDBADMIN</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```
    
      Click **Next**

    ![](images/Task1-step8-latest.jpg " ")



9. For storage option
    click on **Use Common Location for PDB Datafiles** radio button.  
    *Storage type* and *Location* field gets auto populated with default values.

    The Temporary Working Directory is auto filled as **/tmp**


    ![](images/Task1-point9.jpg " ")



10. Optionally, you can also select a post-script, which will be executed post PDB creation.

    On the same Storage Configuration page under the **Post Creation Scripts**  , click on  “Select from software library” radio button and click on the magnifier to choose the script. 
  ![](images/Task1-poin10.jpg " ")

  In the dialog box that appears, type “**unlock**” and click on the magnifier. select the script '*Script to unlock account*' and click **select**

  ![](images/Unock-helper.jpg " ")

  Verify all the parameters on the page and click **Next**

  ![](images/7d3fcabc8fe5f6f80fe20e55bb28655d.jpg " ")




11. Schedule **Immediately** or later. 

    Click **Next**.

    ![](images/Task1-step10.jpg " ")



12. In the Review page, review the details you have provided for the deployment procedure and  click **Submit**

    You can now click on **View Execution Details** link to see details.

    ![](images/d12c1a1d5e3c3f394248da7d12813b6b.jpg " ")



13. On Procedure Activity, select specific execution step from the procedure step tree to see details of the execution log.

    Setup View Data to be refreshed with specific time interval to refresh page. The procedure takes about 2-3 minutes to complete. 

    Wait for **Status: Succeeded** which indicates the procedure ran successfully.
    

    ![](images/3657eb9bb536b26d163c148e40a99332.jpg " ")



14. You can **Navigate to Targets >> Databases**.

    ![](images/Target-Database-Navigation.jpg " ")

    Click on drop down arrow next to **CDB186** and click on the pluggable database drop down arrow, you will see the newly created PDB

    ![](images/Task1-step14.jpg " ")

## Task 2: Unplug/Plug an existing Pluggable Database (PDB)

1. Navigate to the ***Enterprise menu >> Provisioning and Patching >> Database provisioning***.

    ![](images/DB_provisioning-flow-main.jpg " ")

2. In the Database Provisioning page, in the Related Links section of the left menu pane, click “**Provision Pluggable Databases**”

    ![](images/PDB_provisioning-flow-main.jpg " ")

3.  In the Provision Pluggable Database Console, in the Container Database section, click on the magnifier to select the CDB (**cdb186.subnet.vcn.oraclevcn.com**) within which you want to Unplug PDBs.
    ![](images/Select-CDB-main-flow-helper.jpg " ")
    ![](images/Select-CDB-main-flow.jpg " ")

4.  In the PDB Operations section, select **Unplug Pluggable Databases**, then Click **Launch**



    ![](images/b727e1673cfa38c85130ef6e2365055d.jpg " ")

5.  On the Select PDB page in  Pluggable Database section click on the magnifier to choose the PDB you want to unplug. 

    In the pop up search, type `PROV_PDB` and click search. Choose `PROV_PDB` and click Select.
    
    Select Named credentials “ORACLE” in container Database Host Credentials

    Click **Next**

    ![](images/39102476b5e5915a1491e28525af88f5.jpg " ")

6.  On the Destination page, Click on the **Software Library**  radio button to define the location of PDB template. 

    Select **Generate PDB Archive** option to unplug pdb  

    PDB Template Name will be prepopulated using combination of CDB and PDB name but you have option to change it. 

    By default temporary working directory is prepopulated as **/tmp**  but you have option to change it. 
    
    click **Next**

    ![](images/Task2-step6-latest.jpg " ")

7.   Schedule **immediately** or choose later .
    
     Click **Next**.
          ![](images/Task2-Step7.jpg " ")



8. In the Review page, verify the details and  click **Submit** .

    ![](images/Task2-step7a.jpg " ")

    Click **View Execution Details**


    ![](images/View_execution_details.jpg " ")


    On the Procedure Activity page, select specific execution step from the procedure step tree to see detail procedure execution log. 

    Setup View Data to be refreshed with specific time interval to refresh page. The procedure takes about 2-3 minutes to complete. 

    Wait for **Status: Succeeded** which indicates the procedure ran successfully.

    ![](images/bdbafe949b2bc880e2a09b82f9edaf8a.jpg " ")

8.  Navigate to **Targets** >> **Databases**.

     Click on drop down arrow next to CDB186 and click on the pluggable database drop down arrow,you will see the PDB you unplugged is no longer in the list.
      

    ![](images/Task2-step8.jpg " ")

9.  Let us continue to the next steps and plug the same PDB back into the container database. 

    Navigate to the **“Enterprise menu >> Provisioning and Patching >> Database provisioning”**.

    ![](images/DB_provisioning-flow-main.jpg " ")

10. In the Database Provisioning page, in the Related Links section of the left menu pane, click **Provision Pluggable Databases**

    ![](images/PDB_provisioning-flow-main.jpg " ")

11. On the Provision Pluggable Database Console, in the Container Database section, click on the magnifier to select the **CDB** (**cdb186.subnet.vcn.oraclevcn.com186**) within which you want to Plug the PDBs.

    ![](images/Select-CDB-main-flow-helper.jpg " ")
      ![](images/Select-CDB-main-flow.jpg " ")

12. In the PDB Operations section, select **Create New Pluggable Databases** and click **Launch**.

    ![](images/2248640eabc0efa2fb32293ec07fb389.jpg " ")

13. On the Create Pluggable Database Wizard, in the PDB Creation Options section, select **Plug an unplugged PDB**. 

    Select Named credentials **“ORACLE”**

    Click **Next**


    ![](images/5427807b6e4c677bd991497cfc5468ce.jpg " ")


14. The Identification page has 3 sections. 

    Under the *PDB Name* section provide a name for the PDB (`prov_pdb`) and select the option *create as clone*, this ensures Oracle generates a unique PDB DBID, GUID, and other identifiers expected for the new PDB.


    In the next section under *PDB Administrator* we will keep the values default and not do any changes as shown below.

      ![](images/2ac79b220d664b868c62e4529791e187.jpg " ")


15. On the same Identification page, in the PDB Template Location section: Select **Software Library** radio button. Click on the magnifier icon placed on Location text box.


    Select the Name which you created during Unplug. 
    In case of multiple options, choose the latest image based on timestamp.
    Click **Select**
      ![](images/Task2-step15-latest.jpg " ")

      ![](images/Task2-step15.jpg " ")
      

    
    Validate all the options and click **Next**

    ![](images/Task2-step16.jpg " ")


16. On the Storage Page select **Use Common Location for PDB Datafiles** , the Storage Type and Location fields are auto populated as showed below.

    Type **/tmp** in temporary working directory option.

    Click **Next**


    ![](images/a6353f812935eeb6148a79693ae0c4fd.jpg " ")

17.  
    Schedule **immediately** or choose to start later.
     Click **Next**.

    ![](images/Task2-step17.jpg " ")

    

18. In the review page, verify the details and click
    **Submit**. 

    You can now click on **View Execution Details** link to see details.
    ![](images/Task2-step18.jpg " ")
    ![](images/View_execution_details.jpg " ")


19. On the Procedure Activity page, select specific execution step from the procedure step tree to see detail procedure execution log.

    Setup View Data to be refreshed with specific time interval to refresh page

    The procedure takes 2-3 minutes to complete.

    Wait for **Status: Succeeded** which indicates the procedure ran successfully.

    ![](images/Task2-step19.jpg " ")

    Optionally,  Click the status link for each step to view the details of the execution of each step. 


20. Navigate to ***Targets >> Databases***. 

    Click on drop down arrow next to CDB186 and click on the pluggable database drop down arrow,you will see the PDB which was recently plugged.


    ![](images/Task1-step14.jpg " ")

    *Note*: You do not have to wait until the steps complete and move on to the next section.

## Task 3: Clone an existing Pluggable Database (PDB)

1.  Navigate to the “***Enterprise menu >> Provisioning and Patching >> Database provisioning***”.

  ![](images/DB_provisioning-flow-main.jpg " ")

2.  In the Database Provisioning page, in the Related Links section of the left menu pane, click Provision Pluggable Databases

  ![](images/PDB_provisioning-flow-main.jpg " ")

3.  In the Provision Pluggable Database Console, in the Container Database section, click on the magnifier to select the CDB (**cdb186.subnet.vcn.oraclevcn.com**) within which you want to clone new PDBs.
  ![](images/Select-CDB-main-flow-helper.jpg " ")
  ![](images/Select-CDB-main-flow.jpg " ")

4.  In the PDB Operations section, select **Create New Pluggable Databases**.

    Click **Launch**

    ![](images/2248640eabc0efa2fb32293ec07fb389.jpg " ")

5.  Under the PDB creation options, select **Clone an Existing PDB** . 

    Select **Full Clone**.

    Click on the magnifier next to source PDB field to choose the source database for clone.

    In the pop up search, type **`PROV_PDB`** and click search. Choose PROV_PDB and click **Select**.

    Leave the Database Link blank.

    Choose the Database Host Named Credential as "Oracle". 

    Click **Next**

    ![](images/472126037592bdeca5eaa6027ebb57a3.jpg " ")

    ![](images/Task3-step5.jpg " ")

6.  On the Identification page , enter new PDB name (**full_clonepdb**).

    You also have an option to create multiple clones by selecting the check box in the PDB Name section. For this lab, we will leave the option unchecked. 

    In the PDB Administrator section, credentials will be inherited from the source PDB, hence this section does not need any inputs.

    Optionally, an additional PDB Administrator user can also be created in case needed. 

    Click **Next**

      ![](images/Task2-step6.jpg " ")

7.  On the Storage Page , select **Use Common Location for PDB Datafiles**. 

    Storage type - Filesystem is auto selected.
    Location - Auto filled with PDB name suffix

    Enter **/tmp** in temporary working directory in case the field is not auto filled. 


    Optionally, you can select the postscript as we did in the creation flow. 
    

    Click **Next** .


    ![](images/ff556eb15570c55dfd477361c20051d6.jpg " ")

8.  On the Schedule page, choose to start  **immediately**.

    Click **Next**.

      ![](images/dblmschedulepage.jpg " ")

9.  Review the details and  click **Submit**. 

    Click on View Execution Details link to see details and of the Procedure.

      ![](images/Task3-step9.jpg " ")
      ![](images/Task3-step9a.jpg " ")
    
     On Procedure Activity page , select specific execution step from the procedure step tree to see detail procedure execution log. 

    Setup View Data to be refreshed with specific time interval to refresh page. The procedure takes about 2-3 minutes to complete.  

    Wait for **Status: Succeeded** which indicates the procedure ran successfully.

      ![](images/Task2-step19.jpg " ")



10.  Navigate to ***Targets >> Databases***. 

   Click on drop down arrow next to **CDB186** and click on the pluggable database drop down arrow, you will see the newly cloned PDB

  ![](images/Task3-step10a.jpg " ")

## Task 4: Compliance Management for Pluggable Database

Securing a provisioned Oracle Database is critical to protect your data. You need to safeguard that data with security controls that restrict access according to your policy by using either industry/regulatory standard benchmarks or custom policies. In this lab, we will use *High Security Configuration for Oracle Pluggable Database* compliance standard to secure configuration of provisioned database.


1. Navigate to ***Enterprise >> Compliance >> Library*** to get started

    ![](images/dblmcompliancelibrary.jpg " ")

2. Click the **Compliance Standards** tab. 

    Click on the Dropdown next to **Search**.
    In the Compliance Standard section type  "High Security" as the key word and hit search.

     Select the row **High Security Configuration for Oracle Pluggable Database**, and then Click the **Associate Targets** tab.


      ![](images/Task4-Compliance-Standard-name.jpg " ")

3.  Click Add and choose the row with your PDB you wish to associate. Choose PROV_PDB, click **Select**.

    Verify the PDB name is added and Click **OK**


    ![](images/Task4-Step3.jpg " ")
    ![](images/Task4-step3aa.jpg " ")

4. In the Save Association dialog box, Click Yes.


    ![](images/0ccc894ff6c91bdd0aa1b7e5f78fbe6e.png " ")

5. Click OK on the Information processing prompt. 


    ![](images/a01dffb956af685a866f02e68eff72b1.png " ")


7. Now Navigate to ***Enterprise >> Compliance >> Results***

    ![](images/1317deb228d80211d9e6a2edf2cbba9e.jpg " ")

8. Click on **High Security Configuration for Oracle Pluggable Database** under Compliance Standards.


    ![](images/Task4-Navigate_to_Compliance-Result-1.jpg " ")



10.  The compliance result shows the target is 100% compliant    against the selected standard with no violations. 
    In case of violations you will dee details like last evaluation date, name of the rule violated and rationale for the violation under the violation tab
    ![](images/Task4-Violations-tab.jpg " ")


12. Compliance Management also provides you an option to have a dashboard view of compliance summary against all the associated targets. 
The Dashboard provides a brief summary of the violations  , corrective actions and compliance standard score.

    
    From the home page Navigate to **Enterprise** >> **Compliance** >> **Dashboard**


    ![](images/Task4-Navigate-to-Dashboard-latest.jpg " ")

    

      **Dashboard View**


    ![](images/Task4-Compliance-Dashboard-latest.jpg " ")


13. You can also generate a comprehensive compliance report for

    A. Each compliance standard and all its associated targets.

    B. Each Target with all Compliance standard associated to it.

    
    Towards bottom of the page in the **Compliance Summary** section, click on the report against each Compliance standard or Targets.

    ![](images/Task4-13a.jpg " ")


    ![](images/Task4-13b.jpg " ")

    **Sample report**

    ![](images/Task4-Compliancereport1.jpg " ")
    ![](images/Task4-Compliancereport2.jpg " ")
    ![](images/Task4-Compliancereport3.jpg " ")
    ![](images/Task4-Compliancereport4.jpg " ")






 Now that you have gone through PDB life cycle operations, we will switch focus and cover the use case of building a private cloud using Enterprise Manager and how to quickly provision (with minimal inputs) and manage PDBs using PDB-as-a-service (PDBaaS). To proceed as a self service user, please logout as SYSMAN.

  ![](images/logout_as_sysman.jpg " ")

## Task 5: Self-Service to Request PDB Using PDBaaS

With the Self-Service Portal, cloud users can request a Pluggable Database through a simple process, monitor resource consumptions, and manage the pluggable database through an intuitive graphical user interface. PDBs are created with a predefined expiry time and is automatically deleted.

The PDBs are created using a precreated service template on CDBs which are virtually grouped as a pool.

1. Login into Enterprise Manager as a Self-Service User.

    Credentials : **cyrus/welcome1**

![](images/login_as_cyrus.jpg " ")

2. By default, you will see the Database Cloud Self Service Portal landing page as shown below.

    Click on  **Create Instance** button.

    ![](images/CMP-HomePage.jpg " ")

3.   
    Select **Provision New Empty Pluggable Database**.

      Note: There are two service templates pertaining to Pluggable Database

      -  **Provision New Empty Pluggable Database**: This     template enables users to create a new empty pluggable database in a container database configured by DBA.
       -  **Provision Pluggable Database with Data**: This template enables users to create a new pluggable database with data from non-container database.


    ![](images/ee694403e4c718e224a01ae91dbc88fd.jpg " ")


4. In the **Pluggable Database Configuration** section,


      **Step 1**

      Enter PDB Name , Service and Size details:
      
      ```
      PDB Name: AS_PDB2
      ```
      ```
      Database Service Name : Service_AS_PDB2
      ```
      ```
      Workload Size: Small
      ```


      **Step 2**

      Enter the credentials as suggested below. 
        
      ```
      Administrator Name: PDBADMIN
      ```
      ```
      Password : welcome1
      ```

      Tablespace name is auto populated. 

      ```
      Tablespace name : pdb_tbs1
      ```


    **Step 3**

    **Instance Details** 

    **Request Name** :  Auto filled with latest timestamp. Can be modified in case needed. 

    **Zone** : Auto filled with default option, Sales Infra Zone.

    
    **Properties**  can help user locate an instance more quickly. 
    Click on the dropdown to update. 

      ```
      Contact: <copy>CYRUS</copy>
      ```
      ```
      Lifecycle Status: <copy>Test</copy>
      ```


    **Step 4**

      Instance Duration - 
      
      Start: Accept the default (Immediately).
      
      Duration: Specify 4 hours from the current time by selecting the “Until” radio button, change to current date and specify time to be 4 hours from the current time.


    **Step 5**

    Validate all the details and Click on **Submit** button



    ![](images/Task5-Consolidated.jpg " ")

  What do these options represent? In most cases the PDBaaS options are self-explanatory.
  The self-service user should be able to provision a PDB by entering minimal information. 
  Fields with an ‘\*’ represent mandatory input fields. 
  
  Please refer to the table listed below for a description of each option:

  | **Field**                   | **Description**                                                                                                                                                                                                                                                                                    |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Request Name                | By default, it is the Self-Service User Requestor name with timestamp. This field can be modified                                                                                                                                                                                                  |
| Zone                        | The Zone is a PaaS Zone that represents hosts/vm, where the PDB database will be deployed for this request. The zones are configured by the administrator. Self-service user need not know the host or platform details.                                                                           |
| PDB Name                    | PDB database with user defined will be created for the container database                                                                                                                                                                                                          |
| Database Service Name       | The user defined prefix for the database service or alias for this self-service PDB. The rest of the service name will be system generated and will be associated with a database resource management plan.                                                                                        |
| Workload Size               | The resources allocated to the Database Service. The database resource management plan is derived from this option. You can configure multiple workload sizes. Each service template will contain unique workload sizes. This typically depends on the roles assigned to self-service user.        |
| Schedule Request            | Self-service user has the ability to create a PDB database immediately or choose to create at a later time. In this lab exercise, the administrator has defined a policy, so a self- service user has to specify time duration. The PDB database will be automatically deleted after the duration. |
| Administrator Name/Password | A database user with required administrative privileges will be created on the provisioned PDB. A self-service user will be able to administer the PDB database by logging in as this database user.                                                                                               |

9.  Once you submit a request, you will be redirected back to the “**Database Cloud Services**” Page. 


    Under “**Requests**” region, you should see 2 requests: 
    “**Create**” and “**Delete**” request

    You will also notice the delete operation is scheduled for future (not started yet) time. 

    Click on the **hourglass** icon under status column for the Create Pluggable Database step. You will see details of request.

    ![](images/CMP-Task5-point9.jpg " ")


11. PDB Provisioning perform the following actions:

    *  Create database roles and PDB

    *  Create a resource plan based on the workload size

    *  Create and register the database


    The request should take less than 7 minutes to complete. 
                
    Click on refresh icon or as an alternative set Refresh to 30 seconds. 
                
    The success status indicates that PDB database was successfully created. 

    Click on Close button when the procedure is complete. 

    ![](images/CMP-PDB_creation-success.jpg " ")

12.  The screen indicated the PDB creation is successful.

      ![](images/CMP-Task5-point12.jpg " ")

13. Click on the Home Icon. You will see new PDB instance. Click on the PDB recently created. 

  ![](images/CMP-Task5-point13.jpg " ")

  *Note*: Following widgets are shown on the Database Cloud Services landing Page

      * **Instances** show the number and status (Up/Down) of the DB/PDB Instances provisioned by the self-service user.
      * **Expiry**, shows the expiration summary of DB/PDB Instances.
      * **Usage**, resource usage status for the Self-Service user, status of the resource consumption for this user.
      * **Memory**, current memory consumption against the Quota for this user.
      * **Storage**, current storage consumption against the Quota for this user.

14. On the PDB details page you can use the connection details to connect to the PDB using SQL tools.

    Click on **Resize** button to resize a PDB instance.

    ![](images/9ca31e90c86263e6cddde14da1c6954f.jpg " ")

15. Select **large** and click **resize**

    ![](images/20537907e3a274a9df16e7c54f73713f.jpg " ")

    * Resize allows you to resize your instance to other available resource sizes.
    * We have 2 resource sizes available for Service Template. Small and Large.
    * Current size of PDB instance is Small, you can now resize it to large.

16. Once you click on **Resize**, a job will be submitted to resize instance. 

    In few minutes instance resize is completed. Expand **Resource Usage** section on PDB Home page. 

    This shows now new resource usage limits.


      ![](images/64a8954df11d2e688a930fd92ae38cd8.jpg " ")

17.  Next delete the database Instance: 

      Go to the Database Cloud Services Home page by clicking on **Database Cloud Service Portal link**


      ![](images/a24b112c579e1df59bb4919a0bbe2b67.jpg " ")

18. Click on the action menu for new PDB and delete this instance.

    ![](images/CMP-Task5-point18-latest.jpg " ")

19. While deleting instance you can preserve a backup and create a new instance in case required. 
  Select check-box: **Preserve a backup of this instance**
  
    Click **Ok**

    ![](images/CMP-Task5-point19-latest.jpg " ")

20.  Click **Close** to close the confirmation dialog box. 

   The Instance has been successfully deleted. 

   Click on the refresh icon on the top right in case the PDB is still seen on the page.

## Task 6:  Setup  PDB-as-a-Service (PDBaaS)

Previous exercise demonstrated the process of Self-Service User requesting PDBs using available service templates. In this section, we will see the Administrative setup for PDBaaS.

  Logout as **Cyrus** user. 


Login to the EM Console as super administrator **sysman/welcome1**


![](images/Task6-sysmanlogin.jpg " ")

### **PaaS Infrastructure Zone**

1. On the EM Console, go to **Setup** ->> **Cloud** ->> **Database**.

    ![](images/edfbce40d3abb0f21705992cc042c3ee.jpg " ")

2. Select **Pluggable Database** from the drop-down menu.

  ![](images/cf57fcbd4fe1570c40a1ee7f9b75dcec.jpg " ")

3. Click on **PaaS Infrastructure Zone**. 

    Zone is a pool of Hosts where the PDBs can be provisioned. 
      Click on **Sales Infra Zone**

      ![](images/8ed6c692f382172bbc9f6e2b90179f9e.jpg " ")


4. You are taken to the Zone Home page; you can see all the details of a Zone such as the host members of this zone. 

    You can explore more about the zone on this page.

      ![](images/CMP-Task6-point4.jpg " ")

### **Pluggable Database Pool**

5. On the EM Console, Click on **Setup** --> **Cloud** -->  **Database**. 

      ![](images/edfbce40d3abb0f21705992cc042c3ee.jpg " ")

6. Select **Pluggable Database** from the drop-down menu. 
  ![](images/cf57fcbd4fe1570c40a1ee7f9b75dcec.jpg " ")

   
    Click on **Pluggable Database Pool**. A Pluggable Database Pool consists of a set of Container Databases on which PDBs will be provisioned.

    Click on name of the pool **pdbpool** to see more details.

    ![](images/b49f455842d0fb11dd7de44fcaccfe26.jpg " ")

7. You are taken to the Database pool. Explore the Memory allocation and CPU allocation details

    ![](images/CMP-Task6-point6.jpg " ")

   Scroll down to see details of Members and Service Templates.

    ![](images/243ed347412f16a2159b2184c2dacdf7.jpg " ")

### **Data Sources**

8. On the EM Console, Click on **Setup** --> **Cloud** -->  **Database**.

    Select Pluggable Database from the drop-down menu.

    ![](images/cf57fcbd4fe1570c40a1ee7f9b75dcec.jpg " ") 
    
    
9. Click on **Data Sources**. Observe that the profile is based on Schema Export(s). This Data Profile will be used for provisioning a PDB with data.

    ![](images/d834209bf1c6a238679ae419098ee0f3.jpg " ")

10. Click on the row with profile to see more details. 
    This will open a Provisioning Profile Dialog box with details of PDB name , tablespaces , and creation details.

    Once done, close the Provisioning Profile pop up box. 


    ![](images/532db10bbaab85fcdd83f245bd317a6b.jpg " ")

 

### **Service Templates**
10. From the Cloud Home page , Select Pluggable Database from the drop-down menu.                                                                                   
Click on **Service Templates**. 

    There are two service templates pertaining to Pluggable Database

      * **Provision New Empty Pluggable Database**: This template enables the user to create a new empty pluggable database in a container database configured by DBA
      * **Provision Pluggable Database with Data**: This template enables user to create a new pluggable database with data from a non-container database.
 

    ![](images/47baba2a1e7567bfb0b5f89429a7831d.jpg " ")



11. Click on name of any template to explore more details.

    Once done, close the Service template Pop up window.


    ![](images/a0efb63a12d01e1254593656765ec52a.jpg " ")




    

**This completes the Lab!**

You may now [proceed to the next lab](#next).

## Learn More
- [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
- [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
- [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)
- [Database Cloud Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/cloud.html)

## Acknowledgements
  - **Author** - Harish Niddagatta, Oracle Enterprise Manager Product Management
  - **Contributors** -  Rene Fontcha
  - **Last Updated By/Date** - Sravanth Mouli, Oracle Enterprise Manager Product Management -  June 2022
