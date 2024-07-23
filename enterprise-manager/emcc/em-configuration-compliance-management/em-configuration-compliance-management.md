# Configuration and Compliance Management
## Introduction
The objective of this lab is to highlight Oracle Enterprise Manager Cloud Control 13c’s Lifecycle Management capabilities related to configuration and security compliance management of managed targets. Each activity focuses on the different capabilities of an administrator.

*Estimated Lab Time:* 60 minutes

Watch the video below for a quick walk-through of the lab.
[Configuration and Compliance Management](videohub:1_co6s1vy7)

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
| 4                                                         |  CIS standard Database security Compliance Standard | 10 minutes                    | Apply a industry Standard for Oracle 19c using Traditional Auditing for Oracle Database target, generate report and validate the results.                | Implementing stringent security measures and achieving regulatory compliance by aligning with CIS benchmarks, enhances and operational efficiencies of database management through centralized auditing and monitoring, fostering and enhancing Oracle databases integrity and operational efficiencies.                                                       | Monitor security compliance for host targets from one customized dashboard |
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

    ![em-login-page](../initialize-environment/images/em-login.png " em-login-page ")

2.  From the Enterprise menu, select **Configuration**, then select **Inventory and  Usage Details**.

    ![configuration-inventories-usage-page](images/configuration-inventories-usage.png " configuration-inventories-usage-page ")

    Once, Inventory and  Usage Details is chosen, it appears as below with Linux OS with Hostname.

    ![inventory-and-usage-details-page](images/inventory-and-usage-details-page.png " inventory-and-usage-details-page ")

3.  In the **Show** filter menu, select **Databases** to see all database instances managed by Enterprise Manager.

    ![em-compliance-config-alldbs-page](images/em-compliance-config-alldbs.png " em-compliance-config-alldbs-page ")

4.  Analyze various database versions and the number of instances for each version or you can choose PDBs 19c highlighted above page.

5.  **Table View** can be visible by selecting and adjusting the grid line on the page as shown below.

    ![table-review-grid-line-page](images/table-review-grid-line.png " table-review-grid-line-page ")

    Explore the pie chart to see the breakdown of database inventory by color-code percentages. Also, in the **Graphical View**, choose the **Trend** radio button to see the growth of a given database instance over a period of time.

    ![inventory-usage-detail-page](images/inventory-usage-detail.png " inventory-usage-detail-page ")

6. Click on Table View, further details to explore.

    ![em-inventory-usage-detail-table-select-page](images/em-inventory-usage-detail-table-select.png " em-inventory-usage-detail-table-select-page ")  

    Click **Close**.

7.  In the Details excel file table output below, you will see details as follows

      - Database instance name Target
      - Host on which this database is located
      - Database type - cluster or single instance
      - Database version number
      - OS specific details like OS version, platform, etc.
      - Most importantly, LOB/Department information
        The Details table gives more information about each Database instance for you to get a good understanding of the number of database targets deployed on a given host with OS version. If your organization uses properties like Lifecycle, Line of Business, or Department, then you will be able to determine the number of targets deployed for a given business unit. Explore these features to get a good handle on Inventory and Usage details.

8.  Inventory usage and Details can be exported for offline further reviews and analysis.

    ![em-inventory-detail-export-summary-page](images/em-inventory-detail-export-summary.png " em-inventory-detail-export-summary-page ")

    These details can be exported to an excel file and shared the report with management. With the excel report, you can filter based on the properties you are using to show department or line of business-specific assets allocation and usage, excel file format as shown here.

    ![em-ecm-inv-usage-detail-page](images/em-ecm-inv-usage-detail.png " em-ecm-inv-usage-detail ")  

## Task 2: One-Time Database Comparison

### Overview

In this step, you will compare two database targets to determine configuration differences. One of the databases will act as a reference target that aligns with your configuration policy. Your objective is to compare initialization parameters to ensure it is compliant with the reference target.

### Execution

1.  Log into your Enterprise Manager as **sysman** as indicated in the Prerequisites step if not already done.

2.  From the Enterprise menu, select **Configuration**, then select **Configuration & Drift Management**

    ![em-login-welcome-page](images/em-login-welcome.png " em-login-welcome-page ")

3.  Review the different types of comparisons supported by Clicking on the **i** icon.

    ![comparison-and-driftmanagement-page](images/comparison-and-driftmanagement.png " comparison-and-driftmanagement-page ")

4.	Select the **One-Time Comparison Results** tab on the left side of the dashboard page. Click **Create Comparison**

    ![onetime-create-comparison-page](images/onetime-create-comparison.png " onetime-create-comparison-page ")

5.  Choose the reference target that you want other targets to be compared with.

    ![onetime-comparison-reference-page](images/onetime-comparison-reference.png " onetime-comparison-reference-page ")

6.  Identify the reference target to compare other targets.

    ![select-targets-page](images/select-targets.png " select-targets-page ")

    To begin with, filter ‘Target Type’ to Database Instance.

    Click Search.

    ![select-targets-type-page](images/select-targets-type.png " select-targets-type-page ")

7.  Select **emrep.us.oracle.com** as the reference target.

    ![select-reference-type-target-page](images/select-referencetype-target.png " select-referencetype-target-page ")

8.  Choose Database Instance Template for Comparison Template.

    ![oneime-comparison-template-page](images/oneime-comparison-template.png " oneime-comparison-template-page ")

9.  Provide a name for Comparison, for example, a name like **ECM002-Compare-Demo - One time Comparison**

    ![onetime-database-instance-comparison-page](images/onetime-database-instance-comparison.png " onetime-database-instance-comparison-page ")

10. Add targets to be compared.

    ![add-target-compared-page](images/add-target-compared.png " add-target-compared-page ")

11. Choose **finance.subnet.vcn.oraclevcn.com** target to compare with the reference target.

    ![select-database-target-to-compare-page](images/select-database-target-to-compare.png " select-database-target-to-compare-page ")

    Once the target is chosen, it appears as below.
    Click **Submit**

    ![compared-add-target-submit-page](images/compared-add-target-submit.png " compared-add-target-submit-page ")

12. The comparison would take a few seconds to a minute for selected targets.

    ![comparison-progress-page](images/comparison-progress.png " comparison-progress-page ")

    Below are the results.
    Click **Clear All** at Configuration Items(Differences).

    ![results-clear-all-comparisons-page](images/results-clear-all-comparisons.png " results-clear-all-comparisons-page ")

13. Filter configuration items to review only Initialization Parameters.

    You can see the differences in the Initialization Parameters between the two targets.

    Under the target compared column, you will see a few icons. The icons that appear in the view are mostly intuitive:

    - Equal sign means parameter properties are the same across the reference and target compared
    - Not equal sign indicates parameter properties are different across the reference and target compared
    - A red box with 1 (left only) means that the comparison did not find a matching item to compare, this means 2nd target doesn’t have a property configured to compare
    - A red box 2 (right only) means that the comparison did not find a matching item to compare to the second configuration

    ![comparison-result-initialization-parameters-page](images/comparison-result-initialization-parameters.png " omparison-result-initialization-parameters-page ")

14. Now, let us go to the Comparison and Drift Management dashboard page for further analysis of the results.

    ![configuration-comparison-drift-management-page](images/configuration-comparison-drift-management.png " cconfiguration-comparison-drift-management-page ")

15. On the dashboard page, the donut chart for Comparison Overview gives you the summary result. Click on the **donut chart** to analyze one-time comparison result details.

    ![dashboard-one-time-comparison-results-page](images/dashboard-one-time-comparison-results.png " dashboard-one-time-comparison-results-page ")

    You should see the comparison definition you created on this page.

    ![one-time-comparison-result-page](images/one-time-comparison-result.png " one-time-comparison-result-page ")

16. Export the comparison results into an excel report for further reviews and offline analysis. On the One-Time Comparison Results page, highlight the definition and choose Export Results, You can choose the specific results to export.

    ![export-one-time-comparison-result-page](images/export-one-time-comparison-result.png " export-one-time-comparison-result-page ")

  After Exporting, Click **Cancel** to exit. The zip ECM002-Compare-Demo - One time Comparison_comparisonresult.zip file will be created, downloadable, and available to open in excel format on your system to do offline verification.

17. One-time Database comparison results excel file format as shown here.

    ![compare-demo-one-time-comparison-excel](images/compare-demo-one-time-comparison-excel.png " compare-demo-one-time-comparison-excel ")

<!-- In this step, you learned steps to compare two database targets to determine configuration differences. This one-time database (or any Enterprise Manager managed targets) comparison will help you quickly determine specific configuration changes when compared with reference configuration. This is very ideal for troubleshooting any target configuration parameters. -->

## Task 3: Database Configuration Drift Management

### Overview

In this workshop, you will learn about continuous configuration drift monitoring of database targets against a reference target for initialization parameters using a customized configuration monitoring template.

1.  Log into your Enterprise Manager VM using the IP provided on your cheat sheet.

2.  Navigate to ***Enterprise >> Configuration >> Comparison & Drift Management***, Review the different types of comparisons supported.

    ![em-login-welcome-page](images/em-login-welcome.png " em-login-welcome-page ")

    By Clicking on the **i** icon, review the different types of comparisons.

    Choose Templates left side of the panel of the Dashboard.

    ![cocomparison-and-driftmanagement.pngmparison-and-driftmanagement-page](images/comparison-and-driftmanagement.png " comparison-and-driftmanagement-page ")

3.  Click on Templates on the left panel will navigate to Comparison Templates Page.

    ![comparison-template-page](images/comparison-template.png " comparison-template-page ")

4.  **Sort Name Alphabetically** look for Database Instance Template as shown below.

    ![sort-database-instance-comparison-templates-page](images/sort-database-instance-comparison-templates.png " sort-database-instance-comparison-templates-page ")

    With Database Instance Template highlighted, choose **Create Like** to create **ECM003-Drift_Demo** a copy of this template for further customization. Provide a unique name to the new template and click **OK**.

    ![create-like-comparison-templates-page](images/create-like-comparison-templates.png " create-like-comparison-templates-page ")

5.  A complete copy of the Database Instance template with a unique name is created with all configuration items enabled, click on the **Template Name** field and copy with the name provided below

    ```
      <copy>ECM003-Drift_Demo</copy>

    ```
    And click **Search**.

    ![comparison-drift-management-database-instance-page](images/comparison-drift-management-database-instance.png " comparison-drift-management-database-instance-page ")

    Highlight this new template and click Edit.

    ![comparison-template-edit-page](images/comparison-template-edit.png " comparison-template-edit-page ")

6.  The configuration templates page appears below.

    ![edit-comparison-template-configuration-items-page](images/edit-comparison-template-configuration-items.png " edit-comparison-template-configuration-items-page ")

    To begin with, uncheck all configuration items.
    
    ![comparison-uncheck-compare-template-page](images/comparison-uncheck-compare-template.png " comparison-uncheck-compare-template-page ")

7.  In this lab, we will customize this template and monitor configuration drift for two configuration items.

    Select the following three configuration items only:

    - Instance Caging Information
    - Instance Information
    - Initialization Parameters under Instance Information configuration item
    - Making sure **Instance Information** is highlighted
    - Click Save

    ![comparison-detailinstance-information-page](images/comparison-detailinstance-information.png " comparison-detailinstance-information-page ")

8.  A new customized configuration drift monitoring template is created. This template can be used for drift monitoring.

    ![confirm-comparison-and-drift-management-page](images/confirm-comparison-and-drift-management.png " confirm-comparison-and-drift-management-page ")

    **Search** with Template name **ECM003-Drift_Demo** shows with a Confirmation page

    ![search-comparison-drift-management-page](images/search-comparison-drift-management.png " search-comparison-drift-management-page ")

9.  Go to the Drift Results tab and create a drift definition.

    ![comparison-drift-management-results-page](images/comparison-drift-management-results.png " comparison-drift-management-results-page ")

10. Click on **Create Definition** under Drift Management.

    - Choose Database Instance as the Target Type
    - Select the template created in the previous step
    - Click OK

    ![create-definition-driftdemo-database-instance-page](images/create-definition-driftdemo-database-instance.png " create-definition-driftdemo-database-instance-page ")

11. On the drift definition details page, provide a unique name for the drift definition.

    ![drift-definition-detail-name-page](images/drift-definition-detail-name.png " drift-definition-detail-name-page ")

12. Under Source Configuration, do the following:

    -  Select ‘Latest Configuration’
    -  Click search to choose Source Target

    ![source-target-search-page](images/source-target-search.png " source-target-search-page")

13. Choose **emrep.us.oracle.com** as your source target. Click on **Select**

    ![select-target-name-page](images/select-target-name.png " select-target-name-page ")

14. You will see Source Target (***emrep.us.oracle.com***) is selected that acts as your reference target.

    ![drift-definition-details-save-target-page](images/drift-definition-details-save-target.png " ddrift-definition-details-save-target-page ")

15. Select **Save and Associate Targets** to select targets to be monitored.

    ![drift-definitiontarget-association-page](images/drift-definitiontarget-association.png " ddrift-definitiontarget-association-page ")

16. Click on **Add** to select and associate a target to be monitored for drift.

    ![select-targets-to-target-name-page](images/select-targets-to-target-name.png " select-targets-to-target-name-page ")

17. Select **finance.subnet.vcn.oraclevcn.com** as the target.

    ![select-target-associate-drift-target-page](images/select-target-associate-drift-target.png " select-target-associate-drift-target-page ")

18. Click **Select**, You will see one target selected to be associated with drift definition, Click OK.

    ![drift-definition-target-association-enabled-page](images/drift-definition-target-association-enabled.png " drift-definition-target-association-enabled-page ")

19. A pop-up will ask for confirmation to save the association. Select **Yes**, This will start the association of this target to drift definition and initiate the configuration comparison and continuous drift monitoring.

    ![drift-definition-target-saves-association-page](images/drift-definition-target-saves-association.png " drift-definition-target-saves-association-page ")

20. Once you select Yes in the previous step, drift monitoring is in progress. Go to **Enterprise --> Configuration --> Comparison & Drift Management** Dashboard page. After a minute, refresh the page to see if the drift monitoring is completed. You should see a new or updated donut chart under the ‘Drifted Overview’ dashlet.

    ![comparison-&-drift-management-dashboard-page](images/comparison-&-drift-management-dashboard.png " comparison-&-drift-management-dashboard-page ")

    Click on the Drift Results tab on the left panel (2nd tab from the top).

21. This page will show results for all drift definitions managed by this instance of Enterprise Manager. Identify the drift definition you created for further analysis of configuration drift results.

    ![compared-drift-management-results-page](images/compared-drift-management-results.png " compared-drift-management-results-page ")

22. Review the drift details. Click on the **Drift Definition** (ECM003-Drift-Demo – Drift)

    ![comparison-review-ecm003-drift-demo-drift-page](images/compared-drift-management-results-select.png " comparison-review-ecm003-drift-demo-drift-page ")

    For a detailed analysis of configuration drift. You can see the differences in the Initialization Parameters between the two targets.

    ![comparison-results-ecm003-drift-demodrift-page](images/comparison-results-ecm003-drift-demodrift.png " ccomparison-results-ecm003-drift-demodrift-page ")

    Under the target compared column, you will see a few icons. The icons that appear in the view are mostly intuitive:
     - Equal sign means parameter properties are the same across the reference and target compared
     - Not equal sign indicates parameter properties are different across the reference and target compared
     - A red box with 1 (left only) means that the comparison did not find a matching item to compare, this means 2nd target doesn’t have a property configured to compare
     - A red box 2 (right only) means that the comparison did not find a matching item to compare to the second configuration

23. Go to **Enterprise --> Configuration --> Comparison & Drift Management** Dashboard page.

    ![comparison-&-drift-management-dashboard-page](images/comparison-and-drift-management-dashboard.png " comparison-&-drift-management-dashboard-page ")

    Click on Click on **Drift Results**.

    ![config-drift-dashboard-page](images/config-drift-dashboard.png " cconfig-drift-dashboard-page ")

24. On the Drift Results page, highlight the definition and choose **Export Results**.

    ![export-results-for-created-drift-page](images/export-results-for-created-drift.png " export-results-for-created-drift-page ")

25. You can choose the specific results to export. Click **OK**.

    ![set-of-export-results-view-page](images/set-of-export-results-view.png " set-of-export-results-view-page ")

26. Exported the drift management results into zipping file **ECM003-Drift_Demo - Drift_comparisonresult.zip** accessible in your Downloads folder, excel file is available for further reviews and offline analysis. Drift management results excel file format is as shown here.

  ![ecm003-drift-demo-drift-export-excel](images/ecm003-drift-demo-drift-export-excel.png " ecm003-drift-demo-drift-export-excel ")

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

    ![em-enterprise-compliance-library-page](images/em-enterprise-compliance-library.png " em-enterprise-compliance-libraryß-page ")

3.  The compliance Standards tab contains all standards for various supported targets.

    ![all_compliance-library-standards-page](images/all_compliance-library-standards.png " all_compliance-library-standards-page ")

    Click on Caret Right Icon  ![caret](images/caret-search.png " ") search

4.  In the Compliance Standards tab, search for Compliance Standard by entering **CIS**
and Applicate To drop down column choose **Database Instance** and click on **Search**.

    ![search-compliance-library-database-instance-page](images/search-compliance-library-database-instance.png " search-compliance-library-database-instance-page ")

    Click on collapsable icon ![collapse](images/collapsed-search.png " ") search

    ![library-page](images/compliance-library.png " compliance-library-page ")

5.  Select the **Oracle 19c Database CIS V1.1.0 - Level 1 - RDBMS using Traditional Auditing for Oracle Database** for Oracle Database standard.

    ![choose-cis-compliance-library-page](images/choose-cis-compliance-library.png " choose-cis-compliance-library-page ")


6.  Create a copy of this database standard by clicking on **Create Like**. Give a unique name to the new standard.

    ![create-like-cis-compliance-library-page](images/create-like-cis-compliance-library.png " create-like-cis-compliance-library-page ")

    Here, for example, **CIS_DEMO** you are creating to imply this is a new database standard. Also if you can change the name per your preference and Continue,

    ![create-compliance-cis-demo-for19c-page](images/create-compliance-cis-demo-for19c.png " reate-compliance-cis-demo-for19c-page ")

7.  Review the various compliance rules for CIS Security standards grouped based on the configuration area.

    ![compliance-standard-cis-main-page](images/compliance-standard-cis-main.png " compliance-standard-cis-main-page ")

    Click **Save**

    ![compliance-standard-cis-rules-page](images/compliance-standard-cis-rules.png " compliance-standard-cis-rules-page ")

8.  A new custom database CIS standard is created. Pop-up confirms the successful creation of these standards, Click **OK**

    ![compliance-cis-demo-information-page](images/compliance-cis-demo-information.png " compliance-cis-demo-information-page ")

9.  Select the newly created custom database standard. Click on **Associate Targets** to associate a database target for this newly created custom standard.

    ![cis-compliance-library-associate-target-page](images/cis-compliance-library-associate-target.png " cis-compliance-library-associate-target-page ")

10. When the Associate Target option is chosen, you will be taken to a page to add database targets, Click Add to add targets for association with this compliance standard.

    ![add-cis-compliance-standard-target-page](images/add-cis-compliance-standard-target.png " add-cis-compliance-standard-target-page ")

11. The list of targets chosen will show up on the target association page as shown below, Select **emrep.us.oracle.com** target to check the compliance security posture.

    ![select-targets-compliance-target-page](images/select-targets-compliance-target.png " sselect-targets-compliance-target-page ")

12. The list of targets chosen will show up on the target association page as shown below. Click **OK** and a pop-up window shows to confirm an association.

    ![enabled-compliance-standard-target-association-page](images/enabled-compliance-standard-target-association.png " enabled-compliance-standard-target-association-page ")

13. Click **Yes** to save the association which initiates a compliance check on this target by executing all the compliance rules associated with this compliance standard.

    ![save-association-compliance-target-page](images/save-association-compliance-target.png " save-association-compliance-target-page ")

    The pop-up window shows the process status, Click **OK**

    ![compliance-standard-associate-target-submitted-page](images/compliance-standard-associate-target-submitted.png " compliance-standard-associate-target-submitted-page ")

14. To check if the compliance check is complete, click the target number in the ‘Association Count’ column.

    ![cis-compliance-library-association-count-page](images/cis-compliance-library-association-count.png " cis-compliance-library-association-count-page ")

15. If the Evaluation status indicates **Enabled** and Transfer Status indicates **Successfully Done**, it means the compliance check is complete,
Click the **Cancel** button.

    ![cis-compliance-standard-target-success-page](images/cis-compliance-standard-target-success.png " cis-compliance-standard-target-success-page ")

 16. Go to the **Compliance >> dashboard ** page to check the CIS compliance posture. It takes about few minutes to show up in compliance dashboard results.
 
        ![compliance-results-dashboard-page](images/compliance-results-dashboard.png " compliance-results-dashboard-page ")
       
     Under the Compliance Summary panel at the bottom below page:

     - Explore various tabs to get an understanding of Frameworks, Standards, and target-level compliance
     - For any given standard, if there are Critical, Warning, or Minor Warnings
     - Click on the violation number to see more details of the violationS by clicking the numbers below each column's names

17. By Clicking on the Critical column number, you will see details like each violation, and the last evaluation date.

    ![compliance-dashboard-evaluation-page](images/compliance-dashboard-evaluation.png " compliance-dashboard-evaluation-page ")

    By clicking under Target Name.

    ![cis-compliance-critical-violations-page](images/cis-compliance-critical-violations.png " cis-compliance-critical-violations-page ")

18. Each rule name violated and rationale for the violation can be explored below, And also by clicking on Report.

    ![evaluate-cis-critical-violations-page](images/evaluate-cis-critical-violations.png " evaluate-cis-critical-violations-page ")

    Compliance Evaluation Report will be populated on a separate page that can be used for further analysis of each rule passed or failed.

    ![cis-demo-compliance-report1-page](images/cis-demo-compliance-report1.png " cis-demo-compliance-report1-page ")

    Under Result Details, clicking on the arrow mark at **emrep.us.oracle.com: CIS_DEMO** gives more information on individual rules.

    ![cis-demo-compliance-report2-page](images/cis-demo-compliance-report2.png " cis-demo-compliance-report2-page ")
    ![cis-demo-compliance-report3-page](images/cis-demo-compliance-report3.png " cis-demo-compliance-report3-page ")
    

19. Click **X** to close Critical Violations window

    ![close-evaluate-cis-critical-violations-page](images/close-evaluate-cis-critical-violations.png " close-evaluate-cis-critical-violations-page ")  

20. By going back to the **Compliance Dashboard** page,  click on the standard that you created **CIS_DEMO** in the previous steps to review further evaluations of results.

    ![compliance-dashboard-cis-compliance-summary-page](images/compliance-dashboard-cis-compliance-summary.png " compliance-dashboard-cis-compliance-summary-page ")

    Each rule result can undergo a detailed analysis as shown on this page.

    ![cis-compliance-results-by-standard-rules-page](images/cis-compliance-results-by-standard-rules.png " cis-compliance-results-by-standard-rules-page ")

21. By clicking on **Violations**, each CIS compliance Standard Rules Violations can be seen as follows

    ![cis-compliance-results-by-standard-rules1-page](images/cis-compliance-results-by-standard-rules1.png " cis-compliance-results-by-standard-rules1-page ")

    Click **Close**
    
    Further, each violations event details, recommendations and remediations could be explored

    ![cis-compliance-results-by-standard-rules2-page](images/cis-compliance-results-by-standard-rules2.png " cis-compliance-results-by-standard-rules2-page ")

    Click **Logout**

    ![cis-compliance-results-logout-page](images/cis-compliance-results-logout-page.png " cis-compliance-results-logout-page ")  

    <!-- All of these steps will give you a CIS Compliance security posture of database target. -->  
    

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

    ![em-enterprise-compliance-library-page](images/em-enterprise-compliance-library.png " em-enterprise-compliance-libraryß-page ")

3.  The compliance Standards tab contains all standards for various supported targets.

    ![all_compliance-library-standards-page](images/all-compliance-library-standards.png " call_compliance-library-standards-page ")

4.  In the Compliance Standards tab, search for the Keywords column for the word **HIPAA**

    ![hipaa-compliance-lib-search-page](images/hipaa-compliance-lib-search.png " hipaa-compliance-lib-search-page")

5.  Select Health Insurance Portability and Accountability Act (HIPAA) OL-7 standard, Click on Show Details.

    ![hipaa-compliance-library-show-detail-page](images/hipaa-compliance-library-show-detail.png " hipaa-compliance-library-show-detail-page ")

6. After Selecting  **Show Details** Review Quickly scan various rules available for HIPAA out-of-box, Click on **Done**

    ![compliance-standard-hipaa-ol-7-details-page](images/compliance-standard-hipaa-ol-7-details.png " compliance-standard-hipaa-ol-7-details-page ")

7. Click on **Associate Targets** to associate a database target for this selected standard.

    ![hipaa-compliance-lib-associate-target-page](images/hipaa-compliance-lib-associate-target.png " hipaa-compliance-lib-associate-target-page ")

8. When the Associate Target option is chosen, you will be taken to a page to add host's targets.

    Click Add to add a target for association with this compliance standard.

    ![hipaa-association-compliance-add-target-page](images/hipaa-association-compliance-add-target.png " hipaa-association-compliance-add-target-page ")

9.  There is one host called **emcc.marketplace.com**, select that target to associate.

    ![hipaa-compliance-standard-select-target-page](images/hipaa-compliance-standard-select-target.png " hipaa-compliance-standard-select-target-page ")

10. Now, you see emcc.marketplace.com host target has been added. Now, let's complete the association workflow".

      Click **OK**.

    ![hipaa-compliance-standard-target-enabled-page](images/hipaa-compliance-standard-target-enabled.png " hipaa-compliance-standard-target-enabled-page ")

11. A pop-up window shows up to confirm an association. Click **Yes** to save the association which initiates a compliance check on this host target by executing all compliance rules associated with HIPAA compliance standards.

    ![save-target-hipaa-compliance-standard-page](images/save-target-hipaa-compliance-standard.png " save-target-hipaa-compliance-standard-page ")

12. Once, the Compliance standard host target is been submitted you will be taken to a Compliance Library's page, which shows Compliance Standard is submitted for processing.

    ![information-hipaa-compliance-standard-confirm-page](images/information-hipaa-compliance-standard-confirm.png " information-hipaa-compliance-standard-confirm-page ")

13. To check if the compliance processing is complete, click the target number in the **Association Count** column.

    ![hipaa-association-count-compliance-library-page](images/hipaa-association-count-compliance-library.png " ahipaa-association-count-compliance-library-page ")

14. If evaluation status **Enabled** and Transfer Status indicates **Successfully Done**, it means the compliance check is complete. Click the **Cancel** button.

    ![hipaa-add-target-association-enabled-page](images/hipaa-add-target-association-enabled.png " thipaa-add-target-association-enabled-page ")

15. Go to the **Compliance Dashboard** page to check the compliance posture.

    ![hipaa-compliance-dashboard-page](images/hipaa-compliance-dashboard.png " hipaa-compliance-dashboard-page ")

16. Compliance Dashboard populates:

    - Under the Compliance Summary panel at the bottom, explore various tabs to get an understanding of Frameworks, Standards, target level compliance, and Average Compliance score too
    - For any given standard, if there are Non-Compliant Targets, Critical, Warning, or Minor Warnings, click on the violation number to see more details of the violation

    Click on the number under the **Critical** column. to see details of the host's critical violations.

    ![compliance-dashboard-summary-hipaa-ol-7-page](images/compliance-dashboard-summary-hipaa-ol-7.png " compliance-dashboard-summary-hipaa-ol-7-page ")

17. Host's critical violations can be explored by clicking the **Target name** column arrow.

    ![critical-violations-hipaa-compliance-ol-7-page](images/critical-violations-hipaa-compliance-ol-7.png " critical-violations-hipaa-compliance-ol-7-page ")

    Each critical rule violations status can be seen on this pop-up page in detail.

    Click on  **Report**

    ![critical-violations-hipaa-compliance-rules-ol-7-page](images/critical-violations-hipaa-compliance-rules-ol-7.png " critical-violations-hipaa-compliance-rules-ol-7-page ")

18. It takes you to a separate page that shows Compliance Evaluation Report to see the reports with passed and failed rules.

    ![compliance-evaluation-report1-hipaa-ol-7-page](images/compliance-evaluation-report1-hipaa-ol-7.png " compliance-evaluation-report1-hipaa-ol-7-page ")

    And clicking on the **Result Details arrow emcc.marketplace.com: Health Insurance Portability and Accountability Act (HIPAA) OL-7** to see drill down evaluation details.

    ![compliance-evaluation-report2-hipaa-ol-7-page](images/compliance-evaluation-report2-hipaa-ol-7.png " compliance-evaluation-report2-hipaa-ol-7-page ")
    ![compliance-evaluation-report3-hipaa-ol-7-page](images/compliance-evaluation-report3-hipaa-ol-7.png " compliance-evaluation-report3-hipaa-ol-7-page ")

19. Individual rules can be further explored with select Enterprise Main Menu, then selecting Compliance and Results Page.

    ![compliance-results-for-page](images/compliance-results-for-hipaa.png " compliance-results-for-page ")

    It takes you to the Compliance Results page.

    Click on **Health Insurance Portability and Accountability Act (HIPAA) OL-7**

    ![hipaa-compliance-evaluation-results-ol7-page](images/hipaa-compliance-evaluation-results-ol7.png " hipaa-hipaa-compliance-evaluation-results-ol7-page ")

20. Individual compliance rules success and violations, and evaluations can be explored. Navigate to Results by target, Results by compliance standard Rules tab,  to get an understanding of Frameworks, Standards, and host Targets level compliance visually.

    ![hipaa-compliance-ol-7-host-rule-results-page](images/hipaa-compliance-ol-7-host-rule-results.png " hipaa-compliance-ol-7-host-rule-results-page ")

    Individual standard rule details status and rationale can be further analyzed.

    ![hipaa-compliance-ol-7-individual-rule-detail-page](images/hipaa-compliance-ol-7-individual-rule-detail.png " hipaa-compliance-ol-7-individual-rule-detail-page ")

21. Violations events can be further explored in detail.

    ![hipaa-compliance-ol-7-individual-rule-detail-page](images/hipaa-compliance-ol-7-violation-rule-detail.png " hipaa-compliance-ol-7-individual-rule-detail-page ")

  All these would give you a security posture of the host target.

  <!---- With this step, you got hands-on experience in creating a custom framework to monitor the security compliance of heterogeneous targets (Database and Host, this example). This will help you assess the overall security compliance of all
  Enterprise Manager managed targets from one aggregated view. And if required, you can drill down into each standard to assess details of target-specific security compliance. ---->

  This completes the Lab!

  You may now [proceed to the next lab](#next).

## Learn More

  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)
  - [Database Lifecycle Management Webinar](https://www.youtube.com/watch?v=QjdwUfBn6FI)
  - [Compliance Standards](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emdbc/pluggable-database-compliance-standards.html#GUID-364EC867-C012-4710-B695-2D1BF53E2F86)
  - [Enterprise Manager CIS Benchmark Blog](https://blogs.oracle.com/database/post/enterprise-manager-cis-benchmark-certification-eases-adoption-of-secure-database-best-practices)
  - [HIPAA Compliance with Enterprise Manager](https://blogs.oracle.com/observability/post/secure-linux-configuration-for-hipaa-compliance-with-enterprise-manager)
  - [SCAP Support Blog](https://blogs.oracle.com/observability/post/scap-support-secure-linux-configuration-with-enterprise-manager)
  - [SCAP Standards](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emdbc/scap-supported-standards.html)

## Acknowledgements

  - **Author/Date** - Shiva Prasad, Oracle Enterprise Manager Product Management, July 18th,2024.
  