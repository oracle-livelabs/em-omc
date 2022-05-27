# Manage Initialization Parameters

## Introduction

This lab walks you through the steps to manage initialization parameters in Oracle Enterprise Manager Cloud Control (Oracle EMCC). You can view and modify the initialization parameters to specify the properties of the Database Instance.  

Estimated Time: 15 minutes

### Objectives

View and modify the initialization parameters of the Database Instance from Oracle EMCC.

### Prerequisites

This lab assumes you have -
-   A Free Tier, Paid or LiveLabs Oracle Cloud account
-   Completed all the previous labs succesfully.
-   Oracle EMCC with Oracle Database 21c and listener added as managed targets.

## Task 1: View and modify the initialization parameters

To view and modify the values of the initialization parameters, log in to Oracle EMCC and perform the following steps. 

For this lab, view the initialization parameter `processes` and modify the values for the parameters `open_cursors` and `processes`.

1.  From the **Targets** menu, select **Databases**.

    ![Databases](./images/emcc-target-db.png " ")

    The Databases page displays a list of Oracle Databases added to Oracle EMCC as managed targets.   
	The values may differ depending on the system you are using.

    ![Database List](../shutdown-startup-instance/images/emcc-dbvalues.png " ")  

2.  Click on the Database Instance name, *orcl.us.oracle.com*, to open the instance home page.   
	The values may differ depending on the system you are using.

    ![Instance Homepage](./images/emcc-instance-hompage.png " ")  

3.  From the **Administration** menu, select **Initialization Parameters**.   
	The values may differ depending on the system you are using.

    ![Initialization Parameters](./images/initialize-parameters.png " ")  

    The Database login screen appears.

4.  The Database Login page displays the default option, *Named* Credential, selected. This option fills the          credential details automatically.   
	The values may differ depending on the system you are using.

    ![Login Credentials](./images/db-login.png " ")  

	Click **Login** to proceed.

    ![Initialization Parameters page](./images/initializeparameters-login.png " ")


	The Initialization Parameters window has two tabs:
    - **Current** — This default tab displays all initialization parameter values that are currently active and in memory for the Database Instance.
    - **SPFile** — This tab displays initialization parameter settings in the server parameter file (SPFILE). The window displays the SPFile tab if the Database Instance starts with the SPFile. But if the Database Instance starts with the PFile, the window does not display this tab.  

    **Note:** If the **Value** field for a parameter is not editable, it means that the parameter is not dynamic. You cannot change that parameter for the current instance.

5.  Click the **SPFile** tab to view parameters in the server parameter file.  

    ![SPFile tab](./images/spfile.png " ")  

    The window displays the initialization parameters of the container database.   
	The values may differ depending on the system you are using.

    **Note:** The server parameter file is a binary file that can be written to and read by Oracle Database and is the recommended format for the initialization parameter file.  

6.  On the **SPFile** tab, view the parameter `processes` by performing the following steps.

    - **Name**: *processes*  
	Enter the full name of the parameter. The **Name** field is case-sensitive.  
    - **Basic**: Select **Yes** to limit the display to basic initialization parameters.  
    - **Dynamic**: Select **Yes** to limit the display to dynamic initialization parameters.  
    You could select any category of initialization parameters from the **Category** dropdown to limit the search to that particular category.  

    Click **Go**.  

    ![View SPFile](./images/view-processes-spfile.png " ")  

	The window displays the value of the parameter `processes`. Similarly, you can view the values of other initialization parameters.

7.  Click the **Current** tab. In the **Name** field, enter the full name of the parameter *open_cursors*. Leave the defaults for the other fields and click **Go** to search for the parameter.

    ![Current tab](./images/currenttab.png " ")  

8.	Set the value for the parameter `open_cursors` to, for example, *350*.   
	The **Comments** field is optional. You may enter a text explaining the reason for the change.

    **Note:** Ensure that the **Apply changes in current running instance(s) mode to SPFile** option is not selected. Select this option only to modify the initialization parameter for the currently running instance and record the modifications in the server parameter file before the database restarts.  

    Click **Apply**. A confirmation message appears. The **Current** tab displays the updated value of `open_cursors`.  

    ![Value change confirmation](./images/valuechange-confirmation.png " ")

9.  Click the **SPFile** tab. In the **Name** field, enter the full name of the parameter *processes*. Leave the defaults for the other fields and click **Go** to search for the parameter.

    ![Value change processes](./images/edit-processes-spfile.png " ")  

10. Set the value of the parameter `processes` to, for example, *300*.  
	The **Comments** field is optional. You may enter a text explaining the reason for the change.

  **Note:** Ensure that the **Apply changes in SPFile mode to the current running instance(s)** option is not selected. Select this option only to modify the initialization parameter for the currently running instance and record the modifications in the server parameter file before the database restarts.  

    Click **Apply**. A confirmation message appears. The **SPFile** tab displays the updated value of `processes`.   

    ![Confirmation SPFile](./images/updated-spfile-message.png " ")

Similarly, you can view and modify the initialization parameters of the Container Database (CDB) and Pluggable Database (PDB) by switching between containers from the Database Instance home page.  

![Switch containers](./images/switch-containers.png " ")  

In a PDB, the Initialization Parameters page includes the PDB Modifiable column. Each initialization parameter that can be modified at the PDB level has a check mark in the PDB Modifiable column.

**Note:** Any initialization parameter in a PDB that does not have a check mark in the PDB Modifiable column can be set and modified only in the root. The value set in the root applies to the individual PDBs in the multitenant CDB.

Initialization parameters exist at both the CDB level and the PDB level. By default, initialization parameters at the PDB level inherit the value from the initialization parameters at the CDB level. 

You may now **proceed to the next lab.**

## Acknowledgements

- **Author** - Manisha Mati, Senior User Assistance Developer
- **Contributors** - Suresh Rajan, Manish Garodia, Kurt Engeleiter, Suresh Mohan, Jayaprakash Subramanian, Ashwini R
- **Last Updated By/Date** - Manisha Mati, January 2022
