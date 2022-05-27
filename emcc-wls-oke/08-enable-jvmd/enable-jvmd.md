# (Optional) Enable JVM Diagnostics

## Introduction

Optionally, you can enable Enterprise Manager **JVM Diagnostics (JVMD)** on the WebLogic Servers on Kubernetes. However, because the WebLogic Servers are deployed on Kubernetes pods, where direct communication between OMS and the targets is not available, automated installation of the JVM agent using the EM console is not applicable, and manual arrangements are required.

In this tutorial you will add security rules in the VCN subnet, configure firewall settings in the instance, edit configuration files in each WebLogic pod to prepare for the JVMD agent installation. Then download the agent installer, upload it to the Cloud Shell, transfer it to the admin server pod. Next, use WebLogic Administration Console to manually deploy the JVMD agents to all WebLogic Servers. Finally, verify the JVM targets in the EM Middleware management home page. You can also associate the JVM targets to the WebLogic domain.

   ![JVMD with WLS in OKE diagram](images/0-1-jvmd-oke.png " ")

### JVM Diagnostics Architecture

JVMD consists of a **JVMD engine**, which is a core analytical portion of the JVMD monitoring system, and **JVMD agents**, which are the data collectors of the target JVM.  JVMD agents are deployed inside the application servers and collect real-time JVM monitoring data. The agent transmits the collected data to the JVMD engine, directly using SSL. Note that JVMD does not use an EM agent, having its own channel to communicate with OMS.

   ![JVMD Architecture diagram](images/0-1-jvmd.png " ")

### Limitation

A limitation deploying a JVMD agent to a WebLogic Server, which is already provisioned in a Kubernetes pod, is that the deployment will be lost when the pod is restarted or regenerated. Therefore, the steps described in the Task 2 in this tutorial must be repeated every time such an event happens. To have the JVMD agent persist in the WebLogic Server, deploy it in the Docker image, so that the JVMD agent is pre-deployed, when a pod is created.

Estimated time: 25 minutes

* Completion of the **[Migrating WebLogic Server to Kubernetes on OCI](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=567)** workshop, labs 1, 2, 3 and 4.
* Completion of the preceding tutorials in this workshop


### Objectives
* Enable JVM Diagnostics

## **Task 1**: Configure network and firewall settings


1.  First, you will need to obtain **JVMD SSL Port** from the Middleware agent management page in the EM console. From the EM console, select **Setup** (a gear icon in the menu bar) > **Middleware Management** > **Engines and Agents**.

   ![EM Console, Setup menu](images/1-1-emcc.png " ")

2. In the **Engines and Agents** page, under **RUEI/BTM/JVMD Engines**, locate **SSL Port** of the JVM Diagnostics Engine. This is the port, which needs to be available at the EM host. In the image below, the value is **7301** for an example. Note down the value to a text file.

   ![EM Console, Engines and Agents page](images/1-2-emcc.png " ")

3.  Next, you will need to add the SSL Port to the security rule in the subnet which is used by your OMS instance. Log on to the Oracle Cloud console, select **Compute** > **Compute instance** from the navigation menu.

   ![Oracle Cloud Console, Navigation menu](images/1-3-oci.png " ")

4. In the **Instances** page, select the **Region** and **Compartment** where the OMS instance resides. Then select the link to the OMS instance from the list of your compute instances.

   ![Oracle Cloud Console, Instances](images/1-4-oci.png " ")

    > **NOTE:** Ask your EM Administrator if you do not know the region or compartment of the OMS instance.

5. In the **Instance Details** page, click **Copy** next to the **Public IP address** and **Internal FQDN**, and write down the values to a text file. You will need these values later in this tutorial. Then click the link to the **Subnet**.

   ![Oracle Cloud Console, Instance details](images/1-5-oci.png " ")

6. In the **Subnet Details** page, click a link to your Security List

   ![Oracle Cloud Console, Subnet Details](images/1-6-oci.png " ")

7.  In the **Security Details** page, click **Add Ingress Rules** button.

   ![Oracle Cloud Console, Security List Details](images/1-7-oci.png " ")

8. In the **Add Ingress Rules** window, enter the following information. Specify the JVMD SSL port you obtained in the earlier step in this tutorial (Tutorial 8, Task 1, Step 2) in the **Destination Port Range**. In this example, JVMD SSL port is 7301.

     Ingress Rule 1:
      * Stateless: **No**
      * Source CIDR: **0.0.0.0/0**
      * IP Protocol: **TCP**
      * Source Port Range: **All**
      * Destination Port Range: **7301**
      *  Description: **JVMD SSL upload port**

   ![Oracle Cloud Console, Add Ingress Rules](images/1-8-oci.png " ")

   Click **Add Ingress Rules** button.

9. In the In the **Security Details** page, **Ingress Rules** section, verify the rule was added to the security list.

   ![Oracle Cloud Console, Ingress Rules](images/1-9-oci.png " ")

10. Open a terminal window (or a Putty connection) on your computer, type the following to open an SSH connection to the OMS host.

    ``` bash
    <copy>
    ssh opc@<OMS-Instance-Public-IP> -i "<path-to-the-private-key>/id_rsa"
    </copy>
    ```
    E.g., $ ssh opc@123.456.12.26 -i "/Users/labuser/rsa/id_rsa"

11. Once logged on to the OMS host, run the command below to configure the firewall settings. The image example opens a port 7301 in the OMS host.

    ``` bash
    <copy>
    sudo firewall-cmd --zone=public --permanent --add-port=7301/tcp
    sudo firewall-cmd --reload
    </copy>
    ```

   ![Client PC, terminal window, firewall](images/1-10-oci.png " ")

12. Type exit to logout from the OMS instance and close the terminal.

   ![Client PC, terminal window, exit](images/1-11-oci.png " ")


## **Task 2**: Edit hosts files in WebLogic Server containers


1.  Launch the Oracle Cloud Shell, run the ***oci ce cluster create-kubectl*** command which you saved in the Tutorial 1, Task 1, Step 7.

   ![Oracle Cloud Shell, create-kubectl](images/2-1-oci.png " ")

2. Run the ***kubectl get svc*** command below to list the services in the namespace.  

    ``` bash
    <copy>
    kubectl get svc -n sample-domain1-ns
    </copy>
    ```
    Write down the service names for the WebLogic Servers. The image below shows an example, where the service names are **sample-domain1-admin-server**, **sample-domain1-managed-server1** and **sample-domain1-managed-server2**.

   ![Oracle Cloud Shell, kubectl get svc](images/2-2-oci.png " ")

3. Execute the ***kubectl exec*** command below and log on to the Admin Server pod.  

    ``` bash
    <copy>
    kubectl exec -it sample-domain1-admin-server -n sample-domain1-ns -- /bin/bash
    </copy>
    ```
   ![Oracle Cloud Shell, log in to container](images/2-3-oci.png " ")

4.  Add OMS host information to the ***hosts*** file. You will need to install the vi tool, as there is no editor installed in the pod.

    ``` bash
    <copy>
    yum -y install vi
    </copy>
    ```

   ![Oracle Cloud Shell, install vi](images/2-4-oci.png " ")


   ![Oracle Cloud Shell, install vi](images/2-5-oci.png " ")

5. Open the ***hosts*** file with the vi editor.

    ``` bash
    <copy>
    vi /etc/hosts
    </copy>
    ```

6. Add the **Public IP address** and **FQDN (hostname)** of the OMS instance, which you collected earlier in the steps (Tutorial 8, Task 1, Step 5), in the format: **<Public IP> <FQDN>** to the hosts file.  

    E.g., 123.456.789.10 em135-oketest.sub1234567800.emvcn.oraclevcn.com

    ![Oracle Cloud Shell, edit hosts file](images/2-6-oci.png " ")

    Save and close the file with ***esc + :wq***.

7. Type exit to go back to the Cloud Shell.

    ``` bash
    <copy>
    exit
    </copy>
    ```
    ![Oracle Cloud Shell, exit container](images/2-7-oci.png " ")

8. Repeat the above steps from 2 to 7 for the managed servers and edit the ***hosts*** file for each WebLogic Server pod. You can log on to the managed server pods with the below ***kubectl exec*** commands.

    ``` bash
    <copy>
    kubectl exec -it sample-domain1-managed-server1 -n sample-domain1-ns -- /bin/bash
    </copy>
    ```

    ``` bash
    <copy>
    kubectl exec -it sample-domain1-managed-server2 -n sample-domain1-ns -- /bin/bash

    </copy>
    ```


## **Task 3**: Download JVMD agent and upload to the WebLogic Server pod

In this task, you will download ***jamagent.war*** from the EM console.  

1. In in the EM console, select **Setup** > **Middleware Management** > **Engines and Agents**.

2. In the **Engines and Agents** page, click **Download JVMD Agent**.

    ![EM Console, Engines and Agents page](images/3-1-emcc.png " ")

3. In the **Download JVM Diagnostics Components** window, select **JVMD Agent** from the pull-down menu. Click **OK**.

    ![EM Console, Download JVMD components window](images/3-2-emcc.png " ")

4. In the **JVM Diagnostics Agent web.xml Parameters** page, accept the default settings and click **Download**.

    ![EM Console, JVMD parameters page](images/3-3-emcc.png " ")

5. Click **Allow** on the dialog.

    ![EM Console, confirmation dialog](images/3-4-emcc.png " ")

6. Confirm the ***jamagent.war*** file was downloaded.

    ![EM Console, select file from computer](images/3-5-emcc.png " ")

7. In the Oracle Cloud Shell title bar, click the three-bars icon (three-bar icon) to open the menu. Select **Upload**.

    ![OCI Console, Cloud shell menu, Upload](images/3-6-emcc.png " ")

8. Click **select from your computer** link.

    ![OCI Console, Cloud shell, Upload dialog](images/3-7-emcc.png " ")

9. Go to the download folder, select the ***jamagent.war*** file downloaded from the EMCC. Click **Open**. Then click Upload. This will **upload** the file to the home directory in the Cloud Shell.

    ![OCI Console, Cloud shell, Upload, select from computer](images/3-8-emcc.png " ")


10.  Wait for the File transfer completes, then type the ls command in the Cloud Shell to display the files in the current directory. Confirm the ***jamagent.war*** exists in the home directory.

    ``` bash
    <copy>
    ls
    </copy>
    ```
    ![OCI Console, Cloud shell, File transfers window](images/3-9-oci.png " ")

11.  Next, transfer the ***jamagent.war*** file to the pod by running the following command.

    ``` bash
    <copy>
    kubectl cp jamagent.war  sample-domain1-ns/sample-domain1-admin-server:/u01/oracle/user_projects/domains/sample-domain1
    </copy>
    ```
12. Log on to the admin server pod with the following command. Then hit ls command to list the files in the directory.

    ``` bash
    <copy>
    kubectl exec -it sample-domain1-admin-server -n sample-domain1-ns -- /bin/bash

    ls
    </copy>
    ```
13. Confirm ***jamagent.war*** was copied to the **sample-domain1** directory in the pod.

    ![Oracle Cloud Shell, file upload confirmation](images/3-10-oci.png " ")

14. While still in the container, enter exit to go back to the Cloud Shell.

    ``` bash
    <copy>
    exit
    </copy>
    ```


## **Task 4**: Install JVMD agent to the WebLogic Servers



1. Once the ***jamagent.war*** file was uploaded to the pod, you can deploy it using the WebLogic Administration Console web application. Run the following command to see the external IP of the Traefik load balancer.

    ``` bash
    <copy>
    kubectl get svc -n traefik
    </copy>
    ```
    The output should be similar to the image below. Note down the External-IP.

    ![Oracle Cloud Shell, obtain external IP](images/4-1-oci.png " ")

 2.   On your computer, start a browser and log on to the WebLogic Administration console, with the following URL:

     ``` bash
     <copy>
     http://<External IP of the Traefik load balancer>/console
     </copy>
     ```
     * Username: weblogic
     * Password: Password generated in the WebLogic workshop, Lab 4, Step 1

    ![WebLogic Admin Console, Login page](images/4-2-wls.png " ")

3. Click **Deployments** from the **Domain Structure** tree view.

    ![WebLogic Admin Console, Domain Structure](images/4-3-wls.png " ")

4.  In the **Change Center** section, click **Lock & Edit**.

    ![WebLogic Admin Console, Change Center](images/4-4-wls.png " ")

5. In the **Summary of Deployments** section, **Configuration** tab, click **Install**.

    ![WebLogic Admin Console, Deployments, Install](images/4-5-wls.png " ")

6. Navigate to the path:  ***/u01/oracle/user_projects/domains/sample-domain1*** in the tree view. Select ***jamagent.war***.  Click **Next**.

    ![WebLogic Admin Console, Deployments, Path](images/4-6-wls.png " ")

7.  Ensure **Install this deployment as an application** is selected. Click **Next**.

    ![WebLogic Admin Console, Deployments,Install Application Assistance](images/4-7-wls.png " ")

8. Add check to **admin-server** and **all servers in the cluster**. Click **Next**.

    ![WebLogic Admin Console, Deployments,Install Application Assistance, Servers](images/4-8-wls.png " ")

9. Accept the default values and selections.  Click **Next**.

    ![WebLogic Admin Console, Deployments,Install Application Assistance, security model](images/4-9-wls.png " ")

10. Click **Finish**.

    ![WebLogic Admin Console, Deployments,Install Application Assistance, Review](images/4-10-wls.png " ")

11. In the **Change Center** section, click **Activate Changes**.

    ![WebLogic Admin Console, Settings, Change Center](images/4-11-wls.png " ")

12. Click **Deployments** from the Tree view.

    ![WebLogic Admin Console, Settings, Settings, Confirmation](images/4-12-wls.png " ")

13. Confirm that **jamagent** is listed in the **Deployments** and the State is **Prepared**. Click **Control** tab.

    ![WebLogic Admin Console, Summary of Deployments, Control](images/4-13-wls.png " ")

14. Add check to the **jamagent**j and click **Start**.

    ![WebLogic Admin Console, Summary of Deployments, Start ](images/4-14-wls.png " ")

15.  From the pull-down menu, select **Servicing all requests**.

    ![WebLogic Admin Console, Summary of Deployments, Start, Service all requests](images/4-15-wls.png " ")

16. In the **Start Application Assistant** section, click **Yes** on **Start Deployments**.

    ![WebLogic Admin Console, Start Deployments](images/4-16-wls.png " ")

17. In the **Summary of Deployments** section, verify the Status of the **jamagent** is Active in the **Deployments** table.

    ![WebLogic Admin Console, Start Deployments, confirmation](images/4-17-wls.png " ")

18. Log on to EM console, navigate to the **Middleware** home page. You should see the **JVM Pool** target and **JVM** targets for WebLogic Servers added under the **Default** JVM Pool target. Note that it may take few minutes to see the target status updated. Click the **admin-server_jvm** node.

    ![EM Console, Middleware Home page](images/4-18-emcc.png " ")


    > **NOTE:** You will see the JVM targets appear under a **Default** JVM pool target, and not associated with your OKE WebLogic Domain. This happens because the IP that is registered in the EM is that of the Kubernetes load balancer service, and not of the actual host where JVM runs. You can manually add the association to the WebLogic Domain target, which is explained in the next task.


19. In the JVM target home page, observe that data is coming in to the EMCC.

    ![EM Console, JVM Pool target home page](images/4-19-emcc.png " ")



## **Task 5**: Associate JVM targets with the WebLogic domain


When a JVMD agent is deployed manually to a WebLogic Server in the Kubernetes cluster, JVM targets appear under the **Default** JVM pool target in the EM console, and it is not associated with the WebLogic Domain. In this task, you will manually add associations of the JVM targets to the WebLogic domain target.

1. In EM console, go to the Middleware Home page. Click Default JVM pool target from the table.

    ![EM Console, Middleware Home page, Default JVM pool target node](images/5-1-emcc.png " ")

2.  In the JVM target home page, select **Java Virtual Machine Pool** > **Manage and Troubleshoot JVMD**.

    ![EM Console, Default Pool Target Home page, Target menu](images/5-2-emcc.png " ")

3.  Click Manage Association tab.

    ![EM Console, Default Pool Target Home page, Manage Association](images/5-3-emcc.png " ")

4. Select JVM target of the admin server, then click **Associate**.

    ![EM Console, Default Pool Target Home page, Target Association](images/5-4-emcc.png " ")

5. In the **Select Targets** window, select WebLogic Admin Server target from the OKE-WLS domain, then click **Select**.

    ![EM Console, Default Pool Target Home page, Select Targets](images/5-5-emcc.png " ")

6. Click **OK** on the **Confirmation** window.

    ![EM Console, Default Pool Target Home page, Conformation](images/5-6-emcc.png " ")

7. Repeat the steps 4 to 6 for the managed servers.

    ![EM Console, Default Pool Target Home page, Manage Association](images/5-7-emcc.png " ")

8.  Navigate to the **Middleware** home page and confirm the JVM targets are associated with the OKE-WLS Domain. Now you can remove the empty Default JVM Pool target. Click the **Default** target from the table.  

    ![EM Console, Middleware Home page](images/5-8-emcc.png " ")

9. In the JVM target home page, select **Java Virtual Machine Pool** > **Target Setup** > **Remove Target**.

    ![EM Console, Default Pool Target Home page, Target menu](images/5-9-emcc.png " ")

10. Click **Delete JVM Pool Target** button.

    ![EM Console, Delete Default Pool Target](images/5-10-emcc.png " ")

11. In the Middleware home page, confirm the Default JVM target is removed from the table.

    ![EM Console, Middleware home page](images/5-11-emcc.png " ")



## Conclusions

In this workshop you’ve learned how to add Kubernetes load balancer services to OKE, configure security rules restricted to EM monitoring, set up an EM agent in the Oracle Cloud, remotely discover the WebLogic domain deployed on OKE, and monitor JMX based metrics and configurations from the WebLogic Server targets using EM. You also learned that monitoring of the target continues even after the pods are regenerated, and how to manually set up JVM Diagnostics for the WebLogic Servers on Kubernetes.

Oracle Enterprise Manager Cloud Control is an on-premises based solution that can provide a monitoring solution for Oracle WebLogic Servers deployed either on on-premises, or in a Kubernetes cluster in the Oracle Cloud or in other cloud platforms.

Additionally, you can configure **Oracle Cloud Infrastructure Application Performance Monitoring (APM)** Java Agent and monitor traces and spans of the WebLogic based application runs on Kubernetes. Refer to **[Oracle LiveLabs Use OpenTracing for WebLogic on Kubernetes utilizing Oracle Application Performance Monitoring](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=932)** workshop for details.



## Acknowledgements

* **Author** - Yutaka Takatsu, Product Manager, Enterprise and Cloud Manageability
- **Contributors** -
Rupesh Kumar, Consulting Member of Technical Staff,  
Renjit Clement, Principal Member Technical Staff,  
Ravi Mohan, Senior Software Development Manager,  
Steven Lemme, Senior Principal Product Manager,  
Mahesh Sharma, Consulting Member of Technical Staff,  
Avi Huber, Senior Director, Product Management
* **Last Updated By/Date** - Yutaka Takatsu, March 2022
