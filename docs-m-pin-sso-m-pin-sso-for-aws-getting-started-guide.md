---
content_type: Chunks
title: Docs M-Pin SSO - M-Pin SSO for AWS - Getting Started Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

This section explains the steps that are required to make your M-Pin SSO instance fully operational and manageable by users with administrative privileges. The guide assumes you have created and accessed your M-Pin SSO initial-setup account (as explained in M-Pin SSO for AWS Product Access Instructions). Note that until your first admin user of the system has been created, only the initial-setup account can be accessed and only with the device-browser combination and credentials with which it has been accessed for the first time.

## Creating and Configuring Your First Admin User

To create and configure your first admin user:

1.  (_Conditional_) If you have signed out, **sign in to the initial-setup account**.
    To sign in, with your browser, access the M-Pin SSO Sign-in page of the instance at this URL
     http://HOS
    where HOST is the Public DNS or Public IP address of your M-Pin SSO instance. (The Public DNS or Public IP of the instance can be found on your AWS EC2 management console.

    The page will display the M-Pin PIN Pad with the initial-setup account pre-selected.

     ![Enter your M-Pin](\data\assets\images\chunks\ssogsg1.png "Enter your M-Pin")
    Sign-in with your Pin. You will be taken to the web-based management interface.

    ![Management Portal](\data\assets\images\chunks\ssogsg2.png "Management Portal")
    
    **Note:**
     You can sign in to the initial-setup account repeatedly but only from the device and with the browser from which you have accessed it for the first time. If this device or browser becomes unavailable for some reason, you'll have to terminate this M-Pin SSO instance and create a new one.
2.  **Configure the SMTP server**.
     The email sending capability is needed for validating the email addresses with which the users will sign up, so this is a pre-requisite for creating your first admin user. To configure the SMTP server:

1.  **Access the Server Settings screen** .
     (Administration > Global Settings section >Server settings)
2.  In the Server Settings screen, **configure the SMTP-related options**.

    ![Edit settings](\data\assets\images\chunks\ssogsg3.png "Edit settings")

4.  **Create at least one user with administrative privileges**
     Following the sub-steps below, create one or more users with administrator privileges

    1.  **Create the user**.
        A new user is created by accessing the Sign-in page either by using another browser or by logging out the initial-setup user (by clicking on the name of this user at the top-right and selecting **LOG OUT**). The new user needs to provide a valid email address, and create a PIN after email verification. This can be either you providing your email address or another person in your organization; the important thing is to be able to do the email verification so the process could continue.
         The user needs to access the M-Pin SSO Sign-in page and use the _Add new identity_ functionality of the PIN Pad to provide their email as shown below.
         ![Use Pin Pad to authenticate](\data\assets\images\chunks\ssogsg4.png "Use Pin Pad to authenticate")
        ![Add a new identity to the pin pad](\data\assets\images\chunks\ssogsg5.png "Add a new identity to the pin pad")
        ![enter your identitity](\data\assets\images\chunks\ssogsg6.png "enter your identitity")
        Once the email address has been validated (by accessing the link provided in the verification email message), the user needs to access the Sign-in page again to create their PIN. Upon PIN creation, the new user will be listed in the M-Pin SSO’s web-based management interface. (Administration > M-Pin SSO Settings section > Users). Note that you will not be able to access this part of the interface whilst logged in as the new user as this new account does not yet have administrative privileges.
    2.  **Grant administrative privileges to the user**.
         To do this:
        1.  Logout from your new user’s account, then log back in as the **initial-setup** account using the original PIN you created. (Use the menu icon at the top-right of the PIN pad to display available identities and double-click on the **initial-setup** identity to select it.
        2.  **Access the Select User to Change screen**. (Administration > M-Pin SSO Settings section > Users)![Select a user to change](\data\assets\images\chunks\ssogsg7.png "Select a user to change")
        3.  **Click the user's name** (which is actually a link) to access the Change User screen.
        4.  In the Change User screen, **check the _Staff status_ and _Superuser status_ boxes**. (The _Active_ box must remain checked.)

            ![Change user status](\data\assets\images\chunks\ssogsg8.png "Change user status")
        5.  Save your changes.
5.  (_Optional_) **Delete the initial-setup account**.
    Once you have one or more users with administrative privileges, you can safely delete the **initial-setup** account. (Administration > Users, select the **initial-setup** identity, then scroll to the bottom of the page and select ‘Delete’ followed by ‘Yes, I’m sure’) This will delete the **initial-setup** user and log you out (if you were logged in as this user). You will also notice that the initial-setup user account is still in the PIN pad. You can remove it by accessing the account management page of the PIN pad (click the menu icon at the top-right), then click the pencil icon next to the **initial-setup** user, followed by **Remove Identity** and **Yes, Remove it**.
