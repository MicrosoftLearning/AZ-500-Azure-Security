

# Module 4: Auditing a Database

## Exercise 1: Enable auditing on your database

### Task 1: Lab Setup

1.  Open **PowerShell** and run the following command to deploy a database for the lab:

     ```powershell
    start "https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoftLearning%2FAZ-500-Azure-Security%2Fmaster%2FAllfiles%2FLabs%2FMod4_Lab02%2Fazuredeploy.json" 
     ```

1.  **Under Resource** group click create new and use the default name "**Mod4Lab2**"

1.  You can use the default populated SQL server name

1.  Click **Purchase**
warning
**Note**: You must wait for the SQL database with the test data to deploy

### Task 2: Enable auditing on your databasease

1.  Select your resource group created in the lab setup

2.  **Select** the SQL server **az500labserver2**

3.  **Under Security**, select **Auditing**

4.  **Switch Auditing** to **ON**.

5.  Select storage as the location to send the audit logs to

6.  **Click configure**

7.  Select **Your Subscription**

8.  **Click Create New**.

9.  Name the subscription "**mod4lab2YOURNAME**" to create a unique name

10. **Click OK**.

11. Change the retention days to **5** and click **OK** 

12. Click **Save** to save the **auditing configuration**

## Exercise 2: Review audit logs

### Task 1: Review audit logs on the SQL DB.

1.  To review audit logs for a database return to the resource group created in the lab setup

1.  Click **AZ500LabDb (az500labserver2/AZ500LabDb)** to select your test database

1.  Click **Auditing**
warning
**Note**: that the Auditing looks off here but it is set on the underlying server level so it is turned on for this database


1.  **Click** view **Audit Log**.
warning
**Note**:This is where you will review the output of the audit logs of the Db including any attempted SQL injections, since this is a test database that has been created not log ago the will be minimal audits if any in the log at the current time.
If server auditing is enabled, the database-configured audit will exist side-by-side with the server audit.
Notice that you can select for audit logs to be written to an Azure storage account, to a Log Analytics workspace for consumption by Azure Monitor logs, or to event hub for consumption using an event hub. You can configure any combination of these options, and audit logs will be written to each.



**Results**: You have now setup up auditing on a SQL database and reviewed where to view the auditing output
