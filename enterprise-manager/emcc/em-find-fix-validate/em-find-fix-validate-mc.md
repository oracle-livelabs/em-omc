# Database Performance Management: Find, Fix, Validate

## Introduction

The goal of this lab is to become familiar with on-premise and Oracle Cloud Database performance management (Virtual Machine/Bare Metal/Exadata Cloud Service) capabilities using Oracle Enterprise Manager Cloud Control 13c.

*Estimated Lab Time:* 40 minutes

### About Database Performance Management
Performance Hub is a single pane of glass view of database performance with access to Active Session History (ASH) Analytics, Real-time SQL Monitoring and SQL Tuning together. In this lab you will get familiar with Performance hub, Real-time database operation monitoring, SQL Performance Analyzer, etc.  

### Objectives

In this lab you will learn:


| **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1**  | Performance Hub                               | 15 minutes       | Oracle Enterprise Manager 13c includes a new Jet based unified Performance Hub Jet interface for performance monitoring.                                                                                           | Performance Hub is a single pane of glass view of database performance with access to Active Session History (ASH) Analytics, Real-time SQL Monitoring and SQL Tuning together. The time picker allows the administrator to switch between Real-Time and Historical views of database performance.                                                                                                                                                                                                                                                                      |
| **2**  | Top Activity Lite                               | 5 minutes       | Top Activity Lite is a new feature introduced in 13c RU 15 to provide optimal response time for real-time monitoring for performance monitoring.                                                                                           | Top Activity Lite feature is a simplified version of Performance Hub, optimized for quick response under heavy loads while providing key performance diagnostics information through simple and effective  visualization. This feature helps DBAs monitor their database using a Network Operations Center (NOC) like screen.                                                                                                                                                                                                                                                                      |
| **3**  | Workload Analysis        | 15 minutes       | This a new feature to analyze workload that is running on a database using Enterprise Manager UI.                                                 | In this activity you create two SQL Tuning Sets with different parameter file and compare them using different comparison metrics.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **4**  | SQL Performance Analyzer        | 15 minutes       | The objective of this activity is to demonstrate and use the SQL Performance Analyzer functionality of Real Application Testing capabilities using Enterprise Manager UI.                                                 |  You've been asked to validate SQL performance before upgrade Database from 18.3 to 19.10. How each SQLs in the application's workload (Sales History) performs in new 19.10 upgrade. Sales History workload SQLs gathered in SQL Tuning Set SHSTS.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **5**  | Tuning a SQL in a Pluggable Database (PDB) - Optional                     | 10 minutes       | In this activity see how a pluggable database administrator can tune queries in a PDB.                                                                                                                                        | The DBA for the PDB will not have access to the Container so their view is restricted to the queries running in the PDB assigned to them. This activity identifies a Top SQL in a PDB and then tunes it using SQL Tuning Advisor.                                                                                                                                                                                                                                                                                                                                  |


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository.

## Task 1: Prepare Database
Select between *Task 1A* and *Task 1B*

## Task 1A: Prepare Database Using EM Console

1. On the Browser *Chrome/Firefox* window on the right preloaded with *Enterprise Manager*, click on the *Username* field and select the saved credentials to login. These credentials have been saved within *Chrome/Firefox* and are provided below for reference

    ```
    Username: <copy>sysman</copy>
    ```

    ```
    Password: <copy>welcome1</copy>
    ```

    ![](../initialize-environment/images/em-login.png " ")

2. From the upper left, navigate from **Enterprise** to **Job** to then **Library**

    ![](images/emjobnav.png " ")

3. Locate and select the job name **1-DB\_LAB\_START**, and Click the Submit  button.

    ![](images/emdbstartjob.png " ")

4. Leave default values in the fields and then click the Submit button in the upper right hand of your window.

    ![](images/emjobsubmitbutton.png " ")

5. The workload has started and will take a few minutes to ramp up.

    ![](images/emjobcom.png " ")

## Task 1B: Prepare database Using the terminal

1. Instead of *Task 1A* above, you may run the block below from the terminal as user *oracle*

    ![](images/em-login2.png " ")

    ```
    <copy>
    cd scripts
    source SALESENV
    . ./1-db_lab_start.sh</copy>
    ```

    ![](images/emopt3start.png " ")

## Task 2: Performance Hub

1. Click on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/emffvlab2step1.png " ")

2. Here you will notice different databases listed, such as SALES, HR etc. We will work the sales container database. Select the **Sales** database from the list and this will take you to the DB home page for this database.

    ![](images/emffvlab2step2.png " ")

    ![](images/89801010273a62f99a3da10de8bf5c71.jpg " ")

3.  Click on the **Containers** tab. It is located at the upper right-hand corner of the page, underneath the Performance tile. This will show the list of pluggable databases in the CDB and their activity.

    ![](images/c6bc11e91d6db9627a146b3e79d0ce19.jpg " ")

4.  Notice that the PSALES database is the busiest. We focus our attention to this PDB. Let us now navigate to Performance Hub. Select Performance Hub from the Performance Menu and Click on ASH Analytics and use the sales\_system credential name from the database login screen.

    ![](images/e131e1ce965ab5bb248d5439529fc921.jpg " ")

    ![](images/d4ec276ea05aceb2ff86f5b7ea71c36e.jpg " ")

    ![](images/58e81976fa9957ee57f89139a06c4841.jpg " ")

5. Make sure to slide the time picker on an area of high usage (e.g., CPU, IO or Waits). Notice how the corresponding selected time window also changes in the summary section. You can also resize the slider to entirely cover the time period of your interest.

    Notice the graph at bottom, it is providing more detailed view of the time window you selected. By Default the wait class dimension is selected. On the right hand side of the graph you have a list of wait classes for the time window you selected (blue for user I/O, green for CPU etc.). Notice how the color changes if you hover over either the menu or the graph to highlight the particular wait class.

    Wait class isn’t the only dimension you can drill into the performance issue by. Let us say you wanted to identify the SQL that was causing the biggest performance impact. You can do that by Clicking the drop down list and changing the top dimension from wait class to SQL ID.

6. Select the SQL ID dimension from the list of available dimensions (Under Top Dimensions) using the dropdown box that is currently displaying Wait Class. Top Dimensions SQL ID

    ![](images/32b079f89c002058721d0c8a3e41f993.jpg " ")

7. Hover your mouse on top of the SQL (one at the bottom) and you will be able to see how much activity is consumed by this SQL. Now using the same list of filters select the PDB dimension. Session Identifiers PDB.

    ![](images/95cce3b331aa85fc893b8eecc9a6c0a6.jpg " ")

8. What do you see? The chart changes to activity by the different pluggable databases created in this Container database.Click on the **PSALES** pluggable database on the list to add it to the filter by list and drilldown to activity by this PDB on the same page.

    ![](images/384fdb12e234cbc0d60df1639079dc3e.jpg " ")

    ![](images/07dcb138dcb6773ee6b560681a62ec5f.jpg " ")

9. Click on the SQL Monitoring Tab

      ![](images/6e47bf2703c3c1e4adffd39d2202045f.jpg " ")

10. You can see all the executed SQL during that time along with different attributes like ‘user’,’Start’,’Ended’ etc. The test next to the \@ sign indicates the name of the PDB. Click on any SQL of your choice (e.g. 6kd5jj7kr8swv).

    ![](images/PlanStatistics_Latest.png " ")

11. It will navigate you to show the details of this particular query. You can see the plan, parallelism and activity of the query. **Plan Statistics** tab is selected by default. You can see the plan of this query in graphical mode. In some cases, the Monitored SQL may have aged out and no rows are displayed, in this case try using the time-picker and pick last 24 hours time period to identify the historical SQL that was monitored.

    1.  Tabular view, helps in navigating through a big plan and customize the columns
    
    ![](images/PS_WithTablularView_HL.png " ")

    2.  Graphical view is colour coded and darker the color more the data flow 

    ![](images/PS_GraphicalView.png " ")


12. Select **Parallel** tab. This will give details about parallel coordinator and parallel slaves.

13. Click on the **SQL Text** tab. You can see the query text which has been executed.

14. Click on the **Activity** tab to understand about the activity breakdown for this SQL.

15. Click on the **Optimizer Environment** tab to view the values of the main parameters used by the Oracle optimizer when building the execution plan of a SQL statement.

16. Click on the **Outline** tab is useful for reproducing the execution plan.

17. Click on **Save Report** button on the top right corner of the page. This will help you to save this monitored execution in “.html” format, which can be used to share or to diagnose offline.

## Task 3: Top Activity Lite

1. Click on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/emffvlab2step1.png " ")

2. Here you will notice different databases listed, such as SALES, HR etc. We will work the sales container database. Select the **Sales** database from the list and this will take you to the DB home page for this database.

    ![](images/emffvlab2step2.png " ")

    ![](images/89801010273a62f99a3da10de8bf5c71.jpg " ")

3.  Click on the **Containers** tab. It is located at the upper right-hand corner of the page, underneath the Performance tile. This will show the list of pluggable databases in the CDB and their activity.

    ![](images/c6bc11e91d6db9627a146b3e79d0ce19.jpg " ")

4.  Notice that the PSALES database is the busiest. We focus our attention to this PDB. Let us now navigate to Performance Hub. Select Performance Hub from the Performance Menu and Click on ASH Analytics and use the sales\_system credential name from the database login screen.

    ![](images/e131e1ce965ab5bb248d5439529fc921.jpg " ")

5.  Navigate to **Top Activity Lite**, this page is a simplified version of Performance Hub, which contains **ASH Analytics** and **SQL Monitoring** tabs

    ![](images/TALEntry.jpg " ")

6. Click on **Auto Refresh** and choose one of the refresh options, the tables below gets refreshed, which helps DBAs monitor their database using a Network Operations Center (NOC) like screen

    ![](images/TALAutoRefresh.jpg " ")

7. One can notice the differences between Performance Hub and Top Activity Lite in terms of Time viewport, Summary timeline and Dimensions.

    ![](images/TALEnd.jpg " ")

## Task 4: Workload Analysis

**Create SQL Tuning Set - 1**

1. Download this file 

    [Click here to download file.](./files/SOE_Client_Side_2_NCPFalse.xml?download=1)

2. Login to the terminal and run the following commands which is creating a backup of xml file and replacing it with another xml file

    ```
    <copy>
    cp /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2.xml /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2_backup.xml
    cp /home/oracle/Downloads/SOE_Client_Side_2_NCPFalse.xml /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2.xml
    </copy>
    ```
3. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “sysman/welcome1”.

      ![](images/1876be1823ca17d9ab7e663e128859c4.jpg " ")

4. Go to Enterprise - Job - Library

      ![](images/emratlab2step2.png " ")

5. Pick Job Name **START\_SWINGBENCH\_LOAD** then click Submit

      ![](images/emratlab2step3.png " ")

6. Click Submit, Swingbench workload starts with 40 concurrent users to Pluggable Database OLTP in **sales.subnet.vcn.oraclevcn.com**

     ![](images/emratlab2step4.png " ")

7.  Click on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/emffvlab2step1.png " ")

8. Here you will notice different databases listed, such as SALES, HR etc. We will work the sales container database. Select the **Sales** database from the list and this will take you to the DB home page for this database.

    ![](images/emffvlab2step2.png " ")

    ![](images/89801010273a62f99a3da10de8bf5c71.jpg " ")

9.  Click on the **Containers** tab. It is located at the upper right-hand corner of the page, underneath the Performance tile. This will show the list of pluggable databases in the CDB and their activity.

10. Let us now navigate to Workload Analysis. Select Workload Analysis from the Performance Menu and use the sales\_system credential name from the database login screen.
    
    ![](images/LoginSalesSystem.png " ")

11. Under Performance Menu, go to SQL and choose SQL Tuning Set (STS) to create STS as follows

    ![](images/WLA_STS.png " ")

    ![](images/WLASTSCreate.png " ")

    Enter the name as WLA\_MC\_STS\_1, choose Cursor Cache radio button.

    ![](images/WLASTSName.png " ")

    ![](images/WLASTSCursorCache.png " ")

    Choose the SOE as filter as shown in the image below and click on Finish.

    ![](images/WLASTSFilter.png " ")
    
12. Refresh the page and you could see the count as <em>29</em>

    ![](images/WLASTS1Done.png " ")

13. Pick Job Name **STOP\_SWINGBENCH\_WORKLOAD** then click Submit

    ![](images/WLASTSswStop.png " ") 

**Create SQL Tuning Set - 2**

1. Download this file 

    [Click here to download file.](./files/SOE_Client_Side_2_NOPFalse.xml?download=1)

2. Login to the terminal and run the following commands which is creating a backup of xml file and replacing it with another xml file

    ```
    <copy>
        cp /home/oracle/Downloads/SOE_Client_Side_2_NOPFalse.xml /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2.xml
    </copy>
    ```

3. Click on the Targets, then Databases. You will be directed to the list of Databases in EM. Here you will notice different databases listed, such as SALES, HR etc. We will work the sales container database. Select the **Sales** database from the list and this will take you to the DB home page for this database. Click on the expandable arrow and choose OLTP pluggable database.

    ![](images/WLAoltpDBselection.png " ")

4. Go to SQL under Performance menu and choose SQL Worksheet and run the following commands to make an index invisble and flush the cache.

    ![](images/WLAsqlws.png " ")  
    
Make an index invisible
    1. Connect to OLTP Database
    2.	SQL Worksheet
    3.	Alter index SOE.ORDER_PK invisible
        1.	(check) Auto-commit
        2.	(uncheck) Allow only SELECT statement   

   ![](images/WLAIndexVisible.png " ")                        

5. Alter system flush shared_pool
        1.	(check) Auto-commit
        2.	(uncheck) Allow only SELECT statement

    ![](images/WLAFlush.png " ")

6. Go to Enterprise - Job - Library

      ![](images/emratlab2step2.png " ")

7. Pick Job Name **START\_SWINGBENCH\_LOAD** then click Submit

      ![](images/emratlab2step3.png " ")

8. Click Submit, Swingbench workload starts with 40 concurrent users to Pluggable Database OLTP in **sales.subnet.vcn.oraclevcn.com**

     ![](images/emratlab2step4.png " ")

9.  Click on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/emffvlab2step1.png " ")

10. Here you will notice different databases listed, such as SALES, HR etc. We will work the sales container database. Select the **Sales** database from the list and this will take you to the DB home page for this database.

    ![](images/emffvlab2step2.png " ")

    ![](images/89801010273a62f99a3da10de8bf5c71.jpg " ")

11.  Click on the **Containers** tab. It is located at the upper right-hand corner of the page, underneath the Performance tile. This will show the list of pluggable databases in the CDB and their activity.

12. Let us now navigate to Workload Analysis. Select Workload Analysis from the Performance Menu and use the sales\_system credential name from the database login screen.

13. Under Performance Menu, go to SQL and choose SQL Tuning Set (STS) to create STS as follows

    Under Performance Menu, go to SQL and choose SQL Tuning Set (STS) to create STS as follows

    ![](images/WLA_STS.png " ")

    ![](images/WLASTSCreate.png " ")

    Enter the name as WLA\_MC\_STS\_1, choose Cursor Cache radio button.

    ![](images/WLASTS2Create.png " ")

    ![](images/WLASTSCursorCache.png " ")

    Choose the SOE as filter as shown in the image below and click on Finish.

    ![](images/WLASTSFilter.png " ")

14. Refresh the page and you could see the count as <em>27</em>

    ![](images/WLASTS2withRefresh.png " ")

15. Pick Job Name **STOP\_SWINGBENCH\_LOAD** then click Submit

    ![](images/WLASTSswStop.png " ") 

**Compare STS1 to STS2**

1. Navigate to Workload Analysis from the Performance Menu. Go to One-Time Analysis tab and click on Create Analysis Task.

    ![](images/WLACreateTask.png " ") 

3. Give Name: Compare\_WLA\_MC\_STS1\_2

4. Under Reference Workload, click on search icon to choose WLAMCSTS1 from the dropdown menu. Later choose WLAMCSTS2 from the Compared Workload search

    ![](images/WLASearchIcon.png " ") 

5. In Comparison Metric, you can choose multiple options for the comparison report like Buffer Gets, Elapsed Time, CPU Time and Disk Reads. For now, let's choose Buffer Gets and Elapsed Time.

    ![](images/WLAallInputs.png " ") 

6. Click on submit and refresh. You should see both the reports and click on those reports.
    
    ![](images/WLAComparisonReports.png " ") 

7. You should be able to view the missing, new SQL and plan SQLs which would help in analysing the workload.

    ![](images/WLASampleBufferGetsReport.png " ") 

8. Click on the new plan block, you could see the plans changed for the index we made invisible.

    ![](images/WLANewplanReport.png " ") 

9. Click on the SQLID and you could see the plan changed

    ![](images/WLAPlanChangeReport.png " ") 

**Revert Changes**

1. Make index visible

2.  Copy the parameter back to original with the following command in terminal

    ```
    <copy>
    cp /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2_backup.xml /home/oracle/scripts/swingbench/swingbench/configs/SOE_Client_Side_2.xml
    </copy>
    ```

## Task 5: SQL Performance Analyzer

1.  Log into an Enterprise Manager VM. The Enterprise Manager credentials are “sysman/welcome1”. **Click** on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/1876be1823ca17d9ab7e663e128859c4.jpg " ")

    ![](images/emratlab1step2.png " ")



2. Shutdown Databases cdb186.subnet.vcn.oraclevcn.com, finance.subnet.vcn.oraclevcn.com, hr.subnet.vcn.oraclevcn.com.

  ![](images/emratlab0step2a.png " ")

  ![](images/emratlab0step2b.png " ")

  ![](images/emratlab0step2c.png " ")

  ![](images/emratlab0step2d.png " ")

  ![](images/emratlab0step2e.png " ")

3. In this Lab, we use Databases db19c.subnet.vcn.oraclevcn.com, emrep.us.oracle.com, sales.subnet.vcn.oraclevcn.com. Check if Database db19c.subnet.vcn.oraclevcn.com is open and available. If it is down, please start Database db19c.subnet.vcn.oraclevcn.com. Open Pluggable Databases db19c.subnet.vcn.oraclevcn.com\_OLTP\_CL2, db19c.subnet.vcn.oraclevcn.com\_PSAL\_CL1.

   ![](images/emratlab0step2f.png " ")

   ![](images/emratlab0step2g.png " ")

   ![](images/emratlab0step2h.png " ")

   ![](images/emratlab0step2i.png " ")

   ![](images/emratlab0step2j.png " ")

   ![](images/emratlab0step2k.png " ")

4. **Click** on the Targets, then Databases. You will be directed to the list of Databases in EM.

    ![](images/emratlab1step2.png " ")

5. Here you will notice different databases listed, such as SALES, HR etc., we will work in pluggable database psales inside the sales container database. **Expand** the Sales database from the list, and **Click** sales.subnet.vcn.oraclevcn.com_PSALES

    ![](images/emratlab1step3.png " ")

6. Go to SQL Tuning Set page by **Click** on Performance menu -> SQL -> SQL Tuning Set. Check "Named" on Credential and use SYS_SALES Credential Name from the database login screen

    ![](images/emratlab1step4a.png " ")

    ![](images/emratlab1step4b.png " ")

7. Pick SQL Tuning Set 'shsts1' and **Click** Copy To A Database button

    ![](images/emratlab1step5.png " ")

8. Enter Copy SQL Tuning Set

       - Pick **db19c.subnet.vcn.oraclevcn.com\_PSAL\_CL1** for Destination Database
       - Pick **STSCOPY** for Directory Object
       - Pick **ORACLE** for both Source and Destination Credentials and **SYS_SALES** for Destination Database Credential
       - Click **Ok**

    ![](images/emratlab1step6a.png " ")

    ![](images/emratlab1step6b.png " ")

    ![](images/emratlab1step6c.png " ")

   View on job page to check status of the Copy STS job. It can take 1.5-2 minutes.

9. After the COPY STS job successfully finished, **Click** Target - Database

       - **Click** db19c.subnet.vcn.oraclevcn.com - PDB **PSAL_CLone1**
       - **Click** on menu Performance - SQL - SQL Performance Analyzer

    ![](images/emratlab1step7a.png " ")

    ![](images/emratlab1step7b.png " ")

    ![](images/emratlab1step7c.png " ")

10. In SPA (SQL Performance Analyzer) page, **Click** Guided Workflow

    ![](images/emratlab1step8.png " ")

11. Step 1 Create SPA Task  based on STS

    ![](images/emratlab1step9a.png " ")

       - Enter Name for the Task Name : **SHSPATASK**
       - Enter Description : **Sales History SPA Task**
       - Pick STS : **SHSTS1**

    ![](images/emratlab1step9b.png " ")

       - **Click** Create and back to **Guided Workflow** page

12. Step 2 Create SQL Trial in Initial Environment

    ![](images/emratlab1step10a.png " ")

       - Enter SQL Trial Name : **SHSTS\_SQL\_TRIAL\_18C**
       - Enter Description : Sales History 18C run
       - Creation Method: **Execute SQLs Remotely**

    ![](images/emratlab1step10b.png " ")

       - Default per-SQL Time Limit
       - Click Create Database Link button

    ![](images/emratlab1step10e.png " ")

       - Enter Name :  **PSALES.SUBNET.VCN.ORACLEVCN.COM**
       - Enter Net Service Name :
      ```
      <copy>"(DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = emcc.marketplace.com)(PORT = 1523)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = psales.subnet.vcn.oraclevcn.com)))"</copy>
      ```
         (need to include double quote "")
       - Click on Public - This database link is available to all users
       - Pick Fixed User
       - Enter Username : **SYSTEM**
       - Password : **welcome1**
       - Click Ok

    ![](images/emratlab1step10f.png " ")

       - Click Search button then pick Database Link  **PSALES.SUBNET.VCN.ORACLEVCN.COM**

    ![](images/emratlab1step10c.png " ")

       - **Check** Trial environment established
       - **Click** Submit

13. Back to SQL Performance Analyzer Home page, to check the status of the task run.

    ![](images/emratlab1step11a.png " ")

       - Continue the Workflow **Click** SHSPATASK

    ![](images/emratlab1step11b.png " ")

14. Continue Step 3 in SPA Guided Workflow **SHSPATASK**, and create SQL Trial in Changed Environment

    ![](images/emratlab1step12a.png " ")

       - Enter SQL Trial Name : **SHSTS\_SQL\_TRIAL\_19C**
       - Enter Description : Sales History 19C Run
       - Creation Method: **Execute SQLs Locally**
       - Default per-SQL Time Limit
       - **Check** Trial environment established
       - **Click** Submit

    ![](images/emratlab1step12b.png " ")

15. Back to SQL Performance Analyzer Home page, to check the status of the task run.

    ![](images/emratlab1step13.png " ")

       - Continue the Workflow **Click** SHSPATASK

16. Continue Step 4 in SPA Guided Workflow **SHSPATASK**, and compare Step 2 and Step 3

    ![](images/emratlab1step14a.png " ")

       - Trial 1 Name : **SHSTS\_SQL\_TRIAL\_18C**
       - Trial 2 Name : **SHSTS\_SQL\_TRIAL\_19C**
       - Comparison Metric : **Buffer Get**
       - **Click** Submit

    ![](images/emratlab1step14c.png " ")

17. Continue Step 5 in SPA Guided Workflow **SHSPATASK**, View Trial Comparison report

    ![](images/emratlab1step15a.png " ")

    ![](images/emratlab1step15b.png " ")

       - **Click** one of the SQLID to check the detail of the SQL comparison

    ![](images/emratlab1step15c.png " ")


## Task 6: Tuning a SQL in a PDB - Optional

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “sysman/welcome1”.

    ![](images/8e45436e4fa48b9a5bda495da7b0a674.jpg " ")

2.  Once logged into Enterprise Manager, Select **Targets**, then **Databases** . Click on the **expand** icon on the left and click on the database **sales.subnet.vcn.oraclevcn.com**

    ![](images/63f4072fb3b311db561d2c284bc93ffe.png " ")

3.  You should now see the Database Home page.

    ![](images/611d814ca29dfc9f327a7c8159608093.jpg " ")

4.  From the Performance Menu Click on **Performance Hub**, then **ASH Analytics**.

    ![](images/ea10a67618855f3e0ce1a5f5c7157d71.jpg " ")

5.  In the bottom left of the page, Click on the **activity bar** for the SQL showing highest activity.

    ![](images/1530ad41444abf8120ba3a6bce8d9ba1.jpg " ")

6.  Now schedule the SQL Tuning Advisor by Clicking on the **Tune SQL** button.

    ![](images/4532cfdb72eeef8ade51f86d9974061e.jpg " ")

7.  Accept the default and Submit the **SQL tuning Job**.

    ![](images/528d1e6ee4c55f477811c554c2eeff99.jpg " ")

    ![](images/8aaa9d1d202302cd87c3870ffe51b956.png " ")

8.  Once the job completes. You should see the recommendations for either creating a profile or an index.

    ![](images/64e4e02ca8258d7c1fc54bec446b691a.png " ")

9.  Implement the SQL Profile recommendation. SQL Profiles are a great way of tuning a SQL without creating any new objects or making any code changes.

10. At this point let us now turn off the load: Change directory to scripts and execute the script ***1-db\_lab\_stop.sh*** as shown below

    ![](images/e032d591c5b1132ac156974c6abbe2f4.jpg " ")

    >Alternatively you can use the Enterprise Manager Job Scheduler capability to stop the job.

11. Navigate to Enterprise, then Job, then to Library

    ![](images/emjoblibnav.png " ")

12. Select the job *1-DB\_LAB\_STOP*

    ![](images/emjoblabstop.png " ")

13. And then Submit the job

    ![](images/emlabstopsubmit.png " ")

14. When the job is completed, the workload stops

    ![](images/emlabstopped.png " ")

<!-- This concludes the Database Performance Management lab activity. You can now move on to Real Application Testing lab activity. -->

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/lifecycle.html)

## Acknowledgements
- **Author** - Anusha Vojjola, and Björn Bolltoft, Oracle Enterprise Manager Product Management
* **Contributors** -  Shefali Bhargava, Rene Fontcha
* **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, July 2021
