# Introduction

## About this Workshop

In this hands-on workshop, we will delve into the setup and configuration of observability and management tools specifically tailored for Oracle Database@Azure.

Oracle Database@Azure offers the best of both worlds: the renowned OCI services, with their exceptional performance, security, and availability, seamlessly integrated with Azure's native customer experience and infrastructure. By hosting Oracle's services within Azure data centers, direct private network connectivity is established, ensuring secure and efficient data management.

Throughout this workshop, you will gain practical experience in utilizing OCI Database Management Service and OCI Ops Insights, as well as exploring Azure's own monitoring tools. We will guide you through the essential prerequisites and preparations needed to create an Oracle Exadata infrastructure and an Oracle Exadata VM Cluster, setting the stage for the creation of CDBs and PDBs.

Get ready to enhance your cloud database management skills and discover the seamless integration of Oracle and Azure through this comprehensive LiveLab experience.

Estimated Workshop Time: 3 Hours 30 Minutes

## About Oracle Cloud Infrastructure Database Management (OCI Database Management)

As a DevOps user or Database Administrator, you can use the OCI Database Management service to monitor and manage your Oracle Databases. The Database Management service supports Oracle Databases located on-premises and connected to a resource in the Oracle Cloud Infrastructure External Database service (referred to as External Oracle Databases). Database Management service also supports Oracle Autonomous Databases and Oracle Cloud Databases, which are Oracle Databases on the following Co-managed Oracle Database Cloud solutions:
- Bare Metal and Virtual Machine DB Systems
- Exadata Cloud Service

Database Management supports Oracle Database versions 11.2.0.4 and later. Using the Database Management service you can:

- Monitor the key performance and configuration metrics of all your Oracle Databases together (Fleet of databases).
- You can compare and analyze database metrics over a selected period.
- Group your most important or production Oracle Databases together, or group together databases that reside across compartments into a Database Group, and monitor them.
- Create SQL jobs to perform administrative operations on a single Oracle Database or a Database Group.

## About Ops Insights

Oracle Cloud Infrastructure Ops Insights is an Oracle Cloud Infrastructure (OCI) native service that provides holistic insight into database and host resource utilization and capacity.  Ops Insights (OPSI) provides capacity planning, long-term SQL analysis, and historical performance reports for your Oracle databases. The service has a full offering of features to improve performance and reduce overhead for your resources. The ability to quickly and easily ingest valuable metric data allows administrators, engineers, and executives to make informed decisions on allocating resources to prevent major issues and reduce overhead for managing their infrastructure resources.

Oracle Cloud Infrastructure (OCI) Ops Insights enables administrators to uncover performance issues, forecast consumption, and plan capacity using machine-learning-based analytics on historical and SQL data. Organizations can use these capabilities to make data-driven decisions to optimize resource use, proactively avoid outages, and improve performance.

Ops Insights can help you better manage the Oracle Database@Azure environment: 

Capacity Planning

- Utilization, analysis and forecasting for database and host resources.
- Analyze and forecast resource usage based on long-term historical data.
- Optimize cost of operations by identifying under and overutilized databases and hosts.

Exadata Insights

- Enterprise-wide analysis of resource utilization, capacity planning for Exadata.
- Improve resource utilization by identifying under and overutilized resources.
- Identify Exadata systems projected to reach high utilization.

SQL Insights

- Long-term SQL store for performance and trend analysis of Oracle Databases.
- Proactively identify and mitigate SQL issues.
- Find common patterns in SQL behaviour across databases and applications.

## Workshop Objectives

In this workshop, you will learn how to:
- Step 1. Explore and understand the limitation of the Oracle Database@Azure Monitoring in Azure Cloud
- Step 2. Enable the Database Management service for Oracle Database@Azure Autonomous Database and Exadata Dedicated Infrastructure Container/Pluggable Database.
- Step 3. Monitor the key performance metrics and explore the database administration options of your fleet of Oracle Database@Azure.
- Step 4. Enable the Ops Insights service for Oracle Database@Azure Autonomous Database and Exadata Dedicated Infrastructure Container/Pluggable Database.
- Step 5. Gain Capacity Planning insights across a fleet of databases in Oracle Database@Azure
- Step 6. Analyze SQL Performance at Fleet level and proactively identify SQLs Degrading performance.

## Prerequisites

- An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account
- Familiarity with Oracle Cloud Infrastructure (OCI) is helpful
- Basic knowledge about DB @Azure concepts is helpful
- Familiarity with Oracle Exadata Database is helpful


## Learn More
- You can find more information about Oracle Exadata Database @Azure [here](https://docs.oracle.com/en-us/iaas/Content/multicloud/oaa.htm)
- [Oracle Cloud Infrastructure Database Management]( https://www.oracle.com/manageability/database-management/)
- [Ops Insights]( https://www.oracle.com/manageability/operations-insights/)


## Technical support

For all OCI related issues, Oracle Cloud Support is the first line of support. For any technical issues related to Oracle Exadata Database @Azure, please sign in to the OCI Console, then click the life raft icon.

For all Azure related issues and questions. Get help in the **Help + support** section of the Azure portal.

## Acknowledgements

- **Author** - Royce Fu, Master Principal Cloud Architect, North America Cloud Infrastructure and Engineering
- **Contributors** -  Derik Harlow, Murtaza Husain, Sriram Vrinda
- **Last Updated By/Date** - Royce Fu, January 2025
