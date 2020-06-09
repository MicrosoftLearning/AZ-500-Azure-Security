# Module 1: Lab 6: Manage Identity and Access 


**Scenario**

In this module, you'll learn about Role-Based Access Control as the foundation to organizing and managing an organization's administrative access based on the principle of least privilege. You will also review Azure Active Directory concepts, as well as gain insight into the threat landscape and security risks that are exposed to IT organizations through breach of privileged access. Lessons include:

- Role-Based Access Control
- Azure Active Directory (Refresher)
- Protecting Privileged Access in the Environment


## Exercise 1: Role-Based Access Control

### Task 1: Create a User

1. Sign in to the Azure portal **`https://portal.azure.com/`**

2. Select **Azure Active Directory** and on the overview blade note down your tenant domain.

     ![Screenshot](../Media/Module-1/11eb6969-8efb-462d-8ef0-772b0d75f360.png)

3. Select **Users**, and then select **New user**.


4. On the **User** page, fill out the blade with the following information:

      - **User name**: bill
      - **Name**: Bill Smith


     ![Screenshot](../Media/Module-1/ba852242-eb76-4ab8-8e92-c4c452e9f9cf.png)

5. Show the auto-generated password provided in the **Password** box. You'll need to give this password to the user for the initial sign-in process.
  
  

6. Select **Create**.

    The user is created and added to your Azure AD tenant.

7. Launch **Azure Cloud Shell** by clicking on the PowerShell icon at the top of the Azure Portal and select PowerShell if prompted then run the following command to connect to AzureAD:

    ```powershell
    Connect-AzureAD
    ```

  
8. **Enter the following commands** to create a user in the PS cloud shell **replacing yourdomain** with your domain noted down erlier

    ```powershell
    $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    ```
    ```powershell
    $PasswordProfile.Password = "Pa55w.rd"
    ```
    ```powershell
    New-AzureADUser -DisplayName "Mark" -PasswordProfile $PasswordProfile     -UserPrincipalName "Mark@yourdomain.onmicrosoft.com" -AccountEnabled $true -MailNickName "Mark"
    ```
 
     ![Screenshot](../Media/Module-1/d5e26f07-a18e-4ae4-84aa-318eac3d5b5b.png)

9. Run the following command to get a list of the users in Azure AD 

    ```powershell
    Get-AzureADUser 
    ```
 
10. Change the Azure cloud shell to azure CLI mode with Bash by using the drop down menu

     ![Screenshot](../Media/Module-1/28fe2e25-5b8b-4e7a-b83d-0bc4702b0b38.png)

11. Enter the following command in **azure CLI** to create a user in Azure CLI **replacing yourdomain** with the domain you noted earlier.

    ```cli
    az ad user create --display-name Tracy --password Pa55w.rd --user-principal-name Tracy@yourdomain.onmicrosoft.com
    ```

You should now have 5 users in your Azure AD


### Task 2: Create Groups In Portal, PowerShell, and CLI

1. In the Azure Portal click **Azure Active Directory**  on the **Azure AD blade** click **Groups** and select **New group**.
 
2. Fill in the details with the following details:
  
      - **Group Type**: Security
      - **Group Name**: Senior Admins Group
      - **Membership Type**: Assigned
    
3. In the Members section, click No Members link and search for and select Bill then click **Select**.

4. Click **Create**

5. Launch the **Cloud Shell** in **Bash** mode by clicking the Cloud Shell icon at the top of the Azure Portal.

6. In the **Cloud Shell** enter the following commands:

    ```cli
    az login
    ```

    ```cli
    az ad group create --display-name ServiceDesk --mail-nickname ServiceDesk
    ```

7. Change the Cloud Shell to **PowerShell** and enter the following command:

    ```powershell
    New-AzureADGroup -DisplayName "Junior Admins" -MailEnabled $false -SecurityEnabled $true -MailNickName JuniorAdmins
    ```
 
8. Exit the **Cloud Shell**.

9. In the **Active Directory blade** click **Groups** and confirm you have **5** groups

     ![Screenshot](../Media/Module-1/c4bf8dc8-e4dc-4603-8961-0cdc0ba57cd5.png)


## Exercise 2: Practice - RBAC

### Task 1: Create a resource group

1. In the navigation list, choose **Resource groups**.

2. Choose **Add** to open the **Resource group** blade.

3. For **Resource group name**, enter **myRBACrg**

4. Select your subscription and the location of **East US**.

5. Choose **Review + create** then **Create** to create the resource group.

6. Choose **Refresh** to refresh the list of resource groups.

  The new resource group appears in your resource groups list.

### Task 2: Grant access


In RBAC, to grant access, you create a role assignment.


1. In the list of **Resource groups**, choose the new **myRBACrg** resource group.

1. Choose **Access control (IAM)** to see the current list of role assignments.

      ![Screenshot](../Media/Module-1/fa866a33-93ac-4cc9-adbd-70b8ece05fa5.png)

1. Choose **Add** to open the **Add role assignment** pane.

    If you don't have permissions to assign roles, you won't see the **Add** option.

1. In the **Role** drop-down list, select **Virtual Machine Contributor**.

1. In the **Select** list, select **Bill Smith**.

1. Choose **Save** to create the role assignment.

  After a few moments, the user is assigned the Virtual Machine Contributor role at the myRBACrg resource group scope.

  
### Task 3: Remove access


In RBAC, to remove access, you remove a role assignment.


1. Click the Role Assignments tab.

1. In the list of role assignments, add a checkmark next to user with the Virtual Machine Contributor role.
  
      ![Screenshot](../Media/Module-1/d821d99b-8a35-431b-aa0e-8e2dac57a168.png)

1. Choose **Remove**.

1. In the remove role assignment message that appears, choose **Yes**.  
   
  
## Exercise 3:  Role-based Access Control (RBAC) using PowerShell


In this exercise you use PowerShell to :

-   Use the `Get-AzRoleAssignment` command to list the role assignments
-   Use the `Remove-AzResourceGroup` command to remove access


### Task 1: Grant access
  

To grant access for the user, you use the New-AzRoleAssignment command to assign a role. You must specify the security principal, role definition, and scope.  


1. Launch the **Cloud Shell PowerShell**.
  
1. Get the ID of your subscription using the **`Get-AzSubscription`** command.
  
    ```powershell
    Get-AzSubscription
    ```

  
1. Save the subscription scope in a variable replacing the 000000's with your subscription ID.
  
    ```powershell
    $subScope = "/subscriptions/00000000-0000-0000-0000-000000000000" 
    ```  
  

  
1. Assign the Reader role to the user at the subscription scope by using the following command (replacing your domain with the tenant domain you noted earlier):
  
    ```powershell
    New-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Reader" -Scope $subScope  
    ```
  
      ![Screenshot](../Media/Module-1/f468a5df-aab2-42db-9e28-7ea25a2262ca.png)
  
1. Assign the Contributor role to the user at the resource group scope using the following command:
  
    ```powershell
    New-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Contributor" -ResourceGroupName "myRBACrg"
    ```

  
### Task 2: List access  
  
1. To verify the access for the subscription, use the Get-AzRoleAssignment command to list the role assignments use the following command:
  
    ```powershell
    Get-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -Scope $subScope
    ```

      ![Screenshot](../Media/Module-1/d190e8c5-ffc7-4638-ad7e-cc2643b972a0.png)

    In the output, you can see that the Reader role has been assigned to the RBAC Tutorial User at the subscription scope.

2. To verify the access for the resource group, use the Get-AzRoleAssignment command to list the role assignments using the following command:
  
    ```powershell
    Get-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com     -ResourceGroupName "myRBACrg"
    ```


 In the output, you can see that both the Contributor and Reader roles have been assigned to the RBAC Tutorial User. The Contributor role is at the myRBACrg resource group scope and the Reader role is inherited at the subscription scope.

### Task 3: Remove access
  

To remove access for users, groups, and applications, use `Remove-AzRoleAssignment` to remove a role assignment.


1. Use the following command to remove the Contributor role assignment for the user at the resource group scope.
  
    ```powershell
    Remove-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Contributor" -ResourceGroupName "myRBACrg"
    ```
  
  
1. Use the following command to remove the Reader role assignment for the user at the subscription scope.

    ```powershell
    Remove-AzRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Reader" -Scope $subScope
    ```
  
  
1. Remove the resource group by running the following command (When prompted to confirm press Y and press enter):
  
    ```powershell
    Remove-AzResourceGroup -Name "myRBACrg"
    ```

1. Close the **Cloud Shell**.  


**Results**: You have now completed this lab.
