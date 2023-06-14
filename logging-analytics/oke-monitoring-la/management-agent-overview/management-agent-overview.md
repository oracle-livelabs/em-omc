# Get Familiar with Management Agent Cloud Service UI


## Objectives

In this lab, you will get familiarized with:
* Navigating to Management Agent Service
* Navigating to the Agent Home Page to view its health
* Generating an Install Key for use with Management Agents (Optional)
* Downloading an Install Key file (Optional)

Estimated Time: 5 minutes

## **Task 1:**  Navigating to Management Agent Service

To navigate to the Management Agent Service, follow one of the below two methods.

1. From Navigation Menu ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Management Agent** > **Overview**.
![navigate-to-management-agent](./images/navigate-to-management-agent.gif " ")

2. You can also copy-paste the following link in your browser's address bar to navigate to the Agent Home page.
    ```
         <copy>
            https://cloud.oracle.com/macs?region=us-ashburn-1
         </copy>   
    ```

## **Task 2:**  Navigate to the Agent Home page
Agent Home page will provide diagnostic and health information for the Agent.

Overview of all the agents and alarms in a compartment can be viewed by clicking on the highlighted section.
![agent-overview](images/agent-overview.png "Agent Overviewe")

Click on the highlighted sections to select the agent whose health information you want to view.
![navigate-agent-homepage](images/navigate-agent-homepage-2.png "Navigate to Agent Homepage")

The Agent Home Page provides the availability information for the agent along with some key metrics as shown in this snapshot.
![agent-homepage](images/agent-homepage-2.png "Agent Homepage")



## **Task 3:**  Generating an Install Key for use with Management Agents (Optional)
The following task is optional as the install key will be generated for you.  If you are installing the agent outside the lab environment then you will need to generated for you to use in the lab

Install Key is needed to register the agent with Management Agent Cloud Service.  The key lets the Management Agent Cloud Service know  how many agents are permitted to be installed.  The key can be made restritive: to allow a certain number of agents within a set number of days or can be made unrestricted (unlimited). This key is used only once by the Management Agent during the registration process. 

**Note:** The install key is only used for registration.  Once the agent is installed using a key, the agent functionality is not affected even if the install key expires.

![create-install-key](images/create-install-key.png "Create Install Key")

1. **Key name** to use for the Install key.

2. **Compartment** picker to choose the compartment to use for the Management Agents.

3. **Maximum Installations** to limit the Management Agents that can be installed using this install key.

4. **Valid for** to pick the duration for which Management Agents installations will be allowed using this install key.

5. **Unlimited** checkbox to make this install key unrestricted which will allow unlimited agent installations and the install key will not expire.

## **Task 4:**  Download Install Key File (Optional)
The following task is optional as the install key will be generated for you to use in the lab.  If you are installing the agent outside the lab environment then you will need to generate and use an install key.

The install key that was created in Task 2 can be downloaded and provided to the agent during installation.
![download-install-key](images/download-install-key.png "Download Install Key")

## Acknowledgements
* **Author** - Nirav Gandhi , OCI Management Agent
* **Contributors** -  Zubair Ansari, Nirav Gandhi, Madhavan Arnise Thangaraj, OCI Management Agent
* **Last Updated By/Date** - Nirav Gandhi, June 2023