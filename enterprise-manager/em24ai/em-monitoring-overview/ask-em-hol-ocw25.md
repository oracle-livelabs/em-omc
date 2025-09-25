# Oracle Enterprise Manager 24ai: Powered by GenAI
## Introduction
In today’s fast-paced IT environment, administrators and DBAs face challenges in managing complex systems while ensuring availability and performance. Try out this Hands-On Lab to learn about the new modernized Enterprise Manager 24ai platform that supports Zero Downtime (ZDT) Monitoring. Explore the new EM 24 features such as the new remote agents that will streamline monitoring across your host and database fleet. Converse with the GenAI (Ask EM) assistant to ask questions in natural language and quickly get answers and visual insights for more informed decision making. Check out our latest enhancements to Event Compression and Dynamic Runbooks. 

### Objectives
The objective of this lab is to become familiar with the new modernized Enterprise Manager 24ai platform.

### Prerequisites
This lab assumes you have:

- A Free Tier, Paid or LiveLabs Oracle Cloud account

*Estimated Time*: 70 minutes

### Lab Timing (Estimated)
| **Task Number** | **Feature**  | **Approx. Time** | **Details**                                                                                                                                                                                                                   
  |--------|-----------------------------------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **1**  | Using the Remote Agent                             | 15 minutes       |     Understand how to add a remote host to a remote agent for monitoring.                                                                                                                                                                                                                                                  |
  | **2A**  | Ask EM Assistant — Monitoring                                | 6 minutes       | Use the Ask EM assistant to get answers to monitoring questions.                                                                                                                                                 
  | **2B**  | Ask EM Assistant — Database Performance                        | 6 minutes       | Use the Ask EM assistant to get answers to database performance questions.                                                                                                                                                      
  | **2C**  | Ask EM Assistant — Database Patching and Compliance                              | 6 minutes       | Use the Ask EM assistant to get answers to database patching and compliance questions.  
| **3A**  | Event Compression Policies                              | 10 minutes       | View an example of a compressed incident and author your own Event Compression Policy.  
| **3B**  | Event Compression Analysis                             | 10 minutes       | Test your Event Compression Policy using the Event Compression Analysis tool and enable it for use in Incident Rules.  
| **4**  | Dynamic Runbooks for Metrics                              | 10 minutes       | Start a Dynamic Runbook session against a metric in the All-Metrics page.  
| **5**  | Dynamic Runbooks for Notification Backlog (Universal Context)                              | 5 minutes       | Understand the use of universal context for Dynamic Runbooks using the “Triage Notification Backlog” runbook as an example.   

## Task 1: Using the Remote Agent

A Remote Agent is a new type of agent that can remotely monitor and manage targets.  Remote Agents are installed on hosts dedicated to the remote agent. These agents use remote protocols for monitoring the host as well as databases and if needed, use SSH to run commands on the target host. No need to deploy and manage an agent on every single host. 

In this exercise the remote agent is already deployed for your convenience through the agent push method. 

The remote agent name is **emrmtagt.livelabs.com**. Here will walkthrough how to add remote host **emrmthost.livelabs.com** of your database target to the remote agent for monitoring. 

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. Click the **hamburger menu** icon.

    ![Enterprise Manager menu icon](ask-em-images/menu-icon.png " ")

3. Navigate to **Setup > Add Target > Add Targets Manually**.

    ![Navigate to Add Targets Manually](ask-em-images/remote-agent/setup-addtargets-addtargetsmanually.png " ")

4. On the **Add Targets Manually** page, click on the **Remote Agent** tab.

    ![Remote Agent Tab](ask-em-images/remote-agent/addtargets-remote-agent.png " ")

5. Under the tile **Remotely Monitor Host Targets**, click on **Add Host Targets to Remote Agent**.

    ![Add Host Targets to Remote Agent](ask-em-images/remote-agent/add-host-targets-remote-agent.png " ")

6. We will walk through the inputs needed to add the host target to remote agent.

7. For **Remote Agent**, search and select the agent named **emrmtagt.livelabs.com** and **Click on OK**.

    ![Select Remote Agent](ask-em-images/remote-agent/remote-agent-target-selector.png " ")

8. For the **Host Monitoring Credential**, select **ORACLE(EMADMIN)** from the dropdown.

    For the **Host Admin Credentials**, select **ROOT(SYSMAN)** from the dropdown.

    ![Select credentials](ask-em-images/remote-agent/host-monitoring-creds-host-admin-credentials.png " ")

9.  For the **Remote Cache** location, enter: **/u01/app/rmcache**. 

    For the **Remote Cache Sbin** location, enter: **/u01/app/rmsbincache**.

    ![Specify Remote Cache location](ask-em-images/remote-agent/remote-cache-remote-cache-sbin-location.png " ")

10. **Click on the Add button** on this page to add the remote host to the remote agent for monitoring. 

    Enter the remote host name as **emrmthost.livelabs.com** and **Click on Next**. 

    ![Add remote host to remote agent](ask-em-images/remote-agent/add-remote-host-addition.png " ")

11. On the Add Remote Host Target review screen, verify the details just entered.

    **Click on the “Cancel” button. Do not click on Submit.** 

    ![Final Review Screen](ask-em-images/remote-agent/add-remote-host-target-review.png " ")


## Task 2A: Ask EM Assistant — Monitoring

The Ask EM Assistant (Ask EM) is a GenAI-powered feature that helps you troubleshoot issues, visualize insights, and make informed decisions to boost operational efficiency and provide documentation references. Ask EM requires a connection to the Oracle Cloud Infrastructure (OCI). 

**Note: AI-generated responses may vary each time and might not exactly match the documented lab instructions results.**

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. In the upper right corner, click on the **Ask EM assistant icon** to start it.

    **Note: If the Ask EM assistant does not launch, refresh the browser and try again.**

    ![Start AskEM](ask-em-images/ask-em-monitoring/ask-em-logon1.png " ")

3. The Ask EM assistant should appear with a welcome message:

    ![AskEM Welcome Message](ask-em-images/ask-em-monitoring/ask-em-logon2.png " ")

4. Click on the **Documentation** Tab.

    ![AskEM Documentation Tab](ask-em-images/ask-em-monitoring/ask-em-doc1.png " ")

5. In the Documentation tab, type in the question below and  hit `<`enter`>`:

    **What are the new monitoring features in em24ai?**  

    ![AskEM Documentation - Question on monitoring 1](ask-em-images/ask-em-monitoring/ask-em-doc2.png " ")

    **Review the answer that it returns.**
    
    Note: You may need to scroll up to see the first part of the answer. In the interest of time, you can just skim through the information.

    ![AskEM Documentation - Review question on monitoring 1](ask-em-images/ask-em-monitoring/ask-em-doc3.png " ")

6. Stay in the Documentation tab, ask this question:

    **What is zero downtime monitoring service?**

    ![AskEM Documentation - Question on monitoring 2](ask-em-images/ask-em-monitoring/ask-em-doc4.png " ")

    **Review the answer.**

    ![AskEM Documentation - Review question on monitoring 2](ask-em-images/ask-em-monitoring/ask-em-doc5.png " ")


7. Stay in the Documentation tab, ask this question: 

    **Can I use zero downtime monitoring when upgrading from em 13.5 to em 24ai?**

    ![AskEM Documentation - Question on monitoring 3](ask-em-images/ask-em-monitoring/ask-em-doc6.png " ")

    **Review the answer.**

    ![AskEM Documentation - Review question on monitoring 3](ask-em-images/ask-em-monitoring/ask-em-doc7.png " ")

8. Next, click on the **Telemetry** tab.

    ![AskEM Telemetry - Select telemetry](ask-em-images/ask-em-monitoring/ask-em-tel1.png " ")

9. In the Telemetry tab, ask this question:

    **Do I have any database incidents?**    

    ![AskEM Telemetry - Any DB incidents](ask-em-images/ask-em-monitoring/ask-em-tel2.png " ")

    **Click on “Open” to see findings.**

    ![AskEM Telemetry - Click on Open to see findings](ask-em-images/ask-em-monitoring/ask-em-tel3.png " ")

    A dashboard should appear with a set of widgets that contain data in response to your question.  In the set of widgets, you should see the “Database Incidents” widget which shows a count of open database incidents.

    ![AskEM Telemetry - Dashboard](ask-em-images/ask-em-monitoring/ask-em-tel4.png " ")

    **Pin the widget.**  
    Note: Pinning the widget means you want to keep this widget in your dashboard.

    ![AskEM Telemetry - Pin the widget](ask-em-images/ask-em-monitoring/ask-em-tel5.png " ")

    **After pinning the widget, it should always be in the dashboard display.**
    ![AskEM Telemetry - Pin the widget complete](ask-em-images/ask-em-monitoring/ask-em-tel6.png " ")

10. In the Telemetry tab, ask this question:

    **Show me a list of database incidents**

    ![AskEM Telemetry - List of DB incidents](ask-em-images/ask-em-monitoring/ask-em-tel7.png " ")

    **After a new set of widgets appear, choose Target Type: Database Instance**

    ![AskEM Telemetry - List of DB incidents, choose DB Instance](ask-em-images/ask-em-monitoring/ask-em-tel8.png " ")

    **Choose Target Name: cdb186.subnet.vcn.oraclevcn.com**

    The “Incidents List” widget should show open incidents for this database.
    
    Notice we have a few incidents on the database dump area being full.

    ![AskEM Telemetry - List of DB incidents, choose target name](ask-em-images/ask-em-monitoring/ask-em-tel9.png " ")

    **Pin the Incidents List widget**

    ![AskEM Telemetry - List of DB incidents, pin the widget](ask-em-images/ask-em-monitoring/ask-em-tel10.png " ")
    
11. In the Telemetry tab, ask this question:

    **Show me trend of dump area**

    This will allow us to review the trend of database dump area usage.

    ![AskEM Telemetry - Show me trend of dump area](ask-em-images/ask-em-monitoring/ask-em-tel11.png " ")

    The dashboard should show a metric chart showing the trend of the dump area used.  
    Note: The metric values for background, core, user dump areas are the same so they may appear as a single line.  They are actually 3 overlapping lines.

    ![AskEM Telemetry - Show me trend of dump area, dashboard](ask-em-images/ask-em-monitoring/ask-em-tel12.png " ")

12. Now **Close** the Ask EM session.

    ![AskEM Close Session](ask-em-images/ask-em-monitoring/ask-em-tel13.png " ")

## Task 2B: Ask EM Assistant — Database Performance

The Ask EM Assistant (Ask EM) is a GenAI-powered feature that helps you troubleshoot issues, visualize insights, and make informed decisions to boost operational efficiency and provide documentation references. Ask EM requires a connection to the Oracle Cloud Infrastructure (OCI).

**Note: AI-generated responses may vary each time and might not exactly match the documented lab instructions results.**

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. In the upper right corner, click on the **Ask EM assistant icon** to start it.

    **Note: If the Ask EM assistant does not launch, refresh the browser and try again.**

    ![Start AskEM](ask-em-images/ask-em/ask-em-start.png " ")

3. The Ask EM assistant should appear with a welcome message:

    ![AskEM Welcome Message](ask-em-images/ask-em/ask-em-welcome.png " ")

4. In the Telemetry tab, ask this question:

    **How is the performance of my databases?**    

    **Click on “Open” to see findings.**

    ![AskEM Telemetry - Click on Open to see findings](ask-em-images/ask-em-db-perf/click-on-open.png " ")

    A new set of widgets appear, choose the following:
    - **Aggregate Target Name: Prod-Grp**
    - **Target Type: Database Instance**
    - **Target Name: cdb186.subnet.vcn.oraclevcn.com**

    ![AskEM Telemetry - Choose target selector info](ask-em-images/ask-em-db-perf/choose-target-details.png " ")

    ![AskEM Telemetry - Results of Db performance 1](ask-em-images/ask-em-db-perf/perfdatabase-1.png " ")

    ![AskEM Telemetry - Results of Db performance 2](ask-em-images/ask-em-db-perf/perfdatabase-2.png " ")

5. In the Telemetry tab, ask this question:

    **Is there a spike in average active sessions on my database?**

    ![AskEM Telemetry - Spike in Avg Active Sessions](ask-em-images/ask-em-db-perf/spike-aas-1.png " ")

6. In the Telemetry tab, ask this question:

    **Show me used and allocated space usage on my database.**

    ![AskEM Telemetry - Allocated space usage on DBs](ask-em-images/ask-em-db-perf/space-allocated-used-1.png " ")

7. In the Telemetry tab, ask this question:

    **What are the top activities on my database**

    ![AskEM Telemetry - Top activities on DBs](ask-em-images/ask-em-db-perf/top-activities-1.png " ")

8. Go to the **Documentation** tab, ask this question:

    **How to troubleshoot busy wait events?**

    ![AskEM Documentation - Troubleshoot busy wait events 1](ask-em-images/ask-em-db-perf/documentation-2.png " ")

    ![AskEM Documentation - Troubleshoot busy wait events 2](ask-em-images/ask-em-db-perf/documentation-3.png " ")

9. Now **Close** the Ask EM session.

    ![AskEM Close Session](ask-em-images/ask-em/ask-em-close.png " ")

## Task 2C: Ask EM Assistant — Database Patching and Compliance

The Ask EM Assistant (Ask EM) is a GenAI-powered feature that helps you troubleshoot issues, visualize insights, and make informed decisions to boost operational efficiency and provide documentation references. Ask EM requires a connection to the Oracle Cloud Infrastructure (OCI).

**Note: AI-generated responses may vary each time and might not exactly match the documented lab instructions results.**

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. In the upper right corner, click on the **Ask EM assistant icon** to start it.

    **Note: If the Ask EM assistant does not launch, refresh the browser and try again.**

    ![Start AskEM](ask-em-images/ask-em/ask-em-start.png " ")

3. The Ask EM assistant should appear with a welcome message:

    ![AskEM Welcome Message](ask-em-images/ask-em/ask-em-welcome.png " ")

4. In the Telemetry tab, ask this question:

    **Show me list of subscribed targets.**    

    ![AskEM Telemetry - List of subscribed targets 1](ask-em-images/ask-em-db-patch/em-db-subscribe.png " ")

5. In the Telemetry tab, ask this question:

    **Which databases are subscribed to 19cDB-Linux-x64-Apps?**

    ![AskEM Telemetry - List of subscribed targets 2](ask-em-images/ask-em-db-patch/em-db-subscribe.png " ")

7. In the Telemetry tab, ask this question:

    **Are my databases compliant with patches?**

    ![AskEM Telemetry - Patch recommendations 2](ask-em-images/ask-em-db-patch/em-db-compliance.png " ")

8. In the Telemetry tab, ask this question:

    **How many critical violations exist?**

    ![AskEM Telemetry - Critical violations](ask-em-images/ask-em-db-patch/em-critical-violations.png " ")

9. Now **Close** the Ask EM session.

    ![AskEM Close Session](ask-em-images/ask-em/ask-em-close.png " ")

## Task 3A: Event Compression Policies

Event Compression is the process of grouping (i.e., compressing) multiple correlated events into a smaller subset of actionable incidents. An Event Compression Policy defines the specific set of related events that should be grouped together. Before incident creation, Event Compression Policies work with Incident Rule Sets to determine if incoming events should be grouped and compressed into a single incident.

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. Click the **hamburger menu** icon.

    ![Enterprise Manager menu icon](ask-em-images/menu-icon.png " ")

3. Navigate to **Enterprise > Monitoring > Incident Manager**.

    ![Navigate to Enterprise menu option](ask-em-images/event-compression-policies/enterprise.png " ")

    ![Navigate to Incident Manager](ask-em-images/event-compression-policies/monitoring.png " ") 

4. Let’s take a look at an example of an incident with event compression. 

    **Select the incident with the summary text: There are 5 target\_availability events on members of db19c.subnet.vcn.oraclevcn.com\_sys.**

    ![Select incident](ask-em-images/event-compression-policies/incident.png " ")

5. Click **Open in new tab**.

    ![Open in new tab](ask-em-images/event-compression-policies/open-in-new-tab.png " ")

6. From here, take a closer look at the incident details to view:
    - The number of events in the incident
    - The Incident Rule and RuleSet used to create the incident
    - The Event Compression Policy used to group the events into this incident
    - The list of events in the incident

    ![Incident Details](ask-em-images/event-compression-policies/incident-details.png " ")

7.	Now let’s take a look at how to use and create Event Compression Policies to create these compressed incidents.

8.	Click the **hamburger menu** icon.

    ![Navigate back to menu](ask-em-images/event-compression-policies/navigate-back-to-menu.png " ")

9.	Navigate to **Setup > Incidents > Event Compression Policies**.

    ![Setup menu option](ask-em-images/event-compression-policies/setup.png " ")

    ![Event Compression Policies menu option](ask-em-images/event-compression-policies/event-compression-policies.png " ")

10. There are 7 Oracle-provided Event Compression Policies. You can also author your own policies for custom compression requirements.

    ![Event Compression Policies page](ask-em-images/event-compression-policies/policy-page.png " ")

11.	Let’s take a look at the policy that created the incident with event compression that we previously viewed.

    **Click the policy with the name: Target down events for a database system and its members**.

    ![Select custom policy](ask-em-images/event-compression-policies/custom-policy.png " ")

12. Here you can view the criteria for how the events were grouped together into the incident.

    ![Custom policy details](ask-em-images/event-compression-policies/custom-policy-details.png " ")

13. Click the **X** icon to exit from the screen.

    ![Leave custom policy details](ask-em-images/event-compression-policies/leave-custom-policy.png " ")

14. Now, we will take a look at and edit a custom policy. In this lab, a custom draft policy has already been created for you that you will modify. This policy groups multiple event types into a singular incident.

15. Select **Actions > Edit** for the following policy: **Target down, metric alert, and metric evaluation error events for a database system and its members**.

    ![Locate new policy details](ask-em-images/event-compression-policies/new-policy.png " ")

    ![Edit new policy details](ask-em-images/event-compression-policies/edit-new-policy.png " ")

16.	In the Event Compression Logic sub-section, you can see the policy applies to:
    - Multiple event types: Target Availability/Down, Metric Alert, and Metric Evaluation Error
    - Target Types: Database System, Database Instance, Pluggable Database
    - Event Severity: Fatal and Critical
    - Time Window: 60 minutes
    
    ![New policy details](ask-em-images/event-compression-policies/new-policy-details.png " ") 

17. Locate the dropdowns under the header **Compress into One Incident By**. This determines the criteria for grouping the events.

    ![Locate dropdown to group the events](ask-em-images/event-compression-policies/compress-by.png " ") 

18. Select the dropdown for **select Group type**. 

    Search for and click on **Database System**. 
    
    This ensures that the specified events for the Database Instance, Pluggable Database, and Database System targets will be grouped into an incident based on the Database System.

    ![Group events by Database System](ask-em-images/event-compression-policies/database-system.png " ") 

19. Click **Save**.

    ![Save new policy](ask-em-images/event-compression-policies/save-new-policy.png " ") 

20. The custom policy you edited is still in a Draft status. 

    ![Draft policy](ask-em-images/event-compression-policies/new-policy-draft.png " ") 

21. Continue to **Task 3B: Event Compression Analysis** to test out the policy, publish it and enable it for use by other EM administrators.


## Task 3B: Event Compression Analysis

**Complete Task 3A: Event Compression Policies prior to beginning this task.**

Event Compression is the process of grouping (i.e., compressing) multiple correlated events into a smaller subset of actionable incidents. An Event Compression Analysis uses historical monitoring data from your environment to analyze the impact Event Compression Policies would have had on your actual incidents had these policies been enabled. 

1. Before publishing and enabling your policy (created in **Task 3A: Event Compression Policies**) for use, test it out using the Event Compression Analysis tool.

2. First **enable** the policy for testing using the toggle button.

    ![Toggle the enable button](ask-em-images/event-compression-analysis/disabled-toggle.png " ")

    ![Submit the enable policy button](ask-em-images/event-compression-analysis/submit-enablement.png " ")

    ![Policy is now enabled](ask-em-images/event-compression-analysis/enabled-toggle.png " ")

3. Click the **Event Compression Analysis** link.

    ![Select Event Compression Analysis link](ask-em-images/event-compression-analysis/link-to-analysis.png " ")

4. The Event Compression Analysis uses real events from your environment to test the effectiveness of these Event Compression Policies against your own events.

    To begin a new analysis, click **Start New Analysis**.

    ![Start new analysis](ask-em-images/event-compression-analysis/start-new-analysis.png " ")

6. Enter the following in the pop-up that displays:
    - Name: **Analysis for DB System and its members**
    - Analyze events from these targets:
        - In the dropdown for **Select a Group**, select: **Prod DB Targets**
    - Events occurred within this time range:
        - From: **07/14/2025**
        - To: **07/28/2025**
    - Click **Include Draft Policy** so that your draft policy is used in the analysis

    At the end, your Compression Policy Analysis criteria should look like the following:

    ![Analysis entry](ask-em-images/event-compression-analysis/analysis-entry.png " ")

7. Click **Start Analysis**. 

    ![Start analysis](ask-em-images/event-compression-analysis/analysis-entry-start.png " ")

8. A job is submitted that will run the analysis. 

    It takes a few seconds for the analysis to complete so **Refresh your browser** to see analysis results.

    ![Analysis job is ran](ask-em-images/event-compression-analysis/refresh-browser.png " ")

9. Click on the analysis name.

    ![Select the analysis name](ask-em-images/event-compression-analysis/select-analysis.png " ")

10. The top boxes are a summary of the analysis:
    - 115 events were analyzed
    - 110 incidents were created <u>without</u> the compression policies enabled
    - 26 incidents would have been created <u>with</u> the compression policies enabled
    - There would have been 76% fewer incidents with compression policies enabled
    - On average, 4.42 events would have been compressed into a singular incident 

    ![Analysis summary](ask-em-images/event-compression-analysis/analysis-summary.png " ")

11.	View the graph for a visual breakdown of the compression: 

    - The **navy bars** represent the number of incidents when Event Compression Policies were not enabled. 
    - The **orange bars** represent number of incidents if Event Compression Policies were used. 
    - The **gray line** represents the number of real events analyzed.

    ![Analysis bar](ask-em-images/event-compression-analysis/analysis-bar.png " ")

13. Click on one of the bars for **Jul 21** to see the exact events mapped from incidents without compression policies to incidents with compression policies.

    ![Select one of the analysis bar](ask-em-images/event-compression-analysis/july-21.png " ")

14. This view allows you to see compression in action. View how multiple events that used to belong to one incident each would be grouped into a smaller number of incidents with Event Compression Policies enabled.

    ![Analysis mappings](ask-em-images/event-compression-analysis/analysis-map.png " ")

15. Click on the orange **Incidents with compression policies** bar to view more details.

    ![Analysis orange bar](ask-em-images/event-compression-analysis/orange-bar.png " ")

    ![Analysis event details](ask-em-images/event-compression-analysis/analysis-events.png " ")

16. Click **OK** once you are finished reviewing the details.

    ![Close analysis events](ask-em-images/event-compression-analysis/close-analysis-events.png " ")

17. Click **OK** again.

    ![Close analysis mappings](ask-em-images/event-compression-analysis/close-map.png " ")

18. Click the **X icon** to exit out of the analysis.

    ![Close analysis summary](ask-em-images/event-compression-analysis/close-analysis-summary.png " ")

19. Now that you have tested and confirmed your policy is working, you will publish it for use.

    **Navigate back to Setup > Incidents > Event Compression Policies**.

    ![Setup menu option](ask-em-images/event-compression-policies/setup.png " ")

    ![Event Compression Policies menu option](ask-em-images/event-compression-policies/event-compression-policies.png " ")

20.	Click the **Actions** icon under your policy and select **Publish**.

    ![Publish your policy](ask-em-images/event-compression-analysis/publish-new-policy.png " ")

    ![Select publish button](ask-em-images/event-compression-analysis/select-publish.png " ")

    ![Policy is now published](ask-em-images/event-compression-analysis/published.png " ")

21. Event Compression Policies work hand-in-hand with Incident Rules to create the incidents with compressed events. Now that your policy has been published, let’s see how it would be enabled for use in Incident Rules.

22. Navigate to **Setup > Incidents > Incident Rules**.

    ![Navigate to Setup](ask-em-images/event-compression-policies/setup.png " ")

    ![Navigate to Incident Rules](ask-em-images/event-compression-analysis/incident-rules.png " ")

23.	An Incident Rule Set has already been created to work with your compression policy.

24.	Select the rule set **Compress Target Down, Metric Alert, Metric Error Events**. 

    **Click Edit**.

    ![Edit the rule set](ask-em-images/event-compression-analysis/edit-incident-rule.png " ")

25.	Scroll down to the Rules section and view the 3 rules for:
    - Compress **Target Down Events** for Oracle Database System, Database Instance, and Pluggable Databases
    - Compress **Metric Alert Events** for Oracle Database System, Database Instance, and Pluggable Databases
    - Compress **Metric Error Events** for Oracle Database System, Database Instance, and Pluggable Databases

    ![View the multiple rules in the rule set](ask-em-images/event-compression-analysis/multiple-rules.png " ")

26.	Notice in the Action Summary column that all the rules Create Incidents that Use Event Compression Policies.

    ![Create incidents that use event compression policies](ask-em-images/event-compression-analysis/use-compression.png " ")

27.	Scroll down to the **Event Compression** section. 

28.	Notice the option, Allow policies to compress events across event types from multiple rules in the rule set (Ruleset Level Compression), has been selected. 

    This enables event compression to work across multiple event types (i.e., target availability/down, metric alert, metric evaluation error).

    ![Multiple event compression enabled](ask-em-images/event-compression-analysis/multi-compression-enabled.png " ")

29.	Scroll back up.

30.	Click **Cancel**.

    ![Cancel incident rule](ask-em-images/event-compression-analysis/cancel-rule.png " ")

31. Since your compression policy has been published, it would now work with this Incident Rule Set to compress the target down, metric alert and metric evaluation error events for your database system and its member targets into a singular incident

    ![Finalized incident rule](ask-em-images/event-compression-analysis/final-rule.png " ")

## Task 4: Dynamic Runbooks for Metrics

Dynamic Runbooks are documented best practice procedures in the form of executable steps that ITOps teams follow to prevent or resolve an issue. Dynamic Runbooks can be executed inside Enterprise Manager in context of a metric, incident, or any other Enterprise Manager context. 

For this task, a Metric-Based Dynamic Runbook has already been published for you to use. You will go through the process of starting a Runbook session against a designated **METRIC**.

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. Click the **hamburger menu** icon.

    ![Enterprise Manager menu icon](ask-em-images/menu-icon.png " ")

3. Navigate to **Targets > Databases**. 

    ![Navigate to Databases](ask-em-images/metric-runbook/targets.png " ")

4. Locate and expand **cdb186.subnet.vcn.oraclevcn.com** to view its pluggable databases (PDBs). 

    ![Locate the CDB target](ask-em-images/metric-runbook/locate-cdb186.png " ")

5. Click the PDB target with the name: **cdb186.subnet.vcn.oraclevcn.com\_TESTPDB**.

    ![Select the PDB target](ask-em-images/metric-runbook/db-fleet.png " ")

6. In the PDB target homepage, navigate to **Oracle Database > Monitoring > All Metrics**.

    ![Navigate to All Metrics](ask-em-images/metric-runbook/all-metrics.png " ")

7. Locate the **Tablespace Full** metric group and expand it. 

    ![Locate the Tablesace full metric group](ask-em-images/metric-runbook/locate-tblspc-full.png " ")

8. Click the **Tablespace Space Used (%)** metric.

    ![Click the tablespace space used metric](ask-em-images/metric-runbook/select-metric.png " ")

9. Click on the **DEMO** tablespace row.

    ![Click the DEMO tablespace](ask-em-images/metric-runbook/select-tablespace.png " ")

10. Notice that the metric is 84% and approaching the warning and critical thresholds of 90% and 97%. 

    ![Metric approaching threhsolds](ask-em-images/metric-runbook/approach-threshold.png " ")

11. You will use a runbook to triage this metric before an alert is triggered and an incident is created.

12. Locate the **Runbook Sessions** section. 

    Under **Current Sessions** section, select the runbook for **Database Tablespace Full Triage: 2025-07-31 09:44:49** to open an existing runbook session.

    ![Locate Runbook sessions](ask-em-images/metric-runbook/open-current-session.png " ")

13. A runbook session appears in a new tab with the metric details carried over. We will walk through the steps needed to triage this Tablespace Space Used metric before it crosses the critical threshold. 

    ![Runbook session started](ask-em-images/metric-runbook/new-session.png " ")

14. Check the **checkbox** to indicate you have read and completed the Overview & Prerequisites step.

    This step describes the runbook purpose and the prerequisites needed to execute the steps. In this lab, the prerequisites have already been completed for you.

    ![Overview and Prereqs Step](ask-em-images/metric-runbook/overview-prereq.png " ")

15. Click the **play icon in Step 2** to review the trend of the Tablespace Full metric. Note if there is an increasing trend.

    ![Step 2 - Metric Data Step](ask-em-images/metric-runbook/play-metric-data.png " ")

16. Notice for Step 3 a gear icon is displayed instead of the play icon. 

    **Click the gear icon**.

    The gear icon means some input properties are required before you can execute the step.

    ![Step 3 - Gear Icon](ask-em-images/metric-runbook/step-3-gear-icon.png " ")

17. Step 3 requires you to select the PDB named credentials to execute the step.

    **Click on the credentials field box**. 

    ![Step 3 - Credentials Field](ask-em-images/metric-runbook/select-db-cred-field.png " ")

19. Ensure the PDB named credential **CDB186\_PDB (EMADMIN)** is selected. 

    **Click Save**.

    Note: You may need to drag the credentials pop-up window up to fully view it on your screen.

    ![Step 3 - Credentials Selected](ask-em-images/metric-runbook/select-db-cred.png " ")

20. **Click the play icon** to find out which tables in the tablespace are consuming the most space.

    ![Step 3 - Click play icon](ask-em-images/metric-runbook/play-step-3.png " ")

21. The ‘Student’ table appears to be consuming the most space. Assume that all the data in the ‘Student’ table is necessary. 

    **Continue to Step 4**.

    ![Step 3 - Results](ask-em-images/metric-runbook/step-3-results.png " ")

22. To increase the tablespace size, first identify the filesystem that is used by the tablespace.

    **Click the play icon in Step 4.** The filesystem path output will be used in Step 5. 
    
    **Continue to Step 5.**
    
    ![Step 4 - Click play icon](ask-em-images/metric-runbook/step-4-results.png " ")

23.	Notice for Step 5 another gear icon is displayed instead of the play icon.

    **Click on the gear icon.**

    ![Step 5 - Gear Icon](ask-em-images/metric-runbook/step-5-gear-icon.png " ")

24. Step 5 requires you to select the host named credentials to execute the step.

    **Click on the credentials field box**. 

    ![Step 5 - Credentials Field](ask-em-images/metric-runbook/select-host-cred-field.png " ")

26. Select the host named credential: **ORACLE (EMADMIN)**.

    **Click Save**.

    Note: You may need to drag the credentials pop-up window up to fully view it on your screen.

    ![Step 5 - Credentials Selected](ask-em-images/metric-runbook/select-host-cred.png " ")

27. **Click the play icon** to check the filesystem for available space. 

    ![Step 5 - Click play icon](ask-em-images/metric-runbook/play-step-5.png " ")

28. There are 342G available in the filesystem which means there is enough space to increase the tablespace size. 

    **Continue to Step 6.**

    ![Step 5 - Results](ask-em-images/metric-runbook/step-5-results.png " ")

29. **Click the play icon in Step 6** to note if there is a decreasing filesystem space available trend that could impact future growth of tablespace.

    ![Step 6 - Results](ask-em-images/metric-runbook/step-6-results.png " ")

30. **Scroll to Step 7**. 

    This step includes a hyperlink to EM’s ‘Tablespace Page’ to allow you to add another 100MG datafile to the tablespace. 
    
    For lab purposes, we will NOT go through the workflow to add a new datafile to the tablespace.

    ![Scroll to Step 7](ask-em-images/metric-runbook/step-7.png " ")

31. **Check the checkbox** to indicate you completed the step.

    ![Step 7 Complete](ask-em-images/metric-runbook/step-7-complete.png " ")

32. The Runbook remains an active session until you Mark as Done. 

    **Click Mark as Done** to indicate that you have gone through all the steps. 

   ![Mark as done](ask-em-images/metric-runbook/mark-as-done.png " ")

33. **Click OK**.

   ![Select OK](ask-em-images/metric-runbook/select-ok.png " ")

34. A page with your completed Runbook Sessions will appear. 

   ![Runbook Sessions](ask-em-images/metric-runbook/runbook-sessions.png " ")

## Task 5: Dynamic Runbooks for Notification Backlog (Universal Context) 

Dynamic Runbooks are documented best practice procedures in the form of executable steps that ITOps teams follow to prevent or resolve an issue. Dynamic Runbooks can be executed inside Enterprise Manager (EM) in context of a metric, incident, or any other EM context (universal context).

A universal context runbook can be used for any functional area in EM.  

As an example of a universal context runbook, you will review the Triage Notification Backlog runbook.

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. Click the **hamburger menu** icon.

    ![Enterprise Manager menu icon](ask-em-images/menu-icon.png " ")

3.	Navigate to **Setup > Manage Enterprise Manager > Health Overview**.

    ![Navigate to Setup](ask-em-images/universal-runbook/setup.png " ")

    ![Navigate to Health Overview](ask-em-images/universal-runbook/health-overview.png " ")

4.	Scroll down to the **Notification Performance** section.

    ![Scroll to Notification Performance](ask-em-images/universal-runbook/notif-performance.png " ")

5. Notice the Oracle provided runbook named **Triage Notification Backlog with Runbook**. This is an example of a universal context runbook.  This runbook helps to triage delayed or missing notifications.

    **Click on the "Triage Notification Backlog with Runbook" link to start a runbook session**. It will open a runbook session in a new tab.

    ![Start new Runbook session](ask-em-images/universal-runbook/universal-runbook.png " ")

6. In this runbook session, notice the universal context description.  This means it does not have a pre-defined context, but it has steps to query and take actions on the appropriate EM components.

    ![Universal Context runbook session started](ask-em-images/universal-runbook/traige-notif-backlog.png " ")

7. **Execute the first 4 steps of the runbook**.  You do not have to execute the remaining steps.

    ![Universal Context Runbook - Overview and Prereqs](ask-em-images/universal-runbook/overview-prereq.png " ")

    ![Universal Context Runbook - Step 1](ask-em-images/universal-runbook/step-2.png " ")

    ![Universal Context Runbook - Step 2](ask-em-images/universal-runbook/step-3.png " ")

    ![Universal Context Runbook - Step 3](ask-em-images/universal-runbook/step-4.png " ")



## Learn More

  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager 24ai Documentation Library](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/24.1/index.html)
  - [Enterprise Manager 24ai Tech Forum Video Playlist](https://www.youtube.com/playlist?list=PLiuPvpy8QsiXvGYMP_N3WA6bddXvUH-Y0)

## Acknowledgements
- **Author** - Desiree Abrokwa, Oracle Enterprise Manager Product Management
- **Contributing Author** - Ana McCollum, Sumesh Balakrishnan, Anusha Vojjola, Harish Niddagatta, Romit Acharya, Anand Prabhu, Oracle Enterprise Manager Product Management
- **Last Updated By/Date** – Desiree Abrokwa, Oracle Enterprise Manager Product Management [August 2025]
