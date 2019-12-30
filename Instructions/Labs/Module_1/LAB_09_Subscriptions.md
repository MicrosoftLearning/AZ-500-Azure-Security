# Module 1: Manage Identity and Access 

# Lab 8: Subscriptions


**Scenario**

Occasionally, a need arises for transferring a subscription from an owner to an Azure AD tenant. In order to transfer a subscription from a Azure AD owner to another subscription you need access to another subscription. If you do not have access to multiple subscriptions,
at this time just review the process outlined below.


## Exercise 1: Transfer Azure subscriptions between Azure AD tenants

### Task 1: To transfer the ownership of an Azure subscription

1.  Sign in at the Azure Portal as the account admin.

1.  Navigate to **Cost Management + Billing** > **Subscriptions** and click **Manage**.

     ![Screenshot](../Media/Module-1/24542a01-fb8a-465d-bebf-d5e0d106f56c.png)

2.  Select your subscription.

3.  Verify that your subscription is eligible for self-serve transfer by checking the Offer and Offer ID against the supported offers list.

    **Note**: At the time of writing, Azure Pass - Sponsorship subscriptions are not eligible for transfer.  Follow this guide through for reference.


4.  Select **Transfer subscription**.

     ![Screenshot](../Media/Module-1/6a745f4e-2bc3-4655-8692-65b4f8e6aeed.png)

5.  Specify the recipient.

    **Note**: If you transfer a subscription to a new Azure AD tenant, all role assignments in RBAC61 will be permanently deleted from the source tenant and not migrated to the target tenant.


     ![Screenshot](../Media/Module-1/077262ca-0d4d-43d6-bb9e-3580912a8589.png)

6.  The recipient automatically gets an email with an acceptance link.
7.  The recipient selects the link and follows the instructions, including entering their payment information

     ![Screenshot](../Media/Module-1/a72dc585-b813-4823-9370-00e92b0b8f00.png)

8.  Azure completes the subscription transfer.

 At this point, billing ownership of the Azure subscription, would be transfer to the new subscription.


**Results**: You have now completed this module.