# Configuration and Compliance Management
## Introduction
The objective of this lab is to highlight Oracle Enterprise Manager Cloud Control 13c’s Lifecycle Management capabilities related to configuration and security compliance management of managed targets. Each activity focuses on the different capabilities of an administrator.

*Estimated Lab Time:* 60 minutes

Watch the video below for a quick walk-through of the lab.
[](youtube:xEKClAvB-Yg)

### About Configuration and Compliance Management

Changes to configuration properties of database and host targets invariably happen, typically because of common events like patches and upgrades. At some point, a change to one component can negatively affect the overall system. Detecting the root cause becomes paramount. With Configuration Management, one can continuously monitor and track configuration drifts of targets against the reference configuration. Enterprise Manager automatically collects a comprehensive set of configuration properties of all managed targets across the data center and cloud.

With Compliance Management, one can run automated, continuous security checks based on industry standards and best practices, such as the Center for Internet Security (CIS), Security Technical Implementation Guide (STIG), Payment Card Industry Data Security Standard (PCI DSS), and Health Insurance Portability and Accountability Act (HIPAA). Reinforce industry standards such as STIG and CIS with custom policies to protect against threats, providing secure databases and hosts for applications. These security checks provide a compliance score to depict the overall compliance of targets against an industry-standard benchmark.

### Objectives

In this lab, you will perform the following steps

| Step No.                                      | Feature                                                                 | Approx. Time | Details                                                                                                                                                                                    | Value proposition                                                                                                   |
|-----------------------------------------------------------|-------------------------------------------------------------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| 1                                                         | Inventory & Usage details                                               | 10 minutes   | IT Manager wants to get an inventory of all existing databases managed by Enterprise Manager including different versions of databases, the number of instances deployed over a period of time | Reduce the number of different configuration sets, and increase standardization across the data center                  |
| 2                                                         | One-time database comparison                                            | 10 minutes   | Compare latest reference configuration to one or more targets to determine the configuration differences                                                                                   | Validate the configuration of the new database provisioned aligns with IT configuration policy                          |
| 3                                                         | Database Configuration drift management                                 | 20 minutes   | Compare the latest or saved target configuration to one or more targets                                                                           | Detect unauthorized changes in the databases that deviate from security best practices and ensure that configuration changes have been done properly|
| 4                                                         |  CIS standard Database security Compliance Standard | 10 minutes                    | Databases target                | Enhance the security posture of your database environments by securing the configuration of each target and aligning with industry-standard CIS Benchmark                                                       | Monitor security compliance for host targets from one customized dashboard |
| 5                                                         | Host Security Compliance                                  | 10 minutes   | Host target                                                                                                                       | Monitor security compliance for host targets from one reference compliance and implement innovative security compliance measures that meet or exceed applicable security regulations and standards |


###  Prerequisites
- A Free Tier, Paid, or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is set up with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository.

## Task 1: Inventory & Usage Details

### Overview

The IT Manager wants to get an inventory of all existing databases managed by the Enterprise Manager including different versions of databases, and the number of instances deployed over some time. This is to reduce the number of different configuration sets and increase standardization across the data center.

All the items in this step are read-only, the primary goal is to learn about inventory usage details within Enterprise Manager for all supported targets.

### Execution
1. On the browser window on the right preloaded with **Enterprise Manager**, if not already logged in, click on the **Username** field and login with the credentials provided below.

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

  ![](../initialize-environment/images/em-login.png " ")

2.  From the Enterprise menu, select **Configuration**, then select **Inventory and  Usage Details**.

  ![](images/configuration_inventoryusages_image1.png)

3.  In the **Show** filter menu, select **Databases** to see all database instances managed by Enterprise Manager.

  ![](images/em_compliance_config_alldbs_image.png " ")

4.  Analyze various database versions and the number of instances for each version or you can choose PDB 18.3 highlighted above page.

5.  Explore the pie chart to see the breakdown of database inventory by color-code percentages. Also, in the **Graphical View**, choose the**Trend** radio button to see the growth of a given database instance over a period of time.

 ![](images/em_config_compliane_dbtrends_image3.png " ")

 Click on Table View, further details explore.

 ![](images/em_config_compliane_dbtrends_image4.png)  

 Click **Close**.

6.  In the Details excel file table output below, you will see details as follows

      - Database instance name Target
      - Host on which this database is located
      - Database type - cluster or single instance
      - Database version number
      - OS specific details like OS version, platform, etc.
      - Most importantly, LOB/Department information
        The Details table gives more information about each Database instance for you to get a good understanding of the number of database targets deployed on a given host with OS version. If your organization uses properties like Lifecycle, Line of Business, or Department, then you will be able to determine the number of targets deployed for a given business unit. Explore these features to get a good handle on Inventory and Usage details.

7. Export inventory details to excel for reports.

  ![](images/em_configs_compliane_db_trends_image5.png " ")

(**Optional**) These inventory details can be exported to an excel file for offline analysis or sharing the report with management. With the excel report, you can filter based on the properties you are using to show department or line of business-specific assets allocation and usage.

  ![](images/ecm1_inventory_usage_details_report.png " ")

## Task 2: One-Time Database Comparison

### Overview

In this step, you will compare two database targets to determine configuration differences. One of the databases will act as a reference target that aligns with your configuration policy. Your objective is to compare initialization parameters to ensure it is compliant with the reference target.

### Execution

1.  Log into your Enterprise Manager as **sysman** as indicated in the Prerequisites step if not already done.

2.  From the Enterprise menu, select **Configuration**, then select **Configuration & Drift Management**

  ![](images/ecm2_one_time_database_comparison_menu.png " ")

3.  Review the different types of comparisons supported by Clicking on the **i** icon.

  ![](images/ecm2_one_time_db_comparison_menu1.png " ")

4.	Select the **One-Time Comparison Results** tab on the left side of the dashboard page. Click **Create Comparison**

  ![](images/em_one_create_comparison_image2.png " ")

5.  Choose the reference target that you want other targets to be compared with.

  ![](images/em_comp_confDrift_mgmt_image3.png " ")

6.  Identify the reference target to compare other targets.

  ![](images/ecm2_one_time_database_comparison_ref_target_image4.png " ")

  To begin with, filter ‘Target Type’ to Database Instance.

  ![](images/ecm2_one_time_database_comparison_ref_target_image5.png " ")

7.  Select **emrep.us.oracle.com** as the reference target.

  ![](images/ecm2_one_time_database_comparison_ref_target_image6.png " ")

8.  Choose Database Instance Template for Comparison Template.

  ![](images/em_comp_conf_drift_mgmt_image4.png)

9.  Provide a name for Comparison, for example, a name like **ECM002-Compare-Demo - One time Comparison**

  ![](images/ecm2_one_time_database_comparison_ref_target_image7.png)

10.  Add targets to be compared.

  ![](images/Em_comp_conf_drift_mgmt_target_image5.png " ")

11. Choose **finance.subnet.vcn.oraclevcn.com** target to compare with the reference target.

  ![](images/em_comp_conf_drifts_mgmt_image6.png " ")

  Once the target is chosen, it appears as below.
  Click **Submit**

  ![](images/em_one_time_database_comparison_referred_target_image8.png " ")

12.  The comparison would take a few seconds for selected targets and below are the results.

  ![](images/em_comp_conf_drift_mgmt_compared_image9.png " ")

   Click **Clear All** at Configuration Items(Differences).

  ![](images/em_comp_conf_drift_mgmt_compared_image10.png " ")

13. Filter configuration items to review only Initialization Parameters.

  You can see the differences in the Initialization Parameters between the two targets.

  Under the target compared column, you will see a few icons. The icons that appear in the view are mostly intuitive:

  - Equal sign means parameter properties are the same across the reference and target compared
  - Not equal sign indicates parameter properties are different across the reference and target compared
  - A red box with 1 (left only) means that the comparison did not find a matching item to compare, this means 2nd target doesn’t have a property configured to compare
  - A red box 2 (right only) means that the comparison did not find a matching item to compare to the second configuration

  ![](images/em_comp_conf_drift_mgmt_compared_image11.png " ")

14. Now, let us go to the Comparison and Drift Management dashboard page for further analysis of the results.

  ![](images/em_comp_conf_drift_mgmt_compared_image12.png " ")

15. On the dashboard page, the donut chart for Comparison Overview gives you the summary result. Click on the **donut chart** to analyze one-time comparison result details.

  ![](images/Em_Comp_Conf_Drift_Mgmt_Dashboard_Image_13.png " ")

  You should see the comparison definition you created on this page.

  ![](images/Em_Comp_Conf_Drift_Mgmt_Dashboard_Image_14.png " ")

16. (**Optional**) Export the comparison results into an excel report for offline analysis. On the One-Time Comparison Results page, highlight the definition and choose Export Results. You can choose the specific results to export.

  ![](images/Em_Comp_Conf_Drift_Mgmt_Dashboard_Image_15.png " ")

  After Exporting, Click **Cancel** to exit

17. (**Optional**) Exported results in excel for offline analysis look like this:

  ![](images/Em_Comp_Conf_Drift_Mgmt_one_time_comparison_Report_Image_15.png " ")

<!-- In this step, you learned steps to compare two database targets to determine configuration differences. This one-time database (or any Enterprise Manager managed targets) comparison will help you quickly determine specific configuration changes when compared with reference configuration. This is very ideal for troubleshooting any target configuration parameters. -->

## Task 3: Database Configuration Drift Management

### Overview

In this workshop, you will learn about continuous configuration drift monitoring of database targets against a reference target for initialization parameters using a customized configuration monitoring template.

1.  Log into your Enterprise Manager VM using the IP provided on your cheat sheet.

2.  Navigate to ***Enterprise >> Configuration >> Comparison & Drift Management***, Review the different types of comparisons supported.

  ![](images/ecm2_One_Tme_Database_Comparison_Menu.png " ")

   By Clicking on the **i** icon, review the different types of comparisons.

   -  Choose Templates left side of the panel of the Dashboard.

  ![](images/ecm2_One_Time_Db_Comparison_Menu-1.png " ")

3.  Go to the Templates library on the left panel, Clicking on Templates will navigate to Comparison Templates Page.

  ![](images/Compare_Drift_Template_Image_1.png " ")

4.  **Sort Name Alphabetically** look for Database Instance Template as shown below.

  ![](images/Compare_And_Drift_Template_Image_2.png " ")

   With Database Instance Template highlighted, choose **Create Like** to create a copy of this template for further customization. Provide a unique name to the new template and click **OK**.

  ![](images/Compare_And_Drift_Demo_Image_3.png " ")

5.  A complete copy of the Database Instance template with a unique name is created with all configuration items enabled, click on the **Template Name** field and copy with the name provided below.

  ```
   <copy>ECM003-Drift_Demo</copy>

  ```
  And click **Search**.

  ![](images/Compare_And_Drift_Demo_Image_4.png " ")

   Highlight this new template and click Edit.

  ![](images/Compared_And_Drift_Demo_Image_5.png " ")

6.  The configuration templates page appears below.

  ![](images/Compare_And_Drift_Demo_Image_6.png " ")

  To begin with, uncheck all configuration items.

  ![](images/Compare_And_Drift_Demo_Image_7.png " ")

7.  In this lab, we will customize this template and monitor configuration drift for two configuration items.

    Select the following three configuration items only:

    - Instance Caging Information
    - Instance Information
    - Initialization Parameters under Instance Information configuration item
    - Making sure **Instance Information** is highlighted
    - Click Save

  ![](images/Compare_And_Drift_Demo_Image_8-1.png " ")

8.  A new customized configuration drift monitoring template is created. This template can be used for drift monitoring.

  ![](images/Compare_And_Drift_Demo_Image_9-1.png " ")

  **Search** with Template name **ECM003-Drift_Demo** shows with a Confirmation page

  ![](images/Compare_And_Drift_Demo_Image_10-1.png " ")

9.  Go to the Drift Results tab and create a drift definition.

  ![](images/Compare_And_Drift_Demo_Image_10.png " ")

10. Click on **Create Definition** under Drift Management.

  ![](images/Compare_And_Drift_Demo_Image_11.png " ")

    - Choose Database Instance as the Target Type
    - Select the template created in the previous step
    - Click OK

  ![](images/Compare_And_Drift_Demo_Image_12.png " ")

11. On the drift definition details page, provide a unique name for the drift definition.

  ![](images/Compare_And_Drift_Demo_Image_13.png " ")

12. Under Source Configuration, do the following:

    -  Select ‘Latest Configuration’
    -  Click search to choose Source Target

  ![](images/Compare_And_Drift_Demo_Image_14.png " ")

13. Choose **emrep.us.oracle.com** as your source target. Click on **Select**

  ![](images/Compare_And_Drift_Demo_Image_15.png " ")

14. You will see Source Target (***emrep.us.oracle.com***) is selected that acts as your reference target.

  ![](images/Compare_And_Drift_Demo_Image_16.png " ")

15. Select **Save and Associate Targets** to select targets to be monitored.

  ![](images/Compare_And_Drift_Demo_Image_17.png " ")

16. Click on **Add** to select and associate a target to be monitored for drift.

  ![](images/Compare_And_Drift_Demo_Image_18.png " ")

17. Select **finance.subnet.vcn.oraclevcn.com** as the target.

  ![](images/Compare_And_Drift_Demo_Image_19-1.png " ")

18. Click **Select**, You will see one target selected to be associated with drift definition, Click OK.

  ![](images/Compare_And_Drift_Demo_Image_20-2.png " ")

19. A pop-up will ask for confirmation to save the association. Select **Yes**, This will start the association of this target to drift definition and initiate the configuration comparison and continuous drift monitoring.

  ![](images/Compare_And_Drift_Demo_Image_21-1.png " ")

20. Once you select Yes in the previous step, drift monitoring is in progress. Go to **Enterprise --> Configuration --> Comparison & Drift Management** Dashboard page. After a minute, refresh the page to see if the drift monitoring is completed. You should see a new or updated donut chart under the ‘Drifted Overview’ dashlet.

  ![](images/Compare_and_Drift_Demo_Image_22.png)

21. Click on the Drift Results tab on the left panel (2nd tab from the top). This page will show results for all drift definitions managed by this instance of Enterprise Manager. Identify the drift definition you created for further analysis of configuration drift results.

  ![](images/Compare_And_Drift_Demo_Image_23.png " ")

22. Review the drift details. Click on the **Drift Definition** (ECM003-Drift-Demo – Drift)

  ![](images/Compare_And_Drift_Demo_Image_23-1.png " ")

 For a detailed analysis of configuration drift. You can see the differences in the Initialization Parameters between the two targets.

  ![](images/Compare_AND_Drift_Demo_Image_24.png " ")

  Under the target compared column, you will see a few icons. The icons that appear in the view are mostly intuitive:

    - Equal sign means parameter properties are the same across the reference and target compared
    - Not equal sign indicates parameter properties are different across the reference and target compared
    - A red box with 1 (left only) means that the comparison did not find a matching item to compare, this means 2nd target doesn’t have a property configured to compare
    - A red box 2 (right only) means that the comparison did not find a matching item to compare to the second configuration


23. Go to Enterprise --> Configuration --> Comparison & Drift Management Dashboard page, Click on **Drift Results**

  ![](images/Compare_and_Drift_Demo_Image_22-1.png " ")

 (**Optional**) Export the comparison results into an excel report for offline analysis. On the Drift Results page, highlight the definition and choose Export Results, You can choose the specific results to export.

  ![](images/Compare_And_Drift_Demo_Image_25-1.png " ")

24. (**Optional**) Exported results in excel for offline analysis look like this:

  ![](images/Compare_And_Drift_Demo_Report_Image_26-1.png " ")

<!-- In this step, you learned about continuous configuration drift monitoring of database targets against a reference target for initialization parameters using a customized configuration monitoring template. This can be customized to align with your policies. By establishing a configuration drift definition, you can continuously monitor any configuration changes that can be potentially secure risk and remediate the drift immediately. -->



## Task 4: Database Security Compliance using CIS standard

### Overview

Compliance Management provides the ability to evaluate the compliance of targets and systems as they relate to business best practices for configuration, security, and storage.

<!-- In this lab, you will set up a compliance standard for monitoring security compliance of Oracle Database target and analyze the compliance score and violations -->

The terminology used in this Compliance specific workshop

### Center of Internet Security compliance(CIS) Standard

The Center for Internet Security compliance(CIS) is a set of Industry standards for IT systems and databases. CIS benchmark provides the baseline configurations to ensure oracle database compliance with CIS standards.  A compliance standard is a collection of checks or rules that follow broadly accepted best practices. It is the Cloud Control representation of a compliance control that must be tested against some set of IT infrastructure to determine if the control is being followed. This ensures that IT infrastructure, applications, business services, and processes are organized, configured, managed, and monitored properly. A compliance standard evaluation can provide information related to platform compatibility, known issues affecting other customers with similar configurations, security vulnerabilities, patch recommendations, and more. A compliance standard is also used to define where to perform real-time change monitoring.

A compliance standard is mapped to one or more compliance standard rules and is associated with one or more targets that should be evaluated.

### Compliance Standard Rule

A compliance standard rule is a specific test to determine if a configuration data change affects compliance. A compliance standard rule is mapped to one or more compliance standards.

### Execution

1.  Log into your Enterprise Manager VM using the IP provided on your cheat sheet.

2.  From the Enterprise menu, select **Compliance**, then select **Library**

  ![](images/CIS_Compliance_Welcome_Image_1-2.png " ")

3.  The compliance Standards tab contains all standards for various supported targets.

  ![](images/CIS_All_Compliance_Libraries_Image_2-2.png " ")

4.  In the Compliance Standards tab, search for Applicate To column **Database Instance** standard.

  ![](images/CIS_Db_Compliance_Libraries_Image_3-1.png " ")

5.  Select the **Oracle 19c Database CIS V1.0.0 - Level 1 - RDBMS using Traditional Auditing for Oracle Database** for Oracle Database standard.

  ![](images/CIS_Db_Compliance_19c_Libraries_Image_4-1.png " ")

6.  Create a copy of this database standard by clicking on **Create Like**. Give a unique name to the new standard.

  ![](images/CIS_Db_Compliance_19c_Create_Like_Image_5-1.png " ")

  Here, for example, **CIS_DEMO** you are creating to imply this is a new database standard. Also if you can change the name per your preference and Continue,

  ![](images/CIS_Db_Compliance_CIS_DEMO_Image_6-1.png " ")

7.  Review the various compliance rules for CIS Security standards grouped based on the configuration area.

  ![](images/CIS_Db_Compliance_CIS_DEMO_Standard_Details_Image_7.png " ")

  Click **Save**

  ![](images/CIS_Db_Compliance_Standard_Details_Save_Image_8-1.png " ")

8.  A new custom database CIS standard is created. Pop-up confirms the successful creation of these standards, Click **OK**

  ![](images/CIS_Db_Compliance_Standard_Create_Image_9-1.png " ")

9.  Select the newly created custom database standard. Click on **Associate Targets** to associate a database target for this newly created custom standard.

  ![](images/CIS_Db_Compliance_Associate_Target_Image_10-2.png " ")

10. When the Associate Target option is chosen, you will be taken to a page to add database targets, Click Add to add targets for association with this compliance standard.

  ![](images/CIS_Db_Compliance_Associate_Target_Image_11-2.png " ")

11. The list of targets chosen will show up on the target association page as shown below, Select **emrep.us.oracle.com** target to check the compliance security posture.

  ![](images/CIS_Db_Compliance_Select_Target_Image_13-2.png " ")

12. The list of targets chosen will show up on the target association page as shown below.

  ![](images/CIS_Db_Compliance_Add_Target_Image_14-2.png " ")

13. Click OK and a pop-up window shows to confirm an association. Click **Yes** to save the association which initiates a compliance check on this target by executing all the compliance rules associated with this compliance standard.

  ![](images/CIS_Db_Compliance_Confirm_Target_Image_15-2.png " ")

  The pop-up window shows the process status, Click **OK**

  ![](images/CIS_Db_Compliance_Confirm_Target_Image_16-1.png " ")

14. To check if the compliance check is complete, click the target number in the ‘Association Count’ column.

  ![](images/CIS_Db_Compliance_Confirm_Target_Image_17-1.png " ")

15. If the Evaluation status indicates **Enabled** and Transfer Status indicates **Successfully Done**, it means the compliance check is complete,
Click the **Cancel** button.

  ![](images/CIS_Db_Compliance_Confirm_Target_Image_18-1.png " ")

16. Go to the **Compliance Dashboard** page to check the CIS compliance posture. It takes about 5 minutes to show up in compliance dashboard results.

  ![](images/CIS_Db_Compliance_Dashboard_Image_20-1.png " ")

  Under the Compliance Summary panel at the bottom below page:

    - Explore various tabs to get an understanding of Frameworks, Standards, and target-level compliance
    - For any given standard, if there are Critical, Warning, or Minor Warnings
    - Click on the violation number to see more details of the violationS by clicking the numbers below each column's names

17. By Clicking on the Critical column number, you will see details like each violation, and the last evaluation date.

  ![](images/CIS_Db_Compliance_Dashb_Image_22-1.png " ")

 By clicking under Target Name.

  ![](images/CIS_Db_Compliance_Dashboard_Image_23-1.png " ")

18. Each rule name violated and rationale for the violation can be explored below, And also by clicking on Report.

  ![](images/CIS_Db_Compliance_Dashboard_Image_24-1.png " ")

  Compliance Evaluation Report will be populated on a separate page that can be used for further analysis of each rule passed or failed.

  ![](images/CIS_Db_Compliance_Report_Image_25-0.png " ")

 Under Result Details, clicking on the arrow mark at **emrep.us.oracle.com: CIS_DEMO** gives more information on individual rules.

  ![](images/CIS_Db_Compliance_Report_Image_26-1.png " ")


19. By going back to the **Compliance Dashboard** page,  click on the standard that you created **CIS_DEMO** in the previous steps to review further evaluations.

  ![](images/CIS_Db_Compliance_Dashboard_Image_27.png " ")

 Each rule result can undergo a detailed analysis as shown on this page.

  ![](images/CIS_Db_Compliance_Results_Image_28.png " ")

  All of these will give you a CIS Compliance security posture of database target.

  ## Task 5: Host Security Compliance

  ### Overview

  Compliance Management provides the ability to evaluate the compliance of targets and systems as they relate to business best practices for configuration, security, and storage.

  <!-- In this workshop, you will set up a compliance standard for monitoring security compliance of Oracle Linux host target and analyze the compliance score and violations -->

  Terminology Used in this Compliance specific workshop

### Compliance Standard

  A compliance standard is a collection of checks or rules that follow broadly accepted best practices. It is the Cloud Control representation of a compliance control that must be tested against some set of IT infrastructure to determine if the control is being followed. This ensures that IT infrastructure, applications, business services, and processes are organized, configured, managed, and monitored properly. A compliance standard evaluation can provide information related to platform compatibility, known issues affecting other customers with similar configurations, security vulnerabilities, patch recommendations, and more. A compliance standard is also used to define where to perform real-time change monitoring.

  A compliance standard is mapped to one or more compliance standard rules and is associated with one or more targets that should be evaluated.

### Compliance Standard Rule

  A compliance standard rule is a specific test to determine if a configuration data change affects compliance. A compliance standard rule is mapped to one or more compliance standards.

  ### Execution

  1.  Log into your Enterprise Manager VM using the IP provided on your cheat sheet.

  2.  From the Enterprise menu, select **Compliance**, then select **Library**

  ![](images/CIS_Compliance_Welcome_Image_1-2.png " ")

  3.  The compliance Standards tab contains all standards for various supported targets.

  ![](images/HIPAA_All_Libraries_Image_2.png " ")

  4.  In the Compliance Standards tab, search for the Keywords column for the word **HIPAA**

  ![](images/HIPAA_All_Libraries_Image_3-1.png " ")

  5.  Select Health Insurance Portability and Accountability Act (HIPAA) OL-7 standard, Click on Show Details.

  ![](images/HIPAA_Standard_Libraries_Image_4-1.png " ")

  6. After Selecting  **Show Details** Review Quickly scan various rules available for HIPAA out-of-box, Click on **Done**

  ![](images/HIPAA_Associate_Target_Image_6-1.png " ")

  7. Click on **Associate Targets** to associate a database target for this selected standard.

  ![](images/HIPAA_Associate_Target_Image_7-1.png " ")

  8. When the Associate Target option is chosen, you will be taken to a page to add host's targets.

    Click Add to add a target for association with this compliance standard.

  ![](images/HIPAA_Associate_Host_Target_Image_8.png " ")

  9.  There is one host called **emcc.marketplace.com**, select that target to associate.

  ![](images/HIPAA_Associate_Host_Target_Image_9-1.png " ")

  10.  Now, you see emcc.marketplace.com host target has been added. Now, let's complete the association workflow".

  Click **OK**.

  ![](images/HIPAA_Associate_List_Image_10-1.png " ")

  11. A pop-up window shows up to confirm an association. Click **Yes** to save the association which initiates a compliance check on this host target by executing all compliance rules associated with HIPAA compliance standards.

  ![](images/HIPAA_Confirm_Host_Target_Image_11-1.png " ")

  12. Once, the Compliance standard host target is been submitted you will be taken to a Compliance Library's page, which shows Compliance Standard is submitted for processing.

  ![](images/HIPAA_Compliance_Submit_Image_12-1.png " ")

  13. To check if the compliance processing is complete, click the target number in the **Association Count** column.

  ![](images/HIPAA_Validate_Submit_Image_13-1.png " ")

  14. If evaluation status **Enabled** and Transfer Status indicates **Successfully Done**, it means the compliance check is complete. Click the **Cancel** button.

  ![](images/HIPAA_Associate_Target_Success_Image_14-1.png " ")

  15. Go to the **Compliance Dashboard** page to check the compliance posture.

  ![](images/HIPAA_Associate_Target_Success_Image_15-1.png " ")

  16. Compliance Dashboard populates:

    - Under the Compliance Summary panel at the bottom, explore various tabs to get an understanding of Frameworks, Standards, target level compliance, and Average Compliance score too
    - For any given standard, if there are Non-Compliant Targets, Critical, Warning, or Minor Warnings, click on the violation number to see more details of the violation

      Click on the number under the **Critical** column. to see details of the host's critical violations.

  ![](images/HIPAA_Dashboard_Results_Image_17-1.png " ")

  17. Host's critical violations can be explored by clicking the **Target name** column arrow.

  ![](images/HIPAA_Crtical_Violations_Image_18-1.png " ")

      Each critical rule violations status can be seen on this pop-up page in detail.

      Click on  **Report**

  ![](images/HIPAA_Crtical_Violations_Image_19-1.png " ")

  18. It takes you to a separate page that shows Compliance Evaluation Report to see the reports with passed and failed rules.

  ![](images/HIPAA_Compliance_Report_Score_Image_20-1.png " ")

      And clicking on the **Result Details arrow emcc.marketplace.com: Health Insurance Portability and Accountability Act (HIPAA) OL-7** to see drill down evaluation details.

  ![](images/HIPAA_Compliance_Report_Score_Image_21-1.png " ")

  19. Individual rules can be further explored with select Enterprise Main Menu, then selecting Compliance and Results Page.

  ![](images/HIPAA_Main_Results_Image_22-1.png " ")

      It takes you to the Compliance Results page.

  ![](images/HIPAA_Compliance_Results_Image_23-1.png " ")

      Click on **Health Insurance Portability and Accountability Act (HIPAA) OL-7**

  20. Individual compliance rules success and violations, and evaluations can be explored. Navigate to Results by target, Results by compliance standard Rules tab,  to get an understanding of Frameworks, Standards, and host Targets level compliance visually.

  ![](images/HIPAA_Compliance_Results_Image_24-1.png " ")

      Individual standard rule details status and rationale can be further analyzed.

  ![](images/HIPAA_Compliance_Results_Image_25-1.png " ")

      All these would give you a security posture of the host target.

  <!---- With this step, you got hands-on experience in creating a custom framework to monitor the security compliance of heterogeneous targets (Database and Host, this example). This will help you assess the overall security compliance of all
  Enterprise Manager managed targets from one aggregated view. And if required, you can drill down into each standard to assess details of target-specific security compliance. ---->

  This completes the Lab!

  You may now [proceed to the next lab](#next).

## Learn More

  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements
  - **Author** - Harish Niddagatta, Oracle Enterprise Manager Product Management
  - **Contributors** -  Rene Fontcha
  - **Last Updated By/Date** - Shiva Prasad, Oracle Enterprise Manager Product Management, June 2022
