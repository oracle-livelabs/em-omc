# Continuous Monitoring using Management dashboards

## Introduction

Let's do a walk through on continuous monitoring of E-Business Suite application and related infrastructure for a large enterprise using Management dashboards.

Estimated Lab Time: 20 minutes

Watch the video below for a quick walk-through of the lab.
[Continuous Monitoring using Management dashboards](videohub:1_99o2xtxy)

### Objectives

In this lab, you will:
* Continuous Monitoring using Management dashboards

## **Task 1:**  Continuous Monitoring using Management dashboards

1. Select 'Dashboards' from the top navigation dropdown in Log explorer to view the 'Dashboards'
   ![](images/la-nav-ebs-dashboard.png "Ui Desc")

2. Select Compartment as  **AIW25\_Log\_Analytics** in the 'Dashboards Scope' section on the left.

   ![](images/la-dash-ebs-compartment.png "Ui Desc")

3. Click on **E-Business Suite Overview** dashboard to see the monitoring dashboard for E-Business Suite.
   ![](images/la-dash-ebs.png "ebs dashboard")


4. Click **Custom** under **Time range** pickerSet, then Click on "Start and End Time".
   ![](images/la-dash-custom-time.png "Ui Desc")

5. Select START time as **Sep 1, 2022 12:00:00 AM**, END Time as **Sep 30, 2022 12:00:00 PM** and Click Apply.
   ![](images/la-custom-time-selection.png "Ui Desc")


6.  Click on **Open/Close filter panel** to close the filter panel.
      ![](images/close-filter-panel.png "close filter")

 
7. A dashboard with multiple widgets is displayed.
 
8. High level view of the E-business application with Active Business Checks, Failed Business Checks and Monitored Components can be seen within below widgets.
   ![](images/ebs1.png "ebs1")

 
9. Topological view showing the interconnected structure of application, middleware, database and compute components can be seen using below widget.
   ![](images/ebs2.png "ebs2")

10. Geo map showing the locations from which the applications are accessed, helping to identify hotspots.
   ![](images/ebs3.png "ebs3")

11. Charts showing distribution of various errors in the application.
   ![](images/ebs4.png "ebs4")

12. A word cloud of various problem labels in each of the entity.
   ![](images/ebs5.png "ebs5")

13. Details of the functional issues in the application including product areas, business impact, SR etc.
   ![](images/ebs6.png "ebs6")

14. Analysis of requests and monitored systems.
   ![](images/ebs7.png "ebs7")









         
   
## Acknowledgements
* **Author** - Gurusamy Poosamalai, Log Analytics Development Team, Supriya Joshi, Log Analytics Development Team
* **Contributors** -  Kumar Varun, Log Analytics Product Management, Jolly Kundu - Log Analytics Development Team
* **Last Updated By/Date** - Sep 10 2025
