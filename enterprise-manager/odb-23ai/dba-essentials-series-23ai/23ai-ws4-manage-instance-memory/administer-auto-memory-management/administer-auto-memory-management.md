# Administer Automatic Memory Management

## Introduction

This lab shows how to enable Automatic Memory Management for Oracle Database from Oracle Enterprise Manager Cloud Control (EM) and SQL command line.

Oracle Database can manage the SGA memory and instance PGA memory. You designate only the total memory size to be used by the instance, and the database dynamically exchanges memory between the SGA and the instance PGA as needed to meet processing demands. This capability is referred to as *Automatic Memory Management*. Allowing the database instance to automatically manage and tune is one of the simplest ways to manage instance memory.

Estimated time: 15 minutes

### Objectives

-   Enable Automatic Memory Management from Oracle Enterprise Manager
-   Disable Automatic Memory Management from Oracle Enterprise Manager
-   Set environment variables 
-   Enable Automatic Memory Management from SQL command line

To enable Automatic Memory Management in both Oracle Enterprise Manager and SQL Command Line you require different Oracle home locations.

> **Note**: This workshop uses two Oracle homes for demonstration purpose. It is not a requirement for Oracle Database to have two homes. A single Oracle home is sufficient to install and manage a single instance container database.

### Prerequisites

This lab assumes you have -

-   An Oracle Cloud account
-   Completed all the previous labs successfully

> **Note**: This lab contains system-specific values and paths. These details might vary depending on the system you are using.

## Task 1: Enable Automatic Memory Management from Oracle Enterprise Manager

After logging in to EM, you can view the status of Automatic Memory Management and enable it.

1.  From the **Targets** menu, select **Databases**.
    ![Databases](../administer-auto-memory-management/images/emcc-target-db.png)
    The Databases page displays a list of Oracle Databases added to EM as managed targets.

    ![Database List](../administer-auto-memory-management/images/emcc-dbvalues.png)  
      
2.  Click the database instance name, *orcl.us.oracle.com*, to open the instance home page.
    ![Instance Home page](../administer-auto-memory-management/images/emcc-instance-hompage.png)  
      
3.  From the **Performance** menu, select **Advisors Home**.
    ![Advisors Home](../administer-auto-memory-management/images/performance-advisorshome.png) 

4.  Click **Login** from Database Login page.
    ![DB Login Page](../administer-auto-memory-management/images/db-loginpage.png)
      
5.  On the Advisors tab, select **Memory Advisors**.
    ![Memory Advisors](../administer-auto-memory-management/images/advisors-memoryadvisors.png) 
      
    > **Note:** The Memory Advisors option is available only from the database instance home page, and not from the PDB home page. You can use Memory Advisors when the Automatic Memory Management feature is disabled. The Memory Advisors automatically adjusts the memory distribution among the various SGA and PGA for optimal performance. These adjustments are made within the boundaries of your total SGA and PGA target values. If the Memory Advisor finds that the current amount of available memory is inadequate and adversely affecting performance, it recommends you to increase your SGA or PGA target value. You can set new values for the SGA and PGA using the Memory Advisor. 
    
    If the **Maximum SGA Size (MB)** field consists of a positive number that is greater than or equal to the total amount of memory to allocate to the database, then you can directly **Enable** Automatic Memory Management option without performing rest of the steps.  

    >**Note:** If Automatic Memory Management is Enbaled, follow the steps of the next task to first Disable it.
      
6.  In the **Maximum SGA Size (MB)** field, enter the maximum permissible size for database memory and click **Apply**. For this lab the Maximum SGA Size entered is *6 GB*.
    ![Maximum SGA Size](../administer-auto-memory-management/images/totalsgasize-greater-maxmemory.png)  
      
    > **Note:** To decide the maximum SGA size, use the sum of the current sizes of the SGA and instance PGA as a guideline, and optionally add some extra values for extension.  
      
7.  An update message appears indicating that changes are made successfully.
    ![Update Message](../administer-auto-memory-management/images/update-message.png) 
         
8.  The Memory Advisors page displays the status of Automatic Memory Management as Disabled. Now click **Enable** to enable this option.  
    ![Enable button](../administer-auto-memory-management/images/enable-with-skip.png)  

9.  On the Enable Automatic Memory Management page, in the Total Memory Size for Automatic Memory Management field, enter the required amount of memory to allocate to the database and then click **OK**. 

	For this lab, 5 GB is used as Total Memory Size for Automatic Memory Management.  
    ![Enable Automatic Memory Management](../administer-auto-memory-management/images/enable-amm-screen.png)

10. A window appears to confirm restarting the database. Click **Yes** to restart the database. 
    ![Restart Database confirmation message](../administer-auto-memory-management/images/restart-confirmation.png)

    The Restart Database page appears which displays Host and Target Database Credentials.

11.  For Host Credentials, specify the following.
    
    - **Credential**: *Named*

    Oracle Enterprise Manager fills in the **UserName** and **Password** fields automatically.  
    You can click **More Details** and then click **Test** to verify that the specified host credentials are working.

12. For Database credentials, specify the following.
    
    - **Credential**: *Preferred*
    - **Preferred Credential Name**: *SYSDBA Database Credentials*.    
	This is the credential you assigned during Oracle Database installation.
    
    Click **OK** to proceed.

13. A window appears to confirm restarting the database. Click **Yes** to restart the database. 
    ![Restart Database confirmation message](../administer-auto-memory-management/images/restart-db-confirmation.png)
    Oracle Database takes a while to restart. After which you receive an update message of successful database restart.

14. Click **Refresh** to return to the Database home page.  
    ![Successful restart confirmation message](../administer-auto-memory-management/images/update-restart-confirmation.png)
    Now, go to the Memory Advisors page and view the status of Automatic Memory Management as follows.   
      
15.  On the Database home page, click the database instance name, *orcl.us.oracle.com*, to open the instance home page.  
    ![Instance Home page](../administer-auto-memory-management/images/emcc-instance-hompage.png)  
      
16.  From the **Performance** menu, select **Advisors Home**.  
    ![Advisors Home](../administer-auto-memory-management/images/performance-advisorshome.png)  
      
17.  In the Advisors section, select **Memory Advisors**.  
    ![Memory Advisors](../administer-auto-memory-management/images/advisors-memoryadvisors.png) 
      
You can verify that the Automatic Memory Management option displays **Enabled**.  
    ![Successful Automatic Memory Management](../administer-auto-memory-management/images/enabled-amm.png)
    
## Task 2: Disable Automatic Memory Management from Oracle Enterprise Manager

From Memory Advisors home page in EM, you can disable Automatic Memory Management for your Oracle Database and manage the memory sizes manually.

1.  Click **Disable** next to the Automatic Memory Management option.
    ![Disable Automatic Memory Management](../administer-auto-memory-management/images/memoryadvisors-disable.png)
    
    You have disabled Automatic Memory Management for your Oracle Database from EM. The Memory Advisors page displays **Disabled** next to the Automatic Memory Management option.
    ![Disabled Automatic Memory Management](../administer-auto-memory-management/images/disabled-amm.png)
    
You can now log out of Oracle Enterprise Manager.
    
## Task 3: Set environment variables

> **Note:** From Task 3 you will use the other Oracle home location. This workshop uses two Oracle homes for demonstration purpose. It is not a requirement for Oracle Database to have two homes. A single Oracle home is sufficient to install and manage a single instance multitenant container database.

[](include:em-manage-instance-task-set-env-var)

## Task 4: Enable Automatic Memory Management from SQL command line

1.  From `$ORACLE_HOME/bin`, log in to SQL command line as `SYSDBA`.  
    ```
    $ <copy> ./sqlplus / as sysdba </copy>
    ```
    ```
    SQL*Plus: Release 23.0.0.0.0 - Production on Mon Oct 7 06:37:16 20XX
    Version 23.4.0.24.05

    Copyright (c) 1982, 2024, Oracle. All rights reserved.

    Connected to:Oracle Database 23ai Enterprise Edition Release 23.0.0.0.0 - Production
    Version 23.4.0.24.05
    
    SQL>
    ```
    
2.  View the values of all initialization parameters with the string `TARGET` in the parameter name.
    ```
    SQL> <copy> show parameter target</copy>
    ```
    It displays the following output.
    ```
    NAME                                     TYPE           VALUE  
    ------------------------------------     -----------    ------------------------------  
    archive_lag_target                       integer        0  
    db_big_table_cache_percent_target        string         0  
    db_flashback_retention_target            integer        1440  
    fast_start_io_target                     integer        0  
    fast_start_mttr_target                   integer        0  
    memory_max_target                        big integer    0  
    memory_target                            big integer    0  
    parallel_servers_target                  integer        80  
    pga_aggregate_target                     big integer    3167M  
    sga_target                               big integer    9504M  
    target_pdbs                              integer        18
    
    NAME                                      TYPE         VALUE  
    ------------------------------------      -----------  ------------------------------  
    txn_auto_rollback_high_priority_wait      integer      2147483647  
    _target  
    txn_auto_rollback_medium_priority_wa      integer      2147483647  
    it_target
    ```
    
    Run the following commands and change the values of the initialization parameters.  
      
    
3.  Set the parameter `memory_max_target` to *6G*.  
    ```
    SQL> <copy> alter system set memory_max_target=6G scope=spfile;</copy>
    ```
    ```
    System altered.
    ```

4.  Set the parameter `memory_target` to *5G*.  
    ```
    SQL> <copy> alter system set memory_target=5G scope=spfile;</copy>
    ```
    ```
    System altered.
    ```

5.  Set the parameter `pga_aggregate_target` to *0*.  
    ```
    SQL> <copy> alter system set pga_aggregate_target=0 scope=spfile;</copy>
    ```
    ```
    System altered.
    ```

6.  Set the parameter `sga_target` to *0*.  

    ```
    SQL> <copy> alter system set sga_target=0 scope=spfile;</copy>
    ```
    ```
    System altered.
    ```

    > **Note:** The preceding steps instruct you to set the parameters `SGA_TARGET` and `PGA_AGGREGATE_TARGET` to *0* so that the size of the SGA and instance PGA are tuned up and down as required, without restrictions.
    
    For the new values of the parameters to take effect, shut down and start the database instance.  
      
7.  Shut down the database instance in *IMMEDIATE* mode.   
    ```
    SQL> <copy> shutdown immediate;</copy>
    ```
    ```
    Database closed.
    
    Database dismounted.
    
    ORACLE instance shut down.
    ```

8.  Start the database instance again and open Oracle Database.  
    ```
    SQL><copy> startup</copy>
    ```
    ```
    ORACLE instance started.
    
    Total System Global Area 9951006048 bytes  
    Fixed Size                 10038624 bytes  
    Variable Size            1543503872 bytes  
    Database Buffers         8388608000 bytes  
    Redo Buffers                8855552 bytes  
    Database mounted.  
    Database opened.
    ```
    The database instance starts in the default _OPEN_ mode.  
      
9.  Execute `show parameter target` command to view the new values of the initialization parameters.  
    ```
    SQL> <copy> show parameter target</copy>
    ```  
    ```
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- -------
    archive_lag_target                   integer     0
    db_big_table_cache_percent_target    string      0
    db_flashback_retention_target        integer     1440
    fast_start_io_target                 integer     0
    fast_start_mttr_target               integer     0
    memory_max_target                    big integer 6G
    memory_target                        big integer 5G
    parallel_servers_target              integer     80
    pga_aggregate_target                 big integer 0
    sga_target                           big integer 0
    target_pdbs                          integer     12

    NAME                                    TYPE        VALUE   
    ------------------------------------    ----------- ------------------------------   
    txn_auto_rollback_high_priority_wait    integer     2147483647   
    _target   
    txn_auto_rollback_medium_priority_wa    integer     2147483647   
    it_target   
    ```
    
    To verify if the Automatic Memory Management has been Enabled, log in to Oracle Enterprise Manager in a web browser and navigate to Advisors Home. The Memory Advisors page shows Automatic Memory Management as *Enabled*.  

Congratulations! You have successfully completed the workshop on *Database Instance and Memory Management*.

## Acknowledgments

-   **Author** - Aayushi Arora, Database User Assistance Development Team
-   **Contributors** - Manish Garodia, Jayaprakash Subramanian, Ashwini R
-   **Last Updated By/Date** - Aayushi Arora, October 2024

