# Lab 3 - Monitor individual components

## Introduction

In this lab, you will explore the various dashboards available in Oracle for monitoring Fusion Applications, Oracle Integration Cloud (OIC), and Oracle Database (DB). These dashboards offer a unified and centralized view of log data, allowing users to efficiently monitor system health, analyze performance, and troubleshoot issues across Fusion Applications, OIC integrations, and database instances.

Estimated Time: 5 minutes

### Objectives
In this lab, you will get an overview of the different dashboards, including their usage and the various widgets provided within each dashboard.

## Task 1: Dashboard Navigation
- To navigate to the Dashboards page use one of the following method.
    From Navigation Menu ![navigation-menu](images/navigation-menu.jpg) > **Observability & Management** > **Management Dashboard** > **Dashboards**.
     
    OR
    
    You can use the direct link to land on the **Dashboards** page.
    ```
         <copy>
            https://cloud.oracle.com/management-dashboard/dashboards?region=us-phoenix-1
         </copy>   
    ```
 -  Dashboards page will be displayed.
      ![dashboards-home](images/dashboards-home.jpg) 

    > **Note** : You will see an authorization error. It is expected as current user doesn't have permission to the root compartment.

 -  Switch to the compartment **AIW25\_Logging\_Analytics**.
    - From the **Compartment** dropdown select the compartment **AIW25\_Logging\_Analytics**.
    - From the **Services** dropdown select the service **Log Analytics**.
    - All the Dashboards in the Compartment **AIW25\_Logging\_Analytics** will be displayed.
      
   ![all-dashboards](images/all-dashboards.jpg)

## Task 2: Overview of Oracle Integration Insight dashboard
  
| Component | Observability Log Source | Functional Components | Upstream and Downstream Systems | Ingestion method | 
|-----------|-----------|-----------------|-------------------|
| **Oracle Integration Cloud** | OIC Activity Stream Logs | integration execution, B2B processing | SaaS ERP Cloud, ADW, APEX | Service Logs via Service Connector |

-  **Oracle Integration Insight**  dashboard provides real-time business monitoring by linking technical integrations to business processes and KPIs. The dashboard enables business users, analysts, and IT teams to visualize the progress, performance, and bottlenecks in their business operations. It consists of different widgets like Summary widget, Milestone progress widget, Transction Performance widget , Transaction Tracking Fields widget etc. 

- In order to view this dashboard one has to search for and click on the **Oracle Integration Insight** dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load.![dashboards-oic-insight](images/dashboards-oic-insight.jpg)
	> **Important tip** : Observe the dashboard widgets & values once they are loaded.
	![oic-insight-dashboard](images/logan-ll-oic-insight-dashboard.jpg)

- **Oracle Integration: Health Overview** dashboard provides an overview of the monitored OIC instances, integrations, and their health based on the metrics and logs. This dashboard is used to gain insights into the current health of your OIC Instances, Integrations, and Flow Instances. Filters can be used to narrow down to a specific OIC Instance, Integration, and Integration Instance. It displays both metrics and log data at the compartment level. 

- In order to view this dashboard one has to search for and click on the **Oracle Integration: Health Overview** from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. ![dashboards-oic-health](images/dashboards-oic-health.jpg)
	> **Important tip** : Observe the dashboard widgets & values once they are loaded.
	![oic-health-dashboard](images/oic-health-dashboard.jpg)

## Task 3: Overview of Oracle Fusion User Access and Audit Dashboard

| Component | Observability Log Source | Functional Components | Upstream and Downstream Systems | Ingestion method | 
|-----------|-----------|-----------------|-------------------|
| **Oracle SaaS Fusion Apps** | Fusion Audit Logs, User Activity, ESS job requests | ESS Audit, User Activity Audit, Fusion Audit, ESS job requests, Business Objects Audit | OIC via REST/SOAP | Fusion REST API endpoints based log ingestion via Management Agent| 

**Oracle Fusion User Access** dashboard provides comprehensive visibility into user authentication and access patterns within Oracle Fusion Applications. This dashboard tracks sign-in and sign-out activities of Fusion users, allowing administrators and security teams to monitor who is accessing the system, when, and from where. 

- In order to view this dashboard one has to search for and click on the **Oracle Fusion User Access** dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. ![dashboards-fusion-user-access](images/dashboards-fusion-user-access.jpg)
      > **Important tip** : Observe the dashboard widgets & values once they are loaded.
      ![db-fusion-user-access-dashboard](images/logan-ll-fusion-user-access-1.png)
	  ![db-fusion-user-access-dashboard](images/logan-ll-fusion-user-access-2.png)   

**Oracle Fusion Apps: OPSS Audit Analysis** dashboard leverages OPSS audit logs to provide comprehensive visibility into authentication and access events within Oracle Fusion Applications. By analyzing OPSS audit logs, this dashboard allows administrators and security teams to track new user creation and role assignment, monitor security-related operations, and identify when and where users accessed the system. The insights derived from OPSS audit logs help ensure compliance, detect suspicious access patterns, and enhance overall security monitoring.

- In order to view this dashboard one has to search for and click on the **Oracle Fusion Apps: OPSS Audit Analysis** dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. ![dashboards-fusion-opss-access](images/logan-ll-dashboards-fusion-opss-access.png)
      > **Important tip** : Observe the dashboard widgets & values once they are loaded.
      ![db-fusion-opss-dashboard](images/logan-ll-fusion-opss.png)

## Task 4: Overview of Oracle Fusion Apps Enterprise Scheduler Service (ESS) Monitoring dashboard

**Oracle Fusion Apps Enterprise Scheduler Service (ESS) Analysis** dashboard provides deep visibility into the execution and status of ESS job requests within Oracle Fusion Applications. By collecting and analyzing ESS logs using OCI Logging Analytics, this dashboard enables you to monitor job execution trends, identify failed or long-running jobs, and troubleshoot scheduling issues. The dashboard leverages log ingestion via the OCI Logging Analytics REST API, offering actionable insights into job request patterns, error rates, and operational bottlenecks. For more details on how ESS logs are collected and analyzed.

- In order to view this dashboard one has to search for and click on the **Oracle Fusion Apps Enterprise Scheduler Service (ESS) Analysis**  dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. ![dashboards-fusion-enterprise](images/dashboards-fusion-enterprise.jpg)
      > **Important tip** : Observe the dashboard widgets & values once they are loaded.
      ![fusion-enterprise-dashboard](images/logan-ll-fusion-enterprise-dashboard.png)

## Task 5: Overview of the Oracle APEX Application dashboard

| Component | Observability Log Source | Functional Components | Upstream and Downstream Systems | Ingestion method | 
|-----------|-----------|-----------------|-------------------|
| **Oracle APEX Application** | User Activity, Application Usage, Error Logs | User Success and Failed Logins, Application and User Activity, Application Errors | ADW, OIC | Database connector based log ingestion via Management Agent |

- **Oracle APEX Application** dashboard provides an overview of the monitored APEX Application, including user activity, application usage, and error logs. This dashboard is used to gain insights into the current health of your APEX Application.
- In order to view this dashboard one has to search for and click on the **APEX User Activity** dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. Time range is set to **Last 7 days**. ![apex-user-activity-access](images/logan-ll-apex-user-activity-access.png)
      > **Important tip** : Observe the dashboard widgets & values once they are loaded.
	![apex-application-dashboard](images/logan-ll-apex-user-activity-dashboard-1.png)
      ![apex-application-dashboard-continued](images/logan-ll-apex-user-activity-dashboard-2.png)

## Task 6: Overview of Oracle Database Audit Analysis dashboard

| Component | Observability Log Source | Functional Components | Upstream and Downstream Systems | Ingestion method | 
|-----------|-----------|-----------------|-------------------|
| **Oracle Autonomous Data Warehouse** | Business data in table/view, Database Audit Logs | Data persistence, analytics queries, access patterns | OIC, APEX | Database SQL connector based log ingestion via Management Agent |

- **Oracle Database Audit Analysis** dashboard provides analysis of audited actions for Oracle Databases monitored by Log Analytics using Unified Database Audit Logs available in DB v12.2 onwards. This dashboard is used to understand user activity, schema changes etc.

- In order to view this dashboard one has to search for and click on the **Oracle Database Audit Analysis** dashboard from the  **Dashboard** home page. It will take few seconds for the dashboard widgets to load. ![dashboards-db-audit](images/dashboards-db-audit.jpg)
      > **Important tip** : Observe the dashboard widgets & values once they are loaded.
      ![db-audit-dashboard](images/logan-ll-db-audit.png)

**Congratulations!** In this lab, you have successfuly completed the following tasks:
- Monitoring different dashboards

## Learn More

* [Fusion Apps Observability by Collecting ESS Logs Using OCI Logging Analytics REST API Ingestion](https://www.ateam-oracle.com/post/fusion-apps-observability-by-collecting-ess-logs-using-oci-logging-analytics-rest-api-ingestion)
* [Oracle Integration Insight Dashboard](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-integration-insight-dashboard.html)
* [Oracle Integration: Health Overview Dashboard](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-integration-health-overview-dashboard.html)
* [Oracle Database Audit Analysis Dashboard](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-database-audit-analysis-dashboard.html)
* [Oracle Fusion User Access Dashboard](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-fusion-user-access-dashboard.html)
* [Oracle Fusion Apps Enterprise Scheduler Service (ESS) Analysis Dashboard](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/oracle-fusion-apps-enterprise-scheduler-service-ess-analysis-dashboard.html)


You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Supriya Joshi, OCI Log Analytics, Royce Fu, Master Principal Cloud Architect, Kumar Varun, Log Analytics Product Management
* **Contributors** -  Supriya Joshi, Jolly Kundu, Kumar Varun, Royce Fu
* **Last Updated By/Date** - Royce Fu, Sep, 2025
