



# Module 4: Classify a SQL Database 

## Exercise 1: Classify your SQL Database

### Task 1: Lab Setup

1.  Open **PowerShell** and run the following command:

     ```powershell
    start "https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoftLearning%2FAZ-500-Azure-Security%2Fmaster%2FAllfiles%2FLabs%2FMod4_Lab01%2Fazuredeploy.json" 
     ```

1.  Under **Resource group** click create new and use the default name "**Mod4Lab1**"

1.  You can use the default **populated SQL server** name

1.  Click **Purchase**. 
warning
**Note**: You must wait for the SQL database with the test data to deploy




1.  Sign-in to the Azure portal.

1.  **Select** the resource group of **Mod4Lab1**

1.  Click **az500labserver**

1.  Under the **Security heading** in the **Azure SQL Database** pane, navigate to **Advanced Data Security**.

1.  Select **ON** under **Advanced Data Security**

1.  **Click Save**

1.  Return to the **Mod4Lab1** resource group

1.  **Select** the **SQL databse AZ500LabDb (az500labserver/AZ500LabDb)**

1.  **Click** Advanced Data Security again 

1.  **Click** the bar at the top **Complete Advanced Data Security setup vy selecting a storage account for Vulnerability Assesment**

1.  Make sure the option for **Advanced Data Security** is set to **On** 

1.  **Click** storage account

1.  **Click** create new

1.  For the name use "**Mod4Lab1YOURNAME**" replacing **YOURNAME** with your name to make it unique but memorable

1.  You can optionally enter your email address here to have scan reports emailed to you when complete

1.  **Select** the save option

1.  **Return** to the previous **Advanced Data Security** pane

1.  **Select** the **Data discovery** and **classification** (**preview**) card.

## Exercise 2: Begin Classification

1.  To begin classifying your data, select the **Classification tab** at the top of the window.

1.  The classification engine scans your database for columns containing potentially sensitive data and provides a list of recommended column classifications.

1.  To view and apply classification recommendations:

   - View the list. To view the list of recommended column classifications, select the **r ecommendations** panel at the bottom of the window. (**Blue Bar**)   
   <br/>
1.  **Click** accept all in the top left to select all reccomendations

  - To manually classify columns as an alternative to or in addition to the recommendation-based classification, in the top menu of the window, select Add classification.

  - In the Add classification blade, configure the five fields that display, and then select Add classification:
     - **Schema name**
     - **Table name**
     - **Column name**
     - **Information type**
     - **Sensitivity label.**
<br/>
1.  **Click Accept Selected Reccomendations**

1.  To complete your classification and persistently label (**tag**) the database columns with the new classification metadata, in the top menu of the window, select **Save**. 

1.  Upon returning to the **Advanced Data Security** pane you will be able to see in the overview pane for Data classification an overview of the data that was classified.


**Results**: You have now classified information in a SQL database on Azure for GPDR and data protection compliance




