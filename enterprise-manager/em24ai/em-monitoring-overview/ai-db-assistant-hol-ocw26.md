# Oracle Enterprise Manager 24ai: Powered by GenAI
## Introduction
Oracle Enterprise Manager 24ai is designed to help DBAs monitor and manage Oracle Database environments. In this hands-on lab, try the Oracle AI Database Assistant, Enterprise Manager’s agentic AI chatbot for conversational operations. Configure it to use EM’s LLM or your own LLM, manage user access, and ask natural-language questions about the health of your database fleet. You’ll also use Event Compression to reduce alert fatigue and incident volume, explore Dynamic Runbooks with auto-run data collection before incident triage, and try the new AI-based runbook generator that converts existing runbooks into executable triage steps in Enterprise Manager. 

### Objectives
The objective of this lab is to become familiar with the new modernized Enterprise Manager 24ai platform.

### Prerequisites
This lab assumes you have:

- A Free Tier, Paid or LiveLabs Oracle Cloud account

*Estimated Time*: 70 minutes
 

## Task 1A: Oracle AI Database Assistant - Monitoring 

Oracle AI Database Assistant combines Enterprise Manager telemetry with Large Language Models (LLMs) to provide an intuitive conversational experience for monitoring and operational investigations.
Instead of manually searching through Enterprise Manager pages, administrators can ask questions such as:
    •	Show open incidents
    •	Show job executions in the last 24 hours
    •	Show target availability status
    •	Show critical alerts for production databases
The assistant can return rich widgets, tables, and visualizations directly within the chat experience, helping users quickly understand and act on operational information.
 

1. Log into Enterprise Manager using the credentials **emadmin/welcome1**. 

    ![Enterprise Manager login](ask-em-images/em24-login.png " ")

2. In the upper right corner click on the **Oracle AI Database Assistant** to start it

    ![Enterprise Manager menu icon](ai-db-assistant-images/ai-db-assistant-monitoring/ai-db-assistant.png " ")

3. The Oracle AI Database Assistant should appear with a welcome message and out-of-box questions to get you started.

    ![AI Dataabse Assistant Welcome page](ai-db-assistant-images/ai-db-assistant-monitoring/ai-db-assistant-welcome.png " ")

4. In the chat window Click on question **Show status summary for all my targets**.

    ![AI DB Assistant OOB Question](ai-db-assistant-images/ai-db-assistant-monitoring/ai-db-assistant-oob-question.png " ")

5. In the widget click on **3 dots** and choose **Maximize Widget**.

    ![Target summary maximize widget](ai-db-assistant-images/ai-db-assistant-monitoring/target-summary-maximize.png " ")

6. Click on the **Down** pie slice and review the targets that are down and click on **Close**.

    ![Down pie widget](ai-db-assistant-images/ai-db-assistant-monitoring/down-target-summary-widget.png " ")

7. Click on **minimize** icon on the upper right corner of the widget.

    ![Minimize Widget](ai-db-assistant-images/ai-db-assistant-monitoring/target-summary-minimize.png " ")

8. In the chat window click on **Show list of open incidents**.

    ![Open Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/list-open-incidents.png " ")

9. In the widget click on **3 dots** and choose **Maximize Widget** and review the incidents. 

    ![Maximize Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/maximize-incidents.png " ")

10. For the first incident in the list click the **3 dots** and choose **Acknowledge**. 

    ![Incident Acknowledgement](ai-db-assistant-images/ai-db-assistant-monitoring/incident-ack.png " ")

11. In the confirmation dialog click **Acknowledge**.

    ![Acknowledge](ai-db-assistant-images/ai-db-assistant-monitoring/acknowledgement-incident.png " ")

    After doing the acknowledgment table should show current user **EMADMIN** is the owner of the incident.

    ![Emadmin inci owner](ai-db-assistant-images/ai-db-assistant-monitoring/emadmin-incident-owner.png " ")

12. Click on **+** button on the upper right corner of the widget and choose **Target Property** 

    ![Incident Target Property](ai-db-assistant-images/ai-db-assistant-monitoring/incident-target-property.png " ")

13. Click on Target Property filter and select **Production**. Table of incidents is filtered to show incidents from production targets.

    ![Production Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/production-incident.png " ")

14. Click on the **3 dots** for the first incident and choose **Add Comment**

    ![Add comment](ai-db-assistant-images/ai-db-assistant-monitoring/add-comments-incident.png " ")

15. Add this comment **Will look at this later** and click on **Save**.

    ![Add comment will look later](ai-db-assistant-images/ai-db-assistant-monitoring/will-look-later.png " ")

16. Click on **minimize** icon on the upper right corner of the widget:

    ![Minimize incident list](ai-db-assistant-images/ai-db-assistant-monitoring/minimize-incidents.png " ")

17. Enter the question **Do I have any escalated incidents?** in the chat window and hit `<`enter`>`:

    ![Escalated Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/any-escalated-incidents.png " ")


18. In the widget click on **3 dots** and choose **Maximize Widget**: 

    ![Maximize Escalated Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/max-escalated-incidents.png " ")

19. Review the list of escalated incidents and click on **minimize icon** on the upper right corner of the widget.

    ![Minimize Escalated Incidents](ai-db-assistant-images/ai-db-assistant-monitoring/mini-escalated-incidents.png " ")

20. Scroll up to the top of the chat window and click on **Show list of Oracle Databases with highest average active sessions** prompt:

    ![DB Active Sessions](ai-db-assistant-images/ai-db-assistant-monitoring/db-aas-question.png " ")

21. In the widget click on **3 dots** and choose **Maximize Widget** and review the database performance metrics:

    ![Maximize DB Perf widget](ai-db-assistant-images/ai-db-assistant-monitoring/max-db-performance-widget.png " ")
    
22. Click on **+** button on the upper right corner of the widget and choose **Show label** and **Key Aggregation**:

    ![Add Filters to Widget](ai-db-assistant-images/ai-db-assistant-monitoring/add-filters-db-perf-widget.png " ")

23. In the Metric Column filter change **Average Active Sessions** to **CPU Utilization (%)** and review the CPU Utilization.

    ![CPU Utilization](ai-db-assistant-images/ai-db-assistant-monitoring/cpu-util-widget.png " ")

24. In the widget change the value of these filters:

    Metric Name to **Tablespaces Full**

    ![Tablespace full](ai-db-assistant-images/ai-db-assistant-monitoring/tbspace-full-metric.png " ")

    Metric Column to **Tablespace Space Used (%)**

    ![Tablespace used](ai-db-assistant-images/ai-db-assistant-monitoring/tbspace-used-widget.png " ")

    Key Aggregation to **Max**. The table shows the highest usage of tablespaces for each database.   Review the values shown:

    ![Key Agg Max](ai-db-assistant-images/ai-db-assistant-monitoring/key-agg-max.png " ")

25. In the table click on the highest number in value under the **Value** column. This should open a new browser tab showing the All Metrics page showing the tablespace with that high usage value.

    ![Tablespace full value Click](ai-db-assistant-images/ai-db-assistant-monitoring/tb-full-metric-value-click.png " ")

    ![All Metrics Page](ai-db-assistant-images/ai-db-assistant-monitoring/all-metrics-page.png " ")

26. Go back to the browser tab with AI Assistant. Click on **minimize icon** on the upper right corner of the widget.

    ![Minimize DB Perf Metric](ai-db-assistant-images/ai-db-assistant-monitoring/mini-db-perf-metric.png " ")

## Task 1B: Oracle AI Database Assistant - Database Patching and Compliance

Oracle AI Database Assistant combines Enterprise Manager telemetry with Large Language Models (LLMs) to provide an intuitive conversational experience for monitoring and operational investigations.

In this task, you use the assistant to assess database fleet readiness before a patch window and verify patch compliance after patching. 
Instead of navigating multiple Enterprise Manager pages, you ask targeted questions in the chat window and use the results to identify drift, missing image subscriptions, patch recommendations, compliance gaps, and critical violations.

The prompts in these tasks are organized into two sections:
* **Steps 1–3:** Assess patching readiness before the patch window.
* **Steps 4–5:** Verify compliance after patching is complete.


1. Review **configuration drift**

    Configuration drift can indicate that a target no longer matches its approved configuration baseline. Review drift before patching so that you can resolve or document exceptions.

    In the **Oracle AI Database Assistant chat window, enter the following prompt and press Enter:**
    ```
    <copy>
    Show configuration drift results by target type
    </copy>
    ```

    ![Configuration Drift Question](ai-db-assistant-images/ai-db-assistant-dblm/configuration-drift-question.png " ")

    Review the results by target type.
    ![Configuration Drift Results](ai-db-assistant-images/ai-db-assistant-dblm/configuration-drift-results.png " ")

2. Check **database subscriptions to gold images**

    Databases must be subscribed to an appropriate gold image to participate in a standardized fleet maintenance patching process. Identify databases that are not subscribed and enroll them before patching.

    In the chat window, **enter the following prompt and press Enter:**
    ```
    <copy>
    Display databases not subscribed to gold image for patching
    </copy>
    ```

    ![Database subscriptions to the image question](ai-db-assistant-images/ai-db-assistant-dblm/db-subcription-question.png " ")

    Review the distribution of subscribed and unsubscribed databases.
    ![Database subscriptions to the image result](ai-db-assistant-images/ai-db-assistant-dblm/db-subcription-result.png " ")

3. Review **patch recommendations**

    Patch recommendations are grouped by classification to help you understand the type and scope of patches required across the database fleet.

    Use these recommendations to update the appropriate gold images. Create a new version of the gold image with the recommended patches so that it is ready for use during the patching cycle.

    In the chat window, **enter the following prompt and press Enter:**
    ```
    <copy>
    Display the distribution of patch recommendations
    </copy>
    ```

    ![Database patch recommendations](ai-db-assistant-images/ai-db-assistant-dblm/db-patchrecom-question.png " ")

    Review the distribution of patch recommendations by classification.

    ![Database subscriptions to the image question](ai-db-assistant-images/ai-db-assistant-dblm/db-patchrecom-result.png " ")

4. Review **database patch compliance** once the patching cycle completes

    Evaluate the fleet after patching to confirm how many databases are patch compliant.

    In the chat window, **enter the following prompt and press Enter:**
    ```
    <copy>
    Display the distribution of databases that are compliant
    </copy>
    ```
    ![Databases with latest patches](ai-db-assistant-images/ai-db-assistant-dblm/db-patchcomplianceqns.png " ")

    Review fleet-level view of database patch compliance.
    ![Compliance violations results](ai-db-assistant-images/ai-db-assistant-dblm/db-patchcomplianceresp.png " ")

5. Review **critical compliance violations**

    Review critical compliance violations after patching. These violations may identify databases or security controls that require remediation or an approved exception.
    
    In the chat window, **enter the following prompt and press Enter:**
    ```
    <copy>
    How many critical compliance violations exist?
    </copy>
    ```

    ![Compliance violations question](ai-db-assistant-images/ai-db-assistant-dblm/db-compliance-question.png " ")

    Review the number of critical violations and investigate the affected databases and controls.
    ![Compliance violations results](ai-db-assistant-images/ai-db-assistant-dblm/db-compliance-results.png " ")

## Learn More

  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Enterprise Manager 24ai Documentation Library](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/24.1/index.html)
  - [Enterprise Manager 24ai Tech Forum Video Playlist](https://www.youtube.com/playlist?list=PLiuPvpy8QsiXvGYMP_N3WA6bddXvUH-Y0)

## Acknowledgements
- **Author** - Sumesh Balakrishnan, Oracle Enterprise Manager Product Management
- **Contributing Author** - Ana McCollum, Anand Prabhu, Oracle Enterprise Manager Product Management