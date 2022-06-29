# Database Instance and Memory Management

## About this Workshop

This workshop features the basic know-how of the Oracle Database Instance and guides you to manage the initialization parameters and memory structures of your Oracle Database.  

Manage the initialization parameters to perform critical tasks on your Oracle Database, such as administer the Database Instance and adjust the size of memory components, in order to improve the performance of the database.

*Estimated Workshop Time:* 1 hour 40 minutes

### Objective
Perform the following from both SQL command line and Oracle Enterprise Manager Cloud Control (Oracle EMCC) - 
- Shut down and start the database instance.
- View and modify the initialization parameters.
- Administer the Automatic Memory Management.

### Prerequisites

This lab assumes you have
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- Or an Oracle account to reserve the workshop on LiveLabs

## Appendix 1: Overview of Oracle Database Instance and Memory Management

An Oracle Database system consists of an Oracle Database and an instance, also known as *Database Instance*. The instance contains a set of background processes that operates on the stored data and the shared allocated memory that the processes use. You can start up or shut down the Oracle instance as the `SYS` user with SYSDBA privileges.

Each instance has an instance ID, also known as a *System ID (SID)*. There are multiple Oracle Databases on a host computer, each with its own set of data files. You must identify the instance to which you want to connect. For a local connection, you identify the instance by setting operating system environment variables `ORACLE_SID` and `ORACLE_HOME`.  

### Starting the Database Instance

The process of starting the instance is as follows.

1.  **Start** the instance using Oracle EMCC or SQL\*Plus command.  Oracle reads the initialization parameter file, allocates the *System Global Area (SGA)* memory, and starts the background processes for the instance.  

2.  The database is then in the **mount** state. This state enables the administrators to perform certain functions which they cannot perform when other users are accessing the database.  

3.  After mounting the database, the instance **opens** the redo log files and datafiles for the database. The database is now open and available for all user access.

The default startup mode for the database is `OPEN` which completes the above three stages in sequence. You can start the instance in the following modes.

- `NOMOUNT`— Starts up the instance without mounting the database.
- `MOUNT`— Starts up the instance and mounts the database, but leaves it closed. This state allows certain DBA activities, but does not allow general access to the database.
- `OPEN` — Starts up the instance, mounts and opens the database. You can do this in unrestricted mode, allowing access to all users, or in restricted mode, allowing access for database administrators only.
- `FORCE`— Forces the instance to start up after a startup problem.

### Shutting down the Database Instance

The process of shutting down the instance is the reverse of starting it. It includes the following stages.

1.  Shut down the database using Oracle EMCC or SQL\*Plus command. Datafiles and log files are closed. Users can no longer access the database after it is shut down.  

2.  The Oracle instance dismounts the database and updates relevant entries in the control file to record a clean shutdown. The control file is closed. The database is now closed and only the instance remains.  

3.  The Oracle instance stops the background processes of the instance and deallocates the shared memory used by the SGA.

You can shut down an instance in the following modes.

- `NORMAL` — The default shutdown mode. It takes long time to shut down.
- `IMMEDIATE` — Shuts down the database quickly.
- `TRANSACTIONAL` — Completes the active transaction and then shuts down the database.
- `ABORT` — Shuts down the database instantaneously without waiting for the transactions to complete.   
	**Note:** Use it in emergency situations only because it can cause loss of data.
- `TIMEOUT` — Waits for active users to disconnect or for the transactions to complete within a limited waiting period. If all events blocking the shutdown do not occur within one hour, the `SHUTDOWN` operation aborts.

### Initialization Parameters

Managing Database Instance includes configuring parameters that affect the basic operation of the Oracle instance. These parameters are called *initialization parameters*. The Database Instance reads the initialization parameters from the `INIT.ORA` file at startup.

During installation, when you select a preconfigured database workload available in Oracle Database Configuration Assistant (DBCA), the initialization parameters are optimized for typical use in the environment that you specified. As the number of database users increases and the workload increases, you might have to alter some initialization parameters.  

The initialization parameters are a very important part of Oracle Database. You must have the basic parameters set for the database to run properly and efficiently. The database will not startup without a valid initialization parameter file. The file is only read at startup and contains the information required to set up the SGA.

The following are two types of parameter files:

- **Server parameter file (SPFile)**- This is the preferred form of initialization parameter file. It is a binary file that can be written to and read by the database. It is stored on the host computer on which Oracle Database is running.

	**Note:** When changing an initialization parameter in the SPFile, you can also specify that the in-memory value be changed, so that your change is reflected immediately in the current instance. If you do not change the in-memory value, then the change does not take effect until you shut down and restart the database.

- **Text initialization parameter file (PFile)**- This type of initialization parameter file can be read by the database server, but it is not written to by the server. In this file, you can set initialization parameters with a text editor for them to be persistent across shutdown and startup.

Oracle reads the initialization parameter values from either a **SPFile** or **PFile** when the Oracle Database starts. The parameters  inform the Oracle Database on how much memory to allocate, where to put files related to the database and the location of existing datafiles.

### About Instance Memory Management

The size of the instance memory structures affects the performance of the Oracle Database server and is controlled by initialization parameters. When you create a database with DBCA, the memory parameters are automatically set to optimal values based on the database workload, such as data warehouse, general purpose, or transaction processing. However, as your database usage expands, you can alter the settings of the memory parameters.  

The basic memory structures associated with Oracle Database include:

-   **System Global Area (SGA)**  
    The SGA is a group of shared memory structures, known as SGA components, that contain data and control information for one Oracle Database instance. The SGA is shared by all server and background processes. Examples of data stored in the SGA include cached data blocks and shared SQL areas.
-   **Program Global Area (PGA)**  
    The PGA is a memory region that contains data and control information for a server process. It is nonshared memory created by Oracle Database when a server process is started. Access to the PGA is exclusive to the server process. There is one PGA for each server process. Background processes also allocate their own PGAs. 

### Automatic Memory Management

Oracle Database can manage the SGA memory and instance PGA memory . You designate only the total memory size to be used by the instance, and the database dynamically exchanges memory between the SGA and the instance PGA as needed to meet processing demands. This capability is referred to as *Automatic Memory Management*. In this memory management mode, the database also dynamically tunes the sizes of the individual SGA components and the sizes of the individual PGAs.  

Upon installation, you can let Oracle Database manage the memory automatically, or select to manually configure the instance memory structures. For both manual and automatic memory management, Oracle Database sends alerts which identify memory sizing problems that require your attention.  

The simplest way to manage instance memory is to allow the Database Instance to automatically manage and tune it for you. You set a target memory size initialization parameter (`MEMORY_TARGET`) and optionally a maximum memory size initialization parameter (`MEMORY_MAX_TARGET`). The total memory that the instance uses remains relatively constant, based on the value of `MEMORY_TARGET`, and the instance automatically distributes memory between the system global area (SGA) and the instance program global area (instance PGA). As memory requirements change, the instance dynamically redistributes memory between the SGA and instance PGA.

If you do not enable Automatic Memory Management for your Oracle Database, then you must manually set the memory for both SGA and PGA. While installing Oracle Database, the installer gives you an option to enable Automatic Memory Management. If you did not enable Automatic Memory Management during database installation, you can enable it as explained in this workshop.

Click on the next lab to **Get Started**.

## Learn More

-   [Basic Initialization Parameters](https://docs.oracle.com/en/database/oracle/oracle-database/21/refrn/basic-initialization-parameters.html)
-   [Oracle Database 21c - Database Concepts](https://docs.oracle.com/en/database/oracle/oracle-database/21/cncpt/index.html)

## Acknowledgements

- **Author** - Manisha Mati, Senior User Assistance Developer
- **Contributors** - Suresh Rajan, Manish Garodia, Kurt Engeleiter, Suresh Mohan, Jayaprakash Subramanian, Ashwini R
- **Last Updated By/Date** - Manisha Mati, January 2022
