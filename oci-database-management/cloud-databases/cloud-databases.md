# Setting up Database Management for Oracle Cloud Databases

## Introduction

In this lab, you will go through the steps to set up Database Management for Oracle Cloud Databases.

Database Management service now also supports Oracle Cloud Databases, which are Oracle Databases on the following Co-managed Oracle Database Cloud solutions:
-	Bare Metal and Virtual Machine DB Systems
-	Exadata Cloud Service

![Architecture](./images/architecture.png " ")

Database Management features for Oracle Cloud Databases are available as part of two Management Options, which you can select when enabling Database Management.

The Full Management option includes all Database Management features for Oracle Database Enterprise Editions, including the following features. The Full Management option is also available for Oracle Database Standard Edition but doesn’t include Performance Hub features.

* Monitoring and managing capabilities for your fleet of databases.
* SKU features, which include advanced Performance Hub features, such as automatic database diagnostic monitor (ADDM) and blocking sessions and other features, such as scheduled fobs, tablespace monitoring, and database parameters.
* Features available as part of Basic Management.

The Basic Management option includes the following features:

* 14 basic monitoring metrics, such as CpuUtilization, StorageAllocated, and UserCalls. These metrics are displayed in the OCI Monitoring service and on the **Database Details** page of the database after Database Management is enabled.
* Active session history (ASH) analytics and SQL monitoring features in Performance Hub for multitenant container databases (CDBs). These features are not available for pluggable databases.

Estimated Time: 50 minutes

### Objectives

Set up Database Management to monitor and manage Oracle Databases on the following Co-managed Oracle Database Cloud solutions:

-   Bare Metal and Virtual Machine DB Systems

-   Exadata Cloud Service

### Prerequisites

This lab assumes you have completed the following labs:
* Oracle Database running on Oracle Database Cloud Service - Please check documentation to [Create a DB System] ( https://docs.oracle.com/en-us/iaas/Content/Database/Tasks/creatingDBsystem.htm#create).

## Task 1: Oracle Cloud Database-related Prerequisite Tasks

1. Set database monitoring user credentials in the Oracle Cloud Database. You must grant a database user, for example, DBSNMP, the privileges required to monitor and manage the Oracle Cloud Database.

    Connect to DBCS database as **SYSDBA** and execute the following :

    ```
    <copy>
    GRANT CREATE PROCEDURE TO dbsnmp;
    GRANT SELECT ANY DICTIONARY, SELECT_CATALOG_ROLE TO dbsnmp;
    GRANT ALTER SYSTEM TO dbsnmp;
    GRANT ADVISOR TO dbsnmp;
    GRANT EXECUTE ON DBMS_WORKLOAD_REPOSITORY TO dbsnmp;
    alter user dbsnmp account unlock;
    alter user dbsnmp identified by "<password>";
    </copy>
    ```

    The database user password checks in Database Management require the password to be Federal Information Processing Standards (FIPS) compliant:

    * Password length must be between 14 to 127 characters.
    * Password must have at least one lowercase, one uppercase, one digit, and one special character.

    ![Management Agents](./images/prereqs.png " ")

## Task 2: Assign IAM permissions

1.  From the Oracle Cloud console navigation menu located in the upper left, click **Identity & Security**. Under **Identity**, click **Policies**.

    ![Management Agents](./images/policy.png " ")

2. Click **Create Policy**. In the **Create Policy** dialog :

    ![Management Agents](./images/policy2.png " ")

     **Name:** Enter **Policy-for-dbmgmt**.

     **Description:** Enter **Policy for OCI DB Management**.

     **Compartment:** Select **root**.

     Enable **Show manual editor**.

     Enter the following in **Policy Builder**:

    ```
    <copy>
    Allow service dpd to read secret-family in compartment dbmgmt-demo
    Allow service dpd to manage objects in compartment dbmgmt-demo
    Allow group dbmgmt-group to manage dbmgmt-family in tenancy
    Allow group dbmgmt-group to read database-family in tenancy
    Allow group dbmgmt-group to manage vnics in tenancy
    Allow group dbmgmt-group to use subnets in tenancy
    Allow group dbmgmt-group to use network-security-groups in tenancy
    Allow group dbmgmt-group to use security-lists in tenancy
    Allow group dbmgmt-group to manage secret-family in compartment dbmgmt-demo
    Allow group dbmgmt-group to read buckets in compartment dbmgmt-demo
    </copy>
    ```

    Click **Create**.

## Task 3: Create OCI Vault

1.  From the Oracle Cloud Console **Navigation menu** located in the upper left, click **Identity & Security** and click **Vault**.

    ![Management Agents](./images/vault.png " ")

2.  On the **OCI Vaults** page, click **Create Vault**.

    ![Management Agents](./images/vault1.png " ")

3.  In the **Create Vault** dialog:
    ![Management Agents](./images/vault2.png " ")

    **Create in Compartment:** Select the name of compartment.

    **Name:** Enter **dbmgmt-vault**.

    Click **Create Vault**.

4.  Click the vault **dbmgmt-vault**.

    ![Management Agents](./images/vault3.png " ")

## Task 4: Create Key

1. On the **Vault Details** page, click **Create Key**. On the **Create Key** page, select all the defaults and enter **"Name" : dbmgmt-key**.

    ![Management Agents](./images/key.png " ")

    Click **Create Key**.

2. On the **Vault Details** page, confirm the **State** of key is **Enabled**. In the left pane, click **Secrets**.

    ![Management Agents](./images/key1.png " ")

## Task 5: Create Secret

1. Click **Create Secret**. On the **Create Secret** page, enter the following :

    ![Management Agents](./images/secret.png " ")

     **Create in Compartment:** Select Compartment Name

     **Name:** dbmgmt-secret

     **Description:** Monitoring user password

     **Encryption Key:** Select **dbmgmt-key**

     **Secret Type Template:** Select default

     **Secret Contents:** Enter the DBSNMP user password

    Click **Create Secret**.

2. Confirm the **Status** of **dbmgmt-secret** is **Active**.

    ![Management Agents](./images/secret1.png " ")

## Task 6: Create a Database Management private endpoint

You must create a private endpoint to connect Database Management to an Oracle Cloud Database.

The private endpoint is a representation of Database Management in the VCN in which the Oracle Cloud Database can be accessed, and acts as a VNIC with private IP addresses in a subnet of your choice. The private endpoint need not be on the same subnet as the Oracle Cloud Database, although, it must be on a subnet that can communicate with the Oracle Cloud Database.

Refer [Create a Database Management Private Endpoint]( https://docs.oracle.com/en-us/iaas/database-management/doc/perform-database-management-prerequisite-tasks.html#GUID-AC816009-3FE9-42A1-A133-83281E0790FD) for best practices.

1.  From the Oracle Cloud Console **Navigation menu** located in the upper left, click **Observability & Management**. Under **Database Management**, click **Administration**.

    ![Management Agents](./images/administration.png " ")

2.  On the left pane on the **Administration** page, click **Private Endpoint** and select the compartment in which you want to create the private endpoint.

    ![Management Agents](./images/endpoint.png " ")

3.  On the **Private Endpoints** page, click **Create Private Endpoint**.

4. In the **Create Private Endpoint** dialog:

    ![Management Agents](./images/endpoint1.png " ")

     **Name:** Enter **dbmgmtpe**.

     **Description:** Enter **Database Management Private Endpoint**.

     **Choose Compartment:** Select the compartment in which you want the private endpoint to reside.

     **Use this private endpoint for RAC databases:** Select this check box if you want to create a Database Management private endpoint for RAC Oracle Cloud Databases in the Virtual Machine DB system and Exadata Cloud service. For the purpose of this livelab/workshop, leave this option unchecked.

     **Virtual Cloud Network:** Select the VCN in which the Oracle Cloud Database can be accessed. Select **labVCN**.

     **Subnet:** Select a subnet within the selected VCN. Select **lab-public-subnet1**.

     **Network Security Group:** Optionally, select an NSG added to the Bare Metal or Virtual Machine DB system or the Exadata VM cluster. You can also click + Another Security Group to select another NSG. Leave as default.

     Click **Create Private Endpoint**.

5.  To view details of the private endpoint, click its name.

    ![Management Agents](./images/endpoint2.png " ")

## Task 7: Add security rules to enable communication

Add the following stateful security rules to the Security List:

Ingress rule for the Virtual Machine DB system's VCN: The Virtual Machine DB system's VCN (on port 1521) can receive incoming traffic from the Database Management private IP address (10.0.0.69/32) from any port.

Egress rule for the Database Management private endpoint: The Database Management private IP address (from any port) can send requests to the Virtual Machine DB system's VCN (10.0.0.0/16) on port 1521.

1.  From the Oracle Cloud Console **Navigation menu** located in the upper left, click **Oracle Database** and then **Bare Metal, VM and Exadata**.

    ![Management Agents](./images/seclist1.png " ")

2.  Click DB System **DBCS**.

    ![Management Agents](./images/seclist2.png " ")

3.  On the **DB System Details** page, click **labVCN**. The **Virtual Cloud Networks** page that lists all the subnets available in the VCN, is displayed.

    ![Management Agents](./images/seclist3.png " ")

4.  Click **lab-public-subnet1** on the **Virtual Cloud Network Details** page.

    ![Management Agents](./images/seclist4.png " ")

5.  On the **Subnet Details** page, click **Default Security List for labVCN** to go to **Security List Details** page. The **Security List Details** page lists the Security List Ingress and Egress Rules.

    ![Management Agents](./images/seclist5.png " ")

6.  Click **Add Ingress Rules** to add a Ingress rule for the Virtual Machine DB system's VCN. The Virtual Machine DB system's VCN (on port 1521) can receive incoming traffic from the Database Management private IP address (10.0.0.69/32) from any port.

    ![Management Agents](./images/seclist6.png " ")

     **Source Type:** Select **CIDR**

     **Source CIDR:** 10.0.0.69/32

     **IP Protocol:** Select **TCP**

     **Source Port Range:** Leave blank

     **Destination Port Range:** 1521

     **Description:** Connection from DB Management Private Endpoint

     Click **Add Ingress Rules**.

7.  From the Oracle Cloud Console **Navigation menu** located in the upper left, click **Observability & Management**. Under **Database Management**, click **Administration**.

    ![Management Agents](./images/administration.png " ")

8.  On the left pane on the **Administration** page, click **Private Endpoint** and click **dbmgmtpe** under Private Endpoints.

9.  On the **Private Endpoint Details** page, click **lab-public-subnet1**.

    ![Management Agents](./images/endpoint3.png " ")

10.  On the **Subnet Details** page, click **Default Security List for labVCN** to go to **Security List Details** page. The **Security List Details** page lists the Security List Ingress and Egress Rules.

    ![Management Agents](./images/seclist5.png " ")

11.  Click **Egress Rules** on the left navigation pane and then click **Add Egress Rules**. Enter following details:

    ![Management Agents](./images/seclist7.png " ")

     **Source Type:** Select **CIDR**

     **Source CIDR:** 10.0.0.0/16

     **IP Protocol:** Select **TCP**

     **Source Port Range:** Leave blank

     **Destination Port Range:** 1521

     **Description:** Egress from DB Management PE to DBCS

     Click **Add Egress Rules**.

## Task 8: Enable Database Management for Oracle Cloud Databases

1.  From the Oracle Cloud Console **Navigation menu** located in the upper left, click **Observability & Management**. Under **Database Management**, click **Administration**.

    ![Management Agents](./images/administration.png " ")

2.  On the **Managed Databases** page, click **Enable Database Management**.

    ![Management Agents](./images/manageddatabases.png " ")

3.  In the **Enable Database Management** dialog:

    ![Management Agents](./images/enabledbmgmt1.png " ")

     **Database Type:** Select **Bare metal, VM**.

     **Database System:** Select **DBCSDB**.

     **Database Home:** Select the name of Database Home.

     **Database:** Select the name of Database.

     **Service Name:** Select the Service Name.

    ![Management Agents](./images/enabledbmgmt2.png " ")

     **Database User Name:** DBSNMP

     **Use existing secret or Create new secret:** Select **Use existing secret**.

     **Database User Password Secret:** Select **dbmgmt-secret**.

     **Private Endpoint:** Select **dbmgmtpe**

     **Management Options:** Select **Full Management**. For information on Management Options, see [About Management Options]( https://docs.oracle.com/en-us/iaas/database-management/doc/enable-database-management.html#GUID-82E59C37-A1EA-4355-8216-769D22F8EFDD).

     Click **Enable Database Management**.

4.  A confirmation message with a link to the Oracle Cloud Database's **Work Requests** page is displayed. Click the link to monitor the progress of the work request.

    ![Management Agents](./images/enabledbmgmt3.png " ")

5.  You can verify if Database Management is successfully enabled on the following pages:

* **Database Management Administration** page: Select the appropriate option in the Deployment Type drop-down list. After Database Management is enabled, the Oracle Cloud Database is listed as a Managed Database. Click Database Name **PROD** to view **Managed Database Details**.

    ![Management Agents](./images/enabledbmgmt4.png " ")

    ![Management Agents](./images/enabledbmgmt7.png " ")

* **Database Details** page of the Oracle Cloud Database: **Database Management** is set to **Full**. Select **Metrics** on the left pane under Resources and check if the database metrics are displayed.

    ![Management Agents](./images/enabledbmgmt5.png " ")

    ![Management Agents](./images/enabledbmgmt6.png " ")

    For ASH Analytics & SQL Monitoring, click **Performance Hub** on the **Database Details** page. Note that the **Performance Hub** on the **Database Details** page does not include all the features that are available when **Performance Hub** is accessed from the Database Management **Managed Database Details** page.

    ![Management Agents](./images/enabledbmgmt8.png " ")    

## Acknowledgements

- **Author** - Vivek Verma, Principal Cloud Architect, North America Cloud Engineering
- **Contributors** - Vivek Verma, Sriram Vrinda, Pratima Chennupati
- **Last Updated By/Date** - Vivek Verma, September 2021
