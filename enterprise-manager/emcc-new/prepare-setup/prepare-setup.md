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
<if type="find-fix-validate">
    - [emcc-mkplc-find-fix-validate.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/e8Kxwmy0-2vSr9xL5je98lkZ-D4AbwsUl28tMDM-rSVex5FqJ1wAkx3Z4uFUv6Zv/n/natdsecurity/b/stack/o/emcc-mkplc-find-fix-validate.zip)
</if>
<if type="fleet-patching">
    - [emcc-mkplc-fleet-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/xyTG8q5fsPm229Z_U79K_B0LBVsvkoDzbhTtCsBz81En5Cywa_oKfqdldaBM7w4s/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-patching.zip)
</if>
<if type="fleet-upgrade">
    - [emcc-mkplc-fleet-upgrade.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/kCQ0PJKMtZV-GWdi_iUbZ17CFbna4BGlIW5Q2ge5hzSJOyi6FkuqKXoN0NA2BQnf/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-upgrade.zip)
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
<if type="rat-overview">
    - [emcc-mkplc-rat-overview.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/SKVYcQm9QiL9ifHuVDbgdJ51s57zUy9VnF3YwXUPRaellpLxuU-IbtHmAZIEYtL8/n/natdsecurity/b/stack/o/emcc-mkplc-rat-overview.zip)
</if>

2.  Save in your downloads folder.

We strongly recommend using this stack to create a self-contained/dedicated VCN with your instance(s). Skip to *Task 3* to follow our recommendations. If you would rather use an exiting VCN then proceed to the next step as indicated below to update your existing VCN with the required Egress rules.

## Task 2: Adding Security Rules to an Existing VCN   
This workshop requires a certain number of ports to be available, a requirement that can be met by using the default ORM stack execution that creates a dedicated VCN. In order to use an existing VCN the following ports should be added to Egress rules

| Port           |Description                            |
| :------------- | :------------------------------------ |
| 22             | SSH                                   |
| 7803           | Enterprise Manager 13c Server         |
| 80             | noVNC Remote Desktop (NGINX proxy)    |
| 6080           | noVNC Remote Desktop                  |

1.  Go to *Networking >> Virtual Cloud Networks*
2.  Choose your network
3.  Under Resources, select Security Lists
4.  Click on Default Security Lists under the Create Security List button
5.  Click Add Ingress Rule button
6.  Enter the following:  
    - Source CIDR: 0.0.0.0/0
    - Destination Port Range: *Refer to above table*
7.  Click the Add Ingress Rules button

## Task 3: Setup Compute   
Using the details from the two steps above, proceed to the lab *Environment Setup* to setup your workshop environment using Oracle Resource Manager (ORM) and one of the following options:
-  Create Stack:  *Compute + Networking*
-  Create Stack:  *Compute only* with an existing VCN where security lists have been updated as per *Task 2* above

## Acknowledgements
  - **Author** - Rene Fontcha, LiveLabs Platform Lead, NA Technology
  - **Contributors** -  
  - **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, February 2022
