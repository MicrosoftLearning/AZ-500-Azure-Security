# Module 4: Lab 6 - Security Playbook in Azure Sentinel


A security playbook is a collection of procedures that can be run from Azure Sentinel in response to an alert. A security playbook can help automate and orchestrate your response, and can be run manually or set to run automatically when specific alerts are triggered. Security playbooks in Azure Sentinel are based on Azure Logic Apps, which means that you get all the power, customizability, and built-in templates of Logic Apps. Each playbook is created for the specific subscription you choose, but when you look at the Playbooks page, you will see all the playbooks across any selected subscriptions.

## Exercise 1: Create and manage a Security Playbook in Azure.

### Task 1: How to create a security playbook.


Follow these steps to create a new security playbook in Azure Sentinel:


1.  Open **Azure Sentinel** dashboard.

2. Under **Management**, select **Playbooks**.

   ![Screenshot](../Media/Module-3/playbookimg.png)

3. In the **Azure Sentinel - Playbooks (Preview)** page, click **Add** button.

   ![Screenshot](../Media/Module-3/create-playbook.png) 

4. In the **Create Logic app** page, type the requested information to create your new logic app, and click **Create**. 

5. In the **Logic App Designer** select the template you want to use. If you select a template that necessitates credentials, you will have to provide them. Alternatively, you can create a new blank playbook from scratch. Select **Blank Logic App**. 

   ![Screenshot](../Media/Module-3/playbook-template.png)

6. You are taken to the Logic App Designer where you can either build new or edit the template. For more information on creating a playbook with Logic Apps].

7. If you are creating a blank playbook, in the **Search all connectors and triggers** field, type *Azure Sentinel*, and select **When a response to an Azure Sentinel alert is triggered**. 
   
   After it is created, the new playbook appears in the **Playbooks** list. If it doesn’t appear, click **Refresh**.

8.  Use the **Get entities** functions, which enable you to get the relevant entities from inside the **Entities** list, such as accounts, IP addresses and hosts. This will enable you to run actions on specific entities.

9.  Now you can define what happens when you trigger the playbook. You can add an action, logical condition, switch case conditions, or loops.

    !![Screenshot](../Media/Module-3/logic-app.png)

### Task 2: How to run a security playbook

You can run a playbook on demand.

To run a playbook on-demand:

1. In the **incidents** page, select an incident and click on **View full details**.

2. In the **Alerts** tab, click on the alert you want to run the playbook on, and scroll all the way to the right and click **View playbooks** and select a playbook to **run** from the list of available playbooks on the subscription. 



## Exercise 2:  Automate threat responses

SIEM/SOC teams can be inundated with security alerts on a regular basis. The volume of alerts generated is so huge, that available security admins are overwhelmed. This results all too often in situations where many alerts can't be investigated, leaving the organization vulnerable to attacks that go unnoticed. 

Many, if not most, of these alerts conform to recurring patterns that can be addressed by specific and defined remediation actions. Azure Sentinel already enables you to define your remediation in playbooks. It is also possible to set real-time automation as part of your playbook definition to enable you to fully automate a defined response to particular security alerts. Using real-time automation, response teams can significantly reduce their workload by fully automating the routine responses to recurring types of alerts, allowing you to concentrate more on unique alerts, analyzing patterns, threat hunting, and more.

### Task 1: Automate Responses

1. Select the alert for which you want to automate the response.
1. In the **Edit alert rule** page, under **Real-time automation**, choose the **Triggered playbook** you want to run when this alert rule is matched.
1. Select **Save**.

   ![Screenshot](../Media/Module-3/rt-configuration.png)




**Results**: In this lab, you learned how to use playbooks in Azure Sentinel.

