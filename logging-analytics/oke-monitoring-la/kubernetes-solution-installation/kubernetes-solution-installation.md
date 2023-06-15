# Kubernetes Solution Installation Using Resource Manager

## Introduction

This lab will walk you through the steps to deploy the Kubernetes Monitoring solution which offers collection of various logs of a Kubernetes cluster into OCI Logging Analytics using open source log collector Fluentd and Management Agent, Kubernetes Dashboards and provides rich analytics on top of the collected logs. 

Watch the video below for a quick walk-through of the lab.


### Objectives

In this lab, you will see step-by-step instructions to install Kubernetes Monitoring solution for your OKE cluster.

Estimated Time: 15 minutes

## Task 1: Navigate to Marketplace

To navigate to Marketplace, follow one of the following two methods.

1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Marketplace** > **All Applications**.
![marketplace-navigation](./images/marketplace-navigation.gif " ")

2. You can also copy-paste the following link in your browser's address bar to navigate to the Marketplace.
    ```
         <copy>
            https://cloud.oracle.com/marketplace/home?region=us-phoenix-1
         </copy>   
    ```

## Task 2: Launch Kubernetes Monitoring and Management application
    
1. In the search bar, enter the text **Kubernetes Monitoring and Management**.

2. Click on the **Kubernetes Monitoring and Management** application to land on the application page.
![k8s-app-search](./images/k8s-app-search.png " ")

3. Select the Compartment from the dropdown.

4. Check the **Terms and Restrictions** checkbox

5. Click on **Launch Stack** to launch the application.
![k8s-app-launch](./images/k8s-app-launch.png " ")

## Task 3: Configure Stack

> **Note:** Screenshots to be changed after the stack is ready for livelab.

1. On **Create Stack** page, you will see the **Stack information**. You can modify the name of the stack. 

  Click on **Next** button to proceed to the Configure variables section.
  ![stack-information](./images/stack-information.png " ")
  

2. In **Configure variables** section, you have to set the following variables for the stack:

    - **OKE Cluster Compartment:** Select the cluster compartment from the dropdown.

    - **OKE Cluster:** Select the OKE cluster from the dropdown.

    - **OCI Logging Analytics Compartment:** Select the compartment from the dropdown where you want to create Dashboards, Log Groups and other Monitoring service resources.

    - **OCI Logging Analytics Log Group:** For log group, follow one of the following two methods.
        - Click the **OCI Logging Analytics Log Group** dropdown and select a log group from the list.

        - If you want to create a new log group, click the checkbox **Check if you want to create a new Log Group** and enter the name of the new log group in the **OCI Logging Analytics Log Group Name** field.

    - **Fluentd Working Directory:** It is the directory on the node used for storing Fluentd related data. By default, it is set to **/var/log/**.

  Click on **Next** button to proceed to the Review section.
  ![configure-varaibles](./images/configure-varaibles.png " ")

3. In **Review** section, you can verify the stack configurations which you have selected in the previous 2 sections.

  If you want to make changes, you can click on **Previous** button to go back and edit the stack configurations.

  Click the checkbox **Run apply**.

  Click on the **Create** button to create the stack.
  ![review-stack](./images/review-stack.png " ")
  

## Task 4: View Dashboards
> **Note:** Screenshots to be changed after the stack is ready for livelab.

After the stack creation is successful, you can click on the **View Dashboards** to view cluster dashboards.
![view-dashboards](./images/view-dashboards.png " ")




**Congratulations!** In this lab, you have successfuly completed the following tasks:
- Installed Kubernetes solution using the Resource manager.

  You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Samarthya Sahu , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Samarthya Sahu, Jun, 2023
