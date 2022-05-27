# Introduction

## About this Workshop
This goal of this workshop is to become familiar with Enterprise Monitoring capabilities using Oracle Enterprise Manager Cloud Control 13c.

*Estimated Workshop Time*: 70 minutes

### About Oracle Enterprise Manager
Oracle Enterprise Manager is Oracle’s on-premise management platform that provides a single dashboard to manage all of your Oracle deployments, in your data center or in the cloud. Through deep integration with Oracle’s product stack, it provides market-leading management and automation support for Oracle applications, databases, middleware, hardware, and engineered systems

Join Oracle's ***Wim Coekaerts***, *senior vice president of software development*, as he describes key innovations delivered in Oracle Enterprise Manager to help customers easily migrate their databases to the cloud and simplify management of hybrid IT environments

[](youtube:MZJQx6MuHA0)

### Objectives
In this workshop, you will learn how to use:
- Enterprise Summary
- Incident Manager
- Metric and Collection Settings
- Corrective Actions
- Metric Extensions
- Monitoring Templates
- Administration Groups and Template Collections
- Incident Rules

## Summary
Oracle Enterprise Manager enables you to get complete monitoring visibility into your IT infrastructure, applications stack and applications that are critical to running your business.

- Single pane of glass monitoring for on-premises, hybrid, and Oracle Cloud Platform

- Comprehensive set of predefined performance and health metrics that enables lights-out monitoring of critical components in your environment, such as applications, application servers, databases, as well as the back-end components on which they rely, such as hosts and storage.

- Rich set of alerting, incident management and notification capabilities to notify IT staff and integrate with your corporate ticketing systems.

- Corrective Actions to auto-correct alerts and minimize service disruption

- Metric Extensions to monitor conditions specific to your environment

#### Applicable Enterprise Manager Management Packs
Labs under this workshop do not need any additional Management Pack and are a core functionality of the Enterprise Manager.

### Content
The following are covered in this workshop:
- Explore Enterprise Summary page and drill down to see a list of down targets
- Triage unassigned incidents from Incident Manager and acknowledge then assign an incident
- Change the Warning and Critical threshold of a metric from Metric and Collection Settings page. Go to the All Metrics page and review the metric in context of the thresholds
- Create a new Corrective Action and associate it with a metric
- Test a Metric Extension on a target to see the results then deploy the same Metric Extension to multiple targets
- Create a Monitoring Template from a Database Instance target and deploy the Monitoring Template to other Database Instance targets to standardize monitoring settings across the enterprise
- View the hierarchy of an existing Administrator Group
- Review out-of-the-box incident rules shipped with Enterprise Manager


### Additional Workshop Supported Use Cases

For additional Enterprise Manager use cases, see below and visit [LiveLabs](http://bit.ly/golivelabs) for the details.
#### 1. Database Lifecycle Automation
-	Create a Pluggable Database (PDB)
-	Un-plug/Plug an existing Pluggable Database
-	Clone an existing Pluggable Database
-	Run Compliance Management for Pluggable Database
-	Self- service to request a PDB using PDBaaS
-	Administrative Setup for PDBaaS (Private Cloud)- Review only

#### 2. Find, Fix, Validate
- View unified Database Performance via Performance Hub
- Use Real-time Database Operations Monitoring to view long running database tasks
- Identify Top SQL in a PDB and tune it using SQL Tuning Advisor
- Use SQL Performance Analyzer Optimizer to gather statistics for validation
- Use Database Workload Replay to run real workload against your changes for additional validation

#### 3. Database Fleet Maintenance - Patching
* Detect Configuration Pollution
* Patch a Database target using a Gold Image
    - All Pluggable Databases in that Container Database will automatically get patched
    - Rollback and Cleanup

#### 4. Database Fleet Maintenance - Upgrade
* Detect Configuration Pollution
* Upgrade Oracle DB Software at scale with minimal downtime
    - All Pluggable Databases in that Container Database will automatically get upgraded
    - Cleanup

#### 5. Compliance and Drift Management
- Analyze, Increase standardization, reduce number of different configuration sets
- Execute a one-time comparison to compare the latest reference configuration to one or more targets to determine the configuration differences
- Continuous drift monitoring of multiple targets against a reference target for initialization parameters using customized configuration monitoring template
- Run a review aggregated security compliance framework and standard for Oracle Database 12c and Oracle Host targets
- Host security compliance using custom compliance standard

#### 6. Job System Automation
* Understand how to create an OS Command Job
* Create a SQL command Job
* Create Database Backup Job using Wizard

#### 7. Real Application Testing
* Run SQL Performance Analyzer to review SQL performance before 19c Upgrade
* Capture workload of 18c Database
* Run Database Replay of 18c Database Workload in 19c Database
* Run Consolidation Replay in 2 separate Pluggable Databases

#### 8. Deploy and Manage Oracle Databases with Ansible and Enterprise Manager
- Install and configure Ansible to work with Oracle Enterprise Manager 13c
- Review Oracle Enterprise Manager DBaaS setup for Pluggable Databases
- Provision, resize, shutdown, start and delete a Pluggable Database using Ansible playbooks and EM's DBaaS capabilities

## More Information on Oracle Enterprise Manager
Managing Your Hybrid Database Fleet
[](youtube:TUaAweMX3S4)

Drive Your Autonomous Future with Oracle Enterprise Manager
[](youtube:7khTglg0_3g)

- [Enterprise Manager Cloud Control Solutions](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/emcon/enterprise-manager-management-focus-areas.html#GUID-7F3BF18C-97DF-44BC-8BB7-6A864AF1A150)
- [Enterprise Manager Cloud Control 13.4 Getting Started](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/index.html)
- [Architecture of Enterprise Manager Cloud Control](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/emcon/enterprise-manager-cloud-control-architecture.html#GUID-1A384373-7CD5-434D-9939-874E940CBF21)
- [Installation and Upgrade](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/install.html)
- [Enterprise Manager Blogs](https://blogs.oracle.com/oem/)
- [Enterprise Manager Videos](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.4/videos.html)
- [Enterprise Manager Licensing Guide](https://docs.oracle.com/cd/E63000_01/OEMLI/introduction.htm#OEMLI108)
- [oracle.com/enterprisemanager](https://www.oracle.com/enterprise-manager/)

## Acknowledgements
- **Author** - Rene Fontcha, Master Principal Solutions Architect, NA Technology
- **Contributors** - Dave Le Roy, Björn Bolltoft - Enterprise Manager Product Management
- **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, February 2022
