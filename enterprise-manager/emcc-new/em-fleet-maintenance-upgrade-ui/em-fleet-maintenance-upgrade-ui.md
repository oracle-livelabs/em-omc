# Automated Database Upgrade at Scale with Fleet Maintenance UI

## Introduction
In this workshop, you will experience the benefits of using the Oracle Enterprise Manager Fleet User Interface to automate the upgrade of multiple Oracle Databases in one flow.

*Estimated Time:* 75 minutes

Watch the video below for a quick walk through of the lab.
[](youtube:SbsS_nNiXHo)

### About the Database Fleet Maintenance UI capability in Oracle Enterprise Manager

Database Fleet Maintenance is an end-to-end automated solution for patching and upgrade of Oracle Databases. Fleet Maintenance enables DBAs to automate patching of a wide range of Oracle Database configurations including Oracle RAC environments with Data Guard Standby.

Starting with Enterprise Manager 13.5 RU1, EM offers a new interface to ease automated patching, update, and upgrade of your database fleet.

Benefits of using the EM Fleet Maintenance capability include:
- Minimizing downtime with use of Out of Place patching
- Enterprise scalability using the Enterprise Manger Deployment Procedures Framework
- A single pane of glass for monitoring and managing the entire patching and upgrade operations
- Ability to schedule/retry/suspend/resume operations.
- Patch Oracle Databases across different infrastructure including engineered systems like Oracle Exadata

  ![](images/em-fleet-maintenance-overview-1.png " ")


### Objectives

In this lab you will perform the following steps:

| Step No. | Feature                                                   | Approx. Time | Details                                                                                                              | Value Proposition |
|----------------------|-----------------------------------------------------------|-------------|----------------------------------------------------------------------------------------------------------------------|-------------------|
| 1                    | Detect Configuration Pollution                            | 10 minutes  | Analyze the database estate using Software Standardization.                                                          |                   |
| 2                    | Oracle Database Upgrade with Fleet Maintenance | 1 hr 5 min   | Upgrade your Oracle Database Software at scale with minimal downtime using Oracle Enterprise Manager 13c Fleet Maintenance. |                   |

### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Oracle Database 19.10 as Oracle Management Repository. Workshop activities included in this lab will be executed both locally on the instance using Enterprise Manager Command Line Interface (EMCLI) or Rest APIs, and the Enterprise Manager console (browser)

## Task 1: Performed in Advance

To save time, the following steps were already completed.

1. An Oracle home was created and pre-patched with an Oracle Database 18.10 release that will be used  to create the gold image [/u01/app/oracle/product/18/db\_home\_src, Orasidb18c\_home1\_2020\_05\_13\_04\_10\_9\_emcc.marketplace.com\_3192]

2. An Oracle home was created and pre-patched with an Oracle Database 19.7 release that will be used to create the gold image [/u01/app/oracle/product/19/db\_home\_src, Orasidb19c\_home1\_2020\_05\_13\_04\_24\_10\_emcc.marketplace.com\_2953]

3. Created of the first version of “Tier\#1” Gold Image

4. Subscription of *finance.subnet.vcn.oraclevcn.com* database to above image

5. Patching of *finance.subnet.vcn.oraclevcn.com* database from 18.8 to 18.10 using Fleet Maintenance

We recommend that you read through each of the steps, review the *emcli* command, its verbs and deployment procedures to get an understanding of what it takes to do it from scratch. For a full end-to-end hands-on execution of “patching” lab, we highly recommend the *Automated Database Patching at Scale with Fleet Maintenance* Lab.

To ensure smooth execution of the use cases, we have pre-hosted the scripts to be used later at */home/oracle/fleet*

## Task 2: Detect Configuration Pollution with Software Standardization Advisor

This exercise enables us to analyze the database estate using Software Standardization.

Software Standardization Advisor enables administrators to understand various database configurations prevailing in their environment. Each deployment with a unique platform, release and patch level is identified as a distinct configuration. This provides the administrators a view of the configuration pollution in their estate. It also analyzes and provides a recommendation to standardize the environment and reduce the number of configurations required for managing the database estate.

  ![](images/em-fleet-maintenance-overview-2.png " ")

1.  On the browser page when the Enterprise Manager Cloud Control 13c login can be seen, copy and paste or type in these username and password credentials into the fields.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![](images/upgrade.png " ")

2.  After successful login, in the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***.

    ![](images/038585c9308635261ae7e4aa956525af.png " ")

3.  On the Databases targets page, click on the ***Administration*** tab, drop down the menu, and select Software ***Standardization Advisor***

    ![](images/software-std-advisor.jpg " ")

4.  Software Standardization Advisor shows two graphs depicting current configuration and recommended configuration.

    ![](images/em-pollution-detection-1.png " ")

    Graphs may look different from the ones represented in the workbook.
    A Software Configuration is identified by the database release, platform, and the patches installed on the target.


    In the analysis performed by the Software Configuration Advisor, it has identified that there are 5 unique software configurations in the environment (pie chart labeled “Current Unique Software Configurations”). The recommendation displayed is for only 2 Software Configurations ( pie chart labeled “Recommended Software Configurations”).

    Next, we will review the report generated.

5.  On the same page, click on **Generate Report**.

6.  On the same page, click on **Current Configurations** to open the Excel report.

    ![](images/em-pollution-detection-2.png " ")

    When you download the report, should a warning on XLS format and file extension mismatch pop up (like below). Simply click on “Yes” to ignore the warning and open the file.

    ![](images/d9ea997d07c30f80083e097f6b578200.png " ")

    From the report, you will see the current environment has five different Oracle home software versions.

    ![](images/84e0ac92b29e45e91b9d17a8e0b3a2da.jpg " ")

7.  Next, click on **Recommended Configurations** to open the Excel Report.

    ![](images/em-pollution-detection-3.png " ")

    The report recommends a reduction of the 5 configurations and standardizing the database estate to 2 configurations (18c and 19c). This means all Oracle homes for Release 18c should uptake the standard 18c configuration and the 19c Oracle homes the standard 19c configuration.

    ![](images/06ff90fdba8aa5abebd066086e33f700.jpg " ")

    The recommendation is based on a union of bugs included in the patches in all Oracle homes and based on the configuration type.

  <!-- This completes Step 1. In this section, you learned how to perform the following:

  - Access the Database Software Standardization Advisor
  - View Configuration summary
  - Generate and download current and recommended configuration reports

  In the next section we will follow these recommendations to perform the following using Enterprise Manager 13c Fleet Maintenance.
  - Patch database “finance.subnet.vcn.oraclevcn.com” from 18.8 to 18.10 [READ-ONLY– This step has already been implemented]
  - Upgrade “finance.subnet.vcn.oraclevcn.com” from 18.10 to 19.7 -->


## Task 3: Oracle Database Upgrade with Fleet Maintenance (Overview)

### **Database Fleet Maintenance**

Enterprise Manager Database Fleet Maintenance is a Gold Image Target subscription-based Out of Place patching solution. Out of Place patching is a method where patching is performed by creating a copy of the Oracle home, applying patches to the copied home, and then switching services to the copied home.
A gold image is the end of state software definition that contains information about the base software version plus the additional patches. Targets, to be upgraded, subscribe to a relevant Gold Image. Target subscription persists through the lifecycle of the Target or Gold Image unless modified by an administrator.


   ![](images/DB_Fleet_Upgrade.png " ")

### **Upgrading with Fleet Maintenance**

We will go through steps for upgrading database target ***finance.subnet.vcn.oraclevcn.com***, a Single Instance Database currently at 18.10.0.0.0 version that was previously patched from 18.8.0.0.0 using Fleet Maintenance. The goal is to upgrade this target to 19.7.0.0.0.

1. Return to the browser page with the Oracle Enterprise Manager Console (log back in if needed) and from the EM home page, select the ***Targets*** drop-down menu and select ***Databases*** to review the status and version of database targets.

    ![](images/ec0b6926d4f65b52a771483ace24055c.png " ")

    ![](images/05ab9d53e622fe6b226647d67750c1dd.jpg " ")

    You will see the *finance.subnet.vcn.oraclevcn.com* database. If the target status is ‘DOWN’, then start the target (using */home/oracle/start\_db\_finance.sh*).

## Task 4: Review Pre-Completed Patching Tasks

Just for your reference, specific tasks related to patching on the target database to be upgraded have already been performed using Fleet Maintenance. These tasks are fully covered by the  *Automated Database Patching at Scale with Fleet Maintenance* Lab and are listed here for your information only

### **Create Gold Image** [READ-ONLY– This step has already been implemented]

1. Now look over the reference home setup *[Which has already been implemented]*

  Gold Image represents a software end state. An Enterprise Manager Software Library Gold Image is a software archive created from a patched oracle home uploaded to EM Software Library. Steps in this section are already implemented and are available here for review.

  To create a Gold Image of the ‘recommended patch configuration’, you manually create an Oracle home as a pre-requisite step.

  The goal is to upgrade Oracle Database target from 18.10 to 19.7, a reference Oracle home fully patched to 18.10 *[Orasidb18c\_home1\_2020\_05\_13\_04\_10\_9\_emcc.marketplace.com\_3192, /u01/app/oracle/product/18/db\_home\_src]* was created and used to create the initial version of the Gold Image as further described in the next steps.

  This reference Oracle home is discovered in Enterprise Manager as shown below and will be used for Gold Image Creation.

2. From the Enterprise Manager menu bar, navigate to the ***Targets*** drop-down menu and then select ***All Targets.***

   Then on the All Targets page, in the upper left search field, type or copy “*Orasidb18c\_home1\_2020\_05\_13\_04\_10\_9\_emcc.marketplace.com\_3192*” in the “Search Target Name” box.

    ```
    <copy>Orasidb18c_home1_2020_05_13_04_10_9_emcc.marketplace.com_3192</copy>
    ```

    ![](images/ea2416958193764cc47426f0ad8a0a67.jpg " ")

3. Review “Create New Gold Image” from the terminal on your remote desktop using the following emcli command

    ```
    <copy>cd ~/fleet
    cat create_image_Tier1_sidb_x64.sh</copy>
    ```

    ![](images/e4a3896e00184146230d4d974e64a528.png " ")

4. List Available Gold Images. Execute the following commands from the terminal to see the list of Gold Images available for deployment, locate ‘Tier \#1 SI DB Linux64*’* in the emcli command output:

    ```
    <copy>emcli db_software_maintenance -getImages</copy>
    ```

    ![](images/81fa9422f35c2dadac8595ef44a5f772.png " ")

    IMAGE ID retrieved from the output of above command is used in further operations like Target Subscription. After retrieving a list of the available images, one can view a list of versions available for a specific image with the following command:

    ```
    <copy>emcli db_software_maintenance -getVersions -image_id=A5F3D8523BDF635BE0531A00000AA55B</copy>
    ```

    ![](images/8c48a86f30874b71459424dc8f69e05f.png " ")

    When a Gold Image is created for the first time, its first version is created as per the input and marked as current. Whenever we run a DEPLOY operation for a target, Gold Image version marked as CURRENT is used to deploy the new Oracle home.

5. Verify if Gold Image is Applicable.
This step verifies if the image can be used to patch a specified database target. This is done by comparing the bug fixes available in the current Oracle home of the database target and the image. In effect this check is run to identify patch conflicts.

    - Review and execute below emcli command:  
    ```
    <copy>emcli db_software_maintenance -checkApplicability -image_id="A5F3D8523BDF635BE0531A00000AA55B" -target_list=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database</copy>
    ```

    ![](images/a7ef76d93e9ee75da1a6a16a7f7620d4.png " ")

    This command can show one of the following results:

    - **Applicable**: The image and database target contain the same set of bug fixes. The image can be applied on the specified target.
    - **Applicable and Image has more bug fixes**: The image contains more bug fixes than those applied on the database. The list of extra bugs is displayed. The image can be applied on the specified target.
    - **Not Applicable**: The database contains more bug fixes than those included in the image. The list of missing bugs is displayed. The administrator has to create a new version of the image that includes the missing bugs before the database can uptake the same.

### **Subscribe Database** - [JUST FOR REFERENCE – This step has already been implemented]

6.  Review emcli command:

    ```
    <copy>emcli db_software_maintenance -subscribeTarget -target_name=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id="A5F3D8523BDF635BE0531A00000AA55B"</copy>
    ```

    ![](images/95439c2138aabd69382c9b0489f14c3b.png " ")

    Where:
      - target\_name – Name of the Database target which needs to be patched
      - target\_type – type of target to be patched. This should be oracle\_database in this case
      - image\_id – ID of the Gold Image to which the target should be patched

### **Deploy Image** - [JUST FOR REFERENCE – This step has already been implemented]

7. Review emcli command encapsulated in shell script

    ```
    <copy>cat deploy1810_finance.sh</copy>
    ```

    ![](images/81d4a98e953a1d2ee999a1b718fd825b.png " ")

### **Migrate Listener** - [JUST FOR REFERENCE – This step has already been implemented]

8. Review emcli command encapsulated in shell script

    ```
    <copy>cat migrate_listener_finance_update.sh</copy>
    ```

    ![](images/17322b2523052b40c7d105c51b6a2967.png " ")

### **Update Database** – Patch to 18.10 - [JUST FOR REFERENCE – This step has already been implemented]

9. Review emcli command encapsulated in shell script

    ```
    <copy>cat update_finance.sh</copy>
    ```

    ![](images/ed90e634e7779548a6f7aebecec5e189.png " ")

## Task 5: Create Gold Image

In this section, we will create Gold Image *Tier1-19 SIDB Linux-x64*

1. Review Reference home Setup

    Just as it was done for the first version of this image, a reference 19.7 Oracle home is needed to create a new version of the image and was setup in advance. [*/u01/app/oracle/product/19/db\_home\_src*]. This reference Oracle home is discovered in Enterprise Manager as shown below and will be used to create and new version of the Gold Image.

2. Navigate to “***Targets >> All Targets***” and type in “*Orasidb19c\_home1\_2020\_05\_13\_04\_24\_10\_emcc.marketplace.com\_2953*” in the “*Search Target Name*” box.

    ![](images/a3ba55228f1e4a239c81bd01ed86c299.png " ")

3. Review and execute the following command to create new Image version 19.7 to "*Tier1 SIDB 19c Linux-x64*"

    ```
    <copy>emcli db_software_maintenance -createSoftwareImage -input_file="data:/home/oracle/fleet/sidb19c_tier1_ui.inp"</copy>
    ```

    **OR**  
    ```
    <copy>sh create_image_version197_tier1_sidb_x64.sh</copy>
    ```

    ![](images/create_image_197.png " ")

4. Navigate to ***Enterprise >> Provisioning and Patching >> Procedure Activity*** to Review Execution Details of this operation via Enterprise Manager Console. Click on ‘CreateGoldImage\*’ run

    ![](images/197_procedure_activity.png " ")

5. Review the Procedure Activity steps performed.

    ![](images/dp_197.png " ")


## Task 6: Subscribe Database

1. Before we deploy a new Oracle home, we need to ensure that we unsubscribe finance database from previous associated image. This step is required for UI as we can not have two different versions of Oracle home (in this case 18c and 19c) in the same image id.

    Review and execute the following command to unsubscribe finance database from ***Tier #1 SI DB Linux64*** image. If finance database is not subscribed to any image, then we can move to next step, where we will subscribe finance database to 19.7 Gold Image.

    ```
    <copy>emcli db_software_maintenance -getTargetSubscriptions -target_name=finance.subnet.vcn.oraclevcn.com  -target_type=oracle_database</copy>
    ```

    ![](images/unsubscribe_finance.png "unsubscribe finance db")

    If the image id is same as the one highlighted above, you may use the below command
    ```
    <copy>emcli db_software_maintenance -unsubscribeTarget -target_name=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id="A5F3D8523BDF635BE0531A00000AA55B"</copy>
    ```
    else make changes in the below command and execute it.

    ```
    <copy>emcli db_software_maintenance -unsubscribeTarget -target_name=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id="{Insert IMAGE ID from above output}"</copy>
    ```

    Review and execute the following command to subscribe finance database to 19.7 image which we had created in step 3 of previous task.   

    ```
    <copy>emcli db_software_maintenance -getImages</copy>
    ```

    ![](images/finance_subscribe_197.png "subscribe finance db to new image")


    If the image id is same as the one highlighted above, you may use the below command

    ```
    <copy>emcli db_software_maintenance -subscribeTarget -target_name=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id="D5807C29FD2A7F92E0538D00000A9A64"</copy>
    ```

    else make changes in the below command and execute it.
    ```
    <copy>emcli db_software_maintenance -subscribeTarget -target_name=finance.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id="{Insert IMAGE ID of 19c from above output}"</copy>
    ```

## Task 7: Deploy Image

1. As we have completed the pre-requisite task (associating database to image in Task 6), we can now upgrade the finance database. From the Enterprise Manager menu bar, navigate to the ***Targets*** drop-down menu and then ***Databases***

    ![](images/navigation.png "navigation")

    and, then from ***Administration*** drop-down menu select ***Fleet Maintenance***

    ![](images/admin-fm.png "navigation admin-fm")

    In order to complete the deployment of new image, we need to modify named credential root and set its scope to global. This can be achieved by running the below command in terminal.

    ```
   <copy>emcli modify_named_credential -cred_name=root -cred_scope=global</copy>
    ```

   ![](images/modify-root-credential.png "update root credential")

2. In this page, we will select relevant ***Image Name***, ***Target Type*** and ***Operation***.

    ![](images/options.png "choose options")

    Where:
    -  Image = Desired version of Oracle home, which our target database should run after successful completion of operation. In this example, we will select ***Tier1 SIDB 19c Linux-x64***.
    -  Target Type = Desired target type, which can be Grid, RAC or SIDB. In this example, we will select ***Database Instance***.
    -  Operation = Name of the operation, which can be update (patch) or upgrade. In this example, we will select ***Upgrade***.
    -  Type to filter = Selection criteria to highlight only those targets which qualify the selection, such as database naming.

3. In this page, we will provide ***new Oracle home location***, select which ***tasks*** can be performed, select ***credential model***, provide ***log file location*** under options and select any   ***custom scripts*** to run as part of the operation.

    ![](images/input-values.png "enter values for operation")

    We can enter following values
    Under Maintenance tasks
        Destination Oracle Home as
        ```
        <copy>/u01/app/oracle/product/19/db_home1</copy>
        ```
    Check both Migrate Listener and Update Database options
    Under Credentials (We have already created these credentials in Enterprise Manager for this workshop. Please choose Named for all the below three options and from the dropdown menu, you can opt for values as suggested below)    
        Normal Host Credentials as ***ORACLE***
        Privileged Host Credentials as ***ROOT***
        SYSDBA Database Credentials as ***SYS_SALES***

    Deployment of new Oracle home does not impact existing Oracle home and hence it is scheduled to run immediately. We can schedule it to run at a different time by selecting later in start schedule and providing new time to run this operation.

    Once deployment of new Oracle home is complete, we can change the schedule of the Deployment Procedure for migrate listener and update database to execute these tasks immediately.

4. We can validate our entries (new Oracle home, log file location, credentials) of previous page and validate the desired operation. Validation acts as a precheck before we submit the main operation.  There are two validation modes Quick and Full. We can select either of these. Full validation mode submits a deployment procedure. In this case choose Quick validation.

    ![](images/validation-modes.png "available validation modes")

5. Review the validation result.

    ![](images/result-validation.png "result validation")

    In case of any error, we can fix it and choose revalidate.

6. ***Submit*** the operation. Here, we can see that we have opted to deploy, migrate and update the database at once. These tasks will be performed independently based on their schedule.

    ![](images/final-review.png "final-review")    

    We need to provide a name to the task, which will help us to view these tasks under Procedure Activity Page. Lets enter

    ```
    <copy>finance_19c_upgrade</copy>
    ```

    ![](images/op-name.png "operation name")

    Click on submit.
    ![](images/submit.png "submit operation")

Clicking on Monitor Progress will take us to Procedure Activity Page. Alternate navigation to review the submitted deployment procedures is ***Enterprise >> Provisioning and Patching >> Procedure Activity***

7. Review the Deployment Procedures (DP).

Select the DP related to Deploy and click on it.
    ![](images/all-dp.png "all-dp-submitted")

It will show details of the activity performed by the DP.
    ![](images/dp-deploy.png "dp-deploy")

Here, we see that the DP has successfully installed new Oracle home.

## Task 8: Migrate Listener to New Upgraded home

1. In task 7 (above), we submitted a migration of the listener. If it needs to be submitted separately, then you need to uncheck migrate listener task (review step 3 of task 6). We see that this task has a scheduled state. In the interest of time and to complete this workshop, we can change it to run immediately. To do so, navigate to ***Enterprise >> Provisioning and Patching >> Procedure Activity*** and select migrate DP.

    Click on reschedule.
    ![](images/migrate-dp.png "migrate-dp")

    In the new page, select immediately for start and reschedule.
    ![](images/51-reschedule.png "reschdule dp")

    We can now see that migrate operation is running.
    ![](images/51-Running.png "dp running post reschedule")
    We can select it and see the various steps performed by it.

    ![](images/dp-migrate-details.png "dp-migrate-details")
    We can now see that the migration operation completed successfully.

    ![](images/dp-migrate-completed.png "dp-migrate-completed")

    Lets validate the version of ***finance*** database. In the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***. We can see the updated version of ***finance*** database.
    ![](images/post_upgrade_db_version.png " ")

## Task 9: Update Database – Upgrade to 19.7

After the deploy operation and migrate listener task have completed successfully, we are ready to run the final UPDATE operation which will upgrade the finance database by switching it to the newly deployed home.

1.  Similar to migrate listener, we had submitted Update Database in task 7. If this needs to be submitted separately, then we had to uncheck update database task ( review step 3 of task 7). In the interest of time and to complete this Live Lab workshop, we can change its schedule to run immediately. Navigate to  ***Enterprise >> Provisioning and Patching >> Procedure Activity*** and select update.

    Click on reschedule.

    ![](images/update.png "update dp")

    In the new page, select immediately for start and reschedule.

    ![](images/53-reschedule.png "update dp reschedule")
    We can now see that update operation is running.
    ![](images/53-running.png "update dp running")
    We can select it and see the various steps performed by it.

    ![](images/update-dp-steps.png "update-dp-steps")

    Update operation has completed successfully.

    ![](images/update-dp-completed.png "update-dp-completed ")

    Lets validate the version of ***finance*** database. In the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***. We can see the updated version of ***finance*** database.
    ![](images/post_upgrade_db_version.png "db version post operation")
## Task 10: Cleanup Old homes

1. Review and execute the following command as a dry-run to report on cleanup impact for *finance.subnet.vcn.oraclevcn.com*  

    ```
    <copy>emcli db_software_maintenance -performOperation -name="Cleanup old oracle homes" -purpose=CLEANUP_SOFTWARE -target_type=oracle_database -normal_credential=ORACLE:SYSMAN -privilege_credential=ROOT:SYSMAN -target_list=finance.subnet.vcn.oraclevcn.com -workDir=/tmp -reportOnly=true</copy>
    ```

    **OR**

    ```
    <copy>sh cleanup_finance_report.sh</copy>
    ```

    ![](images/228ae0280ff2878bb4902cb263529bb9.png " ")

2. Review and execute the following command to cleanup *finance.subnet.vcn.oraclevcn.com*  

    ```
    <copy>emcli db_software_maintenance -performOperation -name="Cleanup old oracle homes" -purpose=CLEANUP_SOFTWARE -target_type=oracle_database -normal_credential=ORACLE:SYSMAN -privilege_credential=ROOT:SYSMAN -target_list=finance.subnet.vcn.oraclevcn.com -workDir=/tmp</copy>
    ```

    **OR**

    ```
    <copy>cd ~/fleet
    sh cleanup_finance.sh</copy>
    ```

    ![](images/3f41abadf32e4b8d4900467985a093ef.png " ")

3. Navigate to the Procedure Activity Page and monitor the progress of this operation with ‘CLEANUP\_SOFTWARE\_...’ deployment procedure instance.

    ![](images/94954554c777d24280599507c28a75d3.png " ")

4. Review the Procedure Activity steps performed

    ![](images/777053c04e0851859856c8d32b9d94c2.png " ")

5. Verify to confirm that the two old Oracle homes reported have been removed

    ```
    <copy>ls -l /u01/app/18c/sales188 /u01/app/oracle/product/18/db_home1</copy>
    ```

    ![](images/58ba7d42eb61331e3d0bec6588086b47.png " ")

6. As part of the cleanup operation, *LISTENER\_1525* which support *“finance.subnet.oraclevcn.com”* is shutdown. Set your environment by passing *“finance”* to *“oraenv”* when prompted.

    ```
    <copy>. oraenv</copy>
    ```
7. start listener *LISTENER\_1525* back up

    ```
    <copy>lsnrctl start LISTENER_1525</copy>
    ```

    ![](images/b3d1a555c6eeb3d0d899da4291a6441c.png " ")

8. Force Listener registration and confirm that it is now servicing “*finance.subnet.vcn.oraclevcn.com*”

    ```
    <copy>sqlplus '/as sysdba'<<EOF
    alter system register;
    EOF
    </copy>
    ```
9. Check status of LISTENER\_1525

    ```
    <copy>lsnrctl status LISTENER_1525</copy>
    ```

    ![](images/7626fd3264e4a514fde576ecd9369456.png " ")


That completes the Automated Database Upgrade at Scale with Fleet Maintenance UI workshop.

<!-- In this lab, you learned how to perform the following:
- Create Oracle Database Software Gold Image
- Subscribe Database to Gold Image
- Deploy Gold Image to Database Host
- Migrate Oracle Database Listener from old Oracle home to newly Deployed Oracle home
- Update (Patch) Database from 18.8 to 18.10
- Add new Version to an Existing Oracle Database Software Gold Image
- Deploy new Gold Image Version to Database Host
- Update (Upgrade) Database from 18.10 to 19.7
- Clean up old Oracle homes -->

You may now proceed to the next lab.

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Oracle Enterprise Manager Fleet Maintenance](https://www.oracle.com/manageability/enterprise-manager/technologies/fleet-maintenance.html)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/lifecycle.html)
  - [Database Cloud Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/cloud.html)

## Acknowledgements
  - **Authors**
    - Shefali Bhargava, Oracle Enterprise Manager Product Management
    - Rene Fontcha, LiveLabs Platform Lead, NA Technology
    - Romit Acharya, Oracle Enterprise Manager Product Management
  - **Contributors** -
  - **Last Updated By/Date** -Romit Acharya, Oracle Enterprise Manager Product Management, January 2022
