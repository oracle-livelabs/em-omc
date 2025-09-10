# Advanced Troubleshooting using 'link' command

## Introduction
Your customers are reporting high response times for EBS application which is affecting customer satisfaction metrics, in addition to negatively impacting the business.

Let's do a walk through on troubleshoot and identify the problematic EBS jobs causing performance degradation and build a query for continuous monitoring.


Estimated Time: 20 minutes

Watch the video below for a quick walk-through of the lab.
[Advanced Troubleshooting using 'link' command](videohub:1_p9tpjdx4)

### Objectives

In this lab, you will:
* Use Advanced Troubleshooting using 'link' command
* Troubleshoot and identify the problematic EBS jobs causing performance degradation
* Build a query for continuous monitoring

## **Task 1:** Analyse **EBS Concurrent Requests** for Troubleshooting    

  1. Clear Scope Filter for Log Group Compartment and Entity selection.
  ![](images/la-scope-filter-clear.png "UIdescription")

  2. Click on "Actions" -> "Create New" to return to the default Log Explorer view

  ![](images/create-new.png "UIdescription")

  The below screenshot shows default view of Log Analytics explorer page.

  ![](images/default-landing-le.png "UIdescription")

  2. Next, you'll open a **Saved Search** by clicking Actions and then Open.  

  ![](images/open.png "UIdescription")

  3. Search and Select "ebs-lab-9522" in the "Widget Compartment" drop-down and search for keyword "EBS" and select "EBS Concurrent Requests Analysis" card and click 'Open'

  ![](images/ss-ebs-saved-search.png "UIdescription")

  The below screenshot is a saved search for "EBS Concurrent Request Analysis" for analysing the logs.

  ![](images/link-goal.png "UIdescription")

  4. This visualization shows concurrent request jobs running under different applications such as Receivables, Human Resources and size of the bubbles corresponds to the time-taken by those jobs. Hover on top of any bubble to see more details.

  ![](images/link-hover.png "UIdescription")

  Next, we want to slice-and-dice this data based on Time Taken, Application.

## **Task 2:** Slice-And-Dice log data based on **Time Taken**

  1. Click on the **Gear** icon on the top left of the chart and select **Filter Options** which will launch "Filter Options" a pop-up.

  ![](images/link-filter-options.png "UIdescription")

  2. Next, select "Show Search Filters" checkbox in 'Filter Options' pop-up. All other check-boxes should also be in selected state.

  ![](images/link-filter-select.png "UIdescription")

  3. Click Close, you will see list of Jobs running for every EBS Applications and time taken by each job to complete.

  ![](images/link-with-filter.png "UIdescription")

  4. Click on "3 mins, 48 sec (1)" which is the job with longest run-time to filter that job.

  ![](images/3-min-select.png "UIdescription")

  ![](images/3-min-select-1.png "UIdescription")

  This job with long run-time belongs to 'human resources' application and we want to know whether all HR jobs taking this long indicating application level problem.

## **Task 3:** Slice-And-Dice log data based on **Application**
In this task you will learn whether all HR jobs taking this long indicating application level problem.

  1. Deselect "3 mins, 48 sec (1)" to come to the same view as step #2 and click on 'human resources (19)' under the Application section in the chart.

  ![](images/hr-selected.png "UIdescription")

  2. This chart now show the time-taken by all the 'human resources' application job. You can hover on top of the two larger bubbles to identify which jobs were taking relatively longer time to complete.

  ![](images/data-update-process.png "UIdescription")

  As shown in the chart the 'data update process status report' job in 'human resources' application is taking long time to complete. You can now drill down into specific jobs to review analyze further by simply clicking on a bubble.

## Acknowledgements
* **Author** - Gurusamy Poosamalai, Log Analytics Development Team, Supriya Joshi, Log Analytics Development Team
* **Contributors** -  Kumar Varun, Log Analytics Product Management, Jolly Kundu - Log Analytics Development Team
* **Last Updated By/Date** - Sep 10 2025
