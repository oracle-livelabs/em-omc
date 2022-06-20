# Migration Workbench - Oracle Cloud Destinations

## Introduction

You can use the database migration workbench to migrate your on-premises databases to to new destinations in your data center or to Autonomous Database (ADB) in Oracle Cloud Infrastructure (OCI). This lab demonstrate using Migration Workbench for **on-premises** to **Oracle Cloud Infrastructure (OCI)** migration.

*Estimated Lab Time:* 35 minutes

### About Migration Workbench

Oracle Enterprise Manager Database Migration Workbench provides an accurate approach to migration and consolidation by eliminating human errors allowing you to easily move your on-premises databases to Oracle Cloud, Multitenant architecture or upgrade your infrastructure. Advantages of using Database Migration Workbech include: Near Zero Downtime, Assured Zero Data Loss, seamless on-premises or Cloud migrations and, MAA and Cloud Security compliant.

### Objectives

In this lab you will perform the Tasks below. The pre-requisites in task 1 will be mostly performed in a terminal window, but we'll use the Enterprise manager console for the migration tasks. In the the migration task you will create a migration activity, add details, and learn about the various configuration options. After the migration is complete, you will validate the destination database and compare performance before and after the migration.

| Task No.                                      | Description                                                                 | Approx. Time | Details                                                                                                                                                                                    |
|-----------------------------------------------------------|-------------------------------------------------------------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | Perform Migration Workbench Pre-Requisites| 30 minutes | Perform pre-requisites required on the source and destination databases, source hosts and in Enterprise Manager |
| 2 | Migrate and upgrade a 12c non-container database to autonomous database in OCI | 30 minutes   | Source database: orcl, destination database: ATP-ORCL |

### Prerequisites

- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
  - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
  - Lab: Environment Setup
  - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 RU5, and database 19.12 as Oracle Management Repository.

## Task 1: Perform Migration Workbench Pre-Requisites

### **Verify source database discovered in Enterprise Manager**

1. On the browser window on the right preloaded with *Enterprise Manager*, if not already logged in, click on the *Username* field and login with the credentials provided below.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![Login Page](../initialize-environment/images/em-login.png " ")

    The Enterprise Summary page shows some down targets. This is OK as We shut down some databases not used in this workshop.
    ![Enterprise Summary](../em-migration-workbench-onprem/images/t1_01_enterprise_summary.png " ")
2. Click on "Targets"->"Databases":
    ![Databases](images/t1_01_databases.png " ")
    - orcl is our source database

### **Create storage bucket and destination autonomous database**

1. Create Object Storage Bucket in OCI
    - In OCI Console, navigate to Storage->Buckets
    - On the left navigation bar, under "List Scope", choose the compartment you were provided for this workshop
    - Click "Create Bucket"
    - Bucket Name:

        ```
        <copy>bucket-mwb</copy>
        ```

    - Leave all other fields at default and click Create.
2. Create Autonomous Database
    - In OCI Console, navigate to Oracle Database->Autonomous Database
    - On the left navigation bar, under "List Scope", choose the compartment you were provided for this workshop
    - Click on "Create Autonomous Database"
    - On the "Create Autonomous Database" screen:
    - Under "Provide basic information for the Autonomous Database":
        - Compartment field will be already populated
        - Display Name:

            ```
            <copy>ATP-ORCL</copy>
            ```

        - Database Name:

            ```
            <copy>ORCL</copy>
            ```

        - Choose a Workload Type: Transaction Processing
        - Choose a Deployment Type: Shared Infrastructure
    - Under "Configure the database":
        - Leave all fields at default values
    - Under "Create administrator credentials"
        - Enter a password. For the purpose of this demo use:

            ```
            <copy>Welcome12345</copy>
            ```

    - Under "Choose network access":
        - Leave all fields at default values
    - Under "Choose License and Oracle Database Edition":
        - Select "Bring Your Own License (BYOL)"
        - Database Edition options will be shown. Keep selected option (EE)
    - Click "Create Autonomous Database"
    ![Create ATP](images/t1_02_create_atp.png " ")

### **Discover the destination autonomous database in Enterprise Manager**

  1. Download the ATP-ORCL client wallet using OCI console:

    - In OCI Console, navigate to Oracle Database->Autonomous Database
    - Click on the "ATP-ORCL" database to display the database homepage
    ![ATP Home](images/t1_03_atp_home.png " ")
    - Click "Service Console". The database console opens in a new browser tab
    - On the Service Console click on the "Administration" link in the left navigation bar
    - Click on "Download Client Credentials (Wallet)" tile
    - On the pop-up window, enter password and click "Download":
        
        ```
        <copy>welcome1</copy>
        ```

    - The wallet zip file will be downloaded to the local "Downloads" directory:
    ![Wallet Download](images/t1_04_wallet_download.png " ")

  2. Add ATP-ORCL as a target to Enterprise Manager:
  
    - In Enterprise Manager console on the first tab of the browser, navigate to "Setup"->"Add Target"->"Add Target Manually"
    - On the "Add Targets Manually" screen, click the "Add Target Manually" button
    - On the resulting pop-up window:
        - Agent Host:

            ```
            <copy>emcc.marketplace.com</copy>
            ```

        -  Target Type:

            ```
            <copy>autonomous</copy>
            ```

        - Hit Enter
        - Select "Autonomous Transaction Processing" and click "Add":
    ![Add ATP](images/t1_05_add_atp.png " ")
    - On the "Add Autonomous Transaction Processing: Properties" screen, enter:
      - Target Name:
        
        ```
        <copy>ATP-ORCL</copy>
        ```

      - OCI Client Credential (Wallet): click "Choose File" and select the wallet zip file you saved in the previous step
      - Wallet Password:
        
        ```
        <copy>welcome1</copy>
        ```

      - Service Name: Choose "**orcl_high**" from the drop-down list
      - Monitoring Username: The default monitoring user "adbsnmp" is initially locked. For this lab we'll just use the ADMIN user for monitoring. Replace "adbsnmp" with "ADMIN" (upper case):
        
        ```
        <copy>ADMIN</copy>
        ```
    - Monitoring Password:
        
        ```
        <copy>Welcome12345</copy>
        ```

    - Click "Test Connection" (it may take a couple of minutes to get the result back):
    ![ATP Props](images/t1_06_atp_props.png " ")
    - Click Next
    - On the Review screen click Submit
    - Click on "Targets"->"Databases". The new autonomous database has been discovered in Enterprise Manager:
    ![ATP Target](images/t1_07_atp_target.png " ")

### **Create a local directory for migration data**

Execute the following task in a terminal window:

- Create a local directory on the source host for the export data. We'll create a directory object for this directory next. Note we could have used the existing DATA\_PUMP\_DIR directory object and its corresponding directory, but we are opting to separate Migration Workbench data in its own directory.

    ```
    <copy>mkdir -p /u01/app/oracle/mwb</copy>
    ```

### **Prerequisites required by the source database**

Note: The script below may take a few minutes to complete. Do not cancel or close the terminal window. To see the content of the script before executing, replace "sh" with "cat" in the command.
  
  1. For orcl (Source database): Enable archive log mode, create directory object, create export user and assign required privileges.

    ```
    <copy>
    sh $HOME/scripts/mwb/prepare_source_db_orcl.sh
    </copy>
    ```

  2. Create Named Credentials for the Migration Workbench user
    - Using the Enterprise Manager console, navigate to "Setup"->"Security"->"Named Credentials"
    - Click "Create"
    - On the "Create Credential" screen, enter:
    - Credential name:

        ```
        <copy>MWBUSER</copy>
        ```

    - Authenticating Target Type: Database Instance
    - Credential type: Database Credentials
    - Scope: Global
    - UserName:

        ```
        <copy>MWBUSER</copy>
       ```

    - Password:

        ```
        <copy>welcome1</copy>
        ```

    - Role: Normal
      ![MWB User Credential](../em-migration-workbench-onprem/images/t1_03_mwbuser_credential.png " ")
    - Click “Test and Save”. Choose database **orcl** to test. You should get "Confirmation credential operation successful". If not, review the steps above and retry.
      ![Credential Created](../em-migration-workbench-onprem/images/t1_04_credential_created.png " ")

### **Prerequisites required by the destination autonomous database**

  1. Create ATP Credential in OEM
    - Using the Enterprise Manager console, navigate to "Setup"->"Security"->"Named Credentials"
    - Click "Create"
    - On the "Create Credential" screen, enter:

      General Properties
        - Credential name:

            ```
            <copy>ADMIN</copy>
            ```

        - Authenticating Target Type: "**Autonomous Transaction Processing**"
        - Credential type: "**Database Credentials**"
        - Scope: Target
        - Target Type: "**Autonomous Transaction Processing**"
        - Target Name:

            ```
            <copy>ATP-ORCL</copy>
            ```

      Credential Properties
        - UserName:

            ```
            <copy>ADMIN</copy>
            ```

        - Password:

            ```
            <copy>Welcome12345</copy>
           ```

      - Role: Normal

    ![ATP Credential](images/t1_08_atp_credential.png " ")

    - Click “Test and Save”. You should get "Confirmation credential operation successful". If not, review the steps above and retry.

  2. Generate RSA key pair in PEM format

    In the top-right corner of the Console, open the Profile menu (User menu icon), then click User Settings to view the details:
    - In the left navigation bar, under "Resources", click on "API Keys"
    - Under “API Keys” click “Add API Key”.
    - In the pop-up window, keep the default option "Generate API Key Pair" selected
    - Click "Download Private Key" and save it to the Downloads folder in your NoVNC window (the file name will have an extension of ".pem")
    - Click "Add"
    ![Add API Key](images/t1_10_add_api_Key.png " ")
    - The text shown under "Fingerprint" is the public key. Make a note of it as it will be used in a subsequent step. To save it to a text file, click on "Applications" on the top left corner of your NoVNC window, then "Accessories"->"Text Editor". Paste the public key and save the file to the desktop
    ![API Key](images/t1_11_api_Key.png " ")

  3. Create an OCI Auth Token

    While on the same screen in the OCI Console from previous step:
    - In the left navigation bar, under "Resources", click on "Auth Tokens"
    - Under "Auth Tokens" click Generate Token:
      - Description:

          ```
          <copy>Migration Workbench</copy>
          ```

      - Click Generate Token

    - The new Auth Token is displayed
    - Copy the auth token and save it to a file to retrieve it later, it won't be shown again in the Console. Open a new tab in the Text Editor you launched in the previous step, paste the token, and save the file to the desktop
    - Close the Generate Token dialog:
    ![Auth Token](images/t1_09_auth_token.png " ")

  4. Create OCI Credential in Enterprise Manager
    - Make a note of your Tenancy OCID and User OCID:
        - Open a new tab in the Text Editor you launched in the previous step. You will save your tenancy OCID and USer OCID here to use later in this step
        - On the OCI console, click on the user icon on the top right of the screen
        - Click on your tenancy link. Under "Tenancy Information" copy the tenancy OCID to the text editor
        - Click again on the user icon, then click on User Settings
        - Under "User Information" copy your user OCID to the text editor  

    - Using the Enterprise Manager console, navigate to "Setup"->"Security"->"Named Credentials"
    - Click "Create"
    - On the "Create Credential" screen, enter:
  
      General Properties
  
        - Credential name:

            ```
            <copy>OCI</copy>
            ```

        - Authenticating Target Type: **Autonomous Transaction Processing**
        - Credential type: **Oracle Cloud Infrastructure Credential**
        - Scope: Target
        - Target Type: **Autonomous Transaction Processing**
        - Target Name:

            ```
            <copy>ATP-ORCL</copy>
            ```
          
      Credential Properties
  
        - Tenancy OCID: Tenancy OCID you copied earlier in this step
        - User OCID: User OCID you copied earlier in this step
        - Public Key Fingerprint: Public Key Fingerprint you saved to your desktop
        - Private Key: Private Key you saved to the Downloads folder (file with extension of ".pem")

      ![OCI Credential](images/t1_12_oci_credential.png " ")

    - Click Save. You should get "Confirmation credential operation successful". If not, review the steps above and retry

  5. Create Authentication Credential in ADB

    Create an "Auth Token" based credential in the Autonomous Database and set it as a default credential that will be required for authentication between the Autonomous Database and OCI object storage.

    - This step requires your fully qualified OCI username, not your user OCID used in the previous step. In OCI console, click on the user icon on the top right of the page, then click on "User Details". Make a note of your fully qualified username at the top of the screen
    - In OCI Console, navigate to Oracle Database->Autonomous Database
    - Click on the "ATP-ORCL" database to display the database homepage
    ![ATP Home](images/t1_03_atp_home.png " ")
    - Click "Service Console" to display the database console
    - On the Service Console click on the "Development" link, then click on "Database Actions"
    - Username:

        ```
        <copy>ADMIN</copy>
        ```
          
    - Password:

        ```
        <copy>Welcome12345</copy>
        ```
          
    - On the "Development" screen, click on "SQL" (first tile) 
    - Execute the following code:

        ```
        <copy>
        BEGIN
        DBMS_CLOUD.CREATE_CREDENTIAL(
         credential_name => 'OBJ_STORE_CRED',
         username => 'Your fully qualified OCI username from earlier in this step',
        password => 'Value of your Migration Workbench token you saved earlier to the desktop');
        END;
        /
        </copy>
        ```
      ![Obj Store Cred](images/t1_13_obj_store_cred.png " ")
    - Next execute the following SQL statement:

        ```
        <copy>
        ALTER DATABASE PROPERTY SET default_credential = 'ADMIN.OBJ_STORE_CRED';
        </copy>
        ```
      ![ATP Default Cred](images/t1_14_atp_default_cred.png " ")

### **Check the Destination ADB doesn't have the HR schema**

Our source database has the HR sample schema. Our target database does not before the migration. In addition to the validation checks done by the tool, we can do an additional validation to check the existence of this schema in the destination database before and after the migration.

- Using the same SQL Worksheet from the previous step, execute the following query:

    ```
    <copy>select count(*) from dba_users where username='HR';</copy>
    ```

    ![Query Result](images/t1_15_query_result.png " ")

    The query result (**0**) indicates the HR schema doesn't exist in the destination database.

## Task 2: Migrate and upgrade a 12c non-container database to autonomous database in Oracle Cloud

### **Overview**

In this step we'll migrate and upgrade an Oracle 12c database to autonomous database in Oracle Cloud Infrastructure (OCI). For migration to OCI, the Migration Workbench supports the data pump migration method as of EM 13.5 RU5. Additional migration methods may be added in future releases.

### **Execution**

1. Log into your Enterprise Manager as **sysman** as indicated in the Prerequisites step if not already done.
2. From the Enterprise menu, navigate to "Migration and Consolidation"->"Database Migration Workbench"
3. On the "Database Migration" page, collapse the "Getting Started" region and click on "Create Migration Activity"
![Database Migration](../em-migration-workbench-onprem/images/t2_01_database_migration.png " ")
4. On the Create Migration Activity screen:
    - Activity Name:

        ```
        <copy>Database Migration ORCL to ATP-ORCL</copy>
        ```


    - Migrate: Full Database
    - Select Source Database: orcl.subnet.vcn.oraclevcn.com
    - Select Destination Database: ATP-ORCL
    - If you receive a warning on Tools Validation, click "Upload Migration Tools"
      ![Migration Tools](images/t2_01_mig_tools.png " ")
    - Upload the "p32613591\_112048\_Generic.zip" file from the Downloads folder
      ![Select CPAT](images/t2_02_select_cpat.png " ")
      - Click Continue
      ![CPAT Available](images/t2_03_cpat_available.png " ")
5. On the Add Details screen:

    Source:
    - Database Credentials: MWBUSER (Named)
    - Host Credential: ORACLE (Named)

    Target:
    - Database Credential: ADMIN (Named)
    - Agent Host Credential: ORACLE (Named)
    - Service Name: orcl_high (TCPS)

    Action:
    - Migration Method: Data Pump (default)
    - Recompile Invalid Objects After Migration: Unchecked (default)
    - Compare Performance After Migration: Checked (default)
    - Source Data Pump Directory: MWB_DIR
    - Encryption Password:

        ```
        <copy>welcome1</copy>
        ```

    - Cloud Storage URL:

        ```
        <copy>objectstorage.us-ashburn-1.oraclecloud.com</copy>
        ```

    - Bucket Name:

        ```
        <copy>bucket-mwb</copy>
        ```

    - OCI Credential: OCI
    - Database OCI Auth Credential: ADMIN.MWB_CRED
    - Click Next
      ![Add Details](images/t2_04_add_details.png " ")
    - Click Next

6. On the Customize screen
    - Under Export Options/Parallel: change from default to 4
    - Under Import options/Parallel: change from default 2
    - Notice mapping the Users tablespace in the source database to Data table space in the destination database
    - Leave everything else at default for the purpose of this demo
    - Click Review
    ![customize](images/t2_05_customize.png " ")

7. On the Review and Submit screen

    - Review your entries and click Analyze Source.
    ![Anaylze Source](images/t2_06_anayze_source.png " ")
    - When the analysis is completed the button text will change to "View Analysis Report". Click the button and the report will open in a new browser tab. Review CPAT Results
    ![CPAT Results](images/t2_07_cpat_results.png " ")
    - Review the results. In the blockers section, the migration privileges in the source database are not available in autonomous database, this is expected and we can proceed.
    - Note you can download the CPAT results if desired. Click on the previous tab to continue with the migration process.
    ![Validate](images/t2_08_validate.png " ")
    - Click "Validate"

8. Validation checks run for a few minutes and all checks should pass. Click "Close & Submit". If not check your previous steps, fix the error and revalidate
 ![Validate Activity](images/t2_09_validate_activity.png " ")
9. On the Submit Activity screen, check the "Confirm that you have done source analysis" checkbox
  ![Submit Activity](images/t2_10_submit_activity.png " ")
10. Click submit, then click "Close and Go Back to Activities Page"
11. On the activity page, change the Auto Refresh to 1 minute
 ![Activity Page](images/t2_11_activity_page.png " ")
11. Click on the "Running" link under Status to go to the procedure activity page. Choose Show: "Steps Not Skipped"
 ![Procedure Activity](images/t2_12_procedure_activity.png " ")
12. When the procedure completes, it will most likely show there were some errors. We'll check those when we analyze the migration:
 ![Procedure Activity Completed](images/t2_13_procedure_activity_completed.png " ")
13. From the Enterprise Menu, click "Migration and Consolidation"->"Database Migration Workbench" to check the activity page. Notice althouh the status is "Completed with Errors", The summary region at the top shows the exit level of the activity was Warning, not Problems. Click on the View Analysis link.
14. On the "View Analysis" page, examine the errors. You should be able to ignore most of these, but those that need to be addressed are generally specific to the database being migrated and should be addressed by the database administrator as appropriate.
 ![View Analysis](images/t2_14_view_analysis.png " ")
15. Go back to the activity page and click on the "Compare Performance" link.
16. Examine the Performace Comparison report to analyze the database performance before and after the migration
 ![Performance Comparison](images/t2_15_performance_comparison.png " ")
17. Finally let's validate the HR schema has been migrated and has the same number of objects as in the source database:

- In OCI Console, navigate to Oracle Database->Autonomous Database
- Click on the "ATP-ORCL" database to display the database homepage
  ![ATP Home](images/t1_03_atp_home.png " ")
- Click "Service Console" to display the database console
- On the Service Console click on the "Development" link, then click "Database Actions"
- Login with username "ADMIN" and password
- On the "Development" screen, click on "SQL" (first tile)
- Execute the following query:

    ```
    <copy>
    select count(*) from dba_objects where owner='HR';
    </copy>
    ```

    The query result shows the HR schema now exists in the target database and owns **34** objects.
    ![Query Result](images/t2_16_query_result.png " ")
    You have now completed this task.

This completes the Lab!

You may now [proceed to the next lab](#next).

## Learn More

- [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
- [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
- [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements

- **Author** - Amine Tarhini, Systems Management Specialist, Oracle Platform Solution Engineering
- **Contributors** -  Harish Niddagatta, Oracle Enterprise Manager Product Management
- **Last Updated By/Date** - Amine Tarhini, June 2022
