# Problem Labels for Custom Apps-Logs

## Introduction

In this lab, you'll learn how to use a SQL query to pull data from DB Table and ingest each row as a log-record
"SELECT name,total_mb*1024*1024 as total,free_mb*1024*1024 as free FROM v$asm_diskgroup_stat where exists (select 1 from v$datafile where name like '+%')".

Estimated Lab Time: 10 minutes


### Objectives

In this lab, you will:
* Understand how DB Table Log Collection works (Study)
* Learn how to create a DB SQL Log Source for an existing DB Entity
* Create alarm if available free space is 30% or less


## **Task 1:**  Navigate to Detection Rules


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 09 2023
