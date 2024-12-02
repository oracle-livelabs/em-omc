# Access container home page

## Introduction

This lab walks you through the steps to access the container home page from Oracle Enterprise Manager Cloud Control (EM). You will also learn how to switch between containers and manage your favorites.

Estimated time: 15 minutes

### Objectives

 - Access container home page from Oracle Enterprise Manager
 - Switch between home pages for Container Database (CDB), Pluggable Database (PDB), and the database instance
 - Check out the history
 - Add pages to and remove pages from favorites

### Prerequisites

This lab assumes you have -

 -   An Oracle Cloud account
 -   Completed all previous labs successfully
 -   Logged in to Oracle Enterprise Manager in a web browser as *sysman*

> **Note**: [](include:example-values)

## Task 1: Access container home page

In this task, you will access the home page for the database instance, *orcl.us.oracle.com*.

1.  From the **Targets** menu at the top, select **Databases** to open the Databases page.

    ![Databases menu](./images/em-dbhome-001-db-menu.png " ")

	The Databases page displays all database systems added to Oracle Enterprise Manager as managed targets. 

1.  Click the expand/collapse triangle next to the database instance name and then expand the Pluggable Databases. The list displays all PDBs under the selected container.

    ![Databases list](./images/em-dbhome-002-db-list.png " ")

1.	You can click a database name link to access the corresponding home page, that is, the database instance home page or the PDB home page.

	For this task, click the database instance name, for example *orcl.us.oracle.com*, to access the instance home page.

    ![Database instance home page](./images/em-dbhome-003-instance-home.png " ")

	Similarly, you can click the PDB name on the Databases page to open the PDB home page.

You can perform various tasks depending on which home page you access. For example, from the database instance home page, you can monitor and administer your Oracle Database, such as start and shut down the database instance, open and close PDBs, manage the memory, modify initialization parameters, and so on.

From the CDB and the PDB home page, you can perform administrative tasks on the CDB and the PDB respectively.

## Task 2: Switch between containers

You can alter session and switch between containers in Oracle Enterprise Manager during the same login.

That is, from the database instance home page, you can switch to the CDB or PDB home page without logging out of Oracle Enterprise Manager. Similarly, from the PDB home page, you can switch to the CDB or to another PDB, if you have more target PDBs in Oracle Enterprise Manager.

In this task, you will switch between containers and open the CDB, the PDB, and the database instance home page.

1. On the container home page, click the small triangle next to the container name and select **All Containers**.

    ![All containers](./images/em-dbhome-004-all-containers.png " ")

1.  In the Switch Container window, select the CDB, *CDB$ROOT*, from the list and click **OK**.

	![Switch container - CDB](./images/em-dbhome-005-switch-container-cdb.png " ")

	It brings up the CDB home page.

    ![CDB home page](./images/em-dbhome-006-cdb-home.png " ")

	Similarly, follow the same steps to open the PDB home page.

1.  Click the small triangle next to the CDB name and select **All Containers**.

    ![All containers - CDB](./images/em-dbhome-007-all-containers-cdb.png " ")

1. 	 In the Switch Container window, select the PDB, for example *ORCLPDB*, from the list and click **OK**.

    ![Switch container - PDB](./images/em-dbhome-008-switch-container-pdb.png " ")

	It brings up the PDB home page.

    ![PDB home page](./images/em-dbhome-009-pdb-home.png " ")

	> **Note:** The Switch Container option is useful if you have many containers in your database instance. However, you can move directly from one container to another instead of going through this option.

1.	On the PDB home page, click the small triangle next to the PDB name and select the CDB, *CDB$ROOT*.

    ![Select CDB$ROOT](./images/em-dbhome-010-pdb-select-cdb.png " ")

	It opens the CDB home page.

    ![CDB home page](./images/em-dbhome-006-cdb-home.png " ")

1.	Click the **History** menu at the top and select the database instance name, *orcl.us.oracle.com*.

    ![History menu](./images/em-dbhome-011-history.png " ")

	It opens the database instance home page.

    ![Database instance home page](./images/em-dbhome-003-instance-home.png " ")

	> **Note:** You can open a recently visited page from any location in Oracle Enterprise Manager using the **History** menu.

## Task 3: View target information

To view information about a target or to monitor a target, open the target home page. From the home page, you can view details about the target, such as the Oracle home location, agent details, host system, listener information, and so on. 

In this task, you will view target information for the database instance, the CDB, and the PDB.

1.  On the container home page, from the **Oracle Database** menu, select **Target Information** to view details of the database instance.

    ![Target information - database instance](./images/em-dbhome-012-container-target-menu.png " ")

    Alternatively, you can also click the target information icon (the circle with an 'i' in it) next to the container name.

    ![Container information](./images/em-dbhome-013-container-target-inf.png " ")

	Press **Esc** on your keyboard or click the cross (x) icon on the Target Information window to close it.

1.  Click the small triangle next to the database instance name and select the CDB, *CDB$ROOT* to go to the CDB home page.

    ![Select CDB$ROOT](./images/em-dbhome-014-orcl-select-cdb.png " ")

1.  On the CDB home page, from the **Oracle Database** menu, select **Target Information** to view details of the CDB.

    ![Target information - CDB](./images/em-dbhome-015-cdb-target-menu.png " ")

    Alternatively, you can click the target information icon (the circle with an 'i' in it) next to the CDB name, *CDB$ROOT*.

    ![CDB information](./images/em-dbhome-016-cdb-target-inf.png " ")

	Press **Esc** on your keyboard or click the cross (x) icon on the Target Information window to close it.

1.  Click the small triangle next to the CDB name and select the PDB, *ORCLPDB* to go to the PDB home page.

    ![Select ORCLPDB](./images/em-dbhome-017-cdb-select-pdb.png " ")

1.  On the PDB home page, from the **Oracle Database** menu, select **Target Information** to view details of the PDB.

    ![Target information - PDB](./images/em-dbhome-018-pdb-target-menu.png " ")

    Alternatively, you can click the target information icon (the circle with an 'i' in it) next to the PDB name, *ORCLPDB*.

    ![PDB information](./images/em-dbhome-019-pdb-target-inf.png " ")

	Press **Esc** on your keyboard or click the cross (x) icon on the Target Information window to close it.

## Task 4: Manage favorites

Using the favorites option, you can bookmark pages in Oracle Enterprise Manager for quick access.

> **Note:** Go to the page that you want to add to or remove from favorites.

In this task, you will add the CDB home page and the PDB home page to favorites and then remove the CDB home from favorites. Currently, you are on the PDB home page.

1. Add the PDB home page to favorites. Click the **Favorites** menu (star icon) at the top and select **Add Page to Favorites**.

    ![Add page to Favorites](./images/em-dbhome-020-add-page-to-fav.png " ")

    The window displays a confirmation message indicating that you have added the current page to favorites.   

1.  Go to the CDB home page. Click the small triangle next to the PDB name and select the CDB, *CDB$ROOT*.

    ![Select CDB$ROOT](./images/em-dbhome-010-pdb-select-cdb.png " ")

1. Add the CDB home page to favorites. Click the **Favorites** menu (star icon) and select **Add Page to Favorites**.

    ![Add page to Favorites](./images/em-dbhome-020-add-page-to-fav.png " ")

1.	Click the **History** menu at the top and select the database instance name, *orcl.us.oracle.com*.

    ![History menu](./images/em-dbhome-011-history.png " ")

	It opens the database instance home page.

1. Add the database instance home page to favorites. Click the **Favorites** menu (star icon) and select **Add Page to Favorites**.

    ![Add page to Favorites](./images/em-dbhome-020-add-page-to-fav.png " ")

    You have added the PDB, the CDB, and database instance home pages to favorites. Similarly, you can remove pages from favorites. Currently, you are on the database instance page.

1.  Remove the database instance home page from favorites. Click the **Favorites** menu (star icon) and select **Remove Page from Favorites**.  
	You will notice that the menu displays the CDB, the PDB, and the database instance as favorites.    

    ![Remove database instance from Favorites](./images/em-dbhome-021-remove-fav-instance.png " ")

    The window displays a confirmation message indicating that you have removed the page from favorites. You can also remove favorites using the **Manage Favorites** option.

1.	Click the **Favorites** menu (star icon) and select **Manage Favorites**.

    ![Manage Favorites menu](./images/em-dbhome-022-manage-favs-menu.png " ")

1.  In the **Manage Favorites** window, select the page that you want to remove, for example *CDBROOT*, and click **Remove Selected**.
    ![Remove CDB from Favorites](./images/em-dbhome-023-manage-fav-remove-cdb.png " ")

	Click **OK** to remove the CDB home page from favorites.

	> **Note:** In the **Manage Favorites** window, you can select pages one-by-one and then click **Remove Selected**. Finally, when you click **OK**, it removes the pages from favorites.

Congratulations! You have successfully completed of this workshop on *Database administration with Oracle Enterprise Manager*.

In this workshop, you learned about some basic administration of Oracle Database from Oracle Enterprise Manager, such as:
 - View container details from the SQL command line
 - Administer managed targets in Oracle Enterprise Manager
 - Add and remove Oracle Databases and Listeners as targets
 - Access the database instance, CDB, and PDB home pages
 - Switch between containers
 - Add and remove favorites in Oracle Enterprise Manager
 - Check recent history

## Acknowledgments

 - **Author** - Manish Garodia, Database User Assistance Development
 - **Contributors**: Daniela Hansell, Ashwini R, Jayaprakash Subramanian <if type="hidden">Suresh Rajan, Steven Lemme</if>
 - **Last Updated By/Date**: Manish Garodia, October 2024
