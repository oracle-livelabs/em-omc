# Enterprise Manager Fundamentals: Monitoring Quick Tour
## Introduction
Oracle Enterprise Manager enables you to get complete monitoring visibility into your IT infrastructure, applications stack and applications that are critical to running your business.

- Single pane of glass monitoring for on-premises, hybrid, and Oracle Cloud Platform

- Comprehensive set of predefined performance and health metrics that enables lights-out monitoring of critical components in your environment, such as applications, application servers, databases, as well as the back-end components on which they rely, such as hosts and storage

- Rich set of alerting, incident management and notification capabilities to notify IT staff and integrate with your corporate ticketing systems

- Corrective Actions to auto-correct alerts and minimize service disruption

- Metric Extensions to monitor conditions specific to your environment

- Dynamic Runbooks to triage and resolve your incidents  

Watch the video below for a quick walk-through of the lab.
[Enterprise Monitoring Quick Tour](videohub:1_cmd73lma)

### Objectives
The objective of this lab is to become familiar with Enterprise Monitoring capabilities using Oracle Enterprise Manager Cloud Control 13c.

### Prerequistes
This lab assumes you have:

- A Free Tier, Paid or LiveLabs Oracle Cloud account
- All previous labs successfully completed

*Estimated Time*: 65 minutes


### Lab Timing (Estimated)

  | **Step No.** | **Feature**                                   | **Approx. Time** | **Details**                                                                                                                                                                                                                    | **Value proposition**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  |--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **1**  | Enterprise Summary                              | 5 minutes       | Explore Enterprise Summary page and drill down to see a list of down targets. View the list of critical incidents created for the down targets. Filter the Status pane to display a list of Database Instance targets.                         | Enterprise Summary enables you to get complete visibility into the overall status and health of your managed environment.                                                                                                                                                                                                                                            |
  | **2**  | Incident Manager                                | 5 minutes       | Triage unassigned incidents from Incident Manager and acknowledge then assign an incident.                                                 | Incident Manager enables IT Staff to manage, track, and resolve actionable incidents in a collaborative way.|                                                                                                                                        
  | **3A**  | Dynamic Runbooks                               | 5 minutes       | Start a Dynamic Runbook session against an incident in Incident Manager.                                                 | Dynamic Runbooks are documented procedures (steps) that IT Staff follow to resolve an issue.                                                                                                                                                             
  | **3B**  | Dynamic Runbooks                               | 7 minutes       | Modify and publish a Dynamic Runbook draft.                                                 | Dynamic Runbooks are documented procedures (steps) that IT Staff follow to resolve an issue.  
  | **4**  | Metric and Collection Settings                         | 5 minutes       | Change the Warning and Critical threshold of a metric from Metric and Collection Settings page. Go to the All Metrics page and review the metric in context of the thresholds.                                                                                                           | Enterprise Manager provides out-of-box monitoring and alert thresholds for managed targets.  You can still customize these monitoring settings based on your requirements.                                                                                                                                                                                                                                                                                                                                 |
  | **5**  | Corrective Actions                          | 8 minutes       | Create a new Corrective Action and associate it with a metric. | Corrective actions allow you to specify automated responses to metric alerts, saving administrators time and ensuring issues are dealt with before they noticeably impact users.  A corrective action can also be used to gather diagnostic information for an alert.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  | **6**  | Metric Extensions                          | 5 minutes       | Test a Metric Extension on a target to see the results then deploy the same Metric Extension to multiple targets. | Metric Extensions let you extend Enterprise Manager's monitoring capabilities to cover conditions specific to your IT environment, thus enabling you to rely on Enterprise Manager as your single monitoring solution.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
  | **7**  | Monitoring Templates                          | 5 minutes       | Create a Monitoring Template from a Database Instance target. Deploy the Monitoring Template to other Database Instance targets to standardize monitoring settings across the enterprise. | Monitoring Templates enable you to define and implement monitoring standards across all targets in your environment.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
  | **8**  | Administration Groups and Template Collections                          | 10 minutes       | View the hierarchy of an existing Administrator Group. Update the target property for a new target so it can automatically be added to an Administration Group and inherit monitoring settings from that group. | Administration Groups and Template Collections enable you to enforce monitoring standards and automate monitoring setup in a scalable way.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
  | **9**  | Incident Rules                          | 10 minutes       | Review out-of-the-box incident rules shipped with Enterprise Manager. View an example of an incident compression rule set. Create a simple incident rule set to email DBA when there is a critical DB alert. | Incident Rules enable you to automate common incident management and notification actions such as creation of incidents based on events, sending email to IT Staff, opening tickets, auto-assigning incidents, escalating incidents, etc.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

## Task 1: Enterprise Summary

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”. 

    ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Summary”.

    ![Enterprise Manager welcome page](images/enterprise-manager-welcome.png " ")

3. Enterprise Summary presents a single pane of glass view of the health of your Enterprise assets.
The Overview pane shows the Target Status of your IT estate. The Status section shows aggregated target availability so you can get a sense of what percentage is UP vs DOWN at a quick glance. The Green slice of the pie are your targets that are up. The Red slice of the pie are the targets that are down. Targets in red may be down due to unscheduled outages. Let’s drill down and take a look at them.

    ![Enterprise Manager summary page](images/enterprise-manager-summary.png " ")

4. Click on the Red slice of the pie in the “Status” section. **Note:** You can ignore any differences between the count of targets in the screenshots vs. what you see in your lab environment. The number of targets may vary based on your lab environment.

    ![Enterprise Manager summary page, status section](images/enterprise-manager-summary-status.png " ")  

   If a dialog pops up, click on ‘Down’ again.

    ![Enterprise Manager summary page, status section](images/enterprise-manager-summary-status-down.png " ")   

5. In Enterprise Manager we have an “All Targets” page, which shows all of the targets being monitored by EM. When we clicked on the Red slice of the pie, we essentially placed a filter on the All Targets page to display only Down targets. From here, you can click on the individual target to go to the Target Home Page and take necessary actions such as starting up a Database Instance.

    ![Enterprise Manager All targets page](images/enterprise-manager-all-targets.png " ")

6. Click on “Enterprise >> Summary” to go back to the Enterprise Summary page.

    ![Step to navigate back to Enterprise Manager summary page](images/enterprise-manager-summary-2.png " ")

7. Any Incidents, Problems, and Jobs requiring attention is displayed on the Enterprise Summary page with the ability to drill down into them. Click on the incidents link ![Availability symbol](images/noentry.svg " ") for Availability.

    ![Enterprise Manager summary page, status section with Availability incidents selected](images/enterprise-manager-summary-availability.png " ")

8. A list of critical incidents is displayed in Incident Manager. You can manage the incidents by acknowledging, assigning ownership, changing the priority or status, and more.

    ![A list of critical incidents is displayed in Incident Manager](images/enterprise-manager-incident-manager.png " ")

9. Click on “Enterprise >> Summary” to go back to the Enterprise Summary page.

10. You can also filter the view based on the target type. Click on the View dropdown in the “Overview” pane and select “Database Instance” to look at the database status.

    ![Enteprise Manager summary page, status section with filter for target type](images/enterprise-manager-summary-database-instance.png " ")

11.	The Status pane is filtered for Database Instance targets and displays a breakdown of the database statuses.

    ![Enterprise Manager summary page, status section](images/enterprise-manager-summary-database-status-filter.png " ")

12.	The right hand pane of the Enterprise Summary page also has Inventory and Usage, Compliance Summary, and Patch Recommendations sections. Inventory and Usage shows a breakdown of database inventory by release. Compliance Summary shows the compliance score for the selected targets as well as security recommendations. Patch Recommendations links to MOS and shows the recommended patches for your targets.

     ![ Enterprise manager summary page, Compliance Summary, and Patch Recommendations sections](images/enterprise-manager-summary-inventory.png " ")

## Task 2: Incident Manager

Incident Manager provides in one location the ability to search, view, manage, and resolve events, incidents and problems impacting your environment.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

    ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to “Enterprise >> Monitoring >> Incident Manager”.

    ![Enterprise Manager welcome page](images/enterprise-manager-welcome-to-incident-manager.png " ")

3. In Incident Manager, the Views section contains out-of-box views that comes shipped with Enterprise Manager. You can create your own views and share with others as well. By default, “All open incidents” view is displayed.

    ![Incident Manager page](images/incident-manager-all-open-incidents.png " ")

4. We will triage unassigned incidents and then acknowledge and assign an incident to an owner. Click on the incident with Summary text “Target is down; 1 member is down; db19c.subnet.vcn.oraclevcn.com”. Details of the incident will be displayed in the bottom pane.

    ![Incident Manager page](images/incident-manager-target-down-selected.png " ")

5. Click on “Open in new tab” link to open the incident on a separate tab. You may need to temporarily allow popups in the browser.
    ![Incident Manager page](images/incident-manager-open-in-new-tab.png " ")

6. The General tab of an incident contains 4 sections.

      - Incident Details contains information about the incident such as target name, creation date, type, and summary.
      - Tracking provides the priority, status, and ability to manage the incident.
      - Guided Resolution provides the ability to diagnose and take action to resolve the incident.
      - Runbook Sessions provides options to start, create, or view a runbook session against the incident.

     ![Incident Manager page, Incident details](images/incident-manager-incident-details.png " ")

7. Click on “Acknowledge” in the Tracking section to acknowledge the incident. This will automatically assign the incident to the user acknowledging the incident.

     ![Incident Manager page, Incident details](images/incident-manager-incident-details-acknowledge.png " ")

     ![Incident Manager page, Incident details](images/incident-manager-incident-details-acknowledge-completed.png " ")

8. Click on “Manage”.

     ![Incident Manager page, Incident details](images/incident-manager-incident-details-manage.png " ")

9. Update the Status, Priority, and Escalation fields. Add a short comment and click OK.

     ![Incident details, manage incident pop-up box](images/incident-manager-incident-details-manage-tab.png " ")

10.	A confirmation is displayed with the Tracking section updated.

     ![Incident Manager page, Incident details](images/incident-manager-incident-details-tracking-updated.png " ")

11.	Close the Incident Details tab and go back to the Incident Manager tab.

12.	Click on the Dashboard button next to “Incident Manager: All open incidents”.

     ![Incident Manager page](images/incident-manager-dashboard-button.png " ")

13.	Incident Dashboard provides a holistic view of your incidents. It contains 3 sections.

       - Summary: Instant count of incidents that are open, fatal, escalated, unassigned, and unacknowledged. These are the incidents that need to be triaged or worked on immediately. Fatal and Escalated count are highlighted in Red by default.
       - Charts: Provides an easy-to-understand look at the current incident distribution and management status for each incident. Drill down capability with stackable filters to slice and dice data any way you like. Customize to add/update/remove charts to provide a personalized view in Incident Manager.
       - Incident List: Shows the open incidents listed in reverse chronological order by last updated time stamp. From this list, you can perform requisite incident lifecycle actions such as escalating, prioritizing, acknowledging, assigning owners, and adding comments to the incident. The incident list will reflect any filters applied.

     ![Incident Manager, Incident Dashboard](images/incident-manager-dashboard-view.png " ")

14.	Click on the “Fatal” link to drill down into these incidents.

     ![Incident Manager, Incident Dashboard](images/incident-manager-dashboard-fatal-drilldown.png " ")

15.	Incident Dashboard is filtered for incidents with “Fatal” severity.

     ![Incident Manager, Incident Dashboard](images/incident-manager-dashboard-fatal-drilldown-complete.png " ")
     

## Task 3A: Dynamic Runbooks

Dynamic Runbooks are documented procedures that IT staff follow to resolve an issue. Dynamic Runbooks typically consist of a set of ordered instructions (steps) to resolve the issue. Users can execute these steps inside Enterprise Manager in context of an incident. 

For this lab, a Dynamic Runbook has already been published for you to use. You will go through the process of starting a Runbook session against a designated incident.

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Enterprise >> Monitoring >> Incident Manager".
     
     ![Navigate to Incident Manager](images/enterprise-monitoring-incident-manager-3a.png " ")

3. In Incident Manager, the “All open incidents” view is displayed by default. In this view, highlight the incident with Summary text “The value of the Fast Recovery Area % Used is 70.11”. The Fast Recovery Area is a unified storage location for all Oracle Database files related to recovery. Details of the incident will be displayed in the bottom pane. 

     ![Highlighted Incident](images/incident-manager-all-open-incidents-fra.png " ")

4. In the bottom pane, you should see a section called "Runbook Sessions".

     ![Runbook Sessions section in Incident Manager](images/incident-manager-all-open-incidents-fra-runbook-sessions.png " ")

5. Click on "Start Runbook Session".
     
     ![Start Runbook Session](images/incident-manager-start-runbook-session.png " ")

6. At the top of this page, the previous incident details are carried over. These details will be passed to the Runbook once you create a session.  Under the incident details, a table displays the published Runbooks that can be used against the incident.

     ![Start Runbook Session Page](images/runbook-session-page.png " ")

7. To preview the Runbook steps, click on the Runbook name, "Fast Recovery Area Triage". You can click on the  steps to view more details. **Note:** In this task, there is only one published Runbook available. In cases where there are multiple Runbooks, the preview can help you decide which Runbook to use.

     ![Preview Runbook](images/runbook-session-page-preview-runbook.png " ")

8. Click Close when you are done previewing the steps.

9. After previewing the steps, select on the play icon under the Start Session column to begin the Runbook session.

     ![Play Runbook Session](images/runbook-session-page-start-runbook.png " ")

10. Here you can see a detailed view of the steps needed to run the Runbook and triage the issue. Also, notice the incident details have been carried over to the session.

     ![FRA Runbook Session Steps for Incident](images/runbook-fra.png " ")

11. The Overview & Prerequisites step describes what the Runbook does and the prerequisites needed to run it. In this lab, the prerequisites have already been completed for you. You should have access to the Named Credential, **CDB186\_SYS**, for the target database. Access to this Named Credential will allow you to successfully run through all the steps.

     ![Overview & Prerequisites Step](images/runbook-fra-overview-step.png " ")

12. Select the play icon in Step 2 to review the metric, FRAPercentUsed, that triggered the incident. The red vertical dotted line indicates when the incident happened. Notice the increasing trend of the metric before crossing the threshold. The threshold was crossed at approximately 70%. 
     
     **Note:** The metric data was simulated for the purpose of this lab. As a result, your graph may not exactly resemble the image shown below, but it should still show an upwards trend.

     ![Review the Metric - Step 2](images/runbook-fra-metric-step.png " ") 

13. Next, check the FRA size of the database. Notice for Step 3 the gear icon is displayed instead of the play icon. This indicates that certain credentials are required before running the step.

     ![Gear Icon - Step 3](images/runbook-fra-check-fra-size.png " ")

14. Click on the gear icon for Step 3. In the pop-up that appears, enter the credential **CDB186\_SYS** and click Save.

     ![Enter Credentials - Step 3](images/runbook-fra-check-fra-size-enter-credentials.png " ")

15. After saving, the Runbook session is updated and the gear icon for Step 3 will turn into a play icon. The same credentials are needed to run Step 4 and Step 5, so these steps have also been updated to a play icon instead of a gear icon. 

     ![Credentials Saved - Step 3](images/runbook-fra-check-fra-size-play.png " ")

16. Click on the play icon for Step 3 to check the FRA size. A table appears, displaying the FRA size for the database. It should be approximately 13 Gigabytes. According to the Runbook instructions, the FRA size must be set to at least 50 Gigabytes (50G) to comply with the Database standard. 

     ![Check FRA Size - Step 3](images/runbook-fra-check-fra-size-table.png " ")

17. To change the FRA size to 50G, click the play icon on Step 4. You should see a table that indicates that you have successfully increased the FRA size. Increasing the FRA size allows the FRAPercentUsed to decrease.

     ![Change FRA Size - Step 4](images/runbook-fra-change-fra-size.png " ")

18. Run Step 5 to view the updated FRA size and to confirm that it has been set to at least 50G. Your new FRA size should be approximately 53687091200 (50G), which meets the minimum threshold for FRA size.

     ![Check FRA Size Again - Step 5](images/runbook-fra-check-fra-size-again.png " ")

19. Step 6 describes the success criteria: once you have performed all the Runbook steps and the FRA size meets the minimum threshold, then this should have resolved the issue. 

     ![Success Criteria - Step 6](images/runbook-fra-success-criteria.png " ")

     **Note:** For the purpose of this lab, the metric incident was simulated and therefore may still remain in Incident Manager after these steps have been run.

20. The Runbook remains an active session until you Mark as Done. As an active session, your data will be saved which allows you to go back and rerun your steps. This is useful for cases where you may want to leave the session halfway through and return to complete it later. 

21. Select Mark as Done to indicate that you have finished all the steps. Once you Mark as Done, you are unable to run the steps and the Runbook session will become read-only.

     ![Mark as Done](images/runbook-fra-mark-as-done.png " ")

22. Click OK.

     ![Mark as Done - OK](images/runbook-fra-mark-as-done-ok.png " ")

23. A page with all the Runbook Sessions that you have ran will appear. Click the arrow under the Actions column for the "Fast Recovery Area Triage" session to see the actions you can take after a session is complete. In the Actions menu that pops up, you can open the session to have a read-only view, extend the expiration of the session, or delete the session. 

     ![Actions - Complete Runbook Session](images/runbook-sessions-completed-page-actions-menu.png " ")
     

## Task 3B: Dynamic Runbooks

Dynamic Runbooks are documented procedures that IT staff follow to resolve an issue. Dynamic Runbooks typically consist of a set of ordered instructions (steps) to resolve the issue. Users can execute these steps inside Enterprise Manager in context of an incident. 

For this lab, a Dynamic Runbook draft has already been created. You will go through the process of modifying the Runbook and later publishing it to be used by others.  

1. Log into an Enterprise Manager VM (using provided IP). The Enterprise Manager credentials are “emadmin/welcome1”.

     ![Enterprise Manager login](images/enterprise-manager-login.png " ")

2. Navigate to "Enterprise >> Monitoring >> Runbooks".

     ![Navigate to Runbooks](images/enterprise-monitoring-runbooks.png " ")

3. The Runbooks page has Draft Runbooks and Published Runbooks. By default, the Drafts tab is opened. You can create a Runbook through this Runbooks page or directly against an incident in the Incident Manager page. Under the Drafts tab, select the "New Runbook" link. This is the Runbook draft that was created for you and that you will modify.
     
     ![Select New Runbook Draft](images/runbooks-page-new-runbook.png " ")

4. At the top of the page, the previous incident details are carried over. This is the incident that was selected to create a Runbook draft on. You can optionally edit the Runbook name and Description using the pencil icons next to them. 

     ![New Runbook Draft Page](images/runbooks-page-new-runbook-draft-page.png " ")

5. There is an Add a Step drop-down menu, where you can select the desired step type you want to define. There are four step types: Note, Metric Data, Repository SQL, and Target SQL. We have already added the steps for you in this Runbook draft.

     ![Add Step - New Runbook](images/runbooks-page-new-runbook-draft-page-add-step.png " ")

6. To begin modifying the Runbook Draft steps, select the pencil icon to edit Step 1 (Overview and Prerequisites). This is a Note Step: used for any type of text meant to provide information or instruction pertaining to the Runbook. The Note can be plain text but can also accommodate simple formatting via markdown language. 

     ![Step 1 Overview and Prereq - New Runbook](images/new-runbook-draft-page-edit-overview.png " ")  

7. In the text box, add 3 hash signs (###) followed by a space to the beginning of the first sentence, “This runbook can be used to triage and resolve FRA incidents,” to make it header 3. 

     ![Step 1 H3 - New Runbook](images/new-runbook-draft-page-edit-overview-h3.png " ")  

8. Next, place three dashes (---) on their own line under the first sentence to create a horizontal line.

     ![Step 1 Horizontal Line - New Runbook](images/new-runbook-draft-page-edit-overview-line.png " ")  

9. Put two asterisks (**) on both sides of the “Prior to Beginning” text to make it bold. 

     ![Step 1 Asterisks - New Runbook](images/new-runbook-draft-page-edit-overview-asterisks.png " ") 

10. Scroll down in the text box until you see the following sentence: “Make sure you have been granted access to the named credential for the target database **[target name]** on which the FRA Incident has occurred”.

     ![Step 1 Scroll to Target Name Placeholder - New Runbook](images/new-runbook-draft-page-edit-overview-target-placeholder.png " ") 

11. View the "Oracle Provided Variables" on the right side of the screen. Scroll until you see the field for "Target Name".

     ![Step 1 Oracle Variable for Target Name - New Runbook](images/new-runbook-draft-page-edit-overview-oracle-variable-target-name.png " ")     

12. Replace the "[target name]" placeholder in the text box with the value displayed in the Variables table for Target Name: **$ora\_target\_name**. This will now replace the original "[target name]" placeholder text with the target name pulled from the context of the incident.

     ![Step 1 Target Name Placeholder Replacement- New Runbook](images/new-runbook-draft-page-edit-replace-target-placeholder.png " ") 

13. Select Save Step to view the modifications to the text.

14. Your Overview and Prerequisites step should now look like this:
     
     ![New Step 1 - New Runbook](images/new-runbook-draft-page-new-overview.png " ") 

     The first sentence is now a header 3 with a horizontal line under it. The Prior to Beginning text is bolded. And the original [target name] placeholder text is populated by the name of the target from the incident.

15. Step 2 is a Metric Data step which is used to show the time series chart for the specified metric. Notice the instruction text of the step does not specify the actual metric name to review. Also, the graph does not show the trend from before the metric crossed the threshold, which is indicated by the red vertical dotted line.

     ![Step 2 - New Runbook](images/new-runbook-draft-page-metric-step.png " ") 

16. Click the pencil icon to make edits to Step 2. 

     ![Edit Step 2 - New Runbook](images/new-runbook-draft-page-edit-metric-step.png " ") 

17. To specify the metric name, edit the “[metric name]” placeholder to use the value **$ora\_metric\_name**. This will populate the value with the text in the Metric Name field (e.g., FRAPercentUsed).

     ![Step 2 Specify Metric Name - New Runbook](images/new-runbook-draft-page-edit-metric-name.png " ")

18. Click on the Time Range field to modify the times shown in the graph. Change the Start Time field to "evt\_time – 1d" and the End Time field to "evt\_time + 1d". Select Done. Select the Run button. This should now balance the graph to display the trend of the metric before and after it triggered the incident. 

     **Note:** The metric data was simulated for the purpose of this lab. As a result, your graph may not exactly resemble the image shown below, but it should still show an upwards trend.

     ![Step 2 Change Time Range - New Runbook](images/new-runbook-draft-page-edit-metric-time-range.png " ")

     ![Step 2 Updated Graph - New Runbook](images/new-runbook-draft-page-edit-metric-new-graph.png " ")

19. Select Save Step to see results for Step 2. 

20. The metric name value should populate to "FRAPercentUsed", and the graph should now display the red vertical dotted line in the center.

     ![New Step 2 - New Runbook](images/new-runbook-draft-page-metric-step-new.png " ")

21. Step 3 is a Target SQL Step. It allows you to execute SQL against any database target in Enterprise Manager. In our example, the current SQL query will need to be updated to properly check for flashback retention usage. 

     ![Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step.png " ")

22. Select the pencil icon to edit Step 3.

     ![Edit Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit.png " ")

23. Under the Variables section, select the Add Variable button.

     ![Add Variable Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable.png " ")

24. You will see a pop-up box labeled Add a Runbook Variable. In the Name field, enter "user\_flash". In the Display Name field enter "Flash like statement". In the Value used in the Draft field, enter "%flash%". And for the Value used in a Runbook Session, you have the options to select the "User who runs the Runbook session specify the value" or select the "Same value used in the draft". Select "Same value used in the draft". 

     ![Add Variable Pop-up Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable-popup.png " ")

25. Select OK to save the variable.

     ![Save Variable Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-add-variable-popup-save.png " ")

26. Once the variable is saved, it should appear in the Variables section under "Author Defined". You will use this variable for the SQL query. 

     ![Variable Defined Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-variable-defined.png " ")

27. The current SQL query needs to be replaced to check for flashback retention usage. Replace the current SQL query with the following: "select name, value from v$parameter where name LIKE:$user\_flash".

     ![Replace Query Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-replace-query.png " ")

28. To test if the SQL query is correct, scroll to the bottom of the page and select the Run button. The Display section should show a table with the flashback retention usage results, which should list 1440 (i.e., the standard value needed).

     ![Test Query Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-edit-test-query.png " ")

29. Select Save Step.

30. Run Step 3 to view the new results from the updated query. The new results show that the flashback retention usage meets the standard value needed, 1440.

     ![New Step 3 - New Runbook](images/new-runbook-draft-page-target-sql-step-new.png " ")

31. You have now finished making edits to the Runbook and can publish it so that it can be used by others. At the top of the Runbook draft page click on the “Runbooks” link to go back to the Runbooks page.

     ![Runbooks Page Link from Step 3 - New Runbook](images/new-runbook-draft-page-runbooks-page-link.png " ")

32. The Runbook draft that you modified will be displayed in the Drafts tab and will have your updates.

     ![Runbooks Page with Updated Draft - New Runbook](images/emmonlab3bstep32.png " ")

33. Select the arrow under the Actions column to publish the Runbook for use.

     ![Publish Runbook Draft - New Runbook](images/emmonlab3bstep33.png " ")

34. Select OK. 

     ![Select Ok to Publish Runbook Draft - New Runbook](images/emmonlab3bstep34.png " ")

35. The "New Runbook" that you made modifications to has now been published and can now be used by other EM users. 

     ![Published Runbook - New Runbook](images/emmonlab3bstep35.png " ")

36. Select the arrow under the Actions column for the "New Runbook". You have the options to create new version from the published Runbook, hide it or delete. 

     ![Actions on Published Runbook - New Runbook](images/emmonlab3bstep36.png " ")


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

5. Oracle ships with default OOTB Metrics and settings. This includes Metrics, Thresholds, and Collection Schedules. This aims to cover generic use cases to get you started. We recommend that you customize the monitoring settings of your targets according to your requirements.
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

     ![Database target home page, all metrics](images/emmonlab3step14.png " ")

15.	Expand and highlight the Dump Area Metric Group.

     ![Database target home page, all metric](images/emmonlab3step15.png " ")

16.	Click on Dump Area Used(%) under the All Metrics palette and then click on the ‘background’ first row in the Dump Area Used(%) table.  

     ![Database target home page, all metric](images/emmonlab3step16.png " ")

17.	You should see the metric data for Dump Area Used(%) for the background processes.  By default, the last 24 hours are shown but you can change time periods using the View Data dropdown.  In the metric chart, click on Options to view different options for the chart, then click on the Show Thresholds option.

     ![Database target home page, all metric](images/emmonlab3step17.png " ")

18. The Warning and Critical thresholds for the metric will now be shown with the chart as yellow and red lines respectively.  As you review the metric, you can also visually see how close the metric values are to its Warning and Critical thresholds

     ![Database target home page, all metric](images/emmonlab3step18.png " ")

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

9. The Test Results section shows the results of running the Metric Extension on the selected targets.

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
     - step 1: Setup the Administration Groups Hierarchy
     - step 2: Create Template Collections
     - step 3: Associate Template Collections to Administration Groups
     - step 4: Synchronize the targets with the selected items

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

8. The “Compress Related Events into a Single Incident” rule set is a rule set that we created to showcase the new compression feature in EM 13c. Here we have 4 common use cases which are independent from one another. For each of these use cases, Enterprise Manager will compress the related events into a single incident. From a manageability standpoint, it will be much easier for the Administrator to manage one incident containing multiple related  events as a logical unit, as opposed to managing these individually. The Rule set covers the use cases of creating ONE incident when:

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

13.	Configure the following fields and click Next. Type: Metric Alert, All events of type Metric Alert. Severity: In Critical. 

     ![incident rules, create rule set page](images/emmonlab8step13.png " ")

14.	Click Add in the "Create New Rule: Add Actions" page.

     ![incident rules, create rule set page](images/emmonlab8step14.png " ")

15.	Configure the following fields and click Continue.                     

    - Conditions for actions
        - Keep the default of “Always execute the actions”
    - Create Incident or Update Incident  
        - Click on option “Create incident (if not associated with one)”   
        - Keep the default of  “Each event creates a new incident”

     ![incident rules, create rule set add actions page](images/emmonlab8step15.png " ")

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
- **Last Updated By/Date** – Desiree Abrokwa, Oracle Enterprise Manager Product Management [Sept 2022]
