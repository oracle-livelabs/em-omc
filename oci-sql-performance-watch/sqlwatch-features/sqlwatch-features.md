# Exploring Oracle Cloud Infrastructure SQL Performance Watch

## Introduction

SQL Performance Watch helps users predict the impact of system changes on SQL workload and generate the granular level details of a SQL performance. Here are some of the tasks you can perform using SQL Performance Watch, which gives you a glimpse into how to identify the regressions from the SQL Performance Analyzer report.

SQL Performance Watch
-   Obtain an overview of your fleet of databases
-   View the reports of the SQL Performance Watch to obtain an insight into the overall health of the databases
-   Review the report of database upgrade from 19.3 to 19.26
-   Proactively review the impact of adding a new index in an database by assessing the saved SPA report


Estimated Time: 30 minutes

Watch the video below for a quick walk-through of the lab.
[Exploring Oracle Cloud Infrastructure SQL Performance Watch](videohub:1_mpf7rizz)

### Objectives

-   Use Oracle Cloud Infrastructure SQL Performance Watch to identify the regression by proactively testing the changes before implementing on the production database.

### Prerequisites

This lab assumes you have already completed the following:
- An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account

## Task 1: Getting Started with SQL Performance Watch

1. Login to the Oracle Cloud Console, click the **Navigation Menu** in the upper left, navigate to **Observability & Management** and within the **SQL Performance Watch** service.

     ![SQL Performance Watch](./images/oandm-sqlwatch.png " ")

2.  Go to SQL Performance Watch summary page, and view the databases that have SQL Performance Watch enabled in **US West (San Jose)** region and **dbmgmt** compartment

     ![SQL Performance Watch Summary page](./images/sqlwatch-summary.png " ")

3.  Navigate to Administration page and choose external database.

     ![Administration page](./images/sqlwatch-admin.png " ")

     ![External DB administration page](./images/sqlwatch-external.png " ")

4. Go to SQL Performance Watch summary page, and click on one of the listed databases

     ![Database list](./images/sqlwatch-dblist.png " ")


## Task 2: Test the upgrade from 19.3 to 19.26 DB version

1. Go to SQL Performance Watch summary page, and click on **mfg\_sales** database. Review the highlighted sections.

     ![Landing page](./images/sqlwatchlandingpage.png " ")

2. Let's look at the saved reports, to analyze the performance of a SQL during the upgrade and parameter change. To view the reports, go to SQL Performance Watch summary page, and click on one of the saved reports. You can view all the saved reports of any task in the summary page.

     ![Saved Reports](./images/savedreports.png " ")

3.  There are two saved reports - One is testing the upgrade use cases and the other is validating adding the new indexes. First, let's review the upgrade saved reports **Upgrade\_Report\_BufferGets** or **Upgrade\_ElapsedTime\_Report**. Click on **Upgrade\_Report\_BufferGets** to review the granular level details of the SQL Performance while testing the upgrade from 19.3 to 19.26.

     ![Upgrade Reports](./images/upgrade-reports.png " ")

     ![Buffer Gets report](./images/upgrade-report-buffergets.png " ")

4. Review the regressed SQLs and look for plan change **Yes**, indicating that there is a SQL plan change for that specific SQL.    

     ![Regressed SQLs](./images/regressedsqls.png " ")

5. Click on the SQL to review the SQL performance by analyzing the metrics and the plan changes.
 
     ![Regressed SQLs](./images/metrics.png " ")

     ![Regressed SQLs](./images/beforeandafterplan.png " ")

     ![Regressed SQLs](./images/indexchanges.png " ")

6. To do it your own tenancy, please choose change type as **Upgrade** and make sure there are DB links available to run the SPA trials remotely. [Refer to video](https://youtu.be/C9qkLNqj5x4) on how to test the upgrade using SQL Performance Watch.


## Task 3: Parameter Change - Validate New Indexes

1. Let's now review validating adding new indexes report. Click on saved report - **Validate\_New\_Indexes** 

     ![Parameter Change Report](./images/validatingnewindexreport.png " ")

2. Check for improved SQLs and analyze the report for the impact and improvement of the SQLs due to index addition. 

     ![Parameter Change Report](./images/improvedsqls.png " ")

3. Click on the SQL to review the SQL performance by analyzing the metrics and the plan changes.

4. To do it on your own, please choose change type as **Parameter Change** and make sure the indexes are invisible while adding, and choose the parameter as **optimizer\_use\_invisible\_indexes** and change the value to **True**
 
     ![Invisible Index](./images/invisibleindex.png " ")


Finally, you can follow the same steps to go back and check out the **Cloud DB Infrastructure Performance** dashboard.  This dashboard provides various infrastructure and host metrics to monitor a database system in a single location.  Included metric widgets are **Node Status**, **OCPU allocation**, **CPU utilization**, **Memory utilization** and storage metrics such as **File System utilization** and **ASM Disk Group utilization**.

## Learn More

- [Test the upgrade using SQL Performance Watch](https://youtu.be/C9qkLNqj5x4)
- [Assess parameter change using SQL Performance Watch](https://youtu.be/whv2V9WTack)
- [Custom or Guided workflow](hhttps://youtu.be/yzo_zdmvUTE)


## Acknowledgements

- **Author** - Anusha Vojjola, Senior Product Manager, Observability and Management
- **Contributors** - Anusha Vojjola, Anand Prabhu
- **Last Updated By/Date** - Anusha Vojjola, March 2025