# Clean up the workshop environment

## Introduction

In this lab, you will clean up the workshop environment by running commands from the Cloud shell, also manually removing the Oracle cloud resources using the Oracle Cloud console.

Estimated time: 10 minutes

### Objectives

* Remove the lab configurations and resources

### Prerequisites

* Completion of preceding labs in this workshop.

## Task 1: Clean Up the application setup

To delete the workshop setup from your tenancy, follow the steps below using.

1. From the OCI menu, navigate to **Databases** -> **MySQL HeatWave** -> **DB Systems**

2. Click the name of the DB System created in Lab 1. Then click `[More actions]` and choose `[Delete]`.

3. When prompted, click the checkbox to "Delete DB System permanently." and click **`[Delete DB sysme]`**

    ![Oracle Cloud console - DB Systems](images/5-2-0-cleanup.png " ")

    >**Note:** If Termination Protection is active, you will not be able to delete the DB System. You will instead need to Edit the DB System, locate the advanced settings, uncheck the **Termination Protection** box, and save. It will take a few minutes to update before you can then delete the resource.

    ![Oracle Cloud console - DB Systems](images/5-2-1-cleanup.png " ")

4. Use the OCI Menu to navigate to  **Developer Services** -> **Containers & Artifacts** -> **Kubernetes Clusters (OKE)** -> **Kubernetes**. Locate the cluster created in lab 1. 

    ![Oracle Cloud console - OKE](images/5-2-6-cleanup.png " ")
    ![Oracle Cloud console - OKE](images/5-2-7-cleanup.png " ")
    ![Oracle Cloud console - OKE](images/5-2-8-cleanup.png " ")

## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
Eli Schilling, Developer Advocate
* **Last Updated By/Date** - Eli Schilling, February 2024
