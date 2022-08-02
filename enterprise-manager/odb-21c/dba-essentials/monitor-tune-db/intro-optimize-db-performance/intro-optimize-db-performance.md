# Optimize Oracle Database performance

## About this workshop

In this workshop, you will learn to use Oracle Enterprise Manager Cloud Control (Oracle EMCC) for monitoring the performance of your Oracle Database 21c instance and ensuring that it runs optimally. It analyzes the workload running on the database, identifies issues, and implements corrective actions. This workshop helps you to effectively diagnose performance problems using Automatic SQL Tuning Advisor.

Estimated Workshop Time:  1 hour 40 minutes

### Objectives

In this workshop, you will learn how to:

-   Monitor the state of Oracle Database
-   Diagnose problems and improve performance using Automatic SQL Tuning Advisor

### Prerequisites

This lab assumes you have -

-   A Free Tier, Paid or LiveLabs Oracle Cloud account

## Appendix 1: Overview of monitoring and tuning the Database

When problems occur in the database, it is important to perform accurate diagnosis in time. Sometimes you simply look at the symptoms and immediately start changing the system to fix those symptoms.  However, an accurate diagnosis of the problem significantly improves the performance of the database.

Oracle Database consists of a self-diagnostic engine called *Automatic Database Diagnostic Monitor (ADDM)*. ADDM helps the database to diagnose the problems and recommends how to resolve them. The database periodically collects snapshots of its state and workload. These snapshots are stored in *Automatic Workload Repository (AWR)*.

**Primary functions of ADDM**

-   Analyze the data in AWR on a regular basis
-	Identify the performance problems and determine their root cause
-   Provide recommendations for corrective measures

> **Note:** Since AWR is a repository of historical performance data, ADDM analyzes the performance issues after the diagnosis.

**Benefits of ADDM**

-  Generates Automatic Performance Diagnostic report by default
-  Diagnoses problems based on tuning expertise
-  Identifies the root cause of the problems and not the symptoms
-  Recommends solutions to improve database performance

However, it can take multiple tuning cycles to reach acceptable system performance. ADDM provides early warning of performance issues, which can help in development and testing of the database.

Using ADDM, you can resolve various performance issues, including but not limited to the following:

-   **CPU bottlenecks**   
	ADDM verifies whether or not the rate at which system process progresses is limited by the speed of the CPU.

-   **Undersized memory structures**   
	ADDM checks whether or not the SGA, PGA, and buffer cache are adequately sized.

-   **Input/output capacity issues**   
	ADDM checks whether or not the Input/Output system performs as expected.

-   **High load SQL statements**   
	ADDM verifies if any SQL statements consume excessive system resources.

-   **Database configuration issues**    
	ADDM checks if there is any evidence of incorrect sizing of log files, archiving issues, excessive checkpoints, or sub-optimal parameter settings.

### Automatic Performance Tuning features

Oracle Database provides different tools that enable you to gather information on the basis of the database performance. Using these tools, you can monitor performance, diagnose problems, and tune applications. You can administer and monitor the output of the tuning tools with Oracle EMCC.

The automatic performance tuning features include:

-   **AWR**  
    AWR collects, processes, and maintains performance statistics for problem detection and self-tuning purposes.

-   **ADDM**  
    ADDM analyzes the information collected by the AWR for possible performance problems with the Oracle Database.

-   **SQL Tuning Advisor**   
    This advisor allows a quick and efficient technique for optimizing SQL statements without modifying any statements.

-   **SQL Access Advisor**   
    This advisor advices on materialized views, indexes, and materialized view logs.

-   **End-to-End application tracing**  
    It identifies excessive workloads on the system from a particular user, service, or application component.

-   **Server-generated alerts**   
    These alerts automatically provide notifications when the database detects impending problems.

-   **Memory Advisors**   
    This advisor optimizes the memory for the database. Oracle Database uses memory advisors when automatic memory management is not enabled.

### Managing SQL Tuning Advisor

SQL Tuning Advisor takes one or more SQL statements as an input and performs tuning on the statements. The advisor not only provides recommendation along with a rationale but also displays the benefits the database expects. The recommendations include collecting statistics on objects, creating new indexes, restructuring SQL statements or creating an *SQL profile*. You can accept the recommendation to complete the tuning of the SQL statements.

### How the tuning works?

Oracle Database automatically runs SQL tuning advisor on high-load SQL statements that qualify as tuning candidates from the AWR. You can customize the attributes of the maintenance windows, including start and end time, frequency, and days of the week.

After the automatic SQL tuning begins, Oracle Database performs these steps:

1.  Identifies SQL candidates in the AWR for tuning

    The database analyzes statistics in AWR and generates a list of potential SQL statements that are eligible for tuning. These statements include high-load SQL statements that have a significant impact on the database.

    The database tunes only SQL statements that have high potential for improvement. It ignores recursive SQL and statements that were tuned recently (in the last month), Data Manipulation Language (DML), Data Definition Language (DDL), and SQL statements with performance problems caused by concurrency.

    The database selects the candidate SQL statements on the basis of their performance.  The database calculates the impact by summing the CPU time and the I/O times in AWR for the selected statement in the past week.

2.  Tunes each SQL statement individually by calling SQL Tuning Advisor

    During the tuning process, the database considers and reports all recommendation types, but it implements only SQL profiles automatically.

3.  Tests SQL profiles by implementing the SQL statement

	If the database recommends the SQL profile, it tests the new profile and implements the SQL statement both with and without the profile. If the performance improves at least threefold, then the database accepts the SQL profile, else automatic SQL tuning reports the recommendation to create an SQL profile.

4.  Implements the SQL profiles based on threefold performance improvement. This step is optional.

    The database considers other factors when it decides whether to implement the SQL profile. For example, the database does not implement a profile when the objects in the statement no longer represent the latest statistics.
    Every time the database compiles a SQL statement, the optimizer uses a search method on the basis of cost to build a best-cost plan. The optimizer tries to find a matching plan in the *SQL plan baseline*. 
	
	> **Note:** An SQL plan baseline is a set of plans the database accepts for the optimizer to use. 
	
	If it finds the match with the best-cost plan, then the optimizer proceeds with the plan, else it evaluates the cost of each plan you accept in the SQL plan baseline and selects the plan with the lowest cost. When the best-cost plan the optimizer finds does not match any plans in the plan history for the SQL statement, it suggests a new plan.

### What is an SQL Profile?

An SQL profile is a set of additional information specific to an SQL statement. Oracle Database uses this information to improve the execution plans. It contains corrections for the estimates provided by the optimizer. The SQL profile discovers these corrections during the Automatic SQL Tuning.

The SQL profile does not contain information about the individual execution plan. While selecting a plan, the optimizer considers the following information:

-   The environment, which contains the database configuration, bind variable values, optimizer statistics, data set etc.

-   The supplemental statistics in the SQL profile

If the environment or SQL profile change, then the optimizer creates a new plan.

SQL Tuning Advisor invokes the optimizer to generate recommendations. These recommendations  to implement SQL profiles appears in the SQL Tuning Advisor report. When you accept a profile, the database creates the profile and stores it in the data dictionary. You can use the SQL profiles with or without an SQL plan management.

The following diagram illustrates the SQL tuning process. It shows the SQL profile that each SQL statement has. The optimizer uses the profile and the environment to generate a query plan. In this example, the plan is in the SQL plan baseline for the SQL statement.

![SQL Profile](./images/sql-profile.png " ")
  
> **Note:** An SQL profile does not tie the optimizer to a specific plan. The plan fixes incorrect estimates and allows the optimizer the flexibility to pick the best plan as per the requirements.

Click on the next lab to **Get started**.

## Learn More

-   [Monitoring Performance](https://docs.oracle.com/en/database/oracle/oracle-database/21/admin/monitoring-the-database.html#GUID-901CA77F-A241-45C6-940F-6CA68E6D45CC)

-   [Automatic Database Performance Monitoring](https://docs.oracle.com/en/database/oracle/oracle-database/21/tdppt/automatic-database-performance-monitoring.html#GUID-5D73B7DC-BC9A-4029-A741-2BF9EBB45AE9)

-   [SQL Tuning](https://docs.oracle.com/en/database/oracle/oracle-database/21/tdppt/part-IV-sql-tuning.html#GUID-FED9A6D8-49BB-43BE-9F4D-336E6006D366)

## Acknowledgements

-   **Author** - Manisha Mati, Database User Assistance Development team
-   **Contributors** - Suresh Rajan, Jayaprakash Subramanian, Ashwini R, Manish Garodia
-   **Last Updated By/Date** - Manisha Mati, June 2022