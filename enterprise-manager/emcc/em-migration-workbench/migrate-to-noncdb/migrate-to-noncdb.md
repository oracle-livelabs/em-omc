# Migrate and upgrade 12c database to 19c in new destination

## Introduction

You can use Database Migration Workbench to migrate databases to multi-tenant architecture on Exadata on-premises, to Base Database (ExaCC, ExaCS, BM, or VM), and autonomous, using TTS and data pump migration methods. This lab demonstrates using Migration Workbench for **on-premises** to **on-premises** migrations. Since the workshop is fully contained in a single VM, the source and destination databases are on the same host, but the instructions apply when migrating databases to new hosts.

Estimated Time: 30 minutes

Watch the video below for a quick walk-through of the lab.
[Migrate and upgrade 12c database to 19c in new destination](videohub:1_7h09aldy)

### Objectives

In this lab, you will perform the tasks below. Task 1 is to review the prerequisites completed in advance for this lab. In task 2 you will create a migration activity, add details, and learn about the various configuration options. After the migration is complete, you will analyze the migration activity and compare performance before and after the migration.

| Task No.                                      | Description                                                                 | Approx. Time | Details                                                                                                                                                                                    |
|-----------------------------------------------------------|-------------------------------------------------------------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | Review prerequisites completed in advance| 10 minutes | Review prerequisites completed on the source and destination databases, hosts, and in Enterprise Manager |
| 2 | Migrate and upgrade a 12c non-container database to 19c in a new destination | 20 minutes   | Source database: orcl, destination database: orcl19c |

### Prerequisites

- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

>**Note:** This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 RU7, and database 19.12 as Oracle Management Repository.

## Task 1: Review prerequisites completed in advance

In the interest of simplifying the setup and to save time, the following requirements were completed in advance and covered in this lab. Please review accordingly for reference.

1. Source and destination targets are discovered in Enterprise Manager
    - On the browser window on the right preloaded with *Enterprise Manager*, if not already logged in, click on the *Username* field and log in with the credentials provided below

        ```text
        Username: <copy>sysman</copy>
        ```

        ```text
        Password: <copy>welcome1</copy>
        ```

        ![Login Page](../initialize-environment/images/em-login.png " ")
    - Click on "Targets"->"Databases"
    ![Databases](images/databases.png " ")
        - orcl is our source database
        - orcl19 is our destination database
2. Data Pump user requirement
    - For the source database (orcl), an export user (EXP_USER) was created with the password "welcome1" and the required privileges
    - For migrating the database to a new non-container database, an import user (IMP_USER) was created in the target database (orcl19c) with the password "welcome1" and the required privileges
    - To learn more about the required privileges review "[Database Migration Prerequisites](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmwb/database-migration-workbench.html#GUID-3FB0F7B7-F221-43BE-8D29-E36A18EF45C0)" in the Enterprise Manager documentation

3. Named Credential requirement
    - Named Credentials "EXP\_USER" and "IMPUSER" were created in Enterprise Manager for users "EXP\_USER" and "IMP\_USER" on databases "orcl" and orcl19c respectively
    - To review the credentials in the OEM console, navigate to "Setup"->"Security"->"Named Credentials"
    - To learn more about named credentials review "[Named Credentials](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emsec/security-features.html#GUID-345595B0-3FA4-4F2C-A606-596B1A10A13E)" in the Enterprise Manager documentation

4. Data Pump directory requirement

    Migration workbench requires local directories on the source and target databases with sufficient space to host the data pump dump files. In our workshop both the source and target databases are running on the same host.
    - Created the following directory on the host: /u01/app/oracle/migration_workbench
    - Created directory object "MWB_DIR" in both source and target databases pointing to this directory
    - Granted read and write privileges on the directory object in each database to the corresponding user (EXP\_USER in source database and IMP\_USER in target database)

5. Compare performance requirement

    SQL Performance Analyzer (SPA) automates the process of assessing the overall effect of a change on the  SQL workload by identifying performance divergence for each SQL statement. A report that shows the net impact on workload performance due to the change is provided. For regressed SQL statements, SQL Performance Analyzer also provides appropriate execution plan details along with tuning recommendations. As a result, you can remedy any negative outcome before the end-users are affected. Furthermore, you can validate -with time and cost savings- that migration will result in net improvement.

    An SQL Tuning Set (STS) containing the SQL and relevant execution metadata from the source database is needed to compare performance before and after the migration. Database Migration Workbench can create an STS from AWR during migration, or you can create one in advance and pass it to the migration procedure.

    - For this lab, an STS was created in advance (SH2STS) by running a workload against the SH2 schema in the source database and capturing the SQL statements executing during the load test

6. Upload migration tools

    Migration Workbench uses Instant Client and the Cloud Premigration Advisor Tool (CPAT) as part of its migration toolkit. Enterprise Manager automatically downloads the latest version of the tools when set up with either a MOS Proxy or direct internet connection. The tools can also be uploaded manually as described in [Upload Migration Tools] (<https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/emlcm/upload-migration-tools.html>) in the Migration Workbench documentation.

    - For this lab the migration tools were uploaded in advance. For additional detail on the Cloud Premigration Advisor Tool refer to this MOS document: *Cloud Premigration Advisor Tool (CPAT) Analyzes Databases for Suitability of Cloud Migration (Doc ID 2758371.1)*

## Task 2: Migrate and upgrade a 12c non-container database to 19c in a new destination

In this task we'll migrate and upgrade an Oracle 12c database to version 19c in a new destination. This would be the case when refreshing hardware and/or moving the database to a new host in your data center. Our source database is "orcl" and our destination database is "orcl19c".

We'll use the Data Pump migration method in this task.

1. Log into your Enterprise Manager as sysman as indicated in task 1 if not already done
2. From the Enterprise menu
    - Navigate to "Migration and Consolidation"->"Database Migration Workbench"
    ![MWB Menu Item](images/mwb-menu-item.png " ")
3. On the "Database Migration" screen:
    - Expand the "Getting Started" section if collapsed. Examine the Migration Workbench workflow
    ![Getting Started](images/getting-started.png " ")
    - Click on "Create Migration Activity"
4. On the Create Migration Activity screen, enter:
    - Activity Name:

        ```text
        <copy>Database Migration ORCL to ORCL19c</copy>
        ```

    - Migrate: Select "Full Database" from the drop-down list

        Migration Workbench allows you to migrate full database, schemas, or tablespaces. We'll migrate full database in this lab
        ![Migrate Options](images/migrate-options_1.png " ")
    - Select Source Database:  Click inside the field and select "orcl.subnet.vcn.oraclevcn.com" from the drop-down list
    - Select Destination Database:  Click inside the field and select "orcl19c.subnet.vcn.oraclevcn.com" from the drop-down list
    - Notice the checkmark for "Tools Validation". For this lab, CPAT tool was uploaded to Enterprise Manager in advance
    - Select Migration Method: Data Pum from the drop-down list
      ![Create Migration Activity](images/create-migration_activity.png " ")
    - Click Continue
5. On the Add Details screen, enter:
    - Source:
        - Database Credentials: EXP_USER (Named Credential)
        - Host Credential: ORACLE (Named Credential)
    - Destination:
        - Database Credential: IMP_USER (Named Credential)
        - Agent Host Credential: ORACLE (Named Credential)
    - Action:
        - Recompile Invalid Objects After Migration: Unchecked (default)
        - Source Data Pump Directory: MWB_DIR
        - Destination Data Pump Directory: MWB_DIR
        - Encryption Password:

            ```text
            <copy>welcome1</copy>
            ```

      ![Add Details](images/add-details.png " ")
    - Click Next
6. On the Customize screen, enter:
    - Export Options:

        Examine the various export options you can configure with Migration Workbench. For the purpose of this lab, we'll go with the defaults shown except for Parallel. The degree of parallelism you choose depends on the number of CPU cores on your source and target databases. We'll use 2 in this lab
        - Parallel: 2
    - Import Options:

        Examine the various import options you can configure with Migration Workbench. For the purpose of this lab, we'll go with the defaults shown except for Parallel. The degree of parallelism you choose depends on the number of CPU cores on your source and target databases. We'll use 2 in this lab
        - Parallel: 2
    - Compare Performance After Migration:
        - SQL Tuning Set (STS): Select "Use Existing" then choose "EXP_USER -- SH2STS"
    - Custom Scripts:

        Migration Workbench allows customization of your migration activity by allowing you upload and use Pre and Post migration scripts. For more information on Pre and Post scripts see: [Pre/Post Scripts for Provisioning] (<https://docs.oracle.com/pls/topic/lookup?ctx=en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmwb&id=EMLCM-GUID-CDF550E0-9F86-42BC-909C-F224869F58CC>) in Oracle Enterprise Manager Cloud Control Database Lifecycle Management Administrator's Guide and [Pre and Post Request Creation / Deletion Scripts](https://docs.oracle.com/pls/topic/lookup?ctx=en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmwb&id=EMCLO-GUID-223719D5-21B5-4AC3-A94B-0C7A3DFF0831) in Oracle Enterprise Manager Cloud Administration Guide
    - Transfer Options:
        - Datapump Directory is shared: Checked

        ![Customize](images/customize.png " ")
    - Click Review
7. On the "Review & Submit" screen:
    - Review your entries to make sure everything is correct
    ![customize](images/analyze_source.png " ")
    - Click "Check Migration Readiness" in the Source column. The analysis will open in a new browser tab and will take a few minutes to complete
    - When the analysis is complete review Migration Readiness Report. The warnings shown can be ignored for the purpose of this lab. When you run this activity in your environment ensure you address any issues identified on a case by case basis
    ![CPAT Results](images/cpat_results.png " ")
    - Click on the previous tab to continue with the migration process
    ![Validate](images/validate1.png " ")
    - Click Validate
8. On the Validation screen:
    - Validation checks run for a few minutes and all checks should pass. If your results are different check your previous steps, fix the error and revalidate
    ![Validate Activity](images/validate_activity.png " ")
    - Click "Submit"
9. On the Submit Activity screen:
    - Choose Schedule: Start Immediately (default)

        Examine the JSON file. Notice you can copy the generated JSON file to use it with with DevOps tools and REST APIs. For this lab however, we'll complete the migration using the Enterprise Manager graphical console
    ![Submit Activity](images/submit_activity.png " ")
    - Click Submit
    - You should receive the message: "Migration activity submitted successfully."
    ![Close](images/close1.png " ")
    - Click "Go Back to Activities Page"
10. On the Migration Activities screen:
    - The activity status will show "Scheduled" at first. Refresh the page after a few seconds and it will change to "Running". You can also change the Auto Refresh to every minute
    ![Migration Activities](images/migration-activities.png " ")
    - Click on the "Running" link under Status to go to the Procedure Activity screen
11. On the Procedure Activity screen::
    - Click on the "Running" link under Status to go to the procedure activity screen. Choose Show: "Steps Not Skipped". The procedure should take about 5 minutes to complete
    - When the procedure completes, it will most likely show there were some errors. We'll check those when we analyze the migration
    ![Procedure Activity Completed](images/procedure-activity-completed.png " ")
    - From the Enterprise Menu, click "Migration and Consolidation"->"Database Migration Workbench" to go back to the Migration Activities screen
12. On the Migration Activities screen:
    - Expand the drop-down menu on the right of the activity row
    ![View Analysis](images/view-analysis.png " ")
    - Click on View Analysis
13. On the View Analysis screen:

    Examine the analysis report. The report has 2 sections: A summary dashboard at the top, and a detail section with 3 tabs: Validation, Export, and Import.
    - On the summary dashboard, review information and statistics for the validation activity, export phase, and import phase
    - In the details section:
        - Click the Input Validation tab to review validation checks that passed, failed, or skipped
        - Click the Export tab to review details on object errors encountered during export, export options, and export files
        - Click on the Import tab to review details on object errors encountered during import, import options, and import files
        - For further details on the errors review the log file using the Procedure Activity page shown earlier. On that page, you can check the checkbox for any step to display the log file on the screen. You can also download the file for offline viewing
        - In your environment, you may need to take actions such as granting specific object privileges to fix the errors. However, for this lab, the errors shown can be ignored

        ![Analysis](images/analysis1.png " ")

    When you are done analyzing the migration, click on "Migration Activities" in the top left of the report to navigate back to the Migration Activities screen
14. On the Migration Activities screen:
    - Expand the drop-down menu on the right of the activity row
    ![Compare Performance](images/compare-performance.png " ")
    - Click on View Performance
    ![LoginCompperf](images/Logincompareperf.png " ")
    - Click Login
15. On the SQL Performance Analyzer Report screen:

    Examine the Performance Comparison report to analyze the database performance before and after the migration. The report has 3 sections:
    - General Information: Contains information about the task, workload, execution, and analysis before and after migration. The  comparison metric used is "Elapsed Time"
    - Report Summary: Contains 3 sections:
        - Projected Workload Change Impact: This shows the overall impact of the migration on the SQL workload, the improvement impact, and the regression impact
        - SQL Statement Count: This shows the overall statement count, the number of SQLs that improved, regressed, or were unchanged
        - Top 100 SQL Sorted by Absolute Value of Change Impact on the Workload: This shows the top 100 impacted SQLs with absolute percentage improvement. SQLs highlighted in green have improved performance due to improved execution plans or query costs. Those highlighted in red have regressed due to execution plan change or execution problems (for example query returning no rows or number of rows returned is different in the destination than in source, etc.)

            Check regressed SQLs to see execution statistics, before and after migration change analysis. Understand findings provided for each query to see which factors impacted the regressed SQLs. You can then take action based on findings provided in the Report Details section to improve SQL performance
    - Report Details: Contains detailed execution details for each SQL statement in the STS, including the SQL test, execution frequency, executions statistics, notes, findings, and execution plan before and after the migration

        ![Performance Comparison](images/performance_comparison1.png " ")
    - When you are done with performance comparison, click on "Migration Activities" in the top left of the report to navigate back to the Migration Activities screen
16. On the Migration Activities screen:
    - Expand the drop-down menu on the right of the activity row
    ![Mark Completed](images/mark-completed1.png " ")
    - Click Mark as Completed
    - Examine the guidelines on the Confirmation pop-up window, enter any comments as appropriate
    ![Confirmation](images/confirmation1.png " ")
    - Click Yes
     ![Marked Completed](images/marked-completed1.png " ")
    - Activity is marked completed

This completes the Lab!

## Learn More

- [Database Migration Workbench Guide](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmwb/index.html)
- [Migrate Oracle Databases with a safety net using Migration Workbench (Blog)](https://blogs.oracle.com/observability/post/migrate-oracle-database-with-a-safety-net-using-migration-workbench)
- [Migrate Databases to Cloud and On Premises (Video)](https://www.oracle.com/explore/exadata-virtual-events/migrate-databases-to-cloud?lx=W4Fgb9&topic=Oracle%20Exadata%20Master%20Class)

## Acknowledgements

- **Author** - Amine Tarhini, Systems Management Specialist, Oracle Platform Solution Engineering
- **Contributors** -  Harish Niddagatta, Enterprise Manager Product Management, Rajendra Patil, Enterprise Manager Product Manager
- **Last Updated By/Date** - Amine Tarhini, July 2022
