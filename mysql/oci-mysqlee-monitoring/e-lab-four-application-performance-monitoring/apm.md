## Introduction

In this lab, you will explore Database Management for External MySQL DB System. Database Management provides a single-pane-of-glass view of your cloud and on-premises databases in OCI, helping you monitor and detect issues efficiently.

Below are some of the key tasks you will, categorized under database monitoring and management.

Estimated time: 20 minutes

### Objectives

- Use Oracle Cloud Infrastructure Database Management to manage a fleet of MySQL Databases and drill down to a single database for further investigation
- Explore Database Management Summary
- Analyze all Metrics of an External MySQL DB system
- Review Configuration variables of an External MySQL DB system
- Explore Alarm definitions of an External MySQL DB system
- Diagnose database performance issues quickly with Performance Hub

## Task 1: Getting Started with Database Management

1. Login to the Oracle Cloud Console, click the **Navigation Menu** in the upper left, navigate to **Observability & Management**, and select **Database Management**.

     ![Database Management](./images/dbmgmt.png " ")

2. The **MySQL databases** tile (on the **Overview** page) displays the total number of External MySQL DB systems and HeatWave MySQL Databases in the compartment and region for which Database Management is enabled.

     ![Database Management Overview](./images/overview.png " ")

## Task 2: Monitoring a Fleet of MySQL Databases

1. On the left pane, click **Diagnostics & Management** to navigate to the **HeatWave & MySQL fleet summary** page.

     ![Compartment](./images/nav.png " ")

2. The dbmgmt compartment is selected by default in the Compartment field. Set the **Compartment** to **dbmgmt** following the navigation -
     ![Compartment](./images/navigation.png " ")

3. The following tiles are available on the **Fleet Summary** page:

    - **Inventory**: Displays the number of MySQL Databases in the compartment.
    - **Monitoring Status**: Displays the availability status of the managed MySQL Databases in the compartment.
    - **Resource Usage**: Displays a summary of the overall CPU utilization, Storage and Memory allocation for the selected time period on the top-left corner of the page.
    - **Alarms**: Displays the total number of open database alarms in the compartment and the number of alarms by severity.

     ![Fleet Summary](./images/fleet-summary.png " ")

4. Below the tiles, the list of HeatWave and External MySQL DB systems for which Database Management is enabled is displayed along with the following information:
    - **DB system name**: Name of the DB system.
    - **Monitoring status**: Monitoring status of the DB system.
    - **HeatWave**: HeatWave enablement status. Indicates whether a HeatWave cluster is attached to the HeatWave DB system. This information is only displayed for HeatWave DB systems.
    - **HeatWave nodes**: Number of HeatWave nodes in the HeatWave cluster. This information is only displayed for HeatWave DB systems.
    - **Average statements**: Displays the Average number of SQL statements executed per minute.
    - **Average statement latency**: Displays the Average latency (in milliseconds) for the executed SQL statements.
    - **CPU utilization**: Displays the Percentage of CPU utilized by the DB system.
    - **Storage utilization**: Displays the Percentage of storage utilized by the DB system.
    - **Memory utilization**: Displays the Percentage of memory utilized by the DB system.

## Task 3: Monitor a Single External MySQL DB system - Configuration variables

1. In the **Resources** page, click on the **Configuration variables** section. You can monitor the configuration variables that are currently used by running instances.

2. Configuration variables are the user, system, initialization, or service-specific variables that define the operation of the DB system.

     ![Operation Stats](./images/configuration-variables-home.png " ")

3. In the Configuration variables section, you can use filters on the left pane to filter the configuration variables.

     ![Operation Stats](./images/config-variables-filters.png " ")

4. Deselect the Hide unmodified variables check box to view the variables that were not modified. This check box is selected by default.

     ![Operation Stats](./images/configuration.png " ")

5. View the following configuration variable information:

    - **Name**: Name of the configuration variable.
     Click the Arrow icon adjacent to the name of the configuration variable to view the default and current value.

    - **Value**: Value of the configuration variable.
    - **Modified**: Check mark to indicate if the configuration variable was modified.
    - **Dynamic**: Check mark to indicate if the configuration variable is a dynamic variable, which means changing the variable does not require restarting the DB system.
    - **Configurable**: Check mark to indicate if the configuration variable is configurable.
    - **Source**: Source from which the configuration variable was most recently set. For information on the various types of sources, see Performance Schema variables_info Table.
    - **Time set**: Date and time the configuration variable was most recently set.

    ![Operation Stats](./images/view-config-variables.png " ")

## Acknowledgements

- **Author** - Sindhuja Banka, HeatWave MySQL Product Manager
- **Contributors** - Sindhuja Banka, Anand Prabhu, Sriram Vrinda
- **Last Updated By/Date** - Sindhuja Banka, March 2025
