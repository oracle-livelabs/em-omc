# View database details from SQL command line

## Introduction

This lab walks you through the steps to log in to SQL prompt and explore Container Database (CDB) and Pluggable Database (PDB) with basic SQL commands.

Estimated time: 10 minutes

### Objectives

 - Set environment variables
 - Log in to CDB (root container) with *SYSDBA* privileges
 - Run SQL commands to view details of your Oracle Database

### Prerequisites

This lab assumes you have -

 -   An Oracle Cloud account
 -   Completed all previous labs successfully
 -   Logged in to your host as the *oracle* user

> **Note**: [](include:example-values)

## Task 1: Set environment variables

[](include:set-env-var)

> **Tip**: If you have reserved a Livelabs sandbox environment, then you can run the script `.set-env-db.sh` from the home location and enter the corresponding number for the `ORACLE_SID`. It sets the environment variables automatically.

## Task 2: Connect to SQL prompt and explore the database

In this task, you will view some basic details of your database, such as current user, container name, container ID, PDBs, database version, instance name, and instance status.

1.  From `$ORACLE_HOME/bin`, log in to the SQL command line as *SYSDBA*. 

    ```
    $ <copy>./sqlplus / as sysdba</copy>
    ```

	```
	SQL*Plus: Release 23.0.0.0.0 - Production on Fri Oct 4 18:57:25 20XX
	Version 23.4.0.24.05

	Copyright (c) 1982, 2024, Oracle.  All rights reserved.


	Connected to:
	Oracle Database 23ai Enterprise Edition Release 23.0.0.0.0 - Production
	Version 23.4.0.24.05

	SQL>
	```

1.  Check the current user connected to the database.  

    ```
    SQL> <copy>SHOW user</copy>

    USER is "SYS"
    ```

1.  View the container name and the container id.

    ```
    SQL> <copy>SHOW con_name</copy>

    CON_NAME
    ------------------------------`  
    CDB$ROOT
    ```

    ```
    SQL> <copy>SHOW con_id</copy>

    CON_ID
    ------------------------------
    1 
    ```

1.  View all PDBs in the CDB.

    ```
    SQL> <copy>SHOW pdbs</copy>
    ```

	```
		CON_ID CON_NAME                  OPEN MODE  RESTRICTED
	---------- ------------------------- ---------- ----------
			 2 PDB$SEED                  READ ONLY  NO
			 3 ORCLPDB                   READ WRITE NO
	```

1.  Check the version of the core library components. 

    ```
    SQL> <copy>SELECT banner_full FROM v$version;</copy>
    ```
    ```    
    BANNER_FULL
    ------------------------------------------------------------------------
	Oracle Database 23ai Enterprise Edition Release 23.0.0.0.0 - Production
	Version 23.4.0.24.05
    ```

1.  Verify that your Oracle Database is a multitenant container database.   

    ```
    SQL> <copy>SELECT name, cdb, con_id FROM v$database;</copy>    
    ```
    ```
    NAME      CDB     CON_ID
    --------- --- ----------
    ORCL      YES          0
    ```

    The value *0* indicates that the data pertains to the entire CDB.

1.  View the instance name and the status of the CDB.

    ```
    SQL> <copy>SELECT instance_name, status, con_id FROM v$instance;</copy>
    ```
    ```
    INSTANCE_NAME    STATUS           CON_ID
    ---------------- ------------ ----------
    orcl             OPEN                  0
    ```

In this lab, you connected to the SQL command line of your Oracle Database and checked container details, such as current user, container name, container ID, PDBs, and so on.

You may now **proceed to the next lab**.

## Acknowledgments

 - **Author** - Manish Garodia, Database User Assistance Development
 - **Contributors** - Daniela Hansell, Ashwini R, Jayaprakash Subramanian <if type="hidden">Suresh Rajan, Dharma Sirnapalli, Subhash Chandra, Steven Lemme</if>
 - **Last Updated By/Date** - Manish Garodia, October 2024
