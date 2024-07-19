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
    - [emcc-mkplc-config-compliance.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/IW9bVu4ioxIFVbWzFmFJ3v29dNjRE6sc5nrRNqxf--K8U7wkVwaNwpXOW5iAIytg/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-config-compliance.zip)
</if>
<if type="devops-automation">
    - [emcc-mkplc-devops-automation.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/xOjert_Cp_Gd44duvANQa74_MD49T3t5qm5Vhm2r5yCNTfkULNej5o2WL8WXoFHL/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-devops-automation.zip)
</if>
<if type="find-fix-validate">
    - [emcc-mkplc-find-fix-validate.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/RIGLXb1ZD-aVOzFxBA8qglTcKJLaG1OlGrhWNzuNu1rTBLHeYWoyuFup72uATVv0/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-find-fix-validate.zip)
</if>
<if type="fleet-patching">
    - [emcc-mkplc-fleet-patching.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/sJYjuQxqsgLIKpnmrDkvPyOySlvR2ftO4kkqgkKDCgnRHi3Z5lvSv1RcO1nr6kj7/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-fleet-patching.zip)
</if>
<if type="fleet-upgrade">
    - [emcc-mkplc-fleet-upgrade.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/_EzQGMhCX2_Jucll-VAmKwkJbnb03HoM6Iww0rayDVUkeZDVFD9mfYVvGcCaFY-7/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-fleet-upgrade.zip)
</if>
<if type="fundamentals">
    - [emcc-mkplc-fundamentals.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/I4IBoYsyVpJ9GimiR8NZrZESnJiNjN9N_pjMS06qFgZ0kvIs0lsVn1lQ2VCdgaAj/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-fundamentals.zip)
</if>
<if type="job-system-automation">
    - [emcc-mkplc-job-system-automation.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/O4idO--Wi3OHk7Ga6y60b0Db56ycwv6wor9FYhs3kBoFL7RokFSBs_E9LEBuHdad/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-job-system-automation.zip)
</if>
<if type="lifecycle">
    - [emcc-mkplc-lifecycle.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/4COKC5s4DcNvongBW92BKckYdAndE8247gbpNpaK31xaRG6h1LeaZqri6L1QvAEV/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-lifecycle.zip)
</if>
<if type="rat-overview">
    - [emcc-mkplc-rat-overview.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/_T85iVv1QkU8Z8lF_XkDVOqBiathAloKlRvaHE8M6AqILuh7w2funO18WIp9BZ9f/n/c4u02/b/hosted_workshops/o/stacks/emcc-mkplc-rat-overview.zip)
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
