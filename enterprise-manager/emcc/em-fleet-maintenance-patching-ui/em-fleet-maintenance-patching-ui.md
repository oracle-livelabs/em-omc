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

![](images/FM-Overview2024.png "FM-Overview2024")

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

1. Gold Image of Oracle Home was created using Fleet Maintenance Hub.

To ensure smooth execution of the use cases, we have pre-hosted the scripts to be used later at */home/oracle/fleet*. To know more about using this feature, follow the below video link.

[Video Walk-through] (https://www.youtube.com/watch?v=ibEEkTa05iM&t=182s)

## Task 2: Detect Configuration Pollution with Software Standardization Advisor

In this lab activity, you will analyze the database estate to identify any configuration drift (pollution) using the Software Standardization Advisor.

Software Standardization Advisor enables administrators to understand various database configurations prevailing in their environment. Each deployment with a unique platform, release and patch level is identified as a distinct configuration. This provides the administrators a view of the configuration pollution in their estate. It also analyzes and provides a recommendation to standardize the environment and reduce the number of configurations required for managing the database estate.
<!--
  ![](images/em-fleet-maintenance-overview-2.png " ")
-->
  ![](images/new-em-fleet-maintenance-overview-2.png "Fleet Maintenance Overview")

1. On the browser page when the Enterprise Manager Cloud Control 13c login can be seen, copy and paste or type in these username and password credentials into the fields.

    ```
    Username: <copy>emadmin</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![](images/patch.png "vnc home page")

2.  After successful login, in the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***.

    ![](images/Target-Databases-Navig.png "Target-Databases-Navigation")

3.  On the Databases targets page, click on the ***Administration*** tab, drop down the menu, and select ***Software Standardization Advisor***

    ![](images/new-software-std-advisor.png "additional items in drop down ")

4.  Software Standardization Advisor shows two graphs depicting current configuration and recommended configuration.

    ![](images/generate-report.png "pollution detection report generation ")

    Graphs may look different from the ones represented in the workbook.
    A Software Configuration is identified by the database release, platform, and the patches installed on the target.

    In the analysis performed by the Software Configuration Advisor, it has identified that there are 6 unique software configurations in the environment (pie chart labeled “Current Unique Software Configurations”). The recommendation displayed is for only 2 Software Configurations ( pie chart labeled “Recommended Software Configurations”).

    Next, we will review the report generated.


5.  On the same page, click on **Generate Report**. Select yes when it prompts to generate the report.
    ![](images/generate-report-confirmation.png "pollution detection report generation ")


6.  On the same page, click on **Current Configurations** to open the Excel report.

    ![](images/current-config.png " ")

    When you download the report, a warning on XLS format and file extension mismatch pops up (like below). Simply click on “Yes” to ignore the warning and open the file.

    ![](images/Homepage-SSA.png "Homepage-SSA")

    Alternately, you might see a pop up for import options, while opening the file. Select OK and you should be able to view the contents of the file.

    ![](images/open-office-msg.png "pop-up message")

    From the report, you will see the current environment has six different Oracle home software versions.

    ![](images/config-report.png "current-report")

    Incase you are unable to review the report in Livelab VNC, then open the environment url directly on your laptop browser and run the report again. Example: If you see instance IP address as 129.146.247.99, then the url to open on your browser will be https://129.146.247.99:7803/em .

    ![](images/workshop-instance.png " ")

    Please accept any warning message that your browser may show to continue to login to Enterprise Manager.

7.  Next, click on **Recommended Configurations** to open the Excel Report.

    ![](images/recommend-config.png "recommended changes ")

    The reports recommendation is to consolidate the configuration drift (pollution) from the current six database to two (18c and 19c). This recommendation would reduce the number of configurations and standardize the environment for easier management.

    ![](images/recommend-report.png "recommendations ")

    The recommendation is based on a union of bugs included in the patches in all Oracle homes and based on the configuration type.

## Task 3: Database Server update(patching) with Fleet maintenance (Overview)

### **Database Fleet Maintenance**

Starting with Enterprise Manager 13.5 RU16, Enterprise Manager offers a new interface - Fleet Maintenance Hub to ease automated update(patching), and upgrade of your database fleet. The Fleet Maintenance Hub within Enterprise Manager offers a comprehensive solution for managing database vulnerabilities and patch operations. It streamlines the process by identifying potential security risks, providing patch recommendations, and enabling efficient scheduling and monitoring of patching and upgrade operations. With the ability to manage diverse infrastructures and ensure compliance with patch policies, the Fleet Maintenance Hub serves as a centralized and powerful tool for maintaining the security and stability of database assets.

Enterprise Manager Database Fleet Maintenance is a Gold Image Target subscription-based Out of Place patching solution. Out of Place patching is a method where patching is performed by creating a copy of the Oracle home, applying patches to the copied home, and then switching services to the copied home.

A gold image is the end of state software definition that contains information about the base software version plus the additional patches. Targets, to be patched, subscribe to a relevant Gold Image. Target subscription persists through the lifecycle of the Target or Gold Image unless modified by an administrator.

  ![](images/new-db-fleet-patching.png "new interface")

### **Patching with Fleet Maintenance Hub**

We will go through steps for update(patching) database target ***finance.subnet.vcn.oraclevcn.com***, a Single Instance Database that is currently at 19.17.0.0.0 version. The goal is to patch this target to 19.23.0.0.0.

1.  Return to the browser page with the Oracle Enterprise Manager Console (log back in if needed) and from the EM home page, select the ***Targets*** drop-down menu and select ***Databases*** to review the status and version of database targets.
![](images/Target-Databases-Navig.png "Target-Databases-Navigation")

Review version of ***finance.subnet.vcn.oraclevcn.com***
  ![](images/patch-db-layout.png "finance-db-version")

## Task 4: Review Gold Image [Step Already Performed, Read-Only Step]

1. For this lab exercise, we have already created the gold image. To create or refresh a gold image, below are the high level steps:

-  Ensure that latest patch recommendations are uploaded within Enterprise Manager. This can be done either by uploading the patch catalog (this method is meant for those setups which are not internet facing) or by entering MOS credentials and automatically fetching the latest recommendations as and when done. For accuracy of this lab, we have followed approach 1.We suggest that you do not upload latest patch recommendations as this may impact the existing gold images, and you may not be able to complete the lab following the instructions manuals.
-  Review the list of patches recommended
-  Upload these patches in software library
-  Follow the workflow to refresh the gold images

2. From the Database page, navigate to the ***Administration*** drop-down menu and then select ***Fleet Maintenance Hub***.

    ![](images/Launch-Hub.png "Hub Homepage")

    Click on middle Tile 2, which is **Patch Recommendations for Images**. Here, we see two gold images. The highlighted one ***19cDB-Linux-x64-Apps*** is a healthy image, which has all the patch recommendations. We will use this gold image to complete our patching activity in this lab.
    ![](images/Hub-Tile2.png "Hub Homepage")

## Task 5: Subscribe Database

1.  We will subscribe database target ***finance.subnet.vcn.oraclevcn.com***, to the above suggested gold image ***19cDB-Linux-x64-Apps***. To do so, in the Hub, select Tile 1, which is ***Target Subscription***. Click on the ***Subscribe*** button.

    ![](images/Subscribe-Hub.png "Subscribe flow")

2. A new layout will appear. In this layout, select

-  Release as ***19.0.0.0.0***
-  From the drop down, select the gold image name ***19cDB-Linux-x64-Apps***
-  From Unsubscribed Targets, select database target ***finance.subnet.vcn.oraclevcn.com***

   Click on Subscribe button and wait for it to completed.

    ![](images/Subscribe-FinanceDB.png "Subscribe-FinanceDB")

   Once done, click on close button.


## Task 6: Deploy Image

1. From Hub, Navigate to Tile 3, which is ***Target Patch Compliance***. From the below table, we see our target database ***finance.subnet.vcn.oraclevcn.com***. Either click on the update link under column ***Target Compliance*** or select ***Update Databases*** from the Actions column.

    ![](images/Tile3.png "Tile 3.png")

2. A new tab will open. This page is referred as Operator UI or Operator Centric page. All the activities performed so far are termed as Admin centric as we have a healthy image and subscribed relevant targets. In the page, all the selections we have made so far are pre-selected. However, its better to verfiy.

    ![](images/selection.png "selection")

    Where:
    -  Image = Desired version of Oracle home, which our target database should run after successful completion of operation. In this example, we will select ***19cDB-Linux-x64-Apps***.
    -  Target Type = Desired target type, which can be Grid, RAC or SIDB. In this example, we will select ***Database Instance***.
    -  Operation = Name of the operation, which can be update (patch) or upgrade. In this example, we will select ***Update***.
    -  Type to filter = Selection criteria to highlight only those targets which qualify the selection, such as database naming.

    Select Next.

3. In this page, we will provide ***new Oracle home location***, select which ***tasks*** can be performed, select ***credential model***, provide ***log file location*** under options and select any   ***custom scripts*** to run as part of the operation.

    ![](images/finance-patch-screen2.png "input values")


    Under Maintenance tasks, we can enter following values
    - Destination Oracle Home as
    ```
    <copy>/u01/livelabs/db/19c/19.23/finance</copy>
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

4. We can validate our entries (new Oracle home, log file location, credentials) provided in previous page and validate the desired operation. Validation acts as a precheck before we submit the main operation. Click on ***Validate*** and a new pop-up screen will appear.
    ![](images/submit-Validate.png "quick and full valdiation modes")

There are two validation modes - Quick and Full. We can select either of these. Full validation mode submits a deployment procedure. In this lab, choose Quick validation mode and click on Validate.

  ![](images/quick-validate.png "quick and full valdiation modes")

5. Review the validation result.

    ![](images/finance-validation-success.png "result of valdiation")

    Incase of any error, we can fix it and choose revalidate. Else, click on close.

6. ***Submit*** the operation. A new pop-up will appear and we need to provide the name to the tasks.
    Lets enter
    ```
    <copy>finance-update</copy>
    ```

    ![](images/finance-job-name.png "submit operation")    

    Click on submit.
    ![](images/finance-job-monitor.png "monitor")

    Clicking on Monitor Progress will take us to Procedure Activity Page. Alternate navigation to review the submitted deployment procedures is ***Enterprise >> Provisioning and Patching >> Procedure Activity***.
    ![](images/navigate-dp.png " ")

7. Review the Deployment Procedures (DP).

   ![](images/DP.png "review")

   Select DP related to Deploy and click on it. It will show details of the activity performed by the DP.

   ![](images/deploy-complete.png "review dp for layout OH")

   Here, we see that the DP has successfully completed. This DP is responsible for installing new Oracle home at the location that we had specified earlier.

## Task 7: Migrate Listener

1. In task 6 (above), we submitted a task to migrate the listener. If this task needs to be submitted separately, then you need to uncheck migrate listener task (review step 3 of task 6).
    ![](images/uncheck-mig-listener.png " ")

    Select the running task to see the various steps performed.

    ![](images/listener-migrate.png "details of DP")
    We can now see that the migration operation completed successfully.

## Task 8: Update(Patching) Database – Patch 19.17 to 19.23

1. Similar to listener migration, we also submitted operation for Update Database in task 6. If it needs to be submitted separately, then you need to uncheck the update database task (review step 3 of task 6).
    ![](images/uncheck-update-db.png " ")

    Select the running task to see the various steps performed.

    ![](images/patch-complete.png "DP completed")

    Update operation has completed successfully.

    Lets validate the version of ***finance*** database. In the upper toolbar, locate the ***Targets*** icon and click the drop-down menu and then select ***Databases***. We can see the updated version of ***finance*** database.

   ![](images/finance-post-upg-version.png "new version check")

   Also, navigate to Tile3 in Hub and review the status of finance database from compliance perspective.

   ![](images/finance-post-upg-tile3.png "new version check")

## Task 9:  Rollback Database – Reversed Patch 19.23 to 19.17

Once the database is updated(patched), we will perform a rollback to Oracle Database 19.17. In a future release, capability is being planned to perform rollback of an operation using the UI.

1. Review and execute below command from the terminal to rollback database Target ***finance.subnet.vcn.oraclevcn.com***

    ```
    <copy>cd ~/fleet
    sh rollback_finance.sh</copy>
    ```

    ![](images/rollback-finance.png " ")

2. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity*** to review Execution details of this operation via Enterprise Manager Console
    ![](images/navigate-dp.png " ")


3. Review the Procedure Activity steps performed         

    ![](images/rollback-dp.png "rollback complete")

4. Verify the rolled back target by going to ***Targets >> Databases*** as shown
below.

    ![](images/rollback-db-layout.png "sales-ROLLBACK")

## Task 10:  Cleanup Old homes

1. Clean up old oracle homes used by database Finance. In a future release, capability is being planned to perform cleanup of an operation using the UI.

   In order to have an old empty home previously used by “***finance.subnet.vcn.oraclevcn.com***” at our disposal to demonstrate a cleanup operation, we will now re-update(re-patch) the database.

2. Review and execute below command to update(patch) database target ***finance.subnet.vcn.oraclevcn.com*** again to 19.23 version


    ```
    <copy>sh update_finance.sh</copy>
    ```

![](images/post-rollback-finance-update.png " ")


3. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity*** to review Execution details of this operation via Enterprise Manager Console

    ![](images/navigate-dp.png " ")

Below are the list of Deployment Procedures. Select the latest one.

![](images/DP-submission-update.png " ")

Verify that the update has been completed successfully.
    ![](images/update-complete.png "fleet status")

4. Verify and confirm that the target has been re-patched to Oracle Database 19.23 by going to Targets Databases as shown below.

    ![](images/new-finance-status.png "new sales version")

5. Now that finance database has been patched, we have its old Oracle Home for cleanup. Review and execute the following command in terminal as a dry-run to report on cleanup impact for *finance.subnet.vcn.oraclevcn.com*  


    ```
    <copy>sh cleanup_finance_report.sh</copy>
    ```

  ![](images/cleanup-finance-report.png "cleanup report")

6. Review and execute the following command to cleanup *finance.subnet.vcn.oraclevcn.com*   

    ```
    <copy>sh cleanup_finance.sh</copy>
    ```

    ![](images/finance-cleanup-submission.png "cleanup action")

7. From the Enterprise Manager menu bar, navigate to the ***Enterprise*** drop-down menu and then ***Provisioning and Patching >> Procedure Activity***.
    ![](images/navigate-dp.png " ")

    Monitor the progress of this operation with ‘CLEANUP\_SOFTWARE\_...’ deployment procedure instance.

    ![](images/cleanup-success-finance.png "cleanup dp")

8. Verify to confirm the old Oracle home has been removed

    ```
    <copy>ls -ltr /u01/app/19c/finance</copy>
    ```

    ![](images/cleanup-sales-os-layout.png "OS cleanup")


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
  - **Last Updated By/Date** -Romit Acharya, Oracle Enterprise Manager Product Management, May 2024
