# Enterprise Manager Fundamentals: Monitoring Quick Tour
## Introduction
Oracle Enterprise Manager enables you to get complete monitoring visibility into your IT infrastructure, applications stack and applications that are critical to running your business.

- Single pane of glass monitoring for on-premises, hybrid, and Oracle Cloud Platform

- Comprehensive set of predefined performance and health metrics that enables lights-out monitoring of critical components in your environment, such as applications, application servers, databases, as well as the back-end components on which they rely, such as hosts and storage

- Rich set of alerting, incident management and notification capabilities to notify IT staff and integrate with your corporate ticketing systems

- Corrective Actions to auto-correct alerts and minimize service disruption

- Metric Extensions to monitor conditions specific to your environment

- Dynamic Runbooks to triage and resolve your incidents  

- Event Compression Policies to reduce your volume of incidents


Watch the video below for a quick walk-through of the lab.
[Enterprise Monitoring Quick Tour](videohub:1_voigdsx5)

### Objectives
The objective of this lab is to become familiar with Enterprise Monitoring capabilities using Oracle Enterprise Manager Cloud Control 13c.

### Prerequistes
This lab assumes you have:

- A Free Tier, Paid or LiveLabs Oracle Cloud account
- All previous labs successfully completed


*Estimated Time*: 108 minutes


### Lab Timing (Estimated)

  | **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  |--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **1**  | Enterprise Summary                              | 5 minutes       | Explore Enterprise Summary page and drill down to see a list of down targets. View the list of critical incidents created for the down targets. Filter the Status pane to display a list of Database Instance targets.                         | Enterprise Summary enables you to get complete visibility into the overall status and health of your managed environment.                                                                                                                                                                                                                                            |
  | **2**  | Incident Manager                                | 10 minutes       | Triage unassigned incidents from Incident Manager and acknowledge then assign an incident.                                                 | Incident Manager enables IT Staff to manage, track, and resolve actionable incidents in a collaborative way.|                                                                                                                                        
  | **3A**  | Dynamic Runbooks                               | 10 minutes       | Start a Dynamic Runbook session against an incident in Incident Manager.                                                 | Dynamic Runbooks are documented procedures (steps) that IT Staff follow to resolve an issue.                                                                                                                                                             
  | **3B**  | Dynamic Runbooks                               | 20 minutes       | Modify and publish a Dynamic Runbook draft.                                                 | Dynamic Runbooks are documented procedures (steps) that IT Staff follow to resolve an issue.  
  | **4**  | Metric and Collection Settings                         | 5 minutes       | Change the Warning and Critical threshold of a metric from Metric and Collection Settings page. Go to the All Metrics page and review the metric in context of the thresholds.                                                                                                           | Enterprise Manager provides out-of-box monitoring and alert thresholds for managed targets.  You can still customize these monitoring settings based on your requirements.                                                                                                                                                                                                                                                                                                                                 |
  | **5**  | Corrective Actions                          | 8 minutes       | Create a new Corrective Action and associate it with a metric. | Corrective actions allow you to specify automated responses to metric alerts, saving administrators time and ensuring issues are dealt with before they noticeably impact users.  A corrective action can also be used to gather diagnostic information for an alert.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  | **6**  | Metric Extensions                          | 5 minutes       | Test a Metric Extension on a target to see the results then deploy the same Metric Extension to multiple targets. | Metric Extensions let you extend Enterprise Manager's monitoring capabilities to cover conditions specific to your IT environment, thus enabling you to rely on Enterprise Manager as your single monitoring solution.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  | **7**  | Monitoring Templates                          | 5 minutes       | Create a Monitoring Template from a Database Instance target. Deploy the Monitoring Template to other Database Instance targets to standardize monitoring settings across the enterprise. | Monitoring Templates enable you to define and implement monitoring standards across all targets in your environment.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
  | **8**  | Administration Groups and Template Collections                          | 10 minutes       | View the hierarchy of an existing Administrator Group. Update the target property for a new target so it can automatically be added to an Administration Group and inherit monitoring settings from that group. | Administration Groups and Template Collections enable you to enforce monitoring standards and automate monitoring setup in a scalable way.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
  | **9**  | Incident Rules                          | 10 minutes       | Review out-of-the-box incident rules shipped with Enterprise Manager. View an example of an incident compression rule set. Create a simple incident rule set to email DBA when there is a critical DB alert. | Incident Rules enable you to automate common incident management and notification actions such as creation of incidents based on events, sending email to IT Staff, opening tickets, auto-assigning incidents, escalating incidents, etc.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
  | **10A** | Event Compression Policies                | 10 minutes |      View the out-of-box Event Compression Policies to reduce your incidents and create your own policy. | Event Compression Policies reduce overall event noise by compressing related events into a smaller set of actionable incidents.|                            
  | **10B** | Event Compression Analysis                | 10 minutes |      Test your policy using the Event Compression Analysis tool. | An Event Compression Analysis assesses the impact Event Compression Policies would have had on events that generated incidents over a selected time range in the past.
  |

## Task 1: Enterprise Summary

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”. 

    ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Summary”.

    ![Enterprise Manager welcome page](images/enterprise-summary/enterprise-to-summary-welcome-page.png " ")

3. Enterprise Summary presents a single pane of glass view of the health of your Enterprise assets.
The Overview pane shows the Target Status of your IT estate. The Status section shows aggregated target availability so you can get a sense of what percentage is UP vs DOWN at a quick glance. The Green slice of the pie are your targets that are up. The Red slice of the pie are the targets that are down. Targets in red may be down due to unscheduled outages. Let’s drill down and take a look at them.
 
    ![Enterprise Manager summary page](images/enterprise-summary/enterprise-summary-page.png " ") 

4. Click on the Red slice of the pie in the “Status” section. **Note:** You can ignore any differences between the count of targets in the screenshots vs. what you see in your lab environment. The number of targets may vary based on your lab environment.

    ![Enterprise Manager summary page, status section](images/enterprise-summary/pie-chart-red-slice.png " ")  

   If a dialog pops up, click on ‘Down’ again.

    ![Enterprise Manager summary page, status section](images/enterprise-summary/pie-chart-select-down-again.png " ")   

5. In Enterprise Manager we have an “All Targets” page, which shows all of the targets being monitored by EM. When we clicked on the Red slice of the pie, we essentially placed a filter on the All Targets page to display only Down targets. From here, you can click on the individual target to go to the Target Home Page and take necessary actions such as starting up a Database Instance.

    ![Enterprise Manager All targets page](images/enterprise-summary/down-targets-filtered.png " ")

6. Click on “Enterprise >> Summary” to go back to the Enterprise Summary page.

    ![Step to navigate back to Enterprise Manager summary page](images/enterprise-summary/enterprise-to-summary.png " ")

7. Any Incidents, Problems, and Jobs requiring attention is displayed on the Enterprise Summary page with the ability to drill down into them. Click on the incidents link ![Availability symbol](images/noentry.svg " ") for Availability.

    ![Enterprise Manager summary page, status section with Availability incidents selected](images/enterprise-summary/enterprise-summary-availability-link.png " ")

8. A list of critical incidents is displayed in Incident Manager. You can manage the incidents by acknowledging, assigning ownership, changing the priority or status, and more.

    ![A list of critical incidents is displayed in Incident Manager](images/enterprise-summary/incident-manager-availability-incident.png " ")

9. Click on “Enterprise >> Summary” to go back to the Enterprise Summary page.

10. You can also filter the view based on the target type. Click on the View dropdown in the “Overview” pane and select “Database Instance” to look at the database status.

    ![Enteprise Manager summary page, status section with filter for target type](images/enterprise-summary/enterprise-summary-database-instance.png " ")

11.	The Status pane is filtered for Database Instance targets and displays a breakdown of the database statuses.

    ![Enterprise Manager summary page, status section](images/enterprise-summary/enterprise-summary-db-instance-filter.png " ")

12.	The right hand pane of the Enterprise Summary page also has Inventory and Usage, Compliance Summary, and Patch Recommendations sections. Inventory and Usage shows a breakdown of database inventory by release. Compliance Summary shows the compliance score for the selected targets as well as security recommendations. Patch Recommendations links to MOS and shows the recommended patches for your targets.

     ![ Enterprise manager summary page, Compliance Summary, and Patch Recommendations sections](images/enterprise-summary/enterprise-summary-inventory-compliance.png " ")


## Task 2: Incident Manager

Incident Manager provides in one location the ability to search, view, manage, and resolve events, incidents and problems impacting your environment.

1. Open a new terminal in your remote desktop.

     ![Open a new terminal](images/incident-manager/open-new-terminal.png " ")

2. Execute the following script "./scripts/livelabs/update-incidents.sh".

     ![Execute a script](images/incident-manager/execute-script.png " ")

     ![Execute script results](images/incident-manager/execute-script-results.png " ")

3. Close out of the terminal.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

    ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Monitoring >> Incident Manager”.

    ![Enterprise Manager welcome page](images/enterprise-manager-welcome-to-incident-manager.png " ")

3. In Incident Manager, the Views section contains out-of-box views that comes shipped with Enterprise Manager. You can create your own views and share with others as well. By default, “All open incidents” view is displayed.

    ![Incident Manager page](images/incident-manager/all-open-incidents.png " ")

4. We will triage unassigned incidents and then acknowledge and assign an incident to an owner. Click on the incident with Summary text “The database status is UNKNOWN”. Details of the incident will be displayed in the bottom pane.

    ![Incident Manager page](images/incident-manager/db-status-unknown-selected.png " ")

5. Click on “Open in new tab” link to open the incident on a separate tab. You may need to temporarily allow popups in the browser.
    ![Incident Manager page](images/incident-manager/open-in-new-tab.png " ")


6. The General tab of this incident contains 5 sections.

      - Incident Details contains information about the incident such as target name, creation date, type, and summary.
      - Metric Data shows the warning and critical thresholds and the last known value of this metric alert event.
      - Tracking provides the priority, status, and ability to manage the lifecycle of the incident.
      - Guided Resolution provides the ability to diagnose and take action to resolve the incident.
      - Runbook Sessions provides options to start, create, or view a runbook session against the incident.

     ![Incident Manager page, Incident details](images/incident-manager/general-tab-sections.png " ")

7. Click on “Acknowledge” in the Tracking section to acknowledge the incident. This will automatically assign the incident to the user acknowledging the incident.

     ![Incident Manager acknowledge button](images/incident-manager/incident-acknowledge-button.png " ")

     ![Incident Manager acknowledged completed](images/incident-manager/incident-acknowledged.png " ")

8. Click on “Manage”.

     ![Incident Manager page, manage](images/incident-manager/incident-manage-button.png " ")

9. Update the Status, Priority, and Escalation fields. Add a short comment and click OK.

     ![Incident details, manage incident pop-up box](images/incident-manager/incident-manage-popup.png " ")

10.	A confirmation is displayed with the Tracking section updated.

     ![Incident Manager page, Incident details](images/incident-manager/incident-manage-saved.png " ")

11.	Close the Incident Details tab and go back to the Incident Manager tab.

12.	Click on the Dashboard button next to “Incident Manager: All open incidents”.

     ![Incident Manager page](images/incident-manager/incident-select-dashboard.png " ")

13.	Incident Dashboard provides a holistic view of your incidents. It contains 3 sections.

       - Summary: Count of incidents that are open, fatal, escalated, unassigned, and unacknowledged. These are the incidents that need to be triaged or worked on immediately. Fatal and Escalated count are highlighted in Red by default.
       - Charts: Provides an easy-to-understand look at the current incident distribution and management status for each incident. Drill down capability with stackable filters to slice and dice data any way you like. Customize to add/update/remove charts to provide a personalized view in Incident Manager.
       - Incident List: Shows the open incidents listed in reverse chronological order by last updated time stamp. From this list, you can perform requisite incident lifecycle actions such as escalating, prioritizing, acknowledging, assigning owners, and adding comments to the incident. The incident list will reflect any filters applied.

     ![Incident Manager, Incident Dashboard](images/incident-manager/incident-dashboard-view.png " ")

14.	Click on the “Fatal” link to drill down into these incidents.

     ![Incident Manager, Incident Dashboard](images/incident-manager/incident-dashboard-select-fatal.png " ")

15.	Incident Dashboard is filtered for incidents with “Fatal” severity.

     ![Incident Manager, Incident Dashboard](images/incident-manager/incident-fatal-filtered.png " ")

     
## Task 3A: Dynamic Runbooks

Runbooks are documented best practice procedures that IT staff follow to resolve an issue. In Enterprise Manager, you can create Dynamic Runbooks to encapsulate your best practice procedures in the form of steps that your ITOps teams can execute inside Enterprise Manager in context of an incident. To use Dynamic Runbooks, you start a Runbook Session against an incident, choose a Dynamic Runbook, and then follow the steps in the runbook.

For this task, a Dynamic Runbook has already been published for you to use. You will go through the process of starting a Runbook session against a designated incident.

**Note: Only complete steps 1-3 if you did not complete them in Task 2: Incident Manager.**

1. Open a new terminal in your remote desktop.

     ![Open a new terminal](images/incident-manager/open-new-terminal.png " ")

2. Execute the following script "./scripts/livelabs/update-incidents.sh".

     ![Execute a script](images/incident-manager/execute-script.png " ")

     ![Execute script results](images/incident-manager/execute-script-results.png " ")

3. Close out of the terminal.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Enterprise >> Monitoring >> Incident Manager".
     
     ![Navigate to Incident Manager](images/enterprise-monitoring-incident-manager-3a.png " ")

3. In Incident Manager, the “All open incidents” view is displayed by default. In this view, highlight the incident with Summary text “The value of the Fast Recovery Area % Used is 83.446”. Details of the incident will be displayed in the bottom pane.

     **Note**: The Fast Recovery Area (FRA) is a unified storage location for all Oracle Database files related to recovery.  

     ![Highlighted Incident](images/runbooks/fra-incident-highlighted-with-details.png " ")

4. In the bottom pane, you should see a section called "Runbook Sessions".

     ![Runbook Sessions section in Incident Manager](images/runbooks/fra-incident-details-runbook-sessions.png " ")

5. Under "Start Runbook Session", select the runbook named “Fast Recovery Area Triage”.

     ![Start Runbook Session](images/runbooks/fra-start-runbook-session.png " ")

5. You have now started a Runbook session, opened in a new browser tab. Here you can see a detailed view of the steps needed to run the Runbook and triage the issue. Notice the incident details are carried over.

     ![Incident details carried over to runbook session](images/runbooks/fra-incident-details-highlighted.png " ")

11. The Overview & Prerequisites step describes what the Runbook does and the prerequisites needed to run it. In this lab, the prerequisites have already been completed for you. You should have access to the Named Credential, **CDB186\_SYS**, for the target database. Access to this Named Credential will allow you to successfully run through all the steps.

     ![Overview & Prerequisites Step](images/runbooks/fra-step1-highlighted.png " ")

12. Click the play icon in Step 2 to review the metric that triggered the incident. The red vertical dotted line indicates when the incident happened. 

     ![Review the Metric - Step 2](images/runbooks/fra-step2-highlighted.png " ") 

13. Next, go to Step 3 and click the hyperlink for “What’s FRA”. This will open another browser tab to official Oracle documentation on Fast Recovery Area. Runbooks support hyperlinks to external sites to allow you to provide further context for a step that is needed to triage an incident.

     ![What's FRA](images/runbooks/fra-step3-whats-fra-highlighted.png " ")

     ![What's FRA link opened](images/runbooks/fra-whats-new-oradocs.png " ")

14. Close out of the Oracle documentation tab.

14. In Step 3, click the play icon to check the FRA size of the database. A table appears, displaying the FRA size for the database. It is 13 Gigabytes (GB). However, based on the Runbook instructions, the FRA size must be set to at least 50GB to comply with the company’s database standards. Therefore, you will need to increase the FRA size.

     ![Check FRA Size - Step 3](images/runbooks/fra-step3-highlighted.png " ")

15. Before increasing the size, first identify the filesystem used by the FRA. Click the play icon in Step 4.

     ![Identify filesystem - Step 3](images/runbooks/fra-step4-highlighted-not-run.png " ")

16. A table appears with the FRA filesystem path. Make a note of this filesystem path. You will need this for the next Runbook step. 

     ![FRA filesystem path - Step 4](images/runbooks/fra-step4-filesystem-highlighted.png " ")

17. Let's move on to Step 5. Remember in previous steps we determined that the FRA size was below the minimum threshold (i.e., it was 13GB but should be at least 50GB). Before we can increase to meet the requirements, we should check that the filesystem has enough space to increase the FRA size. 

18. Notice for Step 5 a gear icon is displayed instead of the play icon. The gear icon means some input properties are required before you can execute the step. Click the gear icon.

     ![Check filesystem space - Step 5](images/runbooks/fra-step5-unlock.png " ")

19. A pop-up will appear. Step 5 requires you to specify a value before you can run the step. To enable the step, enter the following filesystem path into the text field: "/u01/app/cdb186/fast\_recovery\_area" or copy it from Step 4. Click Save.

     ![Specify value - Step 5](images/runbooks/fra-step5-specify-values-blank.png " ")

     ![Specify value complete - Step 5](images/runbooks/fra-step5-specify-values-complete.png " ")

20. The gear icon switches to a play icon indicating that you may now run the step. Click the play icon. 

     ![Run Step 5](images/runbooks/fra-step5-highlighted.png " ")

18. There is 70GB available in the filesystem where the FRA is located. This shows that there is enough space for us to increase the FRA size.

     ![70GB available in the filesystem  - Step 5](images/runbooks/fra-step5-ran.png " ")

22. To change the FRA size to 50GB, click the play icon in Step 6. You should see a table that indicates that you have successfully increased the FRA size. Increasing the FRA size allows the FRA percent used to decrease.

     ![Change FRA  - Step 6](images/runbooks/fra-step6-ran.png " ")

23. Run Step 7 to view the updated FRA size and to confirm that it has been set to at least 50GB which meets the FRA size required for the database.

     ![Double check FRA size](images/runbooks/fra-step7-highlighted-and-ran.png " ")

19. Step 8 describes the success criteria: once you have performed all the Runbook steps and the FRA size is sized appropriately, then this should have eventually resolved the issue. 

     **Note:** For the purpose of this lab, the metric incident was simulated and therefore may still remain in Incident Manager after these steps have been run.

     ![Success Criteria - Step 8](images/runbooks/fra-step8-highlighted.png " ")

20. The Runbook remains an active session until you Mark as Done. As an active session, your data will be saved which allows you to go back and run (or rerun) your steps. This is useful for cases where you may want to leave the session halfway through and return to complete it later.

21. Click “Mark as Done” to indicate that you have finished all the steps. Once you Mark as Done, you can no longer re-run any steps but you can continue to view the session in read-only mode. This will allow your team to do any post-mortem analysis of the incident and its triage steps. 

     ![Mark as Done](images/runbooks/fra-mark-as-done-highlighted.png " ")

22. Click OK.

     ![Mark as Done - OK](images/runbooks/fra-mark-as-done-ok-highlighted.png " ")

23. A page with all the Runbook Sessions that you have ran will appear. Click the arrow under the Actions column for the "Fast Recovery Area Triage" session to see the actions you can take after a session is complete. In the Actions menu that pops up, you can open the session to have a read-only view, extend the expiration of the session, or delete the session.

     ![Actions - Complete Runbook Session](images/runbooks/fra-runbook-sessions-page.png " ")
     

## Task 3B: Dynamic Runbooks

Runbooks are documented procedures that IT staff follow to resolve an issue. In Enterprise Manager, Dynamic Runbooks consist of a set of ordered steps that users execute to resolve an incident. To create a Dynamic Runbook, you create it in context of an incident. This runbook in development is called a runbook draft. The runbook draft will contain the incident context that includes the target, metric of the incident, etc. against which you can develop and test the runbook steps. Once runbook creation and testing is complete, it can be published for general use.  

For this task, a Dynamic Runbook draft has already been created. You will go through the process of modifying the Runbook and later publishing it to be used by others.  

**Note: Only complete steps 1-3 if you did not complete them in Task 2: Incident Manager or Task 3A: Dynamic Runbooks.**


1. Open a new terminal in your remote desktop.

     ![Open a new terminal](images/incident-manager/open-new-terminal.png " ")

2. Execute the following script "./scripts/livelabs/update-incidents.sh".

     ![Execute a script](images/incident-manager/execute-script.png " ")

     ![Execute script results](images/incident-manager/execute-script-results.png " ")

3. Close out of the terminal.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Enterprise >> Monitoring >> Runbooks".

     ![Navigate to Runbooks](images/enterprise-monitoring-runbooks.png " ")

3. The Runbooks page has Draft Runbooks and Published Runbooks. By default, the Drafts tab is opened. You can create a Runbook through this Runbooks page or directly against an incident in the Incident Manager page. Under the Drafts tab, select the "**New Runbook**" link. This is the Runbook draft that was created for you and that you will modify.
     
     ![Select New Runbook Draft](images/runbooks-page-new-runbook.png " ")

4. At the top of the page, the previous incident details are carried over. This is the incident that was selected to create a Runbook draft on. You can optionally edit the Runbook name and Description using the pencil icons next to them. 

     ![New Runbook Draft Page](images/runbooks/new-runbook-details.png " ")

5. There is an ‘Add a Step’ drop-down menu, where you can select the desired step type you want to define. There are five step types: Note, Metric Data, Repository SQL, Target SQL and OS Command. We have already added the steps for you in this Runbook draft.

     ![Add Step - New Runbook](images/runbooks/new-runbook-add-a-step-highlighted.png " ")

6. To begin modifying the Runbook Draft steps, select the pencil icon to edit Step 1 (Overview and Prerequisites). This step is a special step where you can specify the overall purpose of the runbook and any prerequisites that the user needs to have in order to successfully execute the steps. This step uses the Note step type. The Note step is used for any type of text meant to provide information or instructions. The Note can be plain text but can also accommodate simple formatting via markdown language.

     ![Step 1 Overview and Prereq - New Runbook](images/runbooks/new-runbook-edit-step1.png " ")  

7. In the text box, add 3 hash signs (###) followed by a space to the beginning of the first sentence, “This runbook can be used to triage and resolve FRA incidents,” to make it header 3.

     ![Step 1 H3 - New Runbook](images/runbooks/new-runbook-step1-hashes.png " ")  

8. Next, place three dashes (---) on their own line under the first sentence to create a horizontal line.

     ![Step 1 Horizontal Line - New Runbook](images/runbooks/new-runbook-step1-lines.png " ")  

9. Put two asterisks (**) on both sides of the “Prior to Beginning” text to make it bold. 

     ![Step 1 Asterisks - New Runbook](images/runbooks/new-runbook-step1-asteriks.png " ") 

10. Scroll down in the text box until you see the following sentence: “Make sure you have been granted access to the named credential for the target database **[target name]** on which the FRA Incident has occurred”.

     ![Step 1 Scroll to Target Name Placeholder - New Runbook](images/runbooks/new-runbook-step1-target-name.png " ") 

11. View the "Oracle Provided" section under the "Variables" section on the right side of the screen. Scroll until you see the field for "Target Name".

     ![Step 1 Oracle Variable for Target Name - New Runbook](images/runbooks/new-runbook-step1-variable-target-name.png " ")     

12. Replace the "[target name]" placeholder in the text box with the value displayed in the Variables table for Target Name: **$ora\_target\_name**. This will now replace the original "[target name]" placeholder text with the target name pulled from the context of the incident.

     **Note:** The list of Variables table can be used in runbook steps. The built-in variables contain the incident context such as target name, metric name, etc. You can also create your own variables for use in other steps.  

     ![Step 1 Target Name Placeholder Replacement - New Runbook](images/runbooks/new-runbook-target-name-replaced.png " ")  

13. Select Save Step to view the modifications to the text.

14. Your Overview and Prerequisites step should now look like this:
     
     ![New Step 1 - New Runbook](images/runbooks/new-runbook-step1-highlighted-complete.png " ") 

     The first sentence is now a header 3 with a horizontal line under it. The Prior to Beginning text is bolded. And the original [target name] placeholder text is populated by the name of the target from the incident.

15. Step 2 is a Metric Data step which is used to show the time series chart for the specified metric. Notice the instruction text of the step does not specify the actual metric name to review. Also, there is no graph displayed.

     ![Step 2 - New Runbook](images/runbooks/new-runbook-step2-highlighted.png " ") 

16. Click the pencil icon to make edits to Step 2. 

     ![Edit Step 2 - New Runbook](images/runbooks/new-runbook-step2-edit.png " ") 

17. To specify the metric name, edit the “[metric name]” placeholder to use the value "**$ora\_metric\_name**". This will populate the value with the text in the Metric Name field (e.g., FRAPercentUsed).

     ![Step 2 Specify Metric Name - New Runbook](images/runbooks/new-runbook-step2-metric-name.png " ")

18. Click on the Time Range field to modify the times shown in the graph. Change the Start Time field to "evt\_time – 169d" and the End Time field to "evt\_time + 14d". evt\_time represents the time when the event (and its incident) was triggered, and you can specify a range of time relative to this event time.

     ![Step 2 Change Time Range - New Runbook](images/runbooks/new-runbook-step2-time-range.png " ")

19.  Select Done. 

     ![Step 2 Time Range - Done](images/runbooks/new-runbook-step2-time-range-done.png " ")

20. Click the Run button to preview the metric graph. This should now show the graph and display the trend of the metric before and after it triggered the incident. 

     ![Step 2 Run to view Graph](images/runbooks/new-runbook-step2-run.png " ")

19. Click Save Step to save your changes for Step 2.

     ![Save step 2](images/runbooks/new-runbook-step2-save-step.png " ")

20. The metric name value should populate to "FRAPercentUsed", and a graph displays with a red vertical dotted line to indicate when the incident was triggered.

     ![New Step 2 - New Runbook](images/runbooks/new-runbook-step2-results.png " ")

21. Step 3 is a Target SQL Step. It allows you to execute SQL against any database target in Enterprise Manager. In our example, the current SQL query will need to be updated to properly check for flashback retention usage.

     ![Step 3 - New Runbook](images/runbooks/new-runbook-step3-highlighted.png " ")

22. Select the pencil icon to edit Step 3.

     ![Edit Step 3 - New Runbook](images/runbooks/new-runbook-step3-edit.png " ")

23. Under the Variables section, select the Add Variable button. 

     ![Add Variable Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable.png " ")

24. You will see a pop-up box labeled Add a Runbook Variable. 
     - In the Name field, enter "user\_flash". 
     - In the Display Name field enter "Flash like statement". 
     - In the Value used in the Draft field, enter "%flash%" without the quotes. 
     - And for the Value used in a Runbook Session field, you have the options to select the "User who runs the Runbook Session specify the value" or "Same value used in the draft". Select "Same value used in the draft".

     ![Add Variable Pop-up Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable-popup.png " ")


25. Click OK to save the variable.

     ![Save Variable Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable-popup-save.png " ")

26. Once the variable is saved, it should appear in the Variables section under "Author Defined". You will use this variable for the SQL query. 

     ![Variable Defined Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-variable-defined.png " ")

27. The current SQL query needs to be replaced to check for flashback retention usage. Replace the current SQL query with the following: "select name, value from v$parameter where name LIKE:$user\_flash"

     ![Replace Query Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-replace-query.png " ")

28. To test if the SQL query is correct, scroll to the bottom of the page and click the Run button. The display section should show a table with the flashback retention usage results, which should list 1440 (i.e., the standard value needed).

     ![Test Query Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-test-query.png " ")

29. Click Save Step.

30. Run Step 3 to view the new results from the updated query. The new results show that the flashback retention usage meets the standard value needed, 1440.

     ![New Step 3 - New Runbook](images/runbooks/new-runbook-step3-results.png " ")

31. You have now finished making edits to the Runbook and can publish it so that it can be used by others. **Note:** Your edits are automatically saved. At the top of the Runbook draft page click on the “Runbooks” link to go back to the Runbooks page.

     ![Runbooks Page Link from Step 3 - New Runbook](images/runbooks/new-runbook-go-back-to-runbooks-link.png " ")

32. The Runbook draft that you modified will be displayed in the Drafts tab and will have your updates.

     ![Runbooks Page with Updated Draft - New Runbook](images/runbooks/new-runbook-runbook-drafts-page.png " ")

33. Select the arrow under the Actions column to publish the Runbook for use.

     ![Publish Runbook Draft - New Runbook](images/runbooks/new-runbook-publish-draft.png " ")

34. Click OK. 

     ![Select Ok to Publish Runbook Draft - New Runbook](images/runbooks/new-runbook-publish-draft-popup.png " ")

35. The "New Runbook" that you made modifications to has now been published and can now be used by other EM users. 

     ![Published Runbook - New Runbook](images/runbooks/new-runbook-published-and-highlighted.png " ")

36. Select the arrow under the Actions column for the "New Runbook". You have the options to create a like version, create a new version, export the runbook, hide it or delete.

     ![Actions on Published Runbook - New Runbook](images/runbooks/new-runbook-published-actions.png " ")

37. Also, please note that Oracle provides out-of-the-box Runbooks for use.

     ![OOB Runbook](images/runbooks/oob-runbooks-highlighted.png " ")

38. To preview the Runbook steps for the out-of-the-box Runbook, click on the Runbook name, "Loader Issues causing Agent backoff requests (Oracle)". You can click on the steps to view more details. **Note:** In cases like this where there are multiple Runbooks, the preview can help you decide which Runbook to use.  

     ![Preview OOB Runbook](images/runbooks/oob-runbooks-steps.png " ")

39. Click close when you are done previewing the steps.


## Task 4: Metric and Collection Settings

Metric and Collection Settings page is where we can view and configure thresholds, collection schedules, and Corrective Actions for the metrics being monitored for the target.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Targets >> Databases” to see the list of Database targets.

     ![Enterprise Manager welcome page](images/emmonlab3step2.png " ")

3. Click on “cdb186.subnet.vcn.oraclevcn.com” to go to the target home page.

     ![Databases page](images/emmonlab3step3.png " ")

4. Navigate to “Oracle Database >> Monitoring >> Metric and Collection Settings”.

     ![Database target home page](images/emmonlab3step4.png " ")

5. Oracle ships with default out-of-box Metrics and settings. This includes Metrics, Thresholds, and Collection Schedules. This aims to cover generic use cases to get you started. We recommend that you customize the monitoring settings of your targets according to your requirements.
What we’re looking at right now are database metrics with default settings. These are recommended settings; however, you can modify anything to suit your needs.
As Best Practice:
      - Disable collection for metrics you don’t care about.
      - Set thresholds only on metrics you want to be alerted on.
      - Save the modified metric settings and apply to targets using monitoring templates.

     ![Database target home page, metric and collection settings](images/emmonlab3step5.png " ")

6. By default, the "Metrics with thresholds" view is displayed. This view will show metrics with a Warning or Critical threshold defined.

     ![Database Target Home Page, metric and collection settings](images/emmonlab3step6.png " ")

7. There are other out-of-box views available to select from.

     ![Database target home page, metric and collection settings](images/emmonlab3step7.png " ")

8. Scroll down to “Dump Area Used (%) metric and click on the “Every 30 Minutes” Collection Schedule link.

     ![Database target home page, metric and collection settings](images/emmonlab3step8.png " ")

9. Change the Collection Schedule to 15 minutes and click Continue.

     ![Database target home page, metric and collection settings](images/emmonlab3step9.png " ")

10.	Scroll down to Dump Area Used (%) metric again. Click on the Edit icon to change the Warning and Critical thresholds.

     ![Database target home page, metric and collection settings](images/emmonlab3step10.png " ")

11.	Currently the Warning threshold is set to > 95%. Change the Warning threshold to 85% and Critical threshold to 95% and click Continue.

     ![Database target home page, metric and collection settings](images/emmonlab3step11.png " ")

     The new thresholds should appear in the main Metric and Collection settings page.

12.	Click OK to save changes, then you should see a Confirmation message . Click OK.

     ![Database target home page, metric and collection settings](images/emmonlab3step12pt1.png " ")

     ![Database target home page, metric and collection settings confirmation message](images/emmonlab3step12.png " ")

13.	Navigate to “Oracle Database >> Monitoring >> All Metrics”.

     ![Database target home page](images/emmonlab3step13.png " ")

14.	The All Metrics page shows the collected data for all of the metrics on the target.

     ![Database target home page, all metrics](images/metric-settings/all-metrics-page.png " ")

15.	Expand and highlight the Dump Area Metric Group.

     ![Database target home page, all metric](images/metric-settings/dump-area-expanded.png " ")

16.	Click on Dump Area Used(%) under the All Metrics palette and then click on the ‘background’ first row in the Dump Area Used(%) table.  

     ![Database target home page, all metric](images/metric-settings/dump-area-used-background.png " ")

17.	You should see the metric data for Dump Area Used(%) for the background processes.  By default, the last 24 hours are shown but you can change time periods using the View Data dropdown.  In the metric chart, click on Options to view different options for the chart, then click on the Show Thresholds option.

     ![Database target home page, all metric](images/metric-settings/show-thresholds.png " ")

18. The Warning and Critical thresholds for the metric will now be shown with the chart as yellow and red lines respectively.  As you review the metric, you can also visually see how close the metric values are to its Warning and Critical thresholds. Notice the metric has passed the new Warning threshold of 85. When the next metric collection occurs, the metric will be evaluated against the new Warning threshold of 85 and should generate a Warning alert. (Note: You do not have to wait for the alert, you can move on to the next lab).

     ![Database target home page, all metric](images/metric-settings/warning-and-critical-shown.png " ")

## Task 5: Corrective Actions

Corrective Actions automates response to metric alerts and events. A Corrective Action can start the DB listener when it unexpectedly goes down or it can run shell scripts to collect diagnostic data. You can create a custom Corrective Action once and grant access for other Admins to use. We ship with a long list of pre-defined Corrective Actions to get you started.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Monitoring >> Corrective Actions”.

     ![Enterprise Manager welcome page](images/emmonlab4step2.png " ")

3. Select “Add Space to Tablespace” from the “Create Library Corrective Action” drop down field and click Go. This Corrective Action will automatically increase tablespaces should they reach a user defined threshold.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step3.png " ")

4. Give the Corrective Action a name and click on the “Parameters” tab.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step4.png " ")

5. There are a number of parameters available for the Add Space to Tablespace corrective action. These parameters can be adjusted according to your needs. For the purpose of this lab, we will leave the parameter values as is and click on Save to Library.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step5.png " ")

6. The Corrective Action is created in Draft status. This gives you an opportunity to test your Corrective Action first before making it available for general use.  For this lab, let’s assume we are ready to make it available for general use. Click on Publish to publish the Corrective Action.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step6.png " ")

7. Click on Yes to confirm you want to publish the Corrective Action.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step7.png " ")

8. A Confirmation banner will appear at the top of the page.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step8.png " ")

9. Navigate to “Targets >> Databases”.

     ![Enterprise Monitoring, corrective actions page](images/emmonlab4step9.png " ")

10.	Click on the link for “finance.subnet.vcn.oraclevcn.com” database instance.

     ![Databases page](images/emmonlab4step10.png " ")

11.	Navigate to “Oracle Database >> Monitoring >> Metric and Collection Settings”.

     ![Database target home page](images/emmonlab4step11.png " ")

12.	Scroll down to “Tablespace Space Used (%)” metric and click on the Edit icon.

     ![Database target home page, metric and collection settings](images/emmonlab4step12.png " ")

13.	Click on Edit in the “Monitored Objects” section.

     ![Database target home page, metric and collection settings](images/emmonlab4step13.png " ")

14.	Click Add next to the Warning field under the Corrective Actions section.

     ![Database target home page, metric and collection settings](images/emmonlab4step14.png " ")

15.	Select the Add Space to Tablespace Corrective Action that you just created and click Continue.

     ![Database target home page, metric and collection settings with add corrective actions pop-up](images/emmonlab4step15.png " ")

16.	Notice there is now a Corrective Action specified for Warning threshold violations. The Corrective Action will trigger when Tablespace Space Used (%) >= 85%. Also notice the Warning message at the top of the screen indicating that the metric settings for the target are managed by the monitoring templates associated through the Administration Groups.  Administration Groups will be discussed in Task 8 below, but this message indicates that if we want to keep this setting (i.e. associating the corrective action for this metric), you will also need to click on the ‘Template Override’ option at the bottom of the screen. Click Continue.

     ![Database target home page, metric and collection settings](images/emmonlab4step16.png " ")

    In the screen that comes up, click Continue.

     ![Database target home page, metric and collection settings](images/emmonlab4step16b.png " ")

17.	Click OK.

     ![Database target home page, metric and collection settings](images/emmonlab4step17.png " ")

    Click Continue.

     ![Database target home page, metric and collection settings](images/emmonlab4step17b.png " ")

    Click OK.

     ![Database target home page, metric and collection settings](images/emmonlab4step17c.png " ")

## Task 6: Metric Extensions

Metric Extensions expand Oracle's monitoring capabilities to monitor conditions specific to your IT environment. It allows you to create custom metrics on any target type. You can create it once and deploy it to multiple targets at once.

For this lab, a metric extension has already been created and is in Editable status.  As part of creating a metric extension, you can test it against some targets.  You will go through the process of testing the metric extension against some targets.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.
    ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Monitoring >> Metric Extensions”.
    ![Enterprise manager welcome page](images/emmonlab5step2.png " ")

3. Highlight ME$RunawaySQL metric extension.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step3.png " ")

4. Click on Actions >> Edit.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step4.png " ")

5. Steps 1 through 4 show the SQL and the metric columns of the metric extension that has been already defined for you. Click on Next until you reach “step 5 of 6”.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step5.png " ")

6. Click Add to select targets to test the Metric Extension.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step6.png " ")

7. Hold down the Control key (or the Command Key on Mac) and select 2 database instance targets to test the Metric Extension.

    ![Enterprise Monitoring, metric extensions page with Select targets pop-up](images/emmonlab5step7.png " ")

8. Click on Run Test.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step8.png " ")

9. The Test Results section shows the results of running the Metric Extension on the selected targets. Note: The Test Results may vary based on your lab environment.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step9.png " ")

10.	Click Finish.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step10.png " ")

11.	Highlight ME$RunawaySQL metric extension again and select Actions >> Save as Deployable Draft. At this point, you could deploy the metric extension to different test targets and review the metric data.   If you need to make changes to the metric definition, you will need to create a new version.  For now, let’s assume we’ve reviewed the metric data, verified it is correct and are ready to publish.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step11.png " ")

12.	Click on Actions >> Publish Metric Extension. Once published, the metric extension is ready for general use.  

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step12.png " ")

13.	Click on Deploy To Targets.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step13.png " ")

14.	Click Add and select the same targets that you tested on.

    ![Enterprise Monitoring, metric extensions page with select targets pop-up](images/emmonlab5step14.png " ")

15.	Click Submit to deploy the metric extension to the selected targets.

    ![Enterprise Monitoring, metric extensions deploy to targets page](images/emmonlab5step15.png " ")

16.	A confirmation banner will appear confirming the deployment has been submitted. The Status of the deployment will be “Scheduled”. Manually click on the page refresh icon.

    ![Enterprise Monitoring, metric extensions pending operations page](images/emmonlab5step16.png " ")

17.	When the list is empty in the Pending Operations page, it means the deployment has completed. Click on the Metric Extensions link.

    ![Enterprise Monitoring, metric extensions pending operations page](images/emmonlab5step17.png " ")

18.	The Metric Extensions page shows the ME$RunawaySQL metric extension has been deployed to 2 targets. The RunawaySQL metrics will start to be collected for the 2 targets.

    ![Enterprise Monitoring, metric extensions page](images/emmonlab5step18.png " ")

## Task 7: Monitoring Templates

Monitoring templates enable you to deploy standardized monitoring settings across the targets in your data center. Enterprise Manager allows you to define monitoring settings on one target, and deploy the same settings to other targets. This feature is called Monitoring Template. When a change is made to a template, you can reapply the template across affected targets in order to propagate the new changes. The apply operation can be automated using Administration Groups and Template Collections. For any target, you can preserve custom monitoring settings by specifying metric settings that can never be overwritten by a template.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

    ![Enterprise manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Monitoring >> Monitoring Templates”.

    ![enterprise manager welcome page](images/emmonlab6step2.png " ")

3. Click on Create.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step3.png " ")

4. You can initialize the contents of a monitoring template by copying the existing monitoring settings of a target. Click on the Search icon to search for a target.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step4.png " ")

5. Select Database Instance target type then select cdb186.subnet.vcn.oraclevcn.com.

    ![Enterprise monitoring, monitoring templates page with Search and Select targets pop-up](images/emmonlab6step5.png " ")

6. Click Continue.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step6.png " ")

7. Give the Monitoring Template a meaningful name then click on “Metric Thresholds” tab.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step7.png " ")

8. Any changes can be made to Metric Thresholds and Other Collected Items before saving the Monitoring Template. Click OK to save the template.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step8.png " ")

9. The Monitoring Template is created and we will apply the template to another Database Instance target. Highlight the Monitoring Template you just created and click Apply.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step9.png " ")

10.	In the screen that comes up, click on ‘Add’ to add a target.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step10a.png " ")

    Select db19c.subnet.vcn.oraclevcn.com target.   

    ![Enterprise monitoring, monitoring templates page with select targets pop-up](images/emmonlab6step10.png " ")  

11.	Click Finish to apply the Monitoring Template to the selected target.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step11.png " ")

12.	A Confirmation banner will appear and the Status of the Apply Operation shows Pending.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step12.png " ")

13.	Manually click on the Page Refresh icon. The status of the template apply operation is now Passed.

    ![Enterprise monitoring, monitoring templates page](images/emmonlab6step13.png " ")

## Task 8: Administration Groups and Template Collections

Administration Groups are designed to simplify the process of setting up targets for management in Enterprise Manager. Typically, management settings such as monitoring settings and compliance standards are applied to a target manually or by custom scripts defined by the administrator. With Administration Groups, you first define a hierarchy of Administration Groups where targets in each group have the same management settings.  Next for each Administration Group, define and combine management settings (e.g. monitoring settings, compliance standards and cloud policies) into a container (called template collections) and associate them with the appropriate Administration Group. Once that one-time setup is done, all you need to do is add the target to the appropriate Administration Group, and Enterprise Manager will automatically apply the associated management settings to the target as it joins the group.  This greatly simplifies and streamlines the process of target setup. It also enables a datacenter to easily scale as new targets are added to Enterprise Manager for management.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

    ![Enterprise manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Setup >> Add Target >> Administration Groups".

    ![Enterprise manager welcome page](images/emmonlab7step2.png " ")

3. Click on the Overview tab.

    ![Administration Groups page, overview tab](images/emmonlab7step3.png " ")

4. The Overview tab of Administration Groups and Template Collections provides an introduction of how to get started along with detailed steps to walk you through the process. For the purpose of this lab, we have already created the hierarchy, template collections and associations. However, we will look at each step to see how the Administration Group was designed and constructed.

    ![Administration Groups page, overview tab](images/emmonlab7step4.png " ")

5. There are 4 steps involved to setup an Administration Group and Template Collection.
     - Step 1: Setup the Administration Groups Hierarchy
     - Step 2: Create Template Collections
     - Step 3: Associate Template Collections to Administration Groups
     - Step 4: Synchronize the targets with the selected items

    ![Administration Groups page, overview tab](images/emmonlab7step5.png " ")

6. Click on the Hierarchy tab.

    ![Administration Groups page, overview tab](images/emmonlab7step6.png " ")

7. The Hierarchy tab is where you design the levels of your Administration Group hierarchy. Logically, you can think of the top-level group in the hierarchy as a group containing all the targets.  Next consider how you would sub-divide this group of all targets into different sub-groups based on their monitoring settings.  For example, production targets that have one set of monitoring settings would be in one sub-group, and test targets that have a different set of monitoring settings would be in a different sub-group.  These sub-groups represent the next level in the administration group hierarchy.  
To create this hierarchy, use target properties to define the membership criteria for the groups at each level in the hierarchy.  For our example, we used Lifecycle Status target property (with values of Production and Test) to define the membership criteria of the Production and Test groups respectively.

     ![Administration Groups page, hierarchy tab](images/emmonlab7step7.png " ")     

8. Click on the Template Collections tab.

     ![Administration Groups page, hierarchy tab](images/emmonlab7step8.png " ")

9. Template Collections is a combination of Monitoring Templates, Compliance Standards and/or Cloud Policies that are applied to targets upon joining an Administration Group. In this lab, we have already created two template collections. Highlight “Non-Production Template Collection” and click View.

     ![Administration Groups page, template collections tab](images/emmonlab7step9.png " ")

10.	The Non-Production Template Collection contains two Monitoring Templates. Click OK once you are done reviewing the templates.

     - Dev\_Test\_PDB\_Monitoring\_Template: This monitoring template will be applied to Pluggable Database targets that join the Admin Group with their Lifecycle Status target property defined as "Test".

     - Dev\_Test\_DB\_Instance\_Monitoring\_Template: This monitoring template will be applied to Database Instance targets that join the Admin Group with their Lifecycle Status target property defined as "Test".

     ![Administration Groups page, template collections tab](images/emmonlab7step10.png " ")

11.	Highlight “Production Template Collection” and click View.

     ![Administration Groups page, template collections tab](images/emmonlab7step11.png " ")

12.	The Production Template Collection contains 3 Monitoring Templates. Click OK once you are done reviewing the templates.

     - Prod\_PDB\_Monitoring\_Template: This monitoring template will be applied to Pluggable Database targets that join the Admin Group with their Lifecycle Status target property defined as "Production".

     - Prod\_DB\_Instance\_Monitoring\_Template: This monitoring template will be applied to Database Instance targets that join the Admin Group with their Lifecycle Status target property defined as "Production".

     - Prod\_Host\_Monitoring\_Template: This monitoring template will be applied to Host targets that join the Admin Group with their Lifecycle Status target property defined as "Production".

     ![Administration Groups page, template collections tab](images/emmonlab7step12.png " ")

13.	Click on the Associations tab.

     ![Administration Groups page, template collections tab](images/emmonlab7step13.png " ")

14.	The Associations tab is where the association between Template Collections and Administration Groups take place. In this lab we have already associated the “Production Template Collection” with “Prod-Grp” Admin Group. Any target that joins “Prod-Grp” Admin Group will automatically have the Monitoring Templates from “Production Template Collection” applied.

     ![Administration Groups page, associations tab](images/emmonlab7step14.png " ")

15.	We will go through the exercise of associating a Template Collection with “Test-Grp”. Select “Test-Grp” Admin Group and click on "Associate Template Collection".

     ![Administration Groups page, associations tab](images/emmonlab7step15.png " ")

16.	Highlight "Non-Production Template Collection" and click Select.

     ![Administration Groups page, associations tab](images/emmonlab7step16.png " ")     

17.	A Confirmation window will indicate the number of targets that will have Monitoring Templates applied after associating the Template Collection. Click Continue.

     ![Administration Groups page, associations tab](images/emmonlab7step17.png " ")

18.	A Confirmation banner will display an “Association is successful” message and the “Test-Grp” Admin Group is now associated with “Non-Production Template Collection”.

     ![Administration Groups page, associations tab](images/emmonlab7step18.png " ")

19.	Click on the “Test-Grp” group name to go to its homepage.

     ![Administration Groups page, associations tab](images/emmonlab7step19.png " ")

20.	In the group homepage for Test-Grp, review the Synchronization Status region.  Notice there are 3 targets pending synchronization (i.e. applying of templates) and it is scheduled for a future date specified in the Next Synchronization field.    Instead of waiting for the synchronization to occur, let’s do the synchronization process now by clicking on the “Start Synchronization” button..

     ![Group homepage](images/emmonlab7step20.png " ")

21.	After about a minute or so, you should see the 3 targets synchronized.   You may have to hit the page refresh button to see this.

     ![Group homepage](images/emmonlab7step21.png " ")

22.	We will add a target to “Test-Grp” Admin Group and confirm the monitoring template has been being applied to the target. Navigate to “Targets >> Databases”.

     ![Group homepage with navigation to databases page](images/emmonlab7step22.png " ")

23.	Click on “cd186.subnet.vcn.oraclevcn.com” target.

     ![Databases page](images/emmonlab7step23.png " ")

24.	Navigate to “Oracle Database >> Target Setup >> Properties”.

     ![database target home page](images/emmonlab7step24.png " ")

25.	Click Edit and set the Lifecycle Status for this target to “Test”. Click OK.

     ![database target home page, target setup properties](images/emmonlab7step25.png " ")

26.	Navigate to “Setup >> Add Target >> Administration Groups”.

     ![navigation to administration groups page](images/emmonlab7step26.png " ")

27.	Click on “Test-Grp” Admin Group link to go to the Admin Group homepage.

     ![Administration Groups page, associations tab](images/emmonlab7step27.png " ")

28.	Notice in the Synchronization Status section, there is now one additional (total of 4) synchronized targets for Monitoring Templates. **Note:** You may need to click on the page refresh icon if the count under Synchronized Targets doesn’t update right away.

     ![Group homepage](images/emmonlab7step28.png " ")

## Task 9: Incident Rules

Incident Rules specify actions to be taken on events.  For example, when a target down event occurs, you might want to create an incident for the event and send email notification on the  incident. A rule set is a collection of these rules and they apply to a common set of targets such as hosts, databases, groups. Enterprise Manager ships with out-of-the-box rule sets to get you started. Out-of-the-box rule sets have a Lock icon next to them because they cannot be modified. We recommend making a copy of the rule set, and modifying the copy to suit your needs. Alternatively, you can create new rule sets from scratch.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![enterprise manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Setup >> Incidents >> Incident Rules".

     ![enterprise manager login page](images/emmonlab8step2.png " ")

3. Expand “Incident management rule set for all targets” rule set.

     ![incident rules page](images/emmonlab8step3.png " ")

4. The “Incident management rule set for all targets” rule set covers common use cases for which incidents should be created such as target down events or critical metric alerts. You can enable or disable the rules based on your monitoring requirements. If you want to change a rule, you should make a copy of the rule set and modify it.

   Highlight "Create incident for critical metric alerts" and click View.

     ![incident rules page](images/emmonlab8step4.png " ")

5. The "Create incident for critical metric alerts" incident rule will create an incident when the event type is a metric alert and the Severity is Critical.

     ![incident rules page](images/emmonlab8step5.png " ")

6. Click on the “Incident Rules” link to go back to Incident Rules page.

     ![incident rules page](images/emmonlab8step6.png " ")

7. Scroll down and expand "Compress Related Events into a Single Incident" rule set.

     ![incident rules page](images/emmonlab8step7.png " ")

8. The “Compress Related Events into a Single Incident” rule set is a rule set that we created to showcase the rule-based event compression feature in EM 13c. Here we have 4 common use cases which are independent from one another. For each of these use cases, Enterprise Manager will compress the related events into a single incident. From a manageability standpoint, it will be much easier for the Administrator to manage one incident containing multiple related events as a logical unit, as opposed to managing these individually. The Rule set covers the use cases of creating ONE incident when:

      - One or more members of cluster database targets go down.
      - One or more targets with different target types on the same host go down.
      - One or more members of WebLogic Domain target cross the metric threshold.
      - One or more hosts or entire site goes down (e.g., Site wide outage).

     ![incident rules page](images/emmonlab8step8.png " ")

9. In this lab, we will create a new rule set and add a rule to notify the DBA when there is a critical DB alert. Click on “Create Rule Set”.

     ![incident rules page](images/emmonlab8step9.png " ")

10.	Provide a name for the Rule Set and select the following target types.

     - Database Instance
     - Pluggable Database

     ![incident rules, create rule set page](images/emmonlab8step10.png " ")

11.	Scroll down and click Create in the Rules section.

     ![incident rules, create rule set page](images/emmonlab8step11.png " ")

12.	Keep the default selection of "Incoming events and updates to events" and click Continue.

     ![incident rules, create rule set page with select type of rule to create pop-up](images/emmonlab8step12.png " ")

13.	Configure the following fields and click Next. 
     - Type: Metric Alert, All events of type Metric Alert. 
     - Severity: In Critical. 

     ![incident rules, create rule set page](images/emmonlab8step13.png " ")

14.	Click Add in the "Create New Rule: Add Actions" page.

     ![incident rules, create rule set page](images/emmonlab8step14.png " ")

15.	Configure the following fields and click Continue.                     

    - Conditions for actions
        - Keep the default of “Always execute the actions”
    - Create Incident or Update Incident  
        - Click on option “Create incident (if not associated with one)”   
        - Select “Each event creates a new incident”

     ![incident rules, create rule set add actions page](images/incident-rules/add-actions-incident-rules.png " ")

16.	Click Next.

     ![incident rules, create rule set add actions page](images/emmonlab8step16.png " ")

17.	Enter a name for the Rule and click Next.

     ![incident rules, create rule set specify name and description page](images/emmonlab8step17.png " ")

18.	Click Continue.

     ![incident rules, create rule set review page](images/emmonlab8step18.png " ")

19.	You’ll be brought back to the main page for Create Rule Set.  Scroll down to the Rules section and click on ‘Create’.

     ![incident rules, create rule set page](images/emmonlab8step19.png " ")  

20.	Choose the option “Newly created incidents or updates to incidents” and click Continue.

     ![incident rules, create rule set page with select type of rule to create pop-u](images/emmonlab8step20.png " ")

21.	Choose “Specific Incidents”.   And under this option,  select “Rules that created the incidents” and then select the rule that you just created in the previous step.   Then click Next.

     ![incident rules, create rule set select incidents page](images/emmonlab8step21.png " ")  

22.	Click ‘Add’.

     ![incident rules, create rule set add actions page](images/emmonlab8step22.png " ")

23.	In the ‘Email To” field,  specify DB TARGET USER.       Then click Continue.

     ![incident rules, create rule set add actions page](images/emmonlab8step23.png " ")

24.	Click Next.

     ![incident rules, create rule set add actions page](images/emmonlab8step24.png " ")

25.	Enter a name for the Rule and click Next.

     ![incident rules, create rule set specify name and description page](images/emmonlab8step25.png " ")

26.	Click Continue.

     ![incident rules, create rule set review page](images/emmonlab8step26.png " ")

27.	Click Save.

     ![incident rules, create rule set page](images/emmonlab8step27.png " ")

28.	The new rule set now appears at the bottom of the Incident Rules page.

     ![incident rules page](images/emmonlab8step28.png " ")

    **Note:**  Rule Sets are evaluated and executed in the order specified under the Order column.  When you create your own rule set that has an action to create an incident, you typically want to reorder it such that its order is ahead of the out-of-box rule sets.  This is to ensure that your rule set that creates the incident will be used instead of the out-of-box rule set.   However, for this lab exercise, we can skip this step.

## Task 10A: Event Compression Policies

Event Compression is the process of grouping (i.e., compressing) multiple correlated events into a smaller subset of actionable incidents. An Event Compression Policy defines the specific set of related events that should be grouped together. Event Compression Policies work with your incident rule sets to determine if, before an incident is created, there is an applicable event compression policy that should compress the events in the rule into a single incident. 

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![enterprise manager login](images/enterprise-manager-login.png " ")

2. Navigate to Enterprise > Monitoring > Incident Manager.

     ![navigate to incident manager console](images/event-compression/monitoring-to-incident-manager.png " ")

3. Let’s take a look at an example of Event Compression. Select the incident with the summary text: “There are 5 target\_availability events on members of db19c.subnet.vcn.oraclevcn.com\_sys”.

     ![select compressed incident in incident manager](images/event-compression/incident-manager-compressed-incident-highlighted.png " ")

4. The incident details should display in the bottom pane. Click open in new tab.

     ![open compressed incident in new tab](images/event-compression/incident-manager-compressed-incident-open-in-new-tab.png " ")

5. From here you can take a closer look at the incident details. 

     ![compressed incident opened in new tab](images/event-compression/incident-manager-compressed-incident-opened-in-new-tab.png " ")

6. The incident details display the information about the events that were grouped into this incident. Details include the number of events in the incident, the Event Compression Policy used to compress the events into the incident, the Incident Rule used to create the incident and the list of compressed events in the bottom pane. 

     **Note:** You can ignore any differences between the Last Comment field in the screenshot vs. what you see in your lab environment. The Last Comment was updated for lab purposes.

     ![compressed incident details in new tab](images/event-compression/compressed-incident-important-details-highlighted.png " ")

7. Navigate to the Events Tab.

     ![compressed incident details in new tab](images/event-compression/compressed-incident-events-tab-highlighted.png " ")

8. This tab shows the latest events that were grouped into this incident. 

     ![latest events in the compressed incident](images/event-compression/events-tab.png " ")

9. Now let’s take a look at how to use and create these Event Compression Policies. At the top menu, click Setup > Incidents > Event Compression Policies.

     ![navigate to event compression policies page](images/event-compression/incidents-to-event-compression-policies.png " ")

10. Here is the Event Compression Policies page with all the policies available. There are seven out-of-box policies that collectively represent recommended ways in which related events should be compressed together into a single incident. For example, there is a policy for target down events for a cluster database and its members. Click on any policy name to view more details on the compression. You also have the option to author your own policy if the out of the box policies do not satisfy your use cases. 

     ![event compression policies page](images/event-compression/event-compression-policies-page.png " ")

11. Let’s now take a look at the policy that created the compressed events we previously viewed. Click the policy with the name “Target down events for a database system and its members”. **Note:** This is not one of the seven out-of-box policies. It is a user-defined policy. You can differentiate between a user-defined policy and an out-of-box policy from the ‘Created By’ column.

     ![target down policy for database system and its members](images/event-compression/target-down-db-policy-highlighted.png " ")

12. A screen slides out that has the compression policy information. Here you can view the Event Compression Logic for how the events were grouped together. For this example, the logic groups target availability events for a database system and its members into one incident if the events occurred within a 60 minute time frame. These events were compressed based on the ancestor (i.e., parent) target. Notice it also displays the incident message that will be displayed when the incident is created and cleared.

     ![details of target down policy for database system and its members](images/event-compression/target-down-db-details.png " ")

13. Click the x icon to exit from the screen.

     ![exit from details of target down policy](images/event-compression/target-down-db-close.png " ")

14. Now that you have seen an example of an incident with compressed events and the compression logic for one of the policies, we will walk through the steps of creating your own policy. To begin, click the “Create New Policy” icon.

     ![create new policy](images/event-compression/create-new-policy.png " ")

15. A page displays where you can create your own policy.

     ![create new policy page](images/event-compression/create-new-policy-details-blank.png " ")

16. For our example, you will be creating a compression policy related to target availability events for coherence targets (i.e., Coherence Cluster, Coherence Node, and Coherence Cache). Let’s add a name to the policy such as “Target availability events for a coherence cluster and its members”. We recommend adding a description for your policy to further distinguish what is does. For instance, you can use the following description: “Compress target availability events for a coherence cluster, coherence node and coherence cache occurring within the 60-minute time window”.

     **Note:** An Oracle Coherence Cluster enables organizations to predictably scale mission-critical applications by providing fast and reliable access to frequently used data.

     ![enter policy name and description](images/event-compression/create-new-policy-name.png " ")

17. Now let’s move on to the Event Compression Logic sub-section. 
     - First you need to specify the type of events that will be compressed. You can choose the events from an event rule or manually select the event types. For this lab, you will manually select the events:
          - This policy is for target availability events so under the field “Events of type”, search for “Target Availability” and choose it. 
          - We are also interested in coherence targets so under the field “On targets of type” search the following: “Oracle Coherence Cache”, “Oracle Coherence Cluster” and “Oracle Coherence Node” and choose them. 
          - And finally, for the “With event severity” field, click “Fatal” and “Critical” as these will map to target down and target error events which fall under the target availability umbrella.

     ![enter compression logic part one](images/event-compression/create-new-policy-logic-part1.png " ")

18. Now add a time window for these events. Change the current time window of 45 minutes to 60 minutes. After this, determine the criteria for grouping or compressing the events. 

     The Coherence Cluster target is the parent to the Coherence Cache and Node targets. So you may want to compress together the events from Coherence Cache and Coherence Node targets that are part of the same Coherence Cluster into one incident. Hence, in the “Compress into One incident by” field, choose "same ancestor target type", and in the “select Group type” choose "Oracle Coherence Cluster". 

     ![enter compression logic part two](images/event-compression/create-new-policy-logic-part2.png " ")

19. We provide default incident messages based on your selection for the event compression logic. However, you may modify the default messages as you desire. The default variables will be replaced by the corresponding values once the incident is created. For example, the %EVENT\_COUNT% variable would be replaced by the number of events in the incident. Let’s keep the default message and click Save.

     ![enter incident message](images/event-compression/create-new-policy-incident-message.png " ")

20. This logic essentially compresses into one incident all target availability events with a fatal or critical severity from the coherence cluster, cache and node targets  if it falls within a 60-minute window.

21. The policy you created will now appear on the Event Compression Policies page in a draft state. Notice that the other policies are all under the Published status. The published status allows the policy to be used by other administrators. 

     ![policy created is in draft state](images/event-compression/new-policy-highlighted.png " ")

## Task 10B: Event Compression Analysis

Event Compression is the process of grouping (i.e., compressing) multiple correlated events into a smaller subset of actionable incidents. An Event Compression Analysis uses historical monitoring data from your environment to analyze the impact Event Compression Policies would have had on events that generated incidents over a selected time range in the past. **Note:** Please complete Task 10A before completing this task.

1. Before publishing your policy that you created in Task 10A, we recommend testing it out using the Event Compression Analysis tool. To test out the policy, first enable the policy using the toggle button.

     ![enable policy for testing](images/event-compression/new-policy-disable-button-highlighted.png " ")

     ![confirmation dialog to enable policy for testing](images/event-compression/enable-new-policy.png " ")

     ![policy enabled for testing](images/event-compression/new-policy-enable-button-highlighted.png " ")

2.	Now click the Event Compression Analysis link to navigate to its page.

     ![event compression analysis link](images/event-compression/event-compression-analysis-link.png " ")

3. Here is the Event Compression Analysis page. This analysis uses events from your environment and simulates the creation of incidents without Event Compression Policies and with Event Compression Policies. This allows you to analyze the effectiveness of Event Compression Policies on your own events. 

     ![event compression analysis page](images/event-compression/analysis-page.png " ")

4. To begin a new analysis, click Start New Analysis.

     ![start new analysis button](images/event-compression/start-new-analysis.png " ")

5. A pop-up displays: 
     - Enter a name for the analysis such as “Coherence Targets Policy Analysis” and add an optional description.
     - Next, select the targets for the analysis. For this, let’s keep the default “Group” selection under the field “Select target type”. 
     - In the dropdown ‘Select a Group’ list, select “Coherence Targets”. For the purpose of this lab, the group Coherence Targets has been created that contains targets of type Coherence Cluster, Coherence Cache and Coherence Node. 
     - For the time range of these events, select from April 25, 2023 to May 12, 2023. **Note:** you can specify a time range with a maximum of 31 days. 
     - And finally, because your policy is still in the draft state, click ‘Include Draft Policy’ so that your policy is used in the analysis. 
     
     At the end, your analysis criteria should look like the following: 

     ![start a new analysis details](images/event-compression/start-new-analysis-popup.png " ")

6. Click “Start Analysis”.

     ![select start analysis](images/event-compression/start-new-analysis-popup-saved.png " ")

7. A job is submitted that will run the analysis. It takes a few seconds for the analysis to complete so refresh your page to see the finished analysis. 

     ![analysis submitted and in progress](images/event-compression/analysis-submitted.png " ")

     ![analysis completed](images/event-compression/analysis-complete.png " ")

8. Click on the analysis name to view the results. 

     ![open analysis](images/event-compression/analysis-name-highlighted.png " ")  

     ![analysis details](images/event-compression/analysis-results.png " ")

9. The top boxes serve as a summary to the analysis. It shows the events analyzed, the incidents created and the compression ratio. For this example, 30 events were analyzed, 30 incidents would have been created without compression policies, while 10 incidents would have been created with the compression policies. This is a 66% reduction of incidents and evaluates to a compression ratio of 3.

     ![analysis details - summary section](images/event-compression/analysis-results-summary-highlighted.png " ")

10. In the graph, this is a visual representation of the compression. The bars are color coded to specify the number of incidents when Event Compression Policies are not used (i.e., navy) versus the number of incidents when compression policies are used (i.e., orange). The gray line represents the number of events analyzed.

     ![analysis details - graph section](images/event-compression/analysis-results-graph-highlighted.png " ")

11. To further analyze how events and incidents are compressed on a specific date, click on the date's corresponding bars to see another representation of the compression. In this visualization, you will see more information on how events are mapped from incidents without compression policies to incidents with compression policies. For example, click any of the bars under May 10th.

     ![analysis details - click on bars in graph](images/event-compression/analysis-bars-highlighted.png " ")

12. A pop up of a mapping diagram will appear. On the left, the blue bars represent the incidents without compression policies. In the middle, the grey lines represent events. On the right, the orange bars represent incidents with compression policies. The mapping represents how individual events are compressed into incidents using the policies.

     ![analysis mapping](images/event-compression/analysis-mapping.png " ")

13. Click on any of the incidents bars or event lines to view more details. For instance, click on the orange ‘incident with compression policies’ bar on the right:

     ![click on analysis mapping](images/event-compression/analysis-mapping-selected.png " ")

14. The following pop-up appears. Here you can see the individual events that are compressed into the incident based on the policy that you created. It also shows more information of the incident details such as the incident summary, when it was created and the incident rule that created it. 

     ![analysis mapping details](images/event-compression/analysis-bar-details.png " ")

15. Click OK once you are finished reviewing the details. 

     ![select ok once done viewing the analysis mapping details](images/event-compression/analysis-bar-details-ok-highlighted.png " ")

16. Click OK again.

     ![select ok once again](images/event-compression/analysis-mapping-exit.png " ")

17. And exit out of the analysis. 

     ![exit out of the analysis](images/event-compression/analysis-exit.png " ")

18. Now that you have seen the effect of your policy and know that it is working as expected, you may now publish it for use by other administrators. Navigate to Setup > Incidents > Event Compression Policies.

     ![navigate back to event compression policies page](images/event-compression/incidents-to-event-compression-policies-from-analysis.png " ")

19. Click the actions icon under your policy. Select Publish. 

     There are other actions you can complete on this policy such as:
     - Editing the policy when it is in draft state and disabled.
     - Creating a like policy which creates a separate and editable copy of your policy.
     - Reordering your policy in the list so it has higher priority when being evaluated by an event rule. 
     - Deleting your policy.

     ![draft policy actions menu](images/event-compression/new-policy-actions.png " ")

     ![publish draft policy](images/event-compression/publish-the-policy.png " ")

20. Your policy is now published and ready for use by other administrators.

     ![your policy is published](images/event-compression/new-policy-published.png " ")

21. Remember that Event Compression Policies works hand-in-hand with Incident Rules to create the incidents with compressed events. Now that your policy has been created, tested and published, let’s see how the Incident Rules would work with the policies. Navigate to Setup > Incidents > Incident Rules.

     ![navigate to incident rules page](images/event-compression/incidents-to-incident-rules-from-policies.png " ")

22. An incident ruleset has already been created for the purpose of this lab. Let’s review it and enable Event Compression Policies to be used. Select the ruleset “Compress Target Availability Events for Coherence” and click Edit.

     ![edit the ruleset “Compress Target Availability Events for Coherence”](images/event-compression/incident-rules-page-new-rule-for-policy-highlighted.png " ")

23. Note that the rule set has been created to apply to the Coherence targets group (i.e., Coherence Cluster, Coherence Cache and Coherence Node targets). 

     ![targets specified in rule set](images/event-compression/coherence-rule-set-beginning.png " ")

24. Scroll down to the Rules section and select “Compress Target Availability Events for Coherence Cluster, Coherence Node, and Coherence Cache” and “Edit”. 

     ![Scroll down to the Rules section and select coherence rule](images/event-compression/edit-compression-rule.png " ")

25. Review the selected event types and click Next.

     ![Review selected events](images/event-compression/coherence-rule-select-events.png " ")

26. In the Add Actions page, select the action in the list and click edit.

     ![Edit add actions page](images/event-compression/coherence-rule-add-actions-edit.png " ")

27. In the “Create Incident or Update Incident” section change the selection from “Each event creates a new incident” to “Use Event Compression Policies (Recommended)”. Click Continue. 

     ![Add actions with 'each event creates a new incident' selected](images/event-compression/coherence-rule-add-actions-create-incident-before.png " ")

     ![Add actions with 'use event compression policies' selected](images/event-compression/coherence-rule-add-actions-create-incident-after.png " ")

28. The action now updates to use Event Compression Policies rather than creating a new incident for every event. Click Next.

     ![Add actions saved with 'use event compression policies' selected](images/event-compression/coherence-rule-add-actions-saved.png " ")

29. Review the event rule name and description and Click Next.

     ![Review the event rule name and description](images/event-compression/coherence-rule-specify-rule-name.png " ")

30. Click Continue.

     ![Click Continue](images/event-compression/coherence-rule-review.png " ")

31. Click Save.

     ![Click Save](images/event-compression/coherence-rule-rule-set-page-save.png " ")

32. The ruleset and rule has now been successfully saved and will now work with your Event Compression Policy to create compressed incidents for coherence targets. 

     ![ruleset and rule has now been successfully saved](images/event-compression/coherence-rule-fixed-incident-rules-page.png " ")


## Learn More

  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Enterprise Monitoring](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmon/enterprise-monitoring.html)
  - [Enterprise Manager Monitoring Overview Video](https://www.youtube.com/watch?v=oAnF38qa4EA)
  - [Strategies for Scalable, Smarter Monitoring using Oracle Enterprise Manager Cloud Control 13c](https://www.oracle.com/a/otn/docs/enterprise-manager/wp_enterprisemanager13c_monitoringstrategies.pdf)

## Acknowledgements
- **Author** - Karilyn Loui, Oracle Enterprise Manager Product Management
- **Contributing Author** - Ana McCollum, Daniel Suherman, Murtaza Husain, Desiree Abrokwa, Oracle Enterprise Manager Product Management
- **Adapted for Cloud** - Rene Fontcha, Master Principal Solutions Architect, NA Technology
- **Last Updated By/Date** – Desiree Abrokwa, Oracle Enterprise Manager Product Management [July 2023]
