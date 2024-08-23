# Enable application monitoring using Observability and Management Services

## Introduction

In this lab, you'll enable OCI Logging Analytics Service to monitor Oracle Kubernetes Engine and OCI Application Performance Management (APM) for application monitoring and also OCI Database Management for monitoring MySQL HeatWave Database to get end to end visibility of the application and its stack. 

Estimated Time: 40 minutes

### Objectives

In this lab, you will see step-by-step instructions to:
  - Enable APM & Logging Analytics Service
  - Complete visibility into the application using O&M Services 

## Task 1: Monitor MySQL HeatWave Database 

1. From the OCI menu, select **Observability & Management** -> **Database Management** then **Diagnostics & Management**.

    ![Oracle Cloud console Menu](images/4-0-1-dbm.png " ")

2. Select compartment **devliv24** and click on "MySQL HeatWave" to see the fleet Summary - showing MySQL HeatWave Database systems inventory, monitoring status, resource usage & alarms.

    ![Oracle Cloud console Menu](images/4-0-2-dbm.png " ")

3. Click on **mysql-appdev** MySQL HeatWave DB system from the list of monitored deployments

    ![Oracle Cloud console Menu](images/4-0-3-dbm.png " ")

4. Monitor MySQL HeatWave Database 

    - Alarms section allows drill down to specific errors to quickly resolve any issues
    - Monitoring status timeline:  Shows if Database Management can collect monitoring metrics for the resource
    - Monitor database performance attributes in the Summary section

    ![Oracle Cloud console Menu](images/4-0-4-dbm.png " ")

5. Performing MySQL HeatWave DB System Performance Diagnostics

  - Click on **Performance Hub** tab 
    ![Oracle Cloud console Menu](images/4-0-5-dbm.png " ")
  
  - Performance Hub provides holistic performance management capabilities providing a single view of the database performance using a varied set of features, such as Active statement latency, statement count charts, top 100 queries sorted by metrics, and the ability to drill down into specific SQL details.

    ![Oracle Cloud console Menu](images/4-0-6-dbm.png " ")

  - Click on any one of the top query. To see the performance of the query. For example clicking on **UPDATE 'A1P_USERS'** shows the following - your environment may be different.

    ![Oracle Cloud console Menu](images/4-0-7-dbm.png " ")

    Total of 8 executions and all 8 executions got failed. This allows us to quickly identify the database query performance issues using OCI Database Management Service. 

## Task 2: Create an APM domain

1.	From the OCI menu, select **Observability & Management** -> **Application Performance Monitoring** then **Administration**.
	![Oracle Cloud console Menu](images/5-1-1-apmdomain.png " ")

2. Select the **devlive24** compartment from the dropdown and click Create APM domain 
	![Oracle Cloud console Menu](images/5-1-2-apmdomain.png " ")

3.	Name your APM domain as **apm-appdev** and select **devlive24** compartment from the dropdown. click **Create**.
  ![Oracle Cloud console, Create APM Domain](images/5-1-3-apmdomain.png " ")

4. Press the refresh button periodically to check the status. This may take a few minutes.
  ![Oracle Cloud console, Create APM Domain](images/5-1-4-apmdomain.png  " ")

5.	Once the job is completed, the status turns to Active with a green icon.
  ![Oracle Cloud console, Create APM Domain](images/5-1-5-apmdomain.png " ")


## Task 3: Obtain Data Upload Endpoint and Private and Public Data Keys

To upload tracing data to an APM domain, Data Upload Endpoint and both Private and Public Data Keys must be configured in the application’s configuration files. 

1.	Click the link to the APM domain.
  ![Oracle Cloud console, APM Domain](images/5-1-5-apmdomain.png " ")



2. In the **APM Domain Information** tab, find **Data Upload Endpoint**
  - Under **Resources**, click **Data Keys**.
    - find **auto\_generated\_private_data\_key**. 
    - find **auto\_generated\_public_data\_key**. 

   Copy data upload endpoint and data keys (private and public) to a file to be used in later tasks in the workshop. 

  ![Oracle Cloud console, APM Domain](images/5-1-6-apmdomain.png " ")


## Task 4: Enable APM for the **Wine Cellar** application

1. Open Code Editor and then open file **OCI-DEVLIVE-2024 > sb-hol >customapmresource.yaml**

    ![Oracle Cloud console, Cloud Shell](images/4-3-1-1-appmon.png " ")
    ![Oracle Cloud console, Cloud Shell](images/4-3-2-2-appmon.png " ")

2. Update and save the file **customapmresource.yaml** with apm endpoint and private data key 
    - Update field **<apm-endpoint>** (line 11) with APM upload end point obtained from task 3. 
    - Update field **<apm-private-data-key>** (line 13) with private data key obtained from task 3. 
    ![Oracle Cloud console, Cloud Shell](images/4-3-3-3-appmon.png " ")
    - save the file 
    ![Oracle Cloud console, Cloud Shell](images/4-3-4-4-appmon.png " ")

3. Open cloud shell and run **enableapm.sh** to enable APM for the Kubernetes cluster

    enableapm.sh 
    - Installs required libraries to enable K8 Open Telemetry operator 
    - Maps K8 Open Telemetry operator to inject APM java agent 
    - Injects APM java agent at the K8 namespace level through the K8 operator 

    ``` bash
    <copy>
    cd ~/oci-devlive-2024/sb-hol
    chmod 755 enableapm.sh
    ./enableapm.sh
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/4-3-3-appmon.png " ")


4. Verify if the APM is enabled by executing the below command and check for OTEL parameters in the pod parameters. 

    ``` bash
    <copy>
    kubectl get pod wstore-front-0 -o yaml
    </copy>
    ```

    ![Oracle Cloud console, Cloud Shell](images/4-3-4-appmon.png " ")
    Now the APM is enabled for the application proceed to the next task. 

## Task 5: Generate workload by navigating to the app

1.  Click **Login**.

    ![WineCellar Demo App](images/4-1-1-wstore.png " ")


2.  Enter your name (or john) as username, leave the password blank, and click **Login**.

    ![WineCellar Demo App](images/4-1-2-wstore.png " ")


3. Then click around the buttons in the pages, as in the example flow shown below.

    >**Note:** Do not worry if you see the "Failed" messages, or if it takes a long time for the pages to respond. Those are expected because the app is designed to fail every once and often for demo purposes.

    Click **Add** on a couple of products then hit **Shopping Cart**. Then Click **Checkout**.
    ![WineCellar Demo App](images/4-1-3-wstore.png " ")
    ![WineCellar Demo App](images/4-1-4-wstore.png " ")

    Click **Confirm Order**.
    ![WineCellar Demo App](images/4-1-5-wstore.png " ")

    Click **Logout**.
    ![WineCellar Demo App](images/4-1-6-wstore.png " ")


## Task 6: Examine traces in APM Trace Explorer

1. From the OCI menu, select **Observability & Management** > **Trace Explorer**

   ![Oracle Cloud, Navigation Menu](images/5-1-1-traces.png " ")

2. On the Trace Explorer page, select **devlive24** for the **Compartment** and **apm-appdev** for the **APM Domain**.

   ![Oracle Cloud, Trace Explorer](images/5-1-2-traces.png " ")

3.	By default, traces are displayed in the order by the start time. Right mouse click on the **Duration** column, select **Sort Descending** to show the traces by duration in descending order. This will bring the slowest trace to the top of the list.

   ![Oracle Cloud, Trace Explorer](images/5-1-3-traces.png " ")

4. Hover the mouse over the bar in the **Spans** column at the top row. Verify three services are included in the trace, and each color represents a service: wstore-back, wstore-front, and wstore-web

   ![Oracle Cloud, Trace Explorer](images/5-1-4-0-traces.png " ")

5.	Click on the trace **wstore-web: Full Update /winestore/confirm** under Service:Operation name column.

   ![Oracle Cloud, Trace Explorer](images/5-1-4-1-traces.png " ")

   >**Note:** If you do not see a **wstore-web: Full Update /winestore/confirm** trace, you can navigate the WineStore demo app to perform the checkout operation.

6. **Trace Details** page opens. Review the trace information on the upper screen. E.g., Status, Trace ID, Whether it has an error or not, how many spans and services are involved, or the duration of the trace.
   ![Oracle Cloud, Trace Explorer](images/5-1-5-traces.png " ")

7. In the **Topology** view, you can see how the operations are connected within the trace. Different colors indicate different services. Hover the mouse on the icons and the arrows that connect the icons. Review the information in the callouts.
  ![Oracle Cloud, Trace Explorer](images/5-1-6-traces.png " ")

  >**Note:** The operations may look differently in the trace you selected.

8. Scroll down the page to show the **Spans** view. Spans in the trace are displayed in a Gantt chart. A span at the top of the list is the root span, and the child spans are nested below the root span.

  ![Oracle Cloud, Trace Explorer](images/5-1-7-traces.png " ")

9. **Trace Details** shows one span error and find the span that has errored, now lets click on that span to understand the reason for the error. 

  ![Oracle Cloud, Trace Explorer](images/5-1-8-traces.png " ")

Span error message shows that the table **A1P_USERS** is missing in the wine database which resulted in the error in this particular trace.

 >**Note:** With APM its easy to query the trace and span data using the trace query language. Explore other tabs (Users, SQLs, Web Apps, Sessions, etc..) in trace explorer to get quick insights into application performance.


## Task 7: Enable Logging Analytics Service 

1. Navigate to Observability & Management and click Logging Analytics.

    - From Navigation Menu ![navigation-menu](images/4-1-1-okela.png) > **Observability & Management** > **Logging Analytics**.

    - Click **Start Using Logging Analytics**.
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-2-okela.png " ")

    - Review the policies that are automatically created and click **Next**.
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-3-okela.png " ")

    - Enable OCI audit log analysis and Click **Next**.
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-4-okela.png " ")

    - Logging Analytics Service is enabled in the tenancy. Click **Close**.
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-5-okela.png " ")

2. Enable Logging Analytics OKE Solutions 

    - From Navigation Menu ![navigation-menu](images/4-1-6-okela.png) > **Observability & Management** > **Logging Analytics** > **Solutions**.

    - Click on **Kubernetes**
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-7-okela.png " ")

    - Click on **Connect clusters**
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-8-okela.png " ")

    - Click on **Oracle OKE**
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-9-okela.png " ")

    - Select the **devlive24-oke** created in lab 1 and click **Next**
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-10-okela.png " ")

    - Accept defaults and click on **Configure log collection** 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-11-okela.png " ")

    - Configured OKE **devlive24-oke** for monitoring. Click on **Take me to Kubernetes**
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-12-okela.png " ")

    - Collection of metrics and log data is still in progress - wait for 4 to 5 mins for collection to complete 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-13-okela.png " ")

    - Once the collection is complete it shows CPU, memory and latest telemetry data for the cluster 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-14-okela.png " ")

## Task 8: Explore the Logging Analytics solutions for OKE Clusters

1. Click on the cluster **devlive24-oke** 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-15-okela.png " ")

2. Overview of the cluster **devlive24-oke** is shown 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-16-okela.png " ")

3. Filter by namespaces in the cluster 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-17-okela.png " ")

4. Wine Cellar application is deployed on default namespace on filtering by namespace it shows the topology, usuage metrics which makes it easy to quickly identify the issues 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-18-okela.png " ")

5. Dedicated events tab shows all the events occured on the specific namespace
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-19-okela.png " ")

6. Analyze further based on cluster, workload, node and pod 
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-20-okela.png " ")

7. On the right we can see metric widgets as shown below which help us further understand how OKE is performing.
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-21-okela.png " ")
    ![Oracle Cloud console, Enable Logging Analytics](images/4-1-22-okela.png " ")

8. Analyze different metrics together to understand the workload patterns, resource utilization and also for effective troubleshooting. 
    * Click on the expand button which shows when you hover the mouse on a particular metric. Lets select metric **CPU cores(used/allocatable)** 
     ![Oracle Cloud console, Enable Logging Analytics](images/4-1-23-okela.png " ")
    * Click on **Metrics to analyze**
     ![Oracle Cloud console, Enable Logging Analytics](images/4-1-24-okela.png " ")
    * Click on metrics of interest to analyze together (Maximum of 3 metrics are allowed to analyze together). Lets select the metric **Memory Used** 
     ![Oracle Cloud console, Enable Logging Analytics](images/4-1-25-okela.png " ")
    * Click again on **Metrics to analyze** and select the metric **Total API server requests**. Now all the three metrics can be analyzed together to understand workload patterns or for the effective troubleshooting. 
     ![Oracle Cloud console, Enable Logging Analytics](images/4-1-26-okela.png " ")

>Note: OCI Logging Analytics provides one-click end-to-end Kubernetes monitoring solution for the underlying infrastructure, Kubernetes platform and cloud native applications.

[You may now **proceed to the next lab**.](#next)

## Acknowledgements

* **Author** - Anand Prabhu, Principal Member of Technical Staff, Enterprise and Cloud Manageability
- **Contributors** -
Yutaka Takatsu, Senior Principal Product Manager,  
Avi Huber, Vice President, Product Management
* **Last Updated By/Date** - Anand Prabhu, January 2024
