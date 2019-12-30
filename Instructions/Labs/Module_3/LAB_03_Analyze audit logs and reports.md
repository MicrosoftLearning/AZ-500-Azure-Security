

# Module 4: Analyze audit logs and reports

## Exercise 1: Get started with SQL database auditing

### Task 0: Lab Setup

1.  Open **PowerShell** and run the following command to deploy a database for the lab.

     ```powershell
    start "https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoftLearning%2FAZ-500-Azure-Security%2Fmaster%2FAllfiles%2FLabs%2FMod4_Lab03%2Fazuredeploy.json" 
     ```

1.  Under **Resource group** click create new and use the default name "**Mod4Lab3**"

1.  You can use the default populated SQL server name

1.  Click **Purchase** 

### Task 1 - Set up auditing for your database

1.  **Navigate** to **Resource Groups**

1.  **Select** your resource group created above ("**Mod3Lab3**" if you chose the same name as the instructions)

1.  **Click** your **SQL Server** name

1.  On the left pane click auditing

1.  **Change** auditing to **ON** from **OFF**.
warning
**Note**: You now have the option to select where you wish audit logs to be writting to.


1.  **Select** all **3 options**, **Storage**, **Log analytics**, **Event hub**.

1.  **Under Storage**, **Click** configure.

1.  **Click subscription** and select your subscription

1.  **Click** storage account

1.  Under create storage account input a unique name (**e.g. Mod4Lab3YOURNAME**)

1.  **Click OK**.

1.  When validated click **OK** agina

1.  Under Log analytics click configure

1.  **Click** create new workspace

1.  Enter the following settings

     |Log Analytics Workspace|Subscription|Resource Group | Location| Pricing   Tier|
     |-----------------------|------------|---------------|---------|   -------------
     |Mod4Lab3YOURNAME|Your Subscription|The RG you created in the lab setup|   East US | Per GB (2018)|

1.  **Click OK**.
warning
**Note**: Setting up Event hub Requires extra steps as the Azure portal does not allow you to create an event hub from this location


1.  To setup an **Event Hub** for configuration click **Azure Cloud Shell** at the top of the **Portal**.

1.  **Enter** the following **Powerhshell Commands**.

     ```powershell
    New-AzEventHubNamespace -ResourceGroupName Mod4Lab3  -NamespaceName     Mod3Lab4 -Location eastus
     ```

     ```powershell
    New-AzEventHub -ResourceGroupName Mod4Lab3 -NamespaceName Mod3Lab4  -EventHubName Mod3Lab4 -MessageRetentionInDays 3
     ```

1.  When these commands have completed click configure under event hubs

1.  **Select** the following information

     | Subscription|Hub Namespace|Hub Name| Hub Policy Name|
     |-------------|-------------|--------|----------------|
     |Your Subscription| Mod3Lab4|mod3lab4|RootManageSharedAccessKey|


1.  **Click OK**

1.  You can now click **Save** on the **Auditing Settings** page

    **Result**: You have now turned on auditing for your SQL Db 


1.  To access the logs return to the **Resource group** where the **SQL Database** and **Server reside**

1.  **Select** the **Mod3Lab3** Log analytics workspace you created erlier

1.  **Click** logs

1.  In the query space enter the following code and **click Run**.

     ```cli
    Event | where Source  == "MSSQLSERVER" 
     ```

1.  You will not see any results, please read the below warning
warning
**Note**: Because we have set up logs on a new database with test data, there are minimnal log available to see, to show how log are displayed in example we can use example log analytics website that is populated with example data to view.


### Task 2 - Analyze audit logs and reports

1.  Visit **`https://portal.loganalytics.io/demo`** in a new web browser tab

1.  In the query space enter the following code and **click Run**.

     ```cli
    Event | where Source  == "MSSQLSERVER" 
     ```

1.  From here you can expand some of the example audit logs to view what they would look like in a live system

1.  In the query space enter the following code and **Click Run**.

     ```cli
    Event 
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1d) 
    | where Source != "HealthService" 
    | where Source != "Microsoft-Windows-DistributedCOM" 
    | summarize count() by Source
     ```

1.  **Click chart**

1.  From here you can review how log data can be displayed as chart data

1.  **Click** the **Stacked Coloumn** drop down and select **Pie**

1.  Here you can see the same data as a different chart

1.  From the top right of the window you can **Click Export** to export the data as **CSV**.

 The query language used by log analytics is called the Kusto query language, the full documentation for this language can be found here **`https://docs.microsoft.com/en-us/azure/kusto/query/`**



**Results**: You have now completed the setup of logs on a SQL database and run queries against the log analytics workspace to view the audit logs that will be generated


