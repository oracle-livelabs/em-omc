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
    - [emcc-mkplc-config-compliance.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/bitQwycuNAjsM8n7C1ugjbrsRUuceS2TWkfARO3xf-sUX11EsaEg2ug_iLBPCeKF/n/natdsecurity/b/stack/o/emcc-mkplc-config-compliance.zip)
</if>
<if type="devops-automation">
    - [emcc-mkplc-devops-automation.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/BxNLU4NQeb7Y1_j3beNyqJx5Yf4ZosZS16cgdr_ClnhHS_S9vDZwLWCK7dE8uPlZ/n/natdsecurity/b/stack/o/emcc-mkplc-devops-automation.zip)
</if>
<if type="devops-patching">
    - [emcc-mkplc-devops-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/jWhIypO2ggUpXPmYguVGVT5mS2O2MhV1wU6Xce3i6-WTib12dO8sEu1IP4iLOckQ/n/natdsecurity/b/stack/o/emcc-mkplc-devops-patching.zip)
</if>
<if type="find-fix-validate">
    - [emcc-mkplc-find-fix-validate.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/e8Kxwmy0-2vSr9xL5je98lkZ-D4AbwsUl28tMDM-rSVex5FqJ1wAkx3Z4uFUv6Zv/n/natdsecurity/b/stack/o/emcc-mkplc-find-fix-validate.zip)
</if>
<if type="fleet-patching">
    - [emcc-mkplc-fleet-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/xyTG8q5fsPm229Z_U79K_B0LBVsvkoDzbhTtCsBz81En5Cywa_oKfqdldaBM7w4s/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-patching.zip)
</if>
<if type="fleet-patching-ui">
    - [emcc-mkplc-fleet-patching-ui.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/DHOkdjs81xqiB0Mf0K41Wd2IJ-b57rZ7Y_UTgRluPK5mKhoG6LIqk35YpieAExUJ/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-patching-ui.zip)
</if>
<if type="fleet-upgrade">
    - [emcc-mkplc-fleet-upgrade.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/kCQ0PJKMtZV-GWdi_iUbZ17CFbna4BGlIW5Q2ge5hzSJOyi6FkuqKXoN0NA2BQnf/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-upgrade.zip)
</if>
<if type="fleet-upgrade-ui">
    - [emcc-mkplc-fleet-upgrade-ui.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/rfjx3xAgK_IoKEo243_VrNSQTRjZF-WiqaT1jNXyECQwOM7m8pqH7O-5PXavM5i2/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-upgrade-ui.zip)
</if>
<if type="fundamentals">
    - [emcc-mkplc-fundamentals.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/QoRUvKiBlbpcynvexte9UE76FQOVd42HzF8ec2T70wNFjFkdlEwMMp4kDUIKxVxF/n/natdsecurity/b/stack/o/emcc-mkplc-fundamentals.zip)
</if>
<if type="job-system-automation">
    - [emcc-mkplc-job-system-automation.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/kJkOSpPDsfVDdbfMYOYZC3vAfjkZz1OKkaThBZcL4Myzxz6tbvVLGSF88nODa-nZ/n/natdsecurity/b/stack/o/emcc-mkplc-job-system-automation.zip)
</if>
<if type="lifecycle">
    - [emcc-mkplc-lifecycle.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/2Yl1NWUCGCOuI4zbDcg7VF46DJXaGo_ZNUd3C0cE8TNRuJe3-lkYe4Ll806eIzbd/n/natdsecurity/b/stack/o/emcc-mkplc-lifecycle.zip)
</if>
<if type="migration-workbench">
    - [emcc-mkplc-migration-workbench.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/Q6veHpp9MXq--zR-YNkyRZHsUe1hww9cYdV2u9Ucc-K1loj_iWcSmpIbuUaFhM3k/n/natdsecurity/b/stack/o/emcc-mkplc-migration-workbench.zip)
</if>
<if type="migration-workbench-adb">
    - [emcc-mkplc-migration-workbench-adb.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/iG4N8I6m7YWxlMoNbbu30t66Iyc94B_lZKeVeitGRc4ZNZYk61Srv84xPTpxcttp/n/natdsecurity/b/stack/o/emcc-mkplc-migration-workbench-adb.zip)
</if>
<if type="monitoring-overview">
    - [emcc-mkplc-monitoring-overview.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/64Q5ADtxQEomxRjI2HmRirUwFOqa1SJoplWLiwEhIrIoR83nvlgzRhN6AI19wGPU/n/natdsecurity/b/stack/o/emcc-mkplc-monitoring-overview.zip)
</if>
<if type="rat-overview">
    - [emcc-mkplc-rat-overview.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/SKVYcQm9QiL9ifHuVDbgdJ51s57zUy9VnF3YwXUPRaellpLxuU-IbtHmAZIEYtL8/n/natdsecurity/b/stack/o/emcc-mkplc-rat-overview.zip)
</if>

2.  Save in your downloads folder.

We strongly recommend using this stack to create a self-contained/dedicated VCN with your instance(s). Skip to *Task 3* to follow our recommendations. If you would rather use an existing VCN then proceed to the next task to update your existing VCN with the required Ingress rules.

## Task 2: Adding security rules to an existing VCN

This workshop requires a certain number of ports to be available, a requirement that can be met by using the default ORM stack execution that creates a dedicated VCN. In order to use an existing VCN/subnet, the following rules should be added to the security list.

### **(1) Ingress Rules**

|Stateless          |Source Type	|Source CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                |
| :-----------      |  :--------:   |  :--------:   | :----------:  | :------------:    | :-----------------:   | :------------------------ |
|False (unchecked)  |CIDR           |0.0.0.0/0      |TCP            |All                |22                     |SSH                        |
|False (unchecked)  |CIDR           |0.0.0.0/0      |TCP            |All                |80                     |Remote Desktop using noVNC |
{: title="List of Required Network Security Rules (Ingress)"}

<!-- **Notes**: This next table is for reference and should be adapted for the workshop. If optional rules are needed as shown in the example below, then uncomment it and add those optional rules. The first entry is just for illustration and may not fit your workshop -->

|Stateless          |Source Type	|Source CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                            |
| :-----------      |:-----------   |  :--------:   | :----------:  | :------------:    | :-----------------:   | :------------------------             |
|False (unchecked)  |CIDR           |0.0.0.0/0      |TCP            |All                |7803                   |e.g. Remote access for web EM Console  |
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

|Stateless          |Source Type	|Destination CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                |
| :-----------      |  :--------:   |  :--------:       | :----------:  | :------------:    | :-----------------:   | :------------------------ |
|False (unchecked)  |CIDR           |0.0.0.0/0          |TCP            |All                |80                     |Outbound HTTP access       |
|False (unchecked)  |CIDR           |0.0.0.0/0          |TCP            |All                |443                    |Outbound HTTPS access      |
{: title="List of Required Network Security Rules (Egress)"}

<!-- **Notes**: This next table is for reference and should be adapted for the workshop. If optional rules are needed as shown in the example below, then uncomment it and add those optional rules. The first entry is just for illustration and may not fit your workshop -->

<!--
|Stateless          |Source Type	|Destination CIDR	|IP Protocol	|Source Port Range	|Destination Port Range	|Description                                        |
| :-----------      | :-----------  |  :--------:       | :----------:  | :------------:    | :-----------------:   | :------------------------                         |
|False (unchecked)  |CIDR           |0.0.0.0/0          |TCP            |All                |1521                   |e.g. Remote oracle DB Listener anywhere            |
|False (unchecked)  |CIDR           |130.129.10.45/32   |TCP            |All                |1525                   |e.g. Remote oracle DB Listener at IP 130.129.10.45 |
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