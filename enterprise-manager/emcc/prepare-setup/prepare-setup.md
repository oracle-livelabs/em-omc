# Prepare Setup

## Introduction
This lab will show you how to download the Oracle Resource Manager (ORM) stack zip file needed to setup the resource needed to run this workshop. This workshop requires a compute instance running the Oracle Enterprise Manager 13c Marketplace image with monitored database targets and a Virtual Cloud Network (VCN).

*Estimated Time:* 15 minutes

### Objectives
-   Download ORM stack
-   Configure an existing Virtual Cloud Network (VCN)

### Prerequisites
This lab assumes you have:
- An Oracle Free Tier or Paid Cloud account

## Task 1: Download Oracle Resource Manager (ORM) stack zip file
1.  Click on the link below to download the Resource Manager zip file you need to build your environment:

<if type="config-compliance">
    - [emcc-mkplc-config-compliance.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-config-compliance.zip)
</if>
<if type="devops-automation">
    - [emcc-mkplc-devops-automation.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-devops-automation.zip)
</if>
<if type="devops-patching">
    - [emcc-mkplc-devops-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/0kq1pND_WCBBYLXCDnpxD3iR-h1ZRo4pwEydk0g_IydMXOCenJZl65oFtsADn9_e/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-devops-patching.zip)
</if>
<if type="find-fix-validate">
    - [emcc-mkplc-find-fix-validate.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-find-fix-validate.zip)
</if>
<if type="fleet-patching">
    - [emcc-mkplc-fleet-patching.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-fleet-patching.zip)
</if>
<if type="fleet-patching-ui">
    - [emcc-mkplc-fleet-patching-ui.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-fleet-patching-ui.zip)
</if>
<if type="fleet-upgrade">
    - [emcc-mkplc-fleet-upgrade.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-fleet-upgrade.zip)
</if>
<if type="fleet-upgrade-ui">
    - [emcc-mkplc-fleet-upgrade-ui.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-fleet-upgrade-ui.zip)
</if>
<if type="fundamentals">
    - [emcc-mkplc-fundamentals.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-fundamentals.zip)
</if>
<if type="job-system-automation">
    - [emcc-mkplc-job-system-automation.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-job-system-automation.zip)
</if>
<if type="lifecycle">
    - [emcc-mkplc-lifecycle.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-lifecycle.zip)
</if>
<if type="migration-workbench">
    - [emcc-mkplc-migration-workbench.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-migration-workbench-v1.3.zip)
</if>
<if type="migration-workbench-adb">
    - [emcc-mkplc-migration-workbench-adb.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/zqv4ccIzpSf1XX2xm50vy6buPjOjKa-ABMWyuPeh96N7WIJWqx4wMAPSP-8UXt9e/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-migration-workbench-adb.zip)
</if>
<if type="monitoring-overview">
    - [emcc-mkplc-monitoring-overview.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-monitoring-overview.zip)
</if>
<if type="rat-overview">
    - [emcc-mkplc-rat-overview.zip](https://c4u04.objectstorage.us-ashburn-1.oci.customer-oci.com/p/EcTjWk2IuZPZeNnD_fYMcgUhdNDIDA6rt9gaFj_WZMiL7VvxPBNMY60837hu5hga/n/c4u04/b/livelabsfiles/o/em-omc/emcc-mkplc-rat-overview.zip)
</if>
<if type="hybrid-pdbaas">
    - [emcc-mkplc-hybrid-pdbaas.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/-JqErQC8a-AiGJnd9ICNRE9dy8AiA-GEjYLAZEffy9qlGQMl0dOq34LPDhsVy_XS/n/omcinternal/b/EMWorkshopBucket/o/emcc-mkplc-hybrid-pdbaas.zip)
</if>


2.  Save in your downloads folder.

We strongly recommend using this stack to create a self-contained/dedicated VCN with your instance(s). Skip to *Task 3* to follow our recommendations. If you would rather use an existing VCN then proceed to the next task to update your existing VCN with the required Ingress rules.

## Task 2: Adding security rules to an existing VCN

This workshop requires a certain number of ports to be available, a requirement that can be met by using the default ORM stack execution that creates a dedicated VCN. In order to use an existing VCN/subnet, the following rules should be added to the security list.

### **(1) Ingress Rules**

| Stateless         | Source Type | Source CIDR | IP Protocol | Source Port Range | Destination Port Range | Description                |
| :---------------- | :---------: | :---------: | :---------: | :---------------: | :--------------------: | :------------------------- |
| False (unchecked) |    CIDR     |  0.0.0.0/0  |     TCP     |        All        |           22           | SSH                        |
| False (unchecked) |    CIDR     |  0.0.0.0/0  |     TCP     |        All        |           80           | Remote Desktop using noVNC |
{: title="List of Required Network Security Rules (Ingress)"}

<!-- **Notes**: This next table is for reference and should be adapted for the workshop. If optional rules are needed as shown in the example below, then uncomment it and add those optional rules. The first entry is just for illustration and may not fit your workshop -->

| Stateless         | Source Type | Source CIDR | IP Protocol | Source Port Range | Destination Port Range | Description                           |
| :---------------- | :---------- | :---------: | :---------: | :---------------: | :--------------------: | :------------------------------------ |
| False (unchecked) | CIDR        |  0.0.0.0/0  |     TCP     |        All        |          7803          | e.g. Remote access for web EM Console |
{: title="List of Optional Network Security Rules (Ingress)"}

1.  Go to *Networking >> Virtual Cloud Networks*
2.  Choose your network
3.  Under Resources, select Security Lists
4.  Click on Default Security Lists under the Create Security List button
5.  Click *Add Ingress Rules* button
6.  Create a rule for each entry in the *Ingress* table(s) above.  
    - Stateless: Leave unchecked (Default)
    - Source Type: CIDR
    - Source CIDR: 0.0.0.0/0
    - IP Protocol: TCP
    - Source Port Range: All (Keep Default)
    - Destination Port Range: *Select from the above table(s)*
    - Description: *Select the corresponding description from the above table(s)*
7. Click *+Another Ingress Rule* and repeat step [6] until a rule is created for each port listed in the *Ingress* tables
8.  Click the Add Ingress Rules button

### **(2) Egress Rules**

| Stateless         | Source Type | Destination CIDR | IP Protocol | Source Port Range | Destination Port Range | Description           |
| :---------------- | :---------: | :--------------: | :---------: | :---------------: | :--------------------: | :-------------------- |
| False (unchecked) |    CIDR     |    0.0.0.0/0     |     TCP     |        All        |           80           | Outbound HTTP access  |
| False (unchecked) |    CIDR     |    0.0.0.0/0     |     TCP     |        All        |          443           | Outbound HTTPS access |
{: title="List of Required Network Security Rules (Egress)"}

<!-- **Notes**: This next table is for reference and should be adapted for the workshop. If optional rules are needed as shown in the example below, then uncomment it and add those optional rules. The first entry is just for illustration and may not fit your workshop -->

<!--
| Stateless         | Source Type | Destination CIDR | IP Protocol | Source Port Range | Destination Port Range | Description                                        |
| :---------------- | :---------- | :--------------: | :---------: | :---------------: | :--------------------: | :------------------------------------------------- |
| False (unchecked) | CIDR        |    0.0.0.0/0     |     TCP     |        All        |          1521          | e.g. Remote oracle DB Listener anywhere            |
| False (unchecked) | CIDR        | 130.129.10.45/32 |     TCP     |        All        |          1525          | e.g. Remote oracle DB Listener at IP 130.129.10.45 |
{: title="List of Optional Network Security Rules (Egress)"}
-->

1.  Select *Egress Rule* from the left pannel
2.  Click Add Egress Rule button
3.  Create a rule for each entry in the *Egress* table(s) above:  
    - Stateless: Leave unchecked (Default)
    - Source Type: CIDR
    - Destination CIDR: 0.0.0.0/0
    - IP Protocol: TCP
    - Source Port Range: All (Keep Default)
    - Destination Port Range: *Select from the above table(s)*
    - Description: *Select the corresponding description from the above table(s)*
4. Click *+Another Egress Rule* and repeat step [3] until a rule is created for each port listed in the *Egress* tables
5.  Click the Add Egress Rules button

## Task 3: Setup Compute   
Using the details from the two Tasks above, proceed to the lab *Environment Setup* to set up your workshop environment using Oracle Resource Manager (ORM) and one of the following options:
-  Create Stack:  *Compute + Networking*
-  Create Stack:  *Compute only* with an existing VCN where security lists have been updated as per *Task 2* above

You may now proceed to the next lab.

## Acknowledgements
* **Author** - Rene Fontcha, LiveLabs Platform Lead, NA Technology
* **Contributors** - 
* **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, January 2023
