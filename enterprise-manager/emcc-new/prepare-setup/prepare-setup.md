# Prepare Setup

## Introduction
This lab will show you how to download the Oracle Resource Manager (ORM) stack zip file needed to setup the resource needed to run this workshop.

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
    - [emcc-mkplc-devops-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/5XtssTbOV_hAQNJ_6ytSsPAsVTozSCY6WQEvCZ-V0S7cTAaCjt3VoS-RC-CC6uDx/n/natdsecurity/b/stack/o/emcc-mkplc-devops-patching.zip)
</if>
<if type="find-fix-validate">
    - [emcc-mkplc-find-fix-validate.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/e8Kxwmy0-2vSr9xL5je98lkZ-D4AbwsUl28tMDM-rSVex5FqJ1wAkx3Z4uFUv6Zv/n/natdsecurity/b/stack/o/emcc-mkplc-find-fix-validate.zip)
</if>
<if type="fleet-patching">
    - [emcc-mkplc-fleet-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/xyTG8q5fsPm229Z_U79K_B0LBVsvkoDzbhTtCsBz81En5Cywa_oKfqdldaBM7w4s/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-patching.zip)
</if>
<if type="fleet-patching-ui">
    - [emcc-mkplc-fleet-patching-ui.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/YQksITsJY7mt8bT9ksd8l5kddAlSZR1Lt06PeijAGR6X0haxFjGnD_XbotnKAWqV/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-patching-ui.zip)
</if>
<if type="fleet-upgrade">
    - [emcc-mkplc-fleet-upgrade.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/kCQ0PJKMtZV-GWdi_iUbZ17CFbna4BGlIW5Q2ge5hzSJOyi6FkuqKXoN0NA2BQnf/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-upgrade.zip)
</if>
<if type="fleet-upgrade-ui">
    - [emcc-mkplc-fleet-upgrade-ui.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/F2zBX22AcVK1ZusWzUCMZKk5B6bHAW4NG-C38YeM1IL1QqnTPRO8szAMeL8-XTR5/n/natdsecurity/b/stack/o/emcc-mkplc-fleet-upgrade-ui.zip)
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
<if type="monitoring-overview">
    - [emcc-mkplc-monitoring-overview.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/qI0lqJPk2shsPYznYbFcKoL1wr7PLNHAb_t6IvJpnBjdA-pbdHAYcXAcrpO-lI9a/n/natdsecurity/b/stack/o/emcc-mkplc-monitoring-overview.zip)
</if>
<if type="migration-workbench">
    - [emcc-mkplc-mig-workbench.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/ujmg9otLGING_GtfGyMDKrjg4CDRp3LNqmSnRvPRTeE_0Y5od6TiI8WsQ5wFtWzI/n/natdsecurity/b/stack/o/emcc-mkplc-migration-workbench.zip)
</if>
<if type="migration-workbench-oci">
    - [emcc-mkplc-mig-workbench-oci.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/C2dOha4nQ-g4HFAFQLgXBpAC6m2bYoir4o_hROPmsULr-QKBOhpLTA_az2c3LY_s/n/natdsecurity/b/stack/o/emcc-mkplc-migration-workbench-oci.zip)
</if>

2.  Save in your downloads folder.

We strongly recommend using this stack to create a self-contained/dedicated VCN with your instance(s). Skip to *Task 3* to follow our recommendations. If you would rather use an exiting VCN then proceed to the next step as indicated below to update your existing VCN with the required Egress rules.

## Task 2: Adding Security Rules to an Existing VCN
This workshop requires a certain number of ports to be available, a requirement that can be met by using the default ORM stack execution that creates a dedicated VCN. In order to use an existing VCN/subnet, the following rules should be added to the security list.

| Type           | Source Port    | Source CIDR | Destination Port | Protocol | Description                           |
| :-----------   |   :--------:   |  :--------: |    :----------:  | :----:   | :------------------------------------ |
| Ingress        | All            | 0.0.0.0/0   | 22               | TCP      | SSH                                   |
| Ingress        | All            | 0.0.0.0/0   | 80               | TCP      | Remote Desktop using noVNC            |
| Egress         | All            | N/A         | 80               | TCP      | Outbound HTTP access                  |
| Egress         | All            | N/A         | 443              | TCP      | Outbound HTTPS access                 |
{: title="List of Required Network Security Rules"}

<!-- **Notes**: This next table is for reference and should be adapted for the workshop. If optional rules are needed as shown in the example below, then uncomment it and add those optional rules. The first entry is just for illustration and may not fit your workshop -->

| Type           | Source Port    | Source CIDR | Destination Port | Protocol | Description                           |
| :-----------   |   :--------:   |  :--------: |    :----------:  | :----:   | :------------------------------------ |
| Ingress        | All            | 0.0.0.0/0   | 7803             | TCP      | e.g. Remote EM console access         |
{: title="List of Optional Network Security Rules"}

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
  - **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, August 2022
