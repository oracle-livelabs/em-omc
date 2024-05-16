# Assess and Assure Security Posture Across Your Fleet of Databases

## Introduction

Learn how to secure and ensure compliance of your enterprise databases in this workshop. Discover methods to monitor their security, validate configurations, and automate compliance with company, industry, and regulatory standards like CIS and STIG. Explore using Oracle Enterprise Manager to automate inventory and baseline all database targets, including various versions and instances deployed over time.

*Estimated Time*: 60 minutes

You can watch this video below for a quick walk-through of this lab.
[Video Walk-through](videohub:1_vyyju031)

### About key features of Fleet Maintenance Hub in Oracle Enterprise Manager

Starting with Enterprise Manager 13.5 RU16, Enterprise Manager offers a new interface - Fleet Maintenance Hub to ease automated update(patching), and upgrade of your database fleet.
The Fleet Maintenance Hub within Enterprise Manager offers a comprehensive solution for managing database vulnerabilities and patch operations. It streamlines the process by identifying potential security risks, providing patch recommendations, and enabling efficient scheduling and monitoring of patching and upgrade operations. With the ability to manage diverse infrastructures and ensure compliance with patch policies, the Fleet Maintenance Hub serves as a centralized and powerful tool for maintaining the security and stability of database assets.

#### Video Preview
Watch a preview of database patching using Oracle Enterprise Manager Fleet Maintenance:

[](youtube:JlspEvqebHE)

*Note: Interfaces in this video may look different from the interfaces you will see. For updated information, please see steps below.*


### Objectives

In this lab you will perform the following steps:
| Step No. | Feature                                                    | Approx. Time | Details                                                                                                                                                                    | Value Proposition |
|----------------------|------------------------------------------------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| 1                    | Assess patch recommendation and create gold image                             | 5 minutes  | Review the patch recommendations for existing gold images                                                                                                                 | Provides patch recommendations for gold image. Discover the advantages of utilizing patch recommendations, where manual, time-intensive tasks are automated to yield highly precise outcomes.                  |
| 2                    | Secure databases by updating with new gold image | 5 minutes  | Update databases using Gold image | Demonstrate with ease to update a pluggable database                   |
| 3                    | Elevate security posture by auditing for compliance | 5  minutes  | Refresh a Gold Image based on latest patch recommendation | How to steps to create a new version for a gold image. Latest version will be used to update and upgrade process.


### Prerequisites
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

*Note*: This lab environment is setup with Enterprise Manager Cloud Control Release 13.5 and Database 19.10 as Oracle Management Repository. Workshop activities included in this lab will be executed both locally on the instance using Enterprise Manager Command Line Interface (EMCLI) or Rest APIs, and the Enterprise Manager console (browser)

## Task 1: Assess patch recommendation and create gold image [Read-Only Step]

In this task, we will review patch recommendations for existing gold images. Based upon the recommendations, we will create a new version.

1. Login to Enterprise Manager as user - emadmin and password - welcome1

![](images/em-login.png "em-login")

2. Once logged in, navigate to ***Targets >> Databases***  

![](images/em-navig1.png "em-navig1")

   and then ***Administration >> Fleet Maintenance Hub***

![](images/em-navig2.png "em-navig2")

3. This is the homepage of Fleet Maintenance Hub. At the top right corner we see the status of ***Last Patch Recommendation Update***. If you see a date below it, then it suggests that patch recommendation was executed on that particular date. To setup patch recommendation, review [Oracle Enterprise Manager](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emlcm/downloading-patch-recommendations-and-patches.html).

![](images/em-hub.png "em-hub")
   For successful completion of this lab, we suggest that you do not upload any new patch catalog or enter your MOS credential as per above documentation. This will generate new recommendations, which might be different than the one in the upcoming sections of this document.

4. Lets review Tile 2 of Fleet Maintenance Hub, which is referred as Patch Recommendations for Images

![](images/tile2.png "hub-tile2")

Here we see that goldimages - 19cDB-Linux-x64-ERP has 2 patch recommendations, while 19cDB-Linux-x64-APPS has a green tick against it. This suggests that 19cDB-Linux-x64-ERP should have a new version that includes these two recommended patches, whereas 19cDB-Linux-x64-APPS is in good shape and can be used to perform patching.

Follow [Link](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/emlcm/image-maintenance-ui.html) to understand steps involved to refresh a goldimage. For this lab, we will use 19cDB-Linux-x64-APPS image.


## Task 2: Secure databases by updating with new gold image

In this task, we will perform pdb patching. In this usecase, we will unplug one of the pdbs and plug it to a higher version CDB.
We will unplug Finance pdb (associated with CDB -sales) and plug it to HR CDB. Finance is currently at 19.17 version and HR is at 19.23.
![](images/pre-update.png "pre-update")

Lets complete below steps to perform the pdb patching.

1. Subscribe sales CDB to goldimage 19cDB-Linux-x64-APP.

Under Target Subscription tab in Fleet Maintenance Hub, click on ***Subscribe*** button. Select filter 19 under Release. From the dropdown select the goldimage - 19cDB-Linux-x64-APPS. From the list of databases, select sales.subnet.vcn.oraclevcn.com. Click on subscribe at the top right corner.
![](images/sales-subscribe.png "subscribe")

Upon completion, click on close.

2. Go to Tile 3 - Target Patch Compliance in Fleet Maintenance Hub.
![](images/tile3.png "tile3")

Click on doner icon, under Actions for sales CDB and select Update Pluggable Database. This will launch the operator UI of Fleet Maintenance.

3. We are now at the operator UI screen, with pre-selected values for Gold Image, Target Type and Operation.
![](images/patching-ui1.png "patching-ui1")
Select Finance pdb and hit next.

4. In this page, we will select relevant options and enter values wherever required.
Under Maintenance Task, we will select Attach Existing 19cDB
under Attach Existing CDB, we will review the source CDB, which is sales. Under Destination CDB, we will only see HR.
Under credentials, select from the drop down menu as per the image.
Select Next.

![](images/patching-ui2.png "patching-ui2")

5. Click on Validate and then select Quick Validation. Once you get successful validation message, click close and hit submit.
![](images/patching-ui3.png "patching-ui3")

6. A new dialogue box will ask for the name of the deployment procedure, to track the pdb patching. This unique name will allow you to track the operation. We have provided name - Demo_update.
![](images/patching-ui4.png "patching-ui4")

7. There are two Deployment Procedure submitted.
- Attach Existing CDB
- Update PDB

Click on monitor progress, which will open a new window.
![](images/patching-ui5.png "patching-ui5")

8. In the new page, under search, we have entered Demo, so that we only see the two Deployment procedures, which are associated with this lab.
![](images/patching-ui6.png "patching-ui6")

We see that Deployment procedure with name Attach has completed successfully. Lets click on Update and review the steps performed.
![](images/patching-ui7.png "patching-ui7")

9. With both Deployment procedures completed successfully, lets go back to databases homepage by navigating Targets->Databases.
![](images/patching-ui8.png "patching-ui8")

We see that the Finance PDB has moved out of sales and is plugged with HR CDB.


## Task 3: Elevate security posture by auditing for compliance



That completes the Database Patching and Compliance lab.

You may now proceed to the next lab.

## Learn More
  - [Oracle Enterprise Manager](https://www.oracle.com/enterprise-manager/)
  - [Oracle Enterprise Manager Fleet Maintenance](https://www.oracle.com/manageability/enterprise-manager/technologies/fleet-maintenance.html)
  - [Enterprise Manager Documentation Library](https://docs.oracle.com/en/enterprise-manager/index.html)
  - [Database Lifecycle Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/lifecycle.html)
  - [Database Cloud Management](https://docs.oracle.com/en/enterprise-manager/cloud-control/enterprise-manager-cloud-control/13.5/cloud.html)
  - [Oracle Critical Patch Updates, Security Alerts and Bulletins](https://www.oracle.com/in/security-alerts/)

## Acknowledgements
  - **Authors**
    - Romit Acharya, Oracle Enterprise Manager Product Management
    - Shiva Prasad, Oracle Enterprise Manager Product Management
  - **Last Updated By/Date** -Romit Acharya, Oracle Enterprise Manager Product Management, May 2024
