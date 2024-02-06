# Create a Kubernetes cluster

## Introduction

This workshop uses Spring Boot-based Java microservices as a target application connecting to MySQL HeatWave Database and monitor the application end to end using OCI Observability and Management Services. In this lab, first, you will use the Oracle Cloud console to set up an OCI compartment, second, create an Oracle container engine for Kubernetes (OKE) cluster in your tenancy. In Lab 5, you will deploy the application to the OKE.

Estimated time: 5 minutes

### Objectives

* Create a compartment
* Create a Kubernetes cluster

### Prerequisites

* This lab requires an [Oracle Cloud account](https://www.oracle.com/cloud/free/). You may use your cloud account, or a Free tier account, a cloud account that you obtained through a trial.


## Task 1: Create an OCI compartment

1. Open the navigation menu from the top-left corner (aka. hamburger menu) of the Oracle Cloud console and select **Identity & Security** > **Compartments**.
	![Oracle Cloud console Menu](images/1-1-compartments.png " ")
2. Click **Create Compartment**
	![Oracle Cloud console, Create Compartment](images/1-2-compartments.png " ")
3. Enter the following parameters:
*	Compartment name: **appdev**
*	Description: **App Dev compartment**
*	Accept the default values for the other fields, and click, **Create Compartment**
	![Oracle Cloud console, Create Compartment](images/1-3-compartments.png " ")
*	Verify that your appdev compartment is created in the table
	![Oracle Cloud console, Create Compartment](images/1-4-compartments.png " ")

## Task 2: Create an OKE

1. Open the navigation menu from the top left corner (aka. hamburger menu) in the Oracle Cloud console, and select **Developer Services** > **Kubernetes Clusters (OKE)**.

   ![Oracle Cloud console, Navigation Menu](images/2-1-OKE.png " ")

2. Make sure the **appdev** is selected in the Compartment field, then click **Create cluster**

   ![Oracle Cloud console, Clusters in Compartment](images/2-2-OKE.png " ")

3. Quick Create pane is pre-selected. Keep the default selection and click **Submit**.

   ![Oracle Cloud console, Create cluster](images/2-3-OKE.png " ")

4. Name the cluster as **k8-appdev**. Select Kubernetes API endpoint as **Public endpoint** and Node type as **Managed** and keep other fields as default and click **Next**.

   ![Oracle Cloud console, Create cluster](images/2-4-OKE.png " ")
   ![Oracle Cloud console, Create cluster](images/2-5-OKE.png " ")
   ![Oracle Cloud console, Create cluster](images/2-6-OKE.png " ")

5. Review the configuration, and click **Create cluster**.

   ![Oracle Cloud console, Create cluster](images/2-7-OKE.png " ")

6. Make sure all verification steps are cleared. Click **Close**.

   ![Oracle Cloud console, Create cluster](images/2-8-OKE.png " ")

7.  This will start to create a cluster, and takes 7 to 10 minutes to complete. While waiting for the creation of the cluster, you can proceed to the next lab to create an APM domain. In Lab 5, we will resume the steps to build the application.

   ![Oracle Cloud console, Create cluster](images/2-9-OKE.png " ")




You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
* **Last Updated By/Date** - Anand Prabhu, January 2024