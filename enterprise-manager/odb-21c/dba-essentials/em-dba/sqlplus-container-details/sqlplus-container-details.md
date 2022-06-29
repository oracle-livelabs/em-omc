# Connect to SQL Plus and View Container Details

## Introduction

This lab walks you through the steps to log in to SQL Plus and explore the Container Database (CDB) and Pluggable Database (PDB) with basic SQL commands.

*Estimated Time:* 10 minutes

### Objectives
- Set the environment variables and log in to the root container of CDB as the `SYS` user with *SYSDBA* privileges.
- From SQL Plus, explore the container and view details of CDB and PDB with basic SQL commands.

### Prerequisites
This lab assumes you have -
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed -
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Setup Compute Instance
    - Lab: Initialize Environment

**Note:** While connecting to Oracle Database, you do not require a password in the following scenarios.
 - The Oracle Database resides on the localhost.
 - The current user (for this lab, it is *oracle* user) is a member of the OSDBA group.


## Task 1: Set the Environment

To connect to Oracle Database and run SQL commands, set the environment first.

1. Log in to your host as *oracle*, the user who can perform database administration.

2. Open a terminal window and change the current working directory to `$ORACLE_HOME/bin`. 

	```
	$ <copy>cd /u01/app/oracle/product/21.0.0/dbhome_1/bin</copy>
	```

3. Run the command *oraenv* to set the environment variables.

	```
	$ <copy>./oraenv</copy>
	```

4. Enter the Oracle SID *orcl*.

	```
	ORACLE_SID = [oracle] ? <copy>orcl</copy>
	The Oracle base has been set to /u01/app/oracle
	```

	This command also sets the Oracle home path to `/u01/app/oracle/product/21.0.0/dbhome_1`.

You have set the environment variables for the active terminal session. You can now connect to Oracle Database and run the commands.

**Note:** Every time you open a new terminal window, you must set the environment variables to connect to Oracle Database from that terminal. Environment variables from one terminal do not apply automatically to other terminals.

Alternatively, you may run the script file `.set-env-db.sh` from the home location and enter the number for `ORACLE_SID`, for example, *3* for `orcl`. It sets the environment variables automatically. 

## Task 2: Connect to SQL Plus and Explore the Container

1.  From `$ORACLE_HOME/bin`, log in to SQL Plus as *SYSDBA*. 

    ```
    $ <copy>./sqlplus / as sysdba</copy>
    ```

    ```
    SQL*Plus: Release 21.0.0.0.0 - Production on Tue Sep 28 08:23:15 2021
    Version 21.3.0.0.0

    Copyright (c) 1982, 2021, Oracle.  All rights reserved.

    Connected to:
    Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production
    Version 21.3.0.0.0

    SQL>
    ```

2.  View the current user of Oracle Database.  

    ```
    SQL> <copy>show user</copy>

    USER is "SYS"
    ```

3.  View the container name and the container id.

    ```
    SQL> <copy>show con_name</copy>

    CON_NAME
    ------------------------------`  
    CDB$ROOT
    ```

    ```
    SQL> <copy>show con_id</copy>

    CON_ID
    ------------------------------
    1 
    ```

4.  View all PDBs in the CDB.

    ```
    SQL> <copy>show pdbs</copy>
    ```

	``` 
		CON_ID CON_NAME                  OPEN MODE  RESTRICTED
	---------- ------------------------- ---------- ----------
			 2 PDB$SEED                  READ ONLY  NO
			 3 ORCLPDB                   READ WRITE NO
	```

5.  Check the version of the core library components. 

    ```
    SQL> <copy>select banner from v$version;</copy>
    ```
    ```    
    BANNER
    ------------------------------------------------------------------------
    Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production
    ```

6.  Verify that your Oracle Database is a multitenant container database.   

    ```
    SQL> <copy>select name, cdb, con_id from v$database;</copy>    
    ```
    ```
    NAME      CDB     CON_ID
    --------- --- ----------
    ORCL      YES          0
    ```

    The value *0* indicates that the data pertains to the entire CDB.

7.  View the instance name and the status of the CDB.

    ```
    SQL> <copy>select instance_name, status, con_id from v$instance;</copy>
    ```
    ```
    INSTANCE_NAME    STATUS           CON_ID
    ---------------- ------------ ----------
    orcl             OPEN                  0
    ```

In this lab, you have learned how to connect to the SQL command-line and view the container details with basic SQL commands.

You may now **proceed to the next lab**.

## Acknowledgements
- **Author** - Manish Garodia, Principal User Assistance Developer, Database Technologies
- **Contributors** - Suresh Rajan, Kurt Engeleiter, Dharma Sirnapalli, Subhash Chandra, Steven Lemme
- **Last Updated By/Date** - Manish Garodia, December 2021
