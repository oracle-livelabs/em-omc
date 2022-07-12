# Initialize Environment

## Introduction

In this lab we will review and startup all components required to successfully run this workshop.

*Estimated Time:* 10 Minutes.

Watch the video below for a quick walk through of the lab.

[](youtube:6BD2Z4zzEhI)

### Objectives
- Initialize the workshop environment.

### Prerequisites
This lab assumes you have:
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup

## Task 1: Validate That Required Processes are Up and Running.
1. Now with access to your remote desktop session, proceed as indicated below to validate your environment before you start executing the subsequent labs. The following Processes should be up and running:

    - Database Listeners
        - LISTENER
        - LISTENER_1522
        - LISTENER_1523
        - LISTENER_1524
        - LISTENER_1525
    - Database Server Instances
        - emrep
        - sales
        - finance
        - hr
        - cdb186
        - db19c
    - Enterprise Manager - Management server (OMS)
    - Enterprise Manager - Management Agent (emagent)

2. On the browser window on the right preloaded with *Enterprise Manager*, click on the *Username*  and login with the credentials provided below.
(If the browser shows any certificate authority invalid error code, click on *Advanced* and add the exception to proceed as outlined in Appendix 2)

    ```
    Username: <copy>sysman</copy>
    ```
    ```
    Password: <copy>welcome1</copy>
    ```

    ![](images/em-login.png " ")

    If the login page is not functioning properly (Please note that it takes up to 15 minutes after instance provisioning for all processes to fully start), open a terminal session and restart Enterprise Manager Services (OMS and emagent).

    ```
    <copy>
    sudo systemctl restart oracle-emcc
    </copy>
    ```


3. Confirm successful login. Please note that it takes up to 15 minutes after instance provisioning for all processes to fully start.

    ![](images/em-landing-new.png " ")

    If successful, the page above is displayed and as a result your environment is now ready.
    You should see 5 databases down in the EM Page. If you see more databases down, then follow step 4 to bring them up.

4. If you are still unable to login or the login page is not functioning after reloading from the *Workshop Links* bookmark folder, open a terminal session and proceed as indicated below to validate the services.

    - Database services (All databases and Standard Listener)

    ```
    <copy>
    systemctl status oracle-database
    </copy>
    ```

    ![](images/db-service-status.png " ")
    ![](images/db-service-status2.png " ")

    - Listener Service (Non-Standard)

    ```
    <copy>
    systemctl status oracle-db-listener
    </copy>
    ```

    ![](images/listener-service-status.png " ")

    - Enterprise Manager Services (OMS and emagent)

    ```
    <copy>
    systemctl status oracle-emcc
    </copy>
    ```

    ![](images/em-service-status.png " ")

5. If you see questionable output(s), failure or down component(s), restart the corresponding service(s) accordingly

    - Database and Listener

    ```
    <copy>
    sudo systemctl restart oracle-database
    sudo systemctl restart oracle-db-listener
    </copy>
    ```

    - Enterprise Manager Services (OMS and emagent)

    ```
    <copy>
    sudo systemctl restart oracle-emcc
    </copy>
    ```

6. Validate *emcli* connectivity. From the terminal session on your remote desktop, run as user *oracle*

    ```
    <copy>
    . ~/.occ_oms.sh
    emcli login -username=sysman -password=welcome1
    </copy>
    ```

## Task 2: Initialize Enterprise Manager

### **Generate SSH Keys**

1. From your remote desktop session, open a terminal window and run the following to generate the key pair

    ```
    <copy>
    cd ~
    ssh-keygen -b 2048 -t rsa
    </copy>
    ```

2. Accept defaults for file and passphrase by pressing *Enter* three times to create a key with no passphrase.

    ![](images/ssh-key-gen.png " ")

3.  Update *`~/.ssh/authorized_keys`* and copy the *private key* to */tmp*.

    ```
    <copy>
    cd .ssh
    cat id_rsa >/tmp/rsa_priv
    cat id_rsa.pub >>authorized_keys
    </copy>
    ```

    ![](images/update_ssh_creds-0.png " ")

### **Update the Named Credentials with the new SSH Key**

4. From the EM Console as *SYSMAN*, navigate to "***(1) Setup menu >> (2) Security>> (3) Named Credential***" and Select ***(4) ROOT*** credential. Click ***(5) Edit***

5. Replace the existing entry with the *SSH Private Key* you copied to *"/tmp"*. Keep the General section unchanged and update the *Credential Properties* as followed:

    - Username: *oracle*
    - Delete any content from *SSH Public Key* Textbox
    - Click *Browse* to select the *Private Key*

    ![](images/update_ssh_creds-1.png " ")

6. On the file browser, navigate to *"+Other Locations >> tmp"* and select the file *rsa_priv*

    ![](images/update_ssh_creds-2.png " ")

7. Click *Test and Save*

    ![](images/update_ssh_creds-3.png " ")
    ![](images/update_ssh_creds-4.png " ")

8. Setup oracle Named Credentials using Job System. This will set up the user oracle password on the host and update the Named Credentials used in this workshop.
Navigate to "***Enterprise >> Job >> Library***" and select "SETUP ORACLE CREDENTIALS"; Click Submit.

    ![](images/named_creds_job.jpg " ")

9. Click Submit again on the Job submission Page

    ![](images/named_creds_job_submit.jpg " ")

10. The Job will be submitted successfully. Click on SETUP ORACLE CREDENTIALS Job link to view the Job

    ![](images/submitted.jpg " ")

11. The Job should show Status **Succeeded**

    ![](images/named_creds_job_succeeded.jpg " ")

## Appendix 1: Managing Startup Services

1. Database services (All databases and Standard Listener)

    - Start

    ```
    <copy>sudo systemctl start oracle-database</copy>
    ```

    - Stop

    ```
    <copy>sudo systemctl stop oracle-database</copy>
    ```

    - Status

    ```
    <copy>systemctl status oracle-database</copy>
    ```

    - Restart

    ```
    <copy>sudo systemctl restart oracle-database</copy>
    ```

2. Listener Service (Non-Standard)

    - Start

    ```
    <copy>sudo systemctl start oracle-db-listener</copy>
    ```

    - Stop

    ```
    <copy>sudo systemctl stop oracle-db-listener</copy>
    ```

    - Status

    ```
    <copy>systemctl status oracle-db-listener</copy>
    ```

    - Restart

    ```
    <copy>sudo systemctl restart oracle-db-listener</copy>
    ```

3. Enterprise Manager Service (OMS and emagent)

    - Start

    ```
    <copy>sudo systemctl start oracle-emcc</copy>
    ```

    - Stop

    ```
    <copy>sudo systemctl stop oracle-emcc</copy>
    ```

    - Status

    ```
    <copy>systemctl status oracle-emcc</copy>
    ```

    - Restart

    ```
    <copy>sudo systemctl restart oracle-emcc</copy>
    ```

You may now proceed to the next lab.

## Appendix 2: External Web Access

If for any reason you want to login from a location that is external to your remote desktop session such as your workstation/laptop, then refer to the details below.

1.  Enterprise Manager 13c Console

    ```
    Username: <copy>sysman</copy>
    ```
    ```
    Password: <copy>welcome1</copy>
    ```
    ```
    URL: <copy>https://<Your Instance public_ip>:7803/em</copy>
    ```

    *Note:* You may see an error on the browser while accessing the Web Console - “*Your connection is not private*” as shown below. Ignore and add the exception to proceed.

    ![](images/login-em-external-1.png " ")
    ![](images/login-em-external-2.png " ")

<!-- ## Appendix 3: External Terminal Access (using SSH Key Based Authentication)

While you will only need the browser to perform all tasks included in this workshop, you can optionally use your preferred SSH client to connect to the instance should you prefer to run SSH Terminal tasks from a local client (e.g. Putty, MobaXterm, MacOS Terminal, etc.) or need to perform any troubleshooting task such as restarting processes, rebooting the instance, or just look around.

1. Refer to *Lab Environment Setup* for detailed instructions relevant to your SSH client type (e.g. Putty on Windows or Native such as terminal on Mac OS):

    - From the web session where you completed your provisioning request, do:
        - For **Reserve Workshop on LiveLabs** - Navigate to "*My Reservations* >> *Launch Workshop* >> *Workshop Instructions* >> *Lab: Environment Setup*"
        - For **Launch Free Trial Workshop** and **Run on Your Tenancy** - Click on the corresponding provisioning option and open *Lab: Environment Setup*
    - Authentication OS User - “*opc*”
    - Authentication method - *SSH RSA Key*
    - OS User – “*oracle*”.

2. First login as “*opc*” using your SSH Private Key

3. Then sudo to “*oracle*”. E.g.

    ```
    <copy>sudo su - oracle</copy>
    ``` -->

## Acknowledgements
  - **Author** - Rene Fontcha, LiveLabs Platform Lead, NA Technology
  - **Contributors** - Ashish Kumar
  - **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, July 2021
