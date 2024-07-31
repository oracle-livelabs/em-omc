# Hybrid Pluggable Database as a Service
## Introduction

Competitive businesses rely on Pluggable Database as a Service (PDBaaS) to provide the agility needed to meet fast changing market requirements and respond to demands for additional services. In this session, learn how customers can establish Pluggable Database as a Service(PDBaaS) on top of any infrastructure to achieve higher consolidation, and reduce cost of administrative tasks. 
Leverage database service to make database management organized, quickly deploy standardized secure database configurations on demand to meet application requirements.

Gain technical insights to build DevOps environment for application owners to deploy databases on-demand via self-service interface while achieving maximum resource utilization and standardization. 

*Estimated Lab Time: 60 minutes*


### About Cloud Management Pack

Cloud Management Pack (CMP) that resides on top of DBLM, provides  lifecycle management of PDBs in Database Private Cloud. This enables the Self Service Users to Provision, Plug-Unplug , Clone, Migrate and Scale PDBs in the Private Cloud.


### Objectives

The objective of this workshop is to highlight Oracle Enterprise Manager 13c Lifecycle Management capabilities for multitenant databases.

| **Step No.** | **Feature**                                                                | **Approx. Time** | **Description**                                                                                                                                                                      | **Benefits**                                                                                                                                                                                                                   |
|--------|----------------------------------------------------------------------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | Overview of SSA User and associated role                                      | 10min                     |  This guided flow will walk you through the process of creating an SSA users, assigning them the right roles, and granting the necessary privileges. We have a pre-created user named 'cyrus',  explore how to configure their access for configuring self service administration.                                                                                      | Using EM_CLOUD_ADMINISTRATOR role  you can set up and manage the necessary cloud infrastructure for setting up PDB as a Service. An EM_SSA_USER can be associated with application or developers to provision and manager their databases as defined by EM_CLOUD_ADMINISTRATOR. You can take advantage of all the other available roles in setting up role based access control and securing your infrastructure setup. You can check the documentation for more details about defining roles and assigning users. Click here for more details.                                                                                                        |
| 2    | Creation of PDBaaS Infra | 10min                     | The PDBaaS Infrastructure consists of PDBaaS Zone, PDB Pool, Service Templates , Data Source, Quotas and Request settings. In this task we will explore most of these components to get a hands-on experience in building it.    | The PDBaaS infrastructure helps in enhancing control of your database infrastructure and provides you the ability to scale up and scale down easily based on demand. It also provides you visibility into your cost and allows customisation tailored according to your organisational needs.                                                 |
| 3    | Create a PDB as Self Service User       | 5min                      | Request a PDB using service catalogue, resize the PDB and then delete the PDB while preserving the contents. | A service template is like predefined standard logic which will be used to deploy a database resource. A service template defines the characteristics of the instance(s). A Self service user who could be a developer or a BA or even an application owner can now provision and manage databases with very minimal inputs using service templates created by cloud administrator. Self Service users cane be empowered to provision, update, backup, delete and also restore their databases on their own without the intervention of cloud administrators. |
| 4    | Restore the PDB using Service Template                                | 5min                      | Dehydrate and Hydrate a PDB using Self-Service Portal                                                                             | Enterprise Manager provides an option for a Self Service user (SSA) user to create a data profile while deleting the PDB which was created using PDBaaS.The backup is stored in the Software library by default, and the location can be customized. This is referred as Dehydrating a PDB. A service template can be created to provision a PDB using the profile which was created by SSA user while deleting the PDB. This is known as Hydrate. The Dehydrate and Hydrate usecase can be adopted by SSA users which helps in faster and repeatable deployments.  enhanced testing, minimise the storage utilisation and rapid database provisioning with data.   |
| 5    | Patch a PDB as Self Service User | 10min    |  Patch a pluggable database as a SSA User | Patching is generally an time and resource intensive actviity. Fleet Maintenance integrates its functionality with Cloud Management Pack to provide the ability of patching a pluggable database to SSA users without compromising the security and standardisations of the organistion |



### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository. Workshop activities included in this lab will be executed both locally on the instance using Enterprise Manager Command Line Interface (EMCLI) or Rest APIs, and the Enterprise Manager console (browser)

## Task 1: Overview of SSA User and SSA Admin User

1. On the browser window on the right preloaded with *Enterprise Manager*, if not already logged in, click on the *Username* field and login with the credentials provided below.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![em -login-page](images/pdbaas-sysman-login.png " em-login-page ")


2.  On the right, click on the 'Setup' menu and choose 'Security' and then 'Roles'.  

    ![Navigate to Security](images/navigate-to-security.png " Navigate to Security ")

    The "Developer" role you see has been pre-created. This is the role which will be attached to the SSA USER( CYRUS) which will be used in this Demo.

    Click on the "Developer" role to view more details. 
    
    View the target and resource privileges associated with this role.  You will also see a user 'Cyrus' is already associated to this role. 

 
    ![SSA-Role](images/ssa-role.png " SSA Role " )

    Click 'OK'

3. Now, let us view the users which has this roles attached. 

    Click on "Setup"  and choose 'Security' and then 'Administrators'. 

    ![Navigate-to-security](images/demo-admin-user.png " Navigate-to-security ")  
    
    Click 'CYRUS'

    ![Choose-Cyrus-User.png](images/choose-cyrus-user.png " Choose-Cyrus-User.png ") 

    You can see here the "DEVELOPER" role which we reviewed earlier is also attached to the "Cyrus" user. You can also view the Target privileges and resource privileges.
    
    ![cyrus-user-details](images/cyrus-user-details.png " cyrus-user-detail ") 

    Click 'Close'. 

    Click on the Oracle logo on the top left as shown in the image above to take you back to the EM Home Page.

## Task 2: Creation of PDBaaS Infrastructure

    
In  this task we will build all the necessary componets required in setting up PDBaaS Infrastructure. We will continue to do the PDBaaS setup as sysman user. 

  Optionally, you can could also create an SSA_ADMIN role and allocate the relevant privileges to create the required infrastructure.    

1. **Creation of PaaS Infrastructure Zone**: 
    
    Navigate from Setup >> Cloud >> Database

    ![Navigate-to-Cloud](images/navigate-to-cloud.png "Navigate-to-Cloud") 

2. Choose pluggable database from the dropdown. 
    ![Choose-PDB-Dropdown](images/choose-pdb-dropdown.png "Choose-PDB-Dropdown")

3. Click on 'PaaS Infrastucture Zone' on the left menu bar and then click 'Create'. 

    ![Creating-PaaS-Zone](images/creating-paas-zone.png "Creating-PaaS-Zone")

4. Provide a Target Name and Description as suggested below. 

    Click Next

    ![PaaS-zone-Details](images/paaszonedetails.png "PaaS-zone-Details")

5. In the Members page  click on "Add" . 
    From the pop-up dialog box Choose 'emcc.marketplace' and click on "select". 

    ![Paas-memebers](images/paas-memebers.png "Paas-memebers")

    Click Next

6. On the Credentials page , Click on "Named" radio button and choose 
    "Oracle" from the dropdown. 

    Click Next

    ![Paas-zone](images/paas-zone-credentails.png "PaaS Zone")

7. No changes on the "Placement Constraints" page,  let us continue with the
    default value as seen below. 

    Click "Next"

    ![Paas-zone](images/paas-placement.png "PaaS Zone")

8. No changes on the "Characteristics" page. Optionally you can choose to 
   add tags as shown below. You can select a value from the dropdown. 

    Click "Next"

    ![Paas-zone](images/paas-tags.png "PaaS Zone")

9. On the Roles page, click  "Add". Choose the "Developer" role and 
    click  "Select"
    
    Click Next

    ![Paas-zone](images/paas-add-role.png "PaaS Zone")

10. Review the details and click "Submit"
    ![Paas-zone](images/paas-review.png "PaaS Zone")


    The PaaS infra zone has been created successfully. 
    
    ![Paas-zone](images/paas-create-confirm.png "PaaS Zone")

11. **Creation of Pluggable Database Pool**

    Click on 'Pluggable Database Pool' on the left menubar. 
    
    Click Create. 

    ![pdb-pool](images/pdbpool-create.png "pdb-pool")

12. In the **Setup** page section,


    **Step 1 Pool Details**

      ```
        Name: SalesDemoPool
      ```
      ```
      Description : Sales Demo Pool
      ```

    **Step 2 Credentails**

    Click on 'Named' radio button  for all the credentials. Click on the dropdown to choose each of the value

      ```
      Database Home Credentials : ORACLE(SYSMAN)
      ```
      ```
      Root Credentails : ORACLE(SYSMAN)
      ```
      ```
      Grid Infrastructure : ORACLE(SYSMAN)
      ```
      ```
      Database : OEM_SYS(SYSMAN)
      ```
    **Step 3 Container Database**

      Click on the dropdown to choose each of the value

      ```
      PaaS Infrastructure Zone : Sales Demo
      ```
      ```
      Platform: Linux x86_64
      ```
      ```
      Target Type : Database Instance
      ```
      ```
      Version : 19.0.0.0
      ```
    
    ![Paas-zone](images/pdbpool-details1.png "PaaS Zone")

    Next step would be to add the container databases of our choice to the pool.


    Click on **Add** to choose the databases.  
    On the pop up dialog box we will chose both the databases *cdb19c*  and *sales* and 
    
    click **Select**

    ![Paas-zone](images/pdbpool-details2.png "PaaS Zone")

    Validate all the details, and click Next. 

    ![Paas-zone](images/pdbpool-creation1.png "PaaS Zone")

13. In the policies page we can choose to reduce the maximum number of pdbs 
   and adjust the workloads. We will proceed with the default values. 

    ![Paas-zone](images/pdbpool-creation2.png "PaaS Zone")

    Review all the details and click **Submit**

14. The Pluggable database pool has been sucessfuly created. 


    ![Paas-zone](images/pdbpool-creation-confirmation.png "PaaS Zone")

15. **Review Quotas and Data Source**

    Click on "Quotas" from the left pane.  For the "Developer" role a quota has been pre-created as seen below. 
    Optionally, you can choose to edit to adjust the values. 

    ![Paas-zone](images/quota-review.png "PaaS Zone")

16. Click on "Data Sources" from the left pane. 

    A sample data profile has been created which could be used for creating a new database. 

    ![Paas-zone](images/datasource-review.png "PaaS Zone")

17. **Create Service Templates**
    We will attempt to create 2 service templates. 

        1. Template to create an empty pluggable database. 
        2. Template to create a Pluggable database using profile

    
    Click on "Service Templates" from the left pane. 

    Click on "Create".

     ![service-template1](images/service-template1.png "service-template")
     **Step 1 General Details**

      ```
      Name: NewEmptyPDB
      ```
      ```
      Description : Template to create a new pluggable database
      ```
    Click on 'Create Empty Pluggable Database' radio button.    



    In the "Pools and Zones"  section
	Click "Add".  Choose the zone 'Sales Demo' from the pop-up and click 'Select'. 

     ![service-template1](images/service-template2.png "service-template")
	
    
    Click 'Sales Demo' and later Click on "Assign Pool" ,  choose "SalesDemo Pool"  from the pop-up and click 'Select'

     ![service-template1](images/service-template3.png "service-template")
	
    Click on the magnifier icon in 'Reference container database' section,  choose "sales" database from the pop-up and click 'Select'. 

    Click Next

     ![service-template1](images/service-template4.png "service-template")

     In the Configuration page, click "Create" under workloads. 
            ```
            Name: Small
            ```
            ```
            Description: Small
            ```
            ```
            CPU: 0.2
            ```
            ```
            Memory: 0.2
            ```
            ```
            Sessions: 20
            ```
            ```
            Storage : 5
            ```
	    Click Create
     ![service-template1](images/servicetemplate-5.png "service-template")
    
    Let us attempt to create another workload. 
    
    Click "Create" under workloads
        ```
		Name: Large
        ```
        ```
		Description: Large
        ```
        ```
		CPU: 0.2
        ```
        ```
		Memory: 0.2
        ```
        ```
		Sessions: 30
        ```
        ```
		Storage : 5
        ```
		Click Create

    Under the Pluggable Database Administrators Privileges, 
    Click on the radio button "Allow SSA user to create a Data Profile" 
    ```
    Payload Location: /u01/app/oracle
    ```
    ```
    Temporary Working Directory: /tmp
    ```
    Click "Next"
   ![service-template1](images/servicetemplatessa.png "service-template")

    In the Intitialization Parameters Page, you can choose to edit or add new parameters. We will choose to go with default options.
    Click "Next"
     ![service-template1](images/servicetemplate6.png "service-template")
    
    Optionally , in the Customisation page , you can choose to add pre and post script . 
    Click Next

    ![service-template1](images/servicetemplate7.png "service-template")

    On the Roles Page, Click "Add". Choose "Developer" from the pop-up and click "Select"
    Click Next.

    ![service-template1](images/servicetemplate8.png "service-template")

    Review the details and click on "Create". 
    ![service-template1](images/servicetemplate9.png "service-template")
    
    The First Service Template has been created successfully. 



18. Now, let us create the second service template to provision a pluggable database using data profile. 

    Click on "Service Templates" from the left pane. 
    Click on "Create".

    ![service-template1](images/servicetemplate10.png "service-template")

     General Details

      ```
      Name: NewEmptyPDB using Profile
      ```
      ```
      Description : Template to create a new pluggable database using PDB Profile
      ```
    Click on radio button *Create Pluggable database using Data Profile selected by SSA user at request time.*     



    In the "Pools and Zones"  section
	Click "Add".  Choose the zone 'Sales Demo' from the pop-up and click 'Select'. 
    ![service-template1](images/servicetemplate11.png "service-template")
	
    
    Click 'Sales Demo' and later Click on "Assign Pool" ,  choose "SalesDemo Pool"  from the pop-up and click 'Select'
     ![service-template1](images/servicetemplate12.png "service-template")
	
    Click on the magnifier icon in 'Reference container database' section,  choose "sales" database from the pop-up and click 'Select'. 
   Click Next
     ![service-template1](images/servicetemplate13.png "service-template")

     In the Configuration page, click "Create" under workloads. 
            ```
            Name: Small
            ```
            ```
            Description: Small
            ```
            ```
            CPU: 0.2
            ```
            ```
            Memory: 0.2
            ```
            ```
            Sessions: 10
            ```
            ```
            Storage : 5
            ```
	    Click Create
     ![service-template1](images/servicetemplate-5.png "service-template")
    
    Let us attempt to create another workload. 
    
    Click "Create" under workloads
        ```
		Name: Large
        ```
        ```
		Description: Large
        ```
        ```
		CPU: 0.2
        ```
        ```
		Memory: 0.2
        ```
        ```
		Sessions: 20
        ```
        ```
		Storage : 5
        ```
		Click Create

    Under the Pluggable Database Administrators Privileges, 
    Click on the radio button "Allow SSA user to create a Data Profile" 
    ```
    Payload Location: /u01/app/oracle
    ```
    ```
    Temporary Working Directory: /tmp
    ```
    Click "Next"
   ![service-template1](images/servicetemplatessa.png "service-template")

    In the Intitialization Parameters Page, you can choose to edit or add new parameters. We will choose to go with default options.
    Click "Next"
     ![service-template1](images/servicetemplate6.png "service-template")
    
    Optionally , in the Customisation page , you can choose to add pre and post script . 
    Click Next

    ![service-template1](images/servicetemplate7.png "service-template")

    On the Roles Page, Click "Add". Choose "Developer" from the pop-up and click "Select"
    Click Next.

    ![service-template1](images/servicetemplate8.png "service-template")

    Review the details and click on "Create". 
    ![service-template1](images/servicetemplate14.png "service-template")

Both the service templates has been created successfully. 


## Task 3 : Create PDB as Self Service User

1. Logout as sysman and login as cyrus user. 

![deploypdb](images/sysman-logout.png "deploypdb")
                ```
                Username: cyrus
                ```
                ```
                Password: welcome1
                ```
![deploypdb](images/cyrus-login.png "deploypdb")

The PDBs are created using our service template on CDBs which we have virtually grouped as a pool.


2. By default, you will see the Database Cloud Self Service Portal landing page as shown below. 
   Click on Create Instance button.
   ![deploypdb](images/deploypdb1.png "deploypdb")

3. Select " New Empty PDB" 

   ![deploypdb](images/deploypdb2.png "deploypdb")
   
   Note: There are two service templates pertaining to Pluggable Database
   
   New Empty PDB: This template enables users to create a new empty pluggable database in a container database configured by DBA. 
   New PDB using Data Profile: This template enables users to create a new pluggable database using a data profile created earlier by an SSA user
   
4. In the Pluggable Database Configuration section,

	**Step 1**
		
	Enter PDB Name , Service and Size details:
        ```
		PDB Name: DemoSales
        ```
        ```
		Database Service Name : Service_DemoSales
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
        ```
        Confirm Password : welcome1
        ```
		
	    Tablespace name is auto populated.

        ```
		Tablespace name : pdb_tbs1
        ```
			
    **Step 3**

	Instance Details

		Request Name : Auto filled with latest timestamp. Can be modified in case needed.
		Zone : Auto filled with default option, 'Sales Demo' .
		Properties can help user locate an instance more quickly. Click on the dropdown to update.

        ```
		Lifecycle Status: <copy>Test</copy>
        ```
        ```
		Contact: <copy>CYRUS</copy>
        ```

	**Step 4**
		
	Instance Duration - Start: Immediately 
	Duration : Indefinitely 
						
		
	**Step 5**
		
	Validate all the details and Click on Submit button

![deploypdb](images/deploypdb3.png "deploypdb")



5. Once you submit a request, you will be redirected back to the “Database Cloud Services” Page.

	Under “Requests” region, you should see 1 requests for  “Create”  running.
	Click on the hourglass icon under status column for the Create Pluggable Database step. You will see details of request.
      ![deploypdb](images/deploypdb4.png "deploypdb")
	
	The request should take less than 3-4  minutes to complete.
	Click on refresh icon or as an alternative set Refresh to 30 seconds.

      ![deploypdb](images/deploypdb5.png "deploypdb")
		The success status indicates that PDB database was successfully created.
		Click on Close button when the procedure is complete.
      ![deploypdb](images/deploypdb6.png "deploypdb")
      The screen indicated the PDB creation is successful.
 
   
7. Click on the Home Icon. You will see new PDB instance. (Incase the newly created PDB is not reflecting, hit refresh on the top right corner of the page ). 
   
   Click on the PDB recently created.

    ![deploypdb](images/deploypdb7.png "deploypdb") 
   
8. On the PDB details page you can use the connection details to connect to the PDB using SQL tools.

    Click on Resize button to resize a PDB instance.

    ![deploypdb](images/deploypdb8.png "deploypdb") 

	
9. Select large and click resize
   
     Resize allows you to resize your instance to other available resource sizes.
    We have 2 resource sizes available for Service Template. Small and Large.
             Current size of PDB instance is Small, you can now resize it to large.

    ![deploypdb](images/deploypdb9.png "deploypdb") 
	  
10. Once you click on Resize, a job will be submitted to resize instance.
    
    In few minutes instance resize is completed. Expand Resource Usage section on PDB Home page.
    
    This shows now new resource usage limits.

	  
11. Next delete the database Instance:

    Go to the Database Cloud Services Home page by clicking on "Database Cloud Service Portal" link

    ![deploypdb](images/deploypdb10.png "deploypdb") 


12. Click on the action menu for new PDB and delete this instance.
    ![deploypdb](images/deploypdb11.png "deploypdb") 
    
13. While deleting instance you can preserve a backup and create a new instance in case required. 
    
    Select check-box: Preserve a backup of this instance. This will create a profile of this PDB which we can use to restore. 

	Click Ok

    ![deploypdb](images/deploypdb12.png "deploypdb") 

    Click "Close"
    ![deploypdb](images/deploypdb13.png "deploypdb") 
    The delete pdb will be completed in about a minute. Optionally under the requests region you can view the staus of the delete job.

## Task 4 : Restore a PDB as Self Service User
	
1. Now we will try to restore the PDB using the profile which we created during the delete PDB operation.

    Click on "Create Instance"

    Select "New PDB using Data Profile"

    ![deploypdb](images/deploypdb14.png "deploypdb") 

    In the Pluggable Database Configuration section,

	**Step 1**
		
	Choose Profile, PDB Name , Service and Size details:
    On the configuration page, click on the magnifier icon to choose the Data profile. Select the profile name and click Select.

    ```
	PDB Name: NewDemoSales
    ```
    ```
	Database Service Name : Service_NewDemoSales
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
    ```
    Confirm Password : welcome1
    ```
		
	Tablespace name is auto populated.
    ```
	Tablespace name : pdb_tbs1
    ```
		
		
	**Step 3**
		
	Instance Details
		
	Request Name : Auto filled with latest timestamp. Can be modified in case needed.
		
	Zone : Auto filled with default option, 'Sales Demo' .
		
	Properties can help user locate an instance more quickly. Click on the dropdown to update.

    ```
	Lifecycle Status: <copy>Test</copy>
    ```
    ```
	Contact: <copy>CYRUS</copy>
    ```

	**Step 4**
		
	Instance Duration - Start: Immediately 
						   Duration : Indefinitely 
						
		
	**Step 5**
		
	Validate all the details and Click on Submit. 

    ![deploypdb](images/deploypdb16.png "deploypdb")

    Once you submit a request, you will be redirected back to the “Database Cloud Services” Page.

	Under “Requests” region, you should see 1 requests for  “Create”  running.
	Click on the hourglass icon under status column for the Create Pluggable Database step. 
    You will see details of request.
    ![deploypdb](images/deploypdb17.png "deploypdb")
	
	The request should take less than 3-4  minutes to complete.
	Click on refresh icon or as an alternative set Refresh to 15 seconds.
	The success status indicates that PDB database was successfully created.
	Click on Close button when the procedure is complete.

    ![deploypdb](images/deploypdb18.png "deploypdb")
		

    The screen indicated the PDB creation is successful. Click on the Home icon. 

   ![deploypdb](images/pdbdeploy20.png "deploypdb")

## Task 5 : Patch a PDB as a Self Service User

In this task we will patch the "sales_newdemosales" PDB currently associated with "sales" CDB running on version 19.3. Our goal is to patch it to 19.12 by relocating it to container database "cdb19c.subnet.vcn.oraclevcn.com". 

   ![deploypdb](images/ssapatching1.png "deploypdb")

Now minimize the EM browser tab and double click on the terminal to launch it.  
   ![deploypdb](images/ssaptching2.png "deploypdb")

As a prerequisite we have already created a gold image for 19.12. 

1. The first step is to verify the gold image and identify the image_id.  
   Execute the below CLI in the terminal window. 

    ```
    emcli db_software_maintenance -getImages
    ```
    The highlighted row has the Image name and Image ID. 

    ![deploypdb](images/ssapatching3.png "deploypdb")

    "Latest19cimage" is the image which we have created and "F77B5DBB9EC34E78E053BB00000A577E" is our image id


2. The next step is to subscribe the current PDB pool to the gold image. 
    Execute the below CLI in the terminal. 

    ```
     emcli db_cloud_maintenance -subscribeTarget -pool_name=SalesDemoPool -pool_type=pdbaas_pool -image_id=F77B5DBB9EC34E78E053BB00000A577E
    ```
    The emcli verb should show successful status like this.
      ![deploypdb](images/ssapatching4.png "deploypdb")


3. Once we subscribe we attach the PDB Pool to the image created. 

    ```
    emcli db_cloud_maintenance -performOperation -purpose="ATTACH_CDB" -pool_name="SalesDemoPool" -pool_type="pdbaas_pool" -name="Attach an existing CDB" -target_type=oracle_database -description="Attach an existing CDB as the successor" -destinationCDB="cdb19c.subnet.vcn.oraclevcn.com" 
    ```
      ![deploypdb](images/ssapatching5.png "deploypdb")
    
    The Attach operation creates a procedure activity. This procedure takes about 30 seconds to execute. 

4.  After subscribe and attach, the next step would be to activate it. 
    Once you activate the newly attached CDB, any operations done in the exiting pool on sales CDB will be pointed to cdb19c.subnet.vcn.oraclevcn.com. 
    
    ```
    emcli db_cloud_maintenance -performOperation -purpose="ACTIVATE_CDB" -pool_name="SalesDemoPool" -pool_type="pdbaas_pool" -name="Activate the CDBs"  -target_type=oracle_database -description="Activates the newly created CDBs"   -target_list="sales"
    ```
      ![deploypdb](images/ssapatching6.png "deploypdb")

5. The above steps can be automated and can be performed by the Database   
  administrator without having any dependency of the application users, because there is not downtime involved here.  The SSA user can update their database at thier convinient time with a click of a button. 

    Log back to the EM console where you have logged in as cyrus user and click on the PDB as seen below. 

    ![deploypdb](images/ssapatching7.png "deploypdb")

6. Click on "Update Database" and choose to run immediately. 
    Click on "Update". 

    ![deploypdb](images/ssapatching8.png "deploypdb")

7. Click on "Database Cloud Self Service Portal" 

    ![deploypdb](images/ssapatching9.png "deploypdb")

8. Logout as cyrus and login as sysman. 
   ```
   Username: sysman
   ```
   ```
   Password: welcome1
   ```

9. Navigate from *Enterprise >> Provisioning and Patching >> Procedure  
    Activity*

    ![deploypdb](images/ssapatching11.png "deploypdb")

    Click on the Update procedure to view more details about the precedure log. 


10.  Click on the "Oracle" Home icon on the top left. Navigate from *Targets>> Databases*.
    ![deploypdb](images/ssapatching13.png "deploypdb")
    We will now see the PDB has been relocated and updated to 19.12
    ![deploypdb](images/ssapatching14.png "deploypdb")

This concludes the lab. 


## Learn More
- [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
- [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
- [Database Cloud Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/cloud.html)
- [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/lifecycle.html)

## Acknowledgements
  - **Author** - Sravanth Mouli, Oracle Enterprise Manager Product Management
  - **Contributors** -  Anand Prabu 
  - **Last Updated By/Date** - Sravanth Mouli, Oracle Enterprise Manager Product Management -  May 2024
    




    
