# View the storage structures

## Introduction

This lab demonstrates how to view the storage structures in your Oracle Database using Oracle Enterprise Manager Cloud Control.

Estimated time: 15 minutes

### Objectives

-   View storage administration
-   View control files
-   View archive logs

> **Note:** This lab contains many system-specific values. Such details might vary depending on the system you are using.

### Prerequisites

This lab assumes you have:
-   An Oracle Cloud account
-   Completed all previous labs successfully
-   Logged in to Oracle Enterprise Manager Cloud Control in a web browser as *sysman*

## Task 1: View Storage Administration

Perform the following steps to view the Oracle Database storage administration page in the Oracle Enterprise Manager Cloud Control:

1. On the Oracle Enterprise Manager Cloud Control web page, go to the **Targets** menu and select **Databases**.

    ![EMCC Home](./images/L2_T1_S1_emcc_home.png " ")

2. The **Databases** page lists the Oracle Databases as managed targets.

    Select the database instance for which you want to view the details. In this example, the ***orcl1.us.oracle.com*** container database instance is selected.

    ![EMCC target databases](./images/L2_T1_S2_emcc__targets_databases.png " ")

3. View the database instance home page. It displays various details about the selected database.

    ![EMCC database home](./images/L2_T1_S3_emcc_database_home.png " ")

4. On the database instance home page, from the **Administration** menu, go to the **Storage** option and select **Home**.

    ![EMCC Select storage home](./images/L2_T1_S4_emcc_select_storage_home.png " ")

5. View the **Storage Home** page. It displays the storage usage details.

    ![EMCC storage home](./images/L2_T1_S5_emcc_storage_home.png " ")

6. From the **Oracle Database** menu, select **Home** to go to the database instance home page.

    ![EMCC Select database home](./images/L2_T1_S6_emcc_storage_home_select_database_home.png " ")


## Task 2: View Control Files

Control files track the structural changes to the database. When you add, rename, or delete a data file or an online redo log file, the database updates the control files to reflect this change. You can view this information about the **Control Files** page.

Perform the following steps to view the control file information for the database instance:

1. In the **Administration** menu, go to the **Storage** option and select **Control Files**.

    ![EMCC Select storage control files](./images/L2_T2_S1_emcc_select_storage_control_files.png " ")

2. On the **Control Files** page, the **General** tab displays the control files and their location.
    > **Note:** Oracle recommends that you maintain a copy of the control files on different disk drives.

    ![EMCC control files](./images/L2_T2_S2_emcc_control_files_general.png " ")

3. Select the **Advanced** tab to view the status of the data stored in the control file.

    The **Advanced** tab displays the following information:
    -   the Database ID
    -   the type of control file
    -   the time-stamp of control file creation
    -   the current log sequence number
    -   the last changed number
    -   the time-stamp of the last modification
    -   whether the control file has AutoBackup enabled.

    ![EMCC control files advanced](./images/L2_T2_S3_emcc_control_files_advanced.png " ")

4. Select the **Record Section** tab to view the record information of the control file, including associated data files and redo log files.

    ![EMCC control files record section](./images/L2_T2_S4_emcc_control_files_record_section.png " ")

5. From the **Oracle Database** menu, select **Home** to go to the database instance home page.

    ![EMCC control files select database home](./images/L2_T2_S5_emcc_control_files_select_database_home.png " ")


## Task 3: View Archive Logs

Perform the following steps to view the archive log information of your Oracle Database:

1.  In the **Administration** menu, go to the **Storage** option and select **Archive Logs**.

    ![EMCC select storage archive logs](./images/L2_T3_S1_emcc_select_storage_archive_logs.png " ")

2.  View the **Archive Logs** page. It displays the archived redo log information of the Oracle Database. The database must be in `ARCHIVELOG` mode to view the archive log details.

    ![EMCC archive logs](./images/L2_T3_S2_emcc_archive_logs.png " ")

3. From the **Oracle Database** menu, select **Home** to go to the database instance home page.

    ![EMCC archive logs select database home](./images/L2_T3_S3_emcc_archive_logs_select_database_home.png " ")


You may now **proceed to the next lab**.


## Acknowledgements

-	**Author:**  Suresh Mohan, Database User Assistance Development Team
-	**Contributors:** Manisha Mati, Suresh Rajan, Manish Garodia
-	**Last Updated By/Date:** Suresh Mohan, October 2024