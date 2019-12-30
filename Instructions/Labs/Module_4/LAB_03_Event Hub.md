# Module 4: Lab 3 - Event hub


Connect sending and receiving applications with Event Hubs so you can handle extremely high loads without losing data.

In this lab, you will:

- Create an Event Hub using the Azure portal
- Configure applications to send or receive messages through an Event Hub
- Evaluate Event Hub performance using the Azure portal

## Exercise 1: Implementing Event Hub

### Task 1: Enabling Event Hubs Namespace

1.  Log into the Azure portal

2.  In the search bar type **Event Hubs** and select **Event Hubs**

3.  Click **add** to add a new Event Hubs Namespace

    - Populate the fields with the following details:

       - **Name** : yourUniqueName
       - **Pricing Tier** : Standard
       - **Subscription**: yourSubscription
       - **Resource group**: Create New with name "EventHubRG"
       - **Location**: East US
       - **Throughput Units**: 2

4.  Click **create**

### Task 2: Create a storage account for later user


**Note**: We also need to create a storage account and a blob store container to store events that will be sent to the Event Hubs later on


1.  Search for **Storage Accounts** in the search bar and click on **Storage Accounts**

2.  Click **Add**
3.  Choose the Resource Group of **EventHubsRG** (Or the name of your resource group if you chose to use another)
4.  Set the following options:

      - **Storage Account Name**: uniqueName (unique across all of azure)
      - **location**: east US
      - **Performance**: Standard
      - **Account Kind**: General purpose v2
      - **Replication**: Locally-redundent storage (LRS)
      - **Access tier**: Hot

5.  Click **review+create** then click **create**

6.  Wait for the storage account to **create**
7.  Return to storage accounts
8.  select the storage account you created
9.  in the overview pane click **Blobs**
10.  Click **+Container**
11.  For the name type **events**
12.  set the **Public Access Level to Container**
13.  Click OK

### Task 3: Create new event hub

1.  Return to event Hubs click the name of your newly created Event Hub namespace

2.  In the event hub namespace click **Event Hubs** underneath Entities in the selection pane

3.  Click **+Event Hub**

4.  Enter the name of "events"

5.  Click **on** underneath **capture**

    **Note**: This will turn on the dumping of events to the Blob store we created erlier


6.  Click Select **Container**

7.  Select the **storage account name you created erlier**

8.  Select the **blob storage name you created erlier**

9.  click **select**

10.  Click **create**

### Task 4: Collect data to be able to send events into event hubs

1.  Under event hubs namespace click **Shared access policies**

2.  Click **RootManageSharedAccessKey**

3.  Click the copy to clipboard icon next to Primary Key

4.  Open notepad and paste it in there for later use 

5.  Copy the name of the Event Hubs namespace and the name of the Event Hub you created to the same notepad document

**Note**: You will need this primary key and other information for the scripts that will be run later to enter some data into the event hubs system


### Task 5: Download the script files


We will now download the scripts that will be used to create some events to be sent into the Event Hub, this will simulate the Event Hub receiving data from an application in the environment that has been written to communicate with Event Hubs, or from other systems that communicate with Azure Event Hubs. The script files have been developed and published on the PowerShell gallery


1.  Open **PowerShell as administrator** (right click on the PowerShell icaon) and run the following command

     ```powershell
    install-script get-blobevents, send-blobevents
     ```

**Note**: If prompted confirm the installation. The script files have now been downloaded and are available for use in PowerShell


### Task 6: Send some events to Event Hub


For this section you will need the primary key copied from the portal erlier


1.  Open PowerShell

2.  Run the following command 

     ```powershell
    send-blobevents
     ```

3.  This command will prompt you to enter the following data:

      - **primaryKey**:        your primary key copied earlier in the lab
      - **eventhubnamespace**: the name of your namespace
      - **eventhub**:          the name of your event hub
      - **numberOfEvents**:    10 (you can choose more, but they will take longer to send to the Event Hub)
  

If you recieve a series if **401 Unauthorised errors** from the script check the clock on the machine you have executed the code, if using a virtual machine it should be set to UTC. If you have corrected the time you will need to restart the PowerShell shell and re-run the code.


**Note**: This will send a series of events to the Event Hub with randomised data


### Task 7: Review the Events in EventHub and Blob Storage

1.  Return to Event Hubs and your **Event hubs namespace**

2.  Click **Event Hubs** and select your **Event Hub**

3.  In the overview pane review the Event Hub graphs to see the data spikes on incoming messages

4.  Search for and open **Storage Accounts**

5.  Select your **event hubs Storage Account**

6.  Click **Blobs**

7.  Open your **Blob containter** for events storage

**Information**: Here you can review the raw .avro events that have been created by the Event Hubs system, for more information about the .avro format used by Event Hubs see the following wiki article **`https://en.wikipedia.org/wiki/Apache_Avro`**


### Task 8: Review the Events from a REST query to the Blob storage

1.  Launch **PowerShell**

2.  run **get-blobevents** and enter the following when prompted:

  - **blobName**: Name of the storage account
  - **containterName**: Name of the Blob container where the events are stored
</br>

**Note**: You can see this information in your storage account. The script will make a REST query to the Blob storage to list out all the .avro event that are in the storage Blob

| WARNING: Prior to continuting you should remove all resources used for this lab.  To do this in the **Azure Portal** click **Resource groups**.  Select any resources groups you have created.  On the resource group blade click **Delete Resource group**, enter the Resource Group Name and click **Delete**.  Repeat the process for any additional Resource Groups you may have created. **Failure to do this may cause issues with other labs.** |
| --- |


**Results**: You have now completed this lab and can move onto the next lab in the series

