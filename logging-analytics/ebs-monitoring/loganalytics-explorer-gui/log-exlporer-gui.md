# Get Familiar with Logging Analytics Explorer GUI

## Introduction

Let's do a walk through of Log Explorer, which should be the current view on OCI Console.

Your should see a page similar to the one below showing the distribution of different types of logs currently being collected in this tenancy in the last 60 minutes.

Estimated Lab Time: 10 minutes


### Objectives

In this lab, you will:
* Navigate to Log Explorer
* Familiarize user interfaces used in Log Explorer GUI

## **Task 1:**  Navigate to Log Explorer GUI

Open the navigation menu and click **Observability & Management**. Under **Logging Analytics** click **Log Explorer**.
![](./images/oci-console-la-explorer.png " ")

You can also copy-paste the following link to your browser to open fresh Log Explorer.

```
<copy>
https://cloud.oracle.com/loganalytics/explorer?viz=pie&scopeFilters=lg%3Aocid1.compartment.oc1..aaaaaaaaxujlxdn7x745hunya7vhmu3odkxcp4c4vkczi5c2gilbksokvdna%2Ctrue%3Ben%3Aroot%2Ctrue
</copy>
```

## **Task 2:**  Familiarize user interface used in Logging Analytics

Here are the main parts of the user interface that will be used throughout this lab.

![](images/la-explorer-side-by-side.png "Virtual Desktop")

1. **Scope Filter** for setting Entity and Log Group Compartment scope for exploration.

2. **Time range** picker, and **Actions** menu where you can find actions such as, *Open*, *Save*, and *Save as*.

3. **Query bar**, with **Clear**, **Search Help** and **Run** buttons at the right end of the bar.

4. **Fields panel**, where you can select sources and fields to filter your data.

5. **Visualization panel**, where you can select the way to present search data in a form that helps you.

6. **Main panel**, where the visualization outputs appear above the results of the query.

Around 800+ different types of logs (Log Sources) are being collected in Logging Analytics ranging from logs from Oracle Database to Linux OS to Packaged Applications to Cloud Services.

Note: You are working with live logs so it may take a few minutes for logs to show up in your Log Explorer view. Click the **Run** button to re-run the query.

You'll learn log analytics basics and how to use Log Explorer GUI in the next section.

## Acknowledgements
* **Author** - Gurusamy Poosamalai, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management, Jolly Kundu - Logging Analytics Development Team
* **Last Updated By/Date** - Aug 24 2022
