# Continuous Monitoring using Management dashboards

## Introduction

Let's do a walk through on continuous monitoring of E-Business Suite application and related infrastructure for a large enterprise using Management dashboards.

Estimated Lab Time: 20 minutes


### Objectives

In this lab, you will:
* Continuous Monitoring using Management dashboards

## **Task 1:**  Continuous Monitoring using Management dashboards

1. Select 'Dashboards' from the top navigation dropdown in Log explorer to view the 'Dashboards'
   ![](images/la-nav-ebs-dashboard.png "Ui Desc")

2. Select Compartment as 'ebs-lab-9522' in the 'Dashboards Scope' section on the left.

   ![](images/la-dash-ebs-compartment.png "Ui Desc")

3. Click on "E-Business Suite Overview" dashboard to see the monitoring dashboard for E-Business Suite and Virtual Cloud Network Flow Logs analysis.
   ![](images/la-ebs-dashboard.png "Ui Desc")

4. Click **Custom** under **Time range** pickerSet, then Click on "Start and End Time".
   ![](images/la-dash-custom-time.png "Ui Desc")

5. Select START time as **Sep 1, 2022 12:00:00 AM**, END Time as **Sep 30, 2022 12:00:00 PM** and Click Apply.
   ![](images/la-custom-time-selection.png "Ui Desc")

6. The below widget shows Virtual Cloud Network Flow Logs analysis like 'Max Packets In By Source Port' , 'Total Packets In by Destination Port'
   ![](images/la-dash-vcn-packets.png "Ui Desc")

7. The below widgets shows 'VCN Flow Logs Outbound Traffic', 'Traffic By Source IP' and 'Traffic By Destination IP'
   ![](images/la-dash-vcn-traffic.png "Ui Desc")

8. Scroll down to 'Functional Issues Overview' to view EBS Functional issues
   ![](images/la-dash-ebs-functional-overview.png "Ui Desc")

9. Click on the punch-out icon of the widget 'Functional Issues Overview' to analyze further.

   ![](images/la-dash-ebs-functional-issues.png "UIdescription")

10. Next, you can analyze further based EBS Functional Issues.

    ![](images/la-ebs-functional-issue1.png "UIdescription")
    ![](images/la-ebs-functional-issue2.png "UIdescription")

## Acknowledgements
* **Author** - Gurusamy Poosamalai, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management, Jolly Kundu - Logging Analytics Development Team
* **Last Updated By/Date** - Aug 24 2022
