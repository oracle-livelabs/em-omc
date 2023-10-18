# Automated Database Update(Patching) at Scale with Fleet Maintenance UI

## Introduction
In this workshop, you will experience the benefits of using the Oracle Enterprise Manager Fleet Maintenance User Interface to automate the update(patching) of multiple Oracle Databases in one flow.

*Estimated Time*: 60 minutes

You can watch this video below for a quick walk-through of this lab.
[Video Walk-through](videohub:1_vyyju031)

### About the Database Fleet Maintenance UI capability in Oracle Enterprise Manager

Database Fleet Maintenance is an end-to-end automated solution for update(patching) and upgrade of Oracle Databases. Fleet Maintenance enables DBAs to automate update(patching) of a wide range of Oracle Database configurations including Oracle RAC environments with Data Guard Standby.

Starting with Enterprise Manager 13.5 RU1, Enterprise Manager offers a new interface to ease automated update(patching), and upgrade of your database fleet.

Benefits of using the EM Fleet Maintenance capability include:
- Minimizing downtime with use of Out of Place patching
- Enterprise scalability using the Enterprise Manger Deployment Procedures Framework
- A single pane of glass for monitoring and managing the entire update(patching) and upgrade operations
- Ability to schedule/retry/suspend/resume operations
- Patch Oracle Databases across different infrastructure including engineered systems like Oracle ExaCC

![](images/new-em-fleet-maintenance-overview.png " ")

#### Video Preview
Watch a preview of database patching using Oracle Enterprise Manager Fleet Maintenance:

[](youtube:JlspEvqebHE)

*Note: Interfaces in this video may look different from the interfaces you will see. For updated information, please see steps below.*


### Objectives

In this lab you will perform the following steps:
| Step No. | Feature                                                    | Approx. Time | Details                                                                                                                                                                    | Value Proposition |
|----------------------|------------------------------------------------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| 1                    | Detect Configuration Pollution                             | 10 minutes  | Analyze the database estate using Software Standardization.                                                                                                                | Provides recommendation to run minimum version of databases to ease your maintenance activities.                  |
| 2                    | Oracle Database Update(Patching) with Fleet Maintenance | 50  minutes  | Update(Patch) a Database target using a Gold Image. As part of patching the Container Database, all Oracle Pluggable Databases in that Container Database will automatically get patched. | Demonstrate key capabilities and features of Fleet Maintenance to update(patch) Oracle Database.                  |


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository. Workshop activities included in this lab will be executed both locally on the instance using Enterprise Manager Command Line Interface (EMCLI) or Rest APIs, and the Enterprise Manager console (browser)

## Task 1: Performed in Advance

To save time, the following steps were already completed.

1. Gold Image of Oracle Home was exported and imported in the setup. Imported file was then used to create Gold Images, which will be used in the lab.

To ensure smooth execution of the use cases, we have pre-hosted the scripts to be used later at */home/oracle/fleet*

## Task 2: Detect Configuration Pollution with Software Standardization Advisor

In this lab activity, you will analyze the database estate to identify any configuration drift (pollution) using the Software Standardization Advisor.

Software Standardization Advisor enables administrators to understand various database configurations prevailing in their environment. Each deployment with a unique platform, release and patch level is identified as a distinct configuration. This provides the administrators a view of the configuration pollution in their estate. It also analyzes and provides a recommendation to standardize the environment and reduce the number of configurations required for managing the database estate.
<!--
  ![](images/em-fleet-maintenance-overview-2.png " ")
-->
  ![](images/new-em-fleet-maintenance-overview-2.png " ")

1. On the browser page when the Enterprise Manager Cloud Control 13c login can be seen, copy and paste or type in these username and password credentials into the fields.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![](images/patch.png " ")

2.  After successful login, in the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***.

    ![](images/038585c9308635261ae7e4aa956525af.png " ")

3.  On the Databases targets page, click on the ***Administration*** tab, drop down the menu, and select Software ***Standardization Advisor***

    ![](images/new-software-std-advisor.png "additional items in drop down ")

4.  Software Standardization Advisor shows two graphs depicting current configuration and recommended configuration.

    ![](images/generate-report.png "pollution detection report generation ")

    Graphs may look different from the ones represented in the workbook.
    A Software Configuration is identified by the database release, platform, and the patches installed on the target.

    In the analysis performed by the Software Configuration Advisor, it has identified that there are 5 unique software configurations in the environment (pie chart labeled “Current Unique Software Configurations”). The recommendation displayed is for only 2 Software Configurations ( pie chart labeled “Recommended Software Configurations”).

    Next, we will review the report generated.


5.  On the same page, click on **Generate Report**. Select yes when it prompts to generate the report.
    ![](images/generate-report-confirmation.png "pollution detection report generation ")


6.  On the same page, click on **Current Configurations** to open the Excel report.

    ![](images/current-config.png " ")

    When you download the report, a warning on XLS format and file extension mismatch pops up (like below). Simply click on “Yes” to ignore the warning and open the file.

    ![](images/d9ea997d07c30f80083e097f6b578200.png " ")

    Alternately, you might see a pop up for import options, while opening the file. Select OK and you should be able to view the contents of the file.

    ![](images/open-office-msg.png "pop-up message")

    From the report, you will see the current environment has six different Oracle home software versions.

    ![](images/config-report.png "current-report")

    Incase you are unable to review the report in Livelab VNC, then open the environment url directly on your laptop browser and run the report again. Example: If you see instance IP address as 129.146.247.99, then the url to open on your browser will be https://129.146.247.99:7803/em .

    ![](images/workshop-instance.png " ")

    Please accept any warning message that your browser may show to continue to login to Enterprise Manager.

7.  Next, click on **Recommended Configurations** to open the Excel Report.

    ![](images/recommend-config.png "recommended changes ")

    <!-- The report recommends a reduction of the 5 configurations and standardizing the database estate to 2 configurations (18c and 19c). This means all Oracle homes for Release 18c should uptake the standard 18c configuration and the 19c Oracle homes the standard 19c configuration. -->

    The reports recommendation is to consolidate the configuration drift (pollution) from the current six database to two (18c and 19c). This recommendation would reduce the number of configurations and standardize the environment for easier management.

    ![](images/recommend-report.png "recommendations ")

    The recommendation is based on a union of bugs included in the patches in all Oracle homes and based on the configuration type.

  <!-- This completes Step 1. In this section, you learned how to perform the following:

    - Access the Database Software Standardization Advisor
    - View Configuration summary
    - Generate and download current and recommended configuration reports

  In the next section we will follow these recommendations to perform the following using Enterprise Manager 13c Fleet Maintenance.

    - Patch database “hr.subnet.vcn.oraclevcn.com” from 18.3 to 18.10 -->

## Task 3: Database Server update(patching) with Fleet maintenance (Overview)

### **Database Fleet Maintenance**

Enterprise Manager Database Fleet Maintenance is a Gold Image Target subscription-based Out of Place patching solution. Out of Place patching is a method where patching is performed by creating a copy of the Oracle home, applying patches to the copied home, and then switching services to the copied home.

A gold image is the end of state software definition that contains information about the base software version plus the additional patches. Targets, to be patched, subscribe to a relevant Gold Image. Target subscription persists through the lifecycle of the Target or Gold Image unless modified by an administrator.

  <!--![](images/DB_Fleet_Patching.png " ")  -->
  ![](images/new-db-fleet-patching.png "new interface")

### **Patching with Fleet Maintenance**

We will go through steps for update(patching) database target ***sales.subnet.vcn.oraclevcn.com***, a Container Database that is currently at 19.17.0.0.0 version. The goal is to patch this target to 19.18.0.0.0. As part of the update(patching) exercise this Container Database and all Pluggable Databases in that Container Database will automatically get patched.

1.  Return to the browser page with the Oracle Enterprise Manager Console (log back in if needed) and from the EM home page, select the ***Targets*** drop-down menu and select ***Databases*** to review the status and version of database targets.

    ![](images/sales-db-status.png "sales-db-version")

## Task 4: Create Gold Image [Step Already Performed, Read-Only Step]

1. For this lab exercise, we have already created the gold image. To create a gold image, we exported the gold image from another environment and imported it in the setup. You can find further details on export-import of gold images in the Fleet Documentation.

    Gold Image represents a software end state. An Enterprise Manager Software Library Gold Image is a software archive created from a patched oracle home uploaded to EM Software Library.

    To review the Gold Images, we will check the deployment procedure logs.

2. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then select ***Provisioning and Patching***. Then select ***Procedure Activity***.

    ![](images/dp-navigation-gi.png "DP Navigation")

    Lets do a filter using keyword ***Import***. This will result in only DPs which were executed to import the Gold Image. Click on the highlighted DP name.

    ![](images/click-dp-name.png "GI import DPs")

    Here, you will see we have highlighted details of the parameters which were passed during the import process. For more details, please refer to the documentation.
    ![](images/gi-dp-creation-success.png "DP Details")

3. From the terminal on your remote desktop, review the Gold Images using the following emcli command

    If you encounter session timeout error, copy paste the below command to re-login as sysman and re-establish the session.

        ```
        <copy>emcli login -u=sysman -p=welcome1</copy>
        ```

    ![](images/session-timeout.png "session timeout error ")

    If you encounter session timeout error elsewhere in the lab, you can copy and paste the above command in the terminal and continue.

    Default window size of terminal will render output in multiple lines. Its is thus recommended to increase the terminal window size by clicking on maximize option.

    ![](images/window_size.png "Maximize window ")

    Execute the following command to increase the column width.
    ```
    <copy>emctl set property -name oracle.sysman.dbprov.gis.emcli.verbs.tableLength -value 210 -sysman_pwd "welcome1"</copy>
    ```
    ![](images/resize-width.png "resize command")

    Now, we can execute the get images command and it will return output in single line. Execute the following commands in the terminal to see the list of Gold Images available for deployment, locate ‘19cDB-Linux-x64-Apps’ in the emcli command output:

    ```
    <copy>emcli db_software_maintenance -getImages</copy>
    ```

    ![](images/gi1-imageid.png "GI1 image details ")

    IMAGE ID retrieved from the output of above command is used in further operations like Target Subscription.

    After retrieving a list of the available images, one can view a list of versions available for a specific image with the following command:

    If the image id is same as the one highlighted above, you may use the below command. First, we will again resize the column width.
    ```
    <copy>emctl set property -name oracle.sysman.dbprov.gis.emcli.verbs.tableLength -value 240 -sysman_pwd "welcome1"</copy>
    ```
    ```
    <copy>emcli db_software_maintenance -getVersions -image_id=FC6A1AA82CB23A62E0532600000AB0CE</copy>
    ```   

    else make changes in the below command and execute it.

    ```
    <copy>emcli db_software_maintenance -getVersions -image_id={Insert IMAGE ID from List available gold images}</copy>
    ```   

    This command lists Gold Image versions with their VERSION ID and STATUS.

    ![](images/gi1-versionid.png "GI1 version id ")

    When a Gold Image is created for the first time, its first version is created as per the input and marked as current. Whenever we run a DEPLOY operation for a target, Gold Image version marked as CURRENT is used to deploy the new Oracle home.

    In our Lab, we want to update ***sales.subnet.vcn.oraclevcn.com*** to 19.18 version. From the above output we can see that 19.18 version is at Current status, which will be used to deploy the new Oracle Home.

## Task 5: Subscribe Database

1.  Below illustration describes the flow of subscribing Targets to the Selected Gold Image

    ![](images/subscribe-flow.png "Subscribe flow")

2. Execute below command to subscribe the target sales.subnet.vcn.oraclevcn.com to Gold Image

    If the image id is same as the one highlighted above (Task 4, step 3), you may use the below command:
    ```
    <copy>emcli db_software_maintenance -subscribeTarget -target_name=sales.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id=FC6A1AA82CB23A62E0532600000AB0CE</copy>
    ```

    else

    ```
    <copy>emcli db_software_maintenance -subscribeTarget -target_name=sales.subnet.vcn.oraclevcn.com -target_type=oracle_database -image_id={Insert IMAGE ID from List available gold images}</copy>
    ```

    Where:
   -  target\_name – Name of the Database target which needs to be patched
   -  target\_type – type of target to be patched. This should be oracle\_database in this case
   -  image\_id – ID of the Gold Image to which the target should be patched


   We noticed that the subscribe operation failed. Error message suggested that the sales database is already subscribed to another image. A point to remember - One database can be subscribed to only one gold image, but a gold image can have many databases subscribed to it.

   Execute the below command to check the gold image to which sales database is subscribed.

   ```
   <copy>emcli db_software_maintenance -getTargetSubscriptions -target_name=sales.subnet.vcn.oraclevcn.com -target_type=oracle_database</copy>
   ```   

   ![](images/sales-subscription.png "sales subscribe ")

   We see that sales database is already subscribed to the desired gold image. Hence, we can go to next step.

## Task 6: Deploy Image

1. In order to complete the deployment of new image, we need to modify named credential root and set its scope to global. This can be achieved by running the below command in terminal.

    ```
    <copy>emcli modify_named_credential -cred_name=root -cred_scope=global</copy>
    ```

    ![](images/modify-root-credential.png "emcli to modify root credentials")

    From the Enterprise Manager menu bar, navigate to the ***Targets*** drop-down menu and then select ***Databases***

    ![](images/ec0b6926d4f65b52a771483ace24055c.png "navigation")

    and, then from ***Administration*** drop-down menu select ***Fleet Maintenance***

    ![](images/admin-fm.png "navigation")


2. In this page, we will select relevant ***Image Name***, ***Target Type*** and ***Operation***.

    ![](images/selection.png "selection")

    Where:
    -  Image = Desired version of Oracle home, which our target database should run after successful completion of operation. In this example, we will select ***19cDB-Linux-x64-Apps***.
    -  Target Type = Desired target type, which can be Grid, RAC or SIDB. In this example, we will select ***Database Instance***.
    -  Operation = Name of the operation, which can be update (patch) or upgrade. In this example, we will select ***Update***.
    -  Type to filter = Selection criteria to highlight only those targets which qualify the selection, such as database naming.

    Select Next.

3. In this page, we will provide ***new Oracle home location***, select which ***tasks*** can be performed, select ***credential model***, provide ***log file location*** under options and select any   ***custom scripts*** to run as part of the operation.

    ![](images/sales-patch-screen2.png "input values")

    We can enter following values
    Under Maintenance tasks
        Destination Oracle Home as
        ```
        <copy>/u01/livelabs/db/19c/19.18/sales</copy>
        ```

    Check both Migrate Listener and Update Database options
    Under Credentials (We have already created these credentials in Enterprise Manager for this workshop. Please choose Named for all the below three options and from the dropdown menu, you can opt for values as suggested below)    
    -  Normal Host Credentials as ***ORACLE***
    -  Privileged Host Credentials as ***ROOT***
    -  SYSDBA Database Credentials as ***SYS_SALES***
    -  Under Options section, select ***Yes*** for Skip Cluster Verification Utility Checks.

    Deployment of new Oracle home does not impact existing Oracle home and hence it is scheduled to run immediately. We can schedule it to run at a different time by selecting later in start schedule and providing new time to run this operation.

    Once deployment of new Oracle home is complete, the Deployment Procedures for migrate listener and update database will execute immediately ( if we have selected start as Immediately/Auto ).  

    Select Next.

4. We can validate our entries (new Oracle home, log file location, credentials) provided in previous page and validate the desired operation. Validation acts as a precheck before we submit the main operation. Click on ***Validate*** and a new pop-up screen will appear. There are two validation modes - Quick and Full. We can select either of these. Full validation mode submits a deployment procedure. In this case choose Quick validation mode and click on Validate.

    ![](images/validation-mode.png "quick and full valdiation modes")

5. Review the validation result.

    ![](images/sales-validation-success.png "result of valdiation")

    Incase of any error, we can fix it and choose revalidate. Else, click on close.

6. ***Submit*** the operation. A new pop-up will appear and we need to provide the name to the tasks.
    Lets enter
    ```
    <copy>sales-patching</copy>
    ```

    ![](images/sales-job-name.png "submit operation")    

    Click on submit.
    ![](images/sales-job-monitor.png "monitor")

    Clicking on Monitor Progress will take us to Procedure Activity Page. Alternate navigation to review the submitted deployment procedures is ***Enterprise >> Provisioning and Patching >> Procedure Activity***

7. Review the Deployment Procedures (DP).

   ![](images/sales-deploy.png "review")

   Select DP related to Deploy and click on it. It will show details of the activity performed by the DP.

   ![](images/deploy-complete.png "review dp for layout OH")

   Here, we see that the DP has successfully completed. This DP is responsible for installing new Oracle home at the location that we had specified earlier.

## Task 7: Migrate Listener

1. In task 6 (above), we submitted a task to migrate the listener. If this task needs to be submitted separately, then you need to uncheck migrate listener task (review step 3 of task 6).
    ![](images/uncheck-mig-listener.png " ")

    The image below shows the task is in a running state.

    ![](images/listener.png "DP for migrate listener")

    Select the running task to see the various steps performed.

    ![](images/migrate-complete.png "details of DP")
    We can now see that the migration operation completed successfully.

## Task 8: Update(Patching) Database – Patch 19.17 to 19.18

1. Similar to listener migration, we also submitted operation for Update Database in task 6. If it needs to be submitted separately, then you need to uncheck the update database task (review step 3 of task 6).
    ![](images/uncheck-update-db.png " ")

    The image below shows the task is in a running state.

    ![](images/update-running.png "DP update")

    Select the running task to see the various steps performed.

    ![](images/update-success.png "DP completed")

    Update operation has completed successfully.

    Lets validate the version of ***sales*** database. In the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***. We can see the updated version of ***sales*** database.

   ![](images/sales-post-upg-version.png "new version check")

## Task 9:  Rollback Database – Reversed Patch 19.18 to 19.17

Once the database is updated(patched), we will perform a rollback to Oracle Database 19.17. In a future release capability is being planned to perform rollback of an operation using the UI.

1. Review and execute below command from the terminal to rollback database Target ***sales.subnet.vcn.oraclevcn.com***

    ```
    <copy>curl -i -X POST https://emcc.marketplace.com:7803/em/websvcs/restful/emws/db/fleetmaintenance/performOperation/rollback -H "Content-Type:application/json" -u sysman:welcome1 --data-binary "@/home/oracle/fleet/rollback_sales_payload.json" --insecure</copy>
    ```

    **OR**

    ```
    <copy>cd ~/fleet
    sh rollback_salesdb.sh</copy>
    ```

    ![](images/rollback-sales.png " ")

2. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity*** to review Execution details of this operation via Enterprise Manager Console
    ![](images/e9091a9e1e04a1a988cb61d9171a483d.png " ")

    Monitor the progress of this operation with ‘Fleet\_ROLLBACK\_...’ deployment procedure instance.

    ![](images/rollback-dp.png "rollback")

3. Review the Procedure Activity steps performed         

    ![](images/rollback-success.png "rollback complete")

4. Verify the rolled back target by going to ***Targets >> Databases*** as shown
below.

    ![](images/post-rollback-sales.png "sales-ROLLBACK")

## Task 10:  Cleanup Old homes

1. Clean up Database Sales. In a future release capability is being planned to perform cleanup of an operation using the UI.

   In order to have an old empty home previously used by “***sales.subnet.vcn.oraclevcn.com***” at our disposal to demonstrate a cleanup operation, we will now re-update(re-patch) the database.

2. Review and execute below command to update(patch) database target ***sales.subnet.vcn.oraclevcn.com*** again to 19.18 version

    ```
    <copy>emcli db_software_maintenance -performOperation -name="Update DB" -purpose=UPDATE_DB -target_type=oracle_database -target_list=sales.subnet.vcn.oraclevcn.com -normal_credential=ORACLE:SYSMAN -privilege_credential=ROOT:SYSMAN -database_credential=sales_SYS:SYSMAN</copy>
    ```

    **OR**

    ```
    <copy>sh update_sales.sh</copy>
    ```

    ![](images/post-rollback-sales-update.png " ")

    Where:
    -  Name – Name of the operation. This is a logical name and should be kept unique.
    -  Purpose – There are standard purposes defined which can be performed by Fleet Operations. “UPDATE\_DB” is one of them.


3. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity*** to review Execution details of this operation via Enterprise Manager Console

    ![](images/e9091a9e1e04a1a988cb61d9171a483d.png " ")

Verify that the update has been completed successfully.
    ![](images/fleet-update.png "fleet status")

4. Verify and confirm that the target has been re-patched to Oracle Database 19.18 by going to Targets Databases as shown below.

    ![](images/038585c9308635261ae7e4aa956525af.png " ")

    Review the version of Sales database.
    ![](images/new-sales-status.png "new sales version")

5. Review and execute the following command as a dry-run to report on cleanup impact for *sales.subnet.vcn.oraclevcn.com*  

    ```
    <copy>emcli db_software_maintenance -performOperation -name="Cleanup old oracle homes" -purpose=CLEANUP_SOFTWARE -target_type=oracle_database -normal_credential=ORACLE:SYSMAN -privilege_credential=ROOT:SYSMAN -target_list=sales.subnet.vcn.oraclevcn.com -workDir=/u01/tmp -reportOnly=true</copy>
    ```

    **OR**

    ```
    <copy>sh cleanup_sales_report.sh</copy>
    ```

    ![](images/cleanup-sales-report.png "cleanup report")

6. Review and execute the following command to cleanup *sales.subnet.vcn.oraclevcn.com*   
    ```
    <copy>emcli db_software_maintenance -performOperation -name="Cleanup old oracle homes" -purpose=CLEANUP_SOFTWARE -target_type=oracle_database -normal_credential=ORACLE:SYSMAN -privilege_credential=ROOT:SYSMAN -target_list=sales.subnet.vcn.oraclevcn.com -workDir=/u01/tmp</copy>
    ```

    **OR**

    ```
    <copy>sh cleanup_sales.sh</copy>
    ```

    ![](images/sales-cleanup-submission.png "cleanup action")

7. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity***.
    ![](images/e9091a9e1e04a1a988cb61d9171a483d.png " ")

    Monitor the progress of this operation with ‘CLEANUP\_SOFTWARE\_...’ deployment procedure instance.

    ![](images/cleanup-success.png "cleanup dp")

8. Verify to confirm the old Oracle home has been removed

    ```
    <copy>ls -ltr /u01/app/19c/sales /u01/db/19c/sales</copy>
    ```

    ![](images/cleanup-sales-os-layout.png "OS cleanup")

9.  As part of the cleanup operation, LISTENER\_1523 which support “***sales.subnet.oraclevcn.com***” is shutdown. Set your environment by passing “***sales***” to “***oraenv***” when prompted and start the listener back up.

    ```
    <copy>. oraenv </copy>
    ```

10. Start LISTENER\_1523 back up

      ```
      <copy>lsnrctl start LISTENER_1523</copy>
      ```

    ![](images/sales-listener.png "sales listener start")

11. Force Listener registration and confirm that it is now servicing “***sales.subnet.vcn.oraclevcn.com***”

    ```
    <copy>sqlplus '/as sysdba'<<EOF
    alter system register;
    EOF
    </copy>
    ```

    ![](images/register-sales.png "register listener")

12. Check status of LISTENER\_1523

    ```
    <copy>lsnrctl status LISTENER_1523</copy>
    ```

    ![](images/new-sales-listener-status.png "listener status")

<!-- This completes Step 2. In this section, you learned how to perform the following:
-   Create Oracle Database Software Gold Image
-   Subscribe Database to Gold Image
-   Deploy Gold Image to Database Host
-   Migrate Oracle Database Listener from old Oracle home to newly Deployed Oracle home
-   Update (Patch) Database from 18.3 to 18.10
-   Rollback (Un-patch) Database from 18.10 to 18.3
-   Clean up old Oracle homes -->

That completes the Automated Database Patching at Scale with Fleet Maintenance UI workshop.

You may now proceed to the next lab.

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Oracle Enterprise Manager Fleet Maintenance](https://www.oracle.com/manageability/enterprise-manager/technologies/fleet-maintenance.html)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/lifecycle.html)
  - [Database Cloud Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/cloud.html)

## Acknowledgements
  - **Authors**
    - Romit Acharya, Oracle Enterprise Manager Product Management
    - Anand Prabhu, Oracle Enterprise Manager Product Management
  - **Last Updated By/Date** -Romit Acharya, Oracle Enterprise Manager Product Management, June 2023
