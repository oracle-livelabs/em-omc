# Introduction

## About this Workshop

The Database Migration Workbench workshop is a fully functional Oracle Enterprise Manager environment configured to run predefined use cases against multiple Oracle Database targets:

- It is intended to familiarize you with Database Migration Workbench which can be invaluable in your journey to 19c and multitenant
- The Workshop VM comes preinstalled with Enterprise Manager 13.5 RU7 and Oracle Database targets 12.2 and 19.12
- It's easy and quick to deploy with everything starting automatically in under 20 minutes

Estimated Time: 60 minutes

### Objectives

In this workshop, you will learn how to:

- Migrate and upgrade a 12c non-container database to autonomous database in Oracle Cloud Infrastructure

### About Migration Workbench

Oracle Enterprise Manager Database Migration Workbench provides an accurate approach to migration and consolidation by eliminating human errors allowing you to easily move your on-premises databases to Oracle Cloud, Multitenant architecture, or upgrade your infrastructure. Advantages of using Database Migration Workbench include: Near-Zero Downtime, Assured Zero Data Loss, seamless on-premises or Cloud migrations, and, MAA and Cloud Security compliant.

- _Analyze Migration Activities:_ Database Migration Workbench offers robust tools for monitoring and troubleshooting your recently completed migrations. Database Migration Workbench also offers clean-up tools that aid in recovering important disk space from dump files. This lab covers both of these features

- _Analyze Migrated Database Performance:_ Migrating a database can change the execution plans of SQL statements, possibly resulting in performance degradation. Database Migration Workbench is integrated with [SQL Performance Analyzer (SPA)] (<https://docs.oracle.com/en/database/oracle/oracle-database/19/ratug/sql-performance-analyzer.html>) which can help you identify and correct performance related issues. This lab uses SPA to compare the performance of the database before and after the migration

- _Security Compliance:_ Since Database Migration Workbench is a component of Oracle Enterprise Manager, your migrated databases are automatically added/updated in Enterprise Manager. You can utilize the [Compliance Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emlcm/manage-compliance.html) feature in Enterprise Manager to improve your database fleet security posture. Enterprise Manager Compliance Management leverages industry/regulatory standards for secure configuration such as CIS Benchmark, DISA STIG, and Oracle Security Best Practices

### Applicable Enterprise Manager Management Packs

Labs under this workshop are covered by the following Management Packs:

- Migration Workbench and SQL Performance Analyzer are licensed under Real Application Testing (RAT) Management Pack
- Compliance Management is licensed under the Database Lifecycle Management Pack (DBLM)

### About Oracle Enterprise Manager

Oracle Enterprise Manager is Oracle’s on-premise management platform that provides a single dashboard to manage all of your Oracle deployments, in your data center or in the cloud. Through deep integration with Oracle’s product stack, it provides market-leading management and automation support for Oracle applications, databases, middleware, hardware, and engineered systems

Join Oracle's ***Wim Coekaerts***, *senior vice president of software development*, as he describes key innovations delivered in Oracle Enterprise Manager to help customers easily migrate their databases to the cloud and simplify management of hybrid IT environments

[](youtube:MZJQx6MuHA0)

### Other Enterprise Manager workshops on LiveLabs

Additional Enterprise Manager workshops are available on [Oracle LiveLabs](http://bit.ly/golivelabs).

## Learn More

Managing Your Hybrid Database Fleet
[](youtube:TUaAweMX3S4)

Drive Your Autonomous Future with Oracle Enterprise Manager
[](youtube:7khTglg0_3g)

- [Enterprise Manager Cloud Control Solutions](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emcon/enterprise-manager-management-focus-areas.html#GUID-7F3BF18C-97DF-44BC-8BB7-6A864AF1A150)
- [Enterprise Manager Cloud Control 13.5 Getting Started](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/index.html)
- [Architecture of Enterprise Manager Cloud Control](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emcon/enterprise-manager-cloud-control-architecture.html#GUID-1A384373-7CD5-434D-9939-874E940CBF21)
- [Installation and Upgrade](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/install.html)
- [Enterprise Manager Blogs](https://blogs.oracle.com/oem/)
- [Enterprise Manager Videos](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/videos.html)
- [Enterprise Manager Licensing Guide](https://www.oracle.com/pls/topic/lookup?ctx=en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5&id=OEMLI-GUID-7B2095D3-4E88-4346-9566-638219FF1130)
- [oracle.com/enterprisemanager](https://www.oracle.com/enterprise-manager/)
- [Database Migration Workbench Guide](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emmwb/index.html)

## Acknowledgements

- **Authors** - Rene Fontcha, Master Principal Solutions Architect, NA Technology, Amine Tarhini, Systems Management Specialist, Oracle Platform Solution Engineering
- **Contributors** - Dave Le Roy, Harish Niddagatta - Enterprise Manager Product Management
- **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, February 2022
