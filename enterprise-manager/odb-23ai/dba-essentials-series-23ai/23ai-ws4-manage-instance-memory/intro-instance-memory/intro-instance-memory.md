<!-- Condition: EMCC -->

# Database Instance <if type="emcc">and Memory</if> Management

## About this workshop

<!-- Condition: EMCC -->

This workshop features the basic know-how of the Oracle Database Instance and guides you to view <if type="emcc">and manage</if> the initialization parameters <if type="emcc">and memory structures</if> of your Oracle Database. 

<!-- Building-Block: EMCC -->

<if type="emcc">
[](include:em-intro-about)
</if>

<!-- Condition: ORDS -->

<if type="db-actions">
This workshop helps you view a graphical representation of information about the database instance associated with a connection.

You use the instance viewer window in the [](var:prod_db_actions) console to view details of a database.

> **Note**: Available only if you sign in as a database user with DBA or PDBDBA privileges.
</if>

Estimated workshop time: 1 hour 40 minutes

### Objective
<!-- Condition: EMCC -->

In this workshop, you will do the following <if type="emcc">from both SQL command line and [](var:prod_emcc_full) (EM)</if>:
<if type="emcc"> -   Shut down and start the database instance</if>
 -   View <if type="emcc">and modify</if> the initialization parameters
<if type="emcc"> -   Administer Automatic Memory Management</if>

### Prerequisites

This lab assumes you have-

-   An Oracle Cloud account
	<!-- Condition: EMCC, ORDS -->
-   Oracle Database and <if type="emcc">[](var:prod_em)</if> <if type="db-actions">[](var:prod_db_actions)</if> installed

## Appendix 1: The Oracle Database Instance

An Oracle Database system consists of a database and an instance, also known as *database instance*. A database instance contains a set of background processes and services that manage the database files.

When a database instance starts, it reads the initialization parameters from a configuration file called `INIT.ORA`.

<!-- Building-Block: EMCC -->

<if type="emcc">

[](include:em-intro-db-instance)

### Starting the database instance

[](include:em-intro-start-db)

### Shutting down the database instance

[](include:em-intro-shutdown-db)

</if>

### About Initialization Parameters

An Oracle Database requires a set of configuration settings for basic operation and proper functioning. The database stores these configurations as initialization parameters to perform various tasks, for example, how much memory to allocate, where to store the data files, and so on. 

**Different types of Initialization Parameters**

Initialization parameters are of the following types:

-   Parameters that name entities such as files or directories
-   Parameters that set limits for a process, database resource, or the database itself
-   Parameters that affect capacity, such as the size of the SGA. These parameters are called variable parameters.

Oracle Database uses the following types of parameter files: 

 -  **Server parameter file (SPFile)** - This is the preferred form of initialization parameter file. It is a binary file that can be written to and read by the database. It is stored on the host computer on which Oracle Database is running.

	> **Note**: When changing an initialization parameter in the SPFile, you can also specify that the in-memory value be changed, so that your change is reflected immediately in the current instance. If you do not change the in-memory value, then the change does not take effect until you shut down and restart the database.

 - **Text initialization parameter file (PFile)** - This type of initialization parameter file can be read by the database server, but it is not written to by the server. In this file, you can set initialization parameters with a text editor for them to be persistent across shutdown and startup.

	> **Note**: An Oracle Database cannot start without a valid parameter file.

When an Oracle Database starts, it reads the initialization parameter values from either an **SPFile** or a **PFile**. 

<!-- Building-Block: EMCC -->

<if type="emcc">
## Appendix 2: Memory Management of Database Instance

[](include:em-intro-db-mem-mgmt)

### Automatic Memory Management

[](include:em-intro-auto-mem-mgmt)

</if>

<!-- Building-Block: ORDS -->

<if type="db-actions">
## Appendix 2: About Oracle Database Actions

[](include:ords-intro-about-db-actions)

</if>

Click the next lab to **Get Started**.

## Learn more

 - [Database Reference - Basic Initialization Parameters](https://docs.oracle.com/en/database/oracle/oracle-database/23/refrn/basic-initialization-parameters.html#GUID-D75F1A77-47E2-4F35-B145-44B3A10ED85C)

 - [Database Concepts - Oracle Instance Architecture](https://docs.oracle.com/en/database/oracle/oracle-database/23/cncpt/index.html)

<!-- Condition: ORDS -->

<if type="db-actions">
 - [About Oracle [](var:prod_db_actions)](https://docs.oracle.com/en/database/oracle/sql-developer-web/sdwad/about-sdw.html#GUID-AF7601F9-7713-4ECC-8EC9-FB0296002C69)
</if>

## Acknowledgments

<!-- Condition: EMCC -->

<if type="emcc">
 - **Author** - Aayushi Arora, Database User Assistance Development Team
 - **Contributors** - Manish Garodia, Jayaprakash Subramanian, Ashwini R
 - **Last Updated By/Date** - Aayushi Arora, October 2024
</if>

<!-- Condition: ORDS -->

<if type="db-actions">
 - **Author** - Aayushi Arora, Database User Assistance Development Team
 - **Contributors** - Jeff Smith, Manish Garodia, Manisha Mati
 - **Last Updated By/Date** - Aayushi Arora, September 2024
</if>

<!--

Legends -

    "prod_em": "Oracle Enterprise Manager",
    "prod_emcc_full": "Oracle Enterprise Manager Cloud Control",
    "prod_db_actions": "Database Actions",
    "prod_db_actions_full": "Oracle Database Actions",
    "prod_ords": "Oracle REST Data Services"


Building Blocks - 

	"em-intro-about": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-about-this-workshop.txt",
	"em-intro-db-instance": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-app1-db-instance.txt",
	"em-intro-shutdown-db": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-app1-shutdown-db-instance.txt",
	"em-intro-start-db": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-app1-start-db-instance.txt",
	"em-intro-auto-mem-mgmt": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-app2-auto-mem-mgmt.txt",
	"em-intro-db-mem-mgmt": "./../../../../dba-essentials-series-23ai/manage-instance-memory-23ai/intro-instance-memory/building-blocks-em/em-manage-instance-intro-app2-mem-mgmt-db-instance.txt",
	"ords-intro-about-db-actions": "./../../intro-db-instance/building-blocks-ords/ords-view-params-intro-app2-about-db-actions.txt",
	"ords-view-params-task-set-env-var": "./../../intro-db-instance/building-blocks-ords/ords-view-params-task-set-env-var.txt",
	"ords-task-view-init-params": "./../../intro-db-instance/building-blocks-ords/ords-view-params-task-view-initialization-params.txt"


Conditions - 

	"db-actions":"Database Actions",
	"emcc":"Oracle Enterprise Manager"

-->
