# Kubernetes Monitoring Solution Deployment

## Introduction

In this lab, you'll deploy Kubernetes Monitoring Solution from OCI Marketplace to enable monitoring of an existing OKE Cluster.

Estimated Time: 15 minutes

### Objectives

In this lab, you will see step-by-step instructions to:

  - Use OCI Marketplace to configure and deploy the Kubernetes Monitoring solution.
  - Verify successful deployment. 
  - Review Application Information.
  - Explore created Kubernetes Dashboards.



## Task 1: Navigate to Kubernetes Monitoring and Management application

To navigate to Kubernetes Monitoring and Management application, follow the given steps:

  - From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Marketplace** > **All Applications**.
![marketplace-navigation](./images/marketplace-navigation.gif " ")

  - In the search bar, enter the text **Kubernetes Monitoring and Management**.

  - Click on the **Kubernetes Monitoring and Management** application to land on the application page.
![k8s-app-search](./images/k8s-app-search.png " ")

  - You will land on the **Kubernetes Monitoring and Management** application page.
![k8s-app](./images/k8s-app.png " ")

  - Quick tip, you can use the direct link to land on the application page:
    ```
         <copy>
            https://cloud.oracle.com/marketplace/application/136942717/overview?region=us-phoenix-1
         </copy>   
    ```


## Task 2: Launch Kubernetes Monitoring and Management application

1. Select the **LiveLabs-V3.0 (7/19/2023)** version from the version dropdown.

2. Select the user Compartment from the dropdown. For your user the Compartment name will be in the format **LL{reservationid}-COMPARTMENT**, for e.g. LL55379-COMPARTMENT.
  >**Note:** The compartment name can be found from **View Login Info** page.

3. Check the **Terms and Restrictions** checkbox.

4. Click on **Launch Stack** button to launch the application.
![k8s-app-launch](./images/k8s-app-launch.png " ")

## Task 3: Configure Stack

1. On **Create Stack** page, you will see the **Stack information**.

  Click on **Next** button to proceed to the Configure variables section.
  ![stack-information](./images/stack-information.png " ")
  

2. In **Configure variables** section, you have to set the following variables for the stack:

    - **OKE Cluster Compartment:** Select the **oke-lab-9501** cluster compartment from the dropdown.

    - **OKE Cluster:** Select the **oke-cw23-II** OKE cluster from the dropdown.

    - **OCI Logging Analytics Compartment:** Select the compartment from the dropdown. The compartment will be in the format **LL{reservationId}-COMPARTMENT**, for e.g. LL55379-COMPARTMENT.

    - **OCI Logging Analytics Log Group:** Select log group from the dropdown. The log group will be in the format **Kubernetes{reservationId}**, for e.g. Kubernetes55379.
      
        >**Note:** The **reservationId** can be found from **View Login Info** page.

  Click on **Next** button to proceed to the Review section.
  ![configure-varaibles](./images/configure-varaibles.png " ")

3. In **Review** section, you can see the stack configurations you selected in the previous steps.

  - Click on the **Create** button to create the stack. This step will create an ORM (Oracle Resource Manager) job that uses [Terraform](https://github.com/oracle-quickstart/oci-kubernetes-monitoring/tree/main/terraform) to deploy the solution.
  
  - It will take around 90 seconds for the stack to get created.
    ![review-stack](./images/review-stack.png " ")
    ![stack-execution](./images/stack-execution.png " ")
  

## Task 4: Navigate to installed dashboards from Application Information tab

1. After the stack creation is successful, it will take few seconds for the **Application information** tab to appear.
![stack-creation](./images/stack-creation.png " ")

2. Click on the **Application information** tab to view the application information.

3. Click on the **View Dashboard** button to view the dashboards.
  ![application-information](./images/application-information.png " ")


## Task 5: Exploring Kubernetes Dashboards

1. After clicking on the **View Dashboards** button, a new tab will open displaying all the dasboards.

2. Click on the **Kubernetes Cluster Summary** dashboard. It will take few seconds for the dashboard widgets to load.
![dashboards](./images/dashboards.png " ")

3. Click on the **Scope Filter** panel.
![scope-filter](./images/scope-filter.png " ")

4. Select your user Compartment from the dropdown in the **Log Group Compartment** field. For your user the Compartment name will be in the format **LL{reservationid}-COMPARTMENT**, for e.g. LL55379-COMPARTMENT. Select **oke-cw23-II** cluster in the **Kubernetes Cluster** field.
![compartment-cluster](images/compartment-cluster.png)

5. You should be able to see the all the widgets displaying the data specific to your OKE Cluster.
![k8s-cluster-summary](images/k8s-cluster-summary.png)

6. Scroll down to the **Container Logs** widget in the dashboard.
![container-logs](images/container-logs.png)

7. Click on the View Query Icon to view the query used to populate the data in widget.

  ![view-query](images/view-query.png)
  ![query](images/query.png)

  After viewing the query, click on **Close** button.

8. Click on the Punch Out Icon on the Container Logs widget.
![punch-out](images/punch-out.png) 

9. This will take you to the **Pie Chart view** of Log Explorer in context of Kubernetes Cluster Name.
![log-explorer](images/log-explorer.png)

10. To navigate back to the Kubernetes Cluster Summary page, click on the **Kubernetes Cluster Summary** as highlighted in the image below.
![summary-page](images/summary-page.png)

11. Similarly you can explore other widgets in the Kubernetes Cluster Summary and other dashboards.





**Congratulations!** In this lab, you have successfuly completed the following tasks:
- Used OCI Marketplace to configure and deploy the Kubernetes Monitoring solution.
- Verified successful deployment.
- Reviewed Application Information.

  You may now proceed to the [next lab](#next).

## Acknowledgements
* **Author** - Samarthya Sahu, OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Samarthya Sahu, Aug, 2023