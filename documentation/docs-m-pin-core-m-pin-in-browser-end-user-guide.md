---
content_type: Chunks
title: Docs M-Pin Core - M-Pin In-Browser End-User Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

M-Pin Core & M-Pin SSO users can authenticate into your services using either their browser or mobile phone. This guide is aimed at users who wish to use the browser client, M-Pin-In-Browser™. Please see the [M-Pin-In-Mobile™ End User Guide](/docs/m-pin-core/mpin-in-mobile-end-user-guide) for details on how to use the mobile client.

Note that this guide describes the default M-Pin workflow, but it is possible for this workflow to be customised, in which case you should contact your system administrator for details.  

Also note that you can use the home icon at the top-left of the PIN pad to return to the PIN pad's home page that gives you the choice to authenticate using either your browser or mobile phone.  

## Registration & Verification

When you first visit a site that is protected with M-Pin, you will see the M-Pin PIN pad displaying the following:  

Select “Sign in from here”:

![MBEUG1](\data\assets\images\chunks\MBEUG1.png)

![MBEUG2](\data\assets\images\chunks\MBEUG2.png)

Select “Sign in with browser”:

![MBEUG3](\data\assets\images\chunks\MBEUG3.png)

Enter your email address and optionally change the “Device name” to something meaningful to yourself, e.g. “My Laptop”. Note that “Device Name” will only be visible if your system administrator has set up device revocation. If device revocation has been set up, this is the name you will need to provide to your system administrator if you want to revoke access from this device in the event that it is for example lost or stolen. Once you have entered the correct information, select “Setup M-Pin™”:

![MBEUG4](\data\assets\images\chunks\MBEUG4.png)

You should now receive an email with an activation link. Click the link in the email, then select “Confirm and activate” on the resulting web page. Now you can select “I confirmed my email”. Note that if the email doesn't arrive, you can select “Resend confirmation email” to request that the email is resent to you.

Next, you will be asked to setup your PIN. Please ensure that nobody can see the PIN that you use either when setting it up or when using it, and we also strongly recommend that you don't write it down anywhere.

![MBEUG5](\data\assets\images\chunks\MBEUG5.png)

Enter 4 digits using your mouse, then select “Setup”:

![MBEUG6](\data\assets\images\chunks\MBEUG6.png)

## Authentication

Now that you have created your PIN, you can select “Sign in now” and the PIN pad will be displayed asking you to enter your PIN. The PIN pad will also automatically be displayed requesting your PIN if you revisit the site or refresh your browser. Note that each PIN is tied to the specific browser that you used to register. So, for example, if you wish to use both Chrome and Firefox to authenticate, you will need to register using both browsers. It is up to you whether you use the same PIN on both.

![MBEUG7](\data\assets\images\chunks\MBEUG7.png)

Simply enter your 4-digit PIN then click “Login” to authenticate into your site.

If you enter an incorrect PIN, you will see the following warning:

![MBEUG8](\data\assets\images\chunks\MBEUG8.png)

Please try again with the correct PIN. If you enter an incorrect PIN 3 times, you will see the following warning and you will need to register again:

![MBEUG9](\data\assets\images\chunks\MBEUG9.png)

## Adding A New Identity

If you use different identities to access your service, or if you are sharing your PC with another user, you can add additional identities to the PIN pad. Click the menu icon to the right of your identity to display the account management screen:

![MBEUG10](\data\assets\images\chunks\MBEUG10.png)

Select “Add new identity” and simply proceed setting up the identity as before.  

## Selecting a Different Identity

When the PIN pad asks for your PIN, it also displays the identity that you are about to login as. If you wish to you another identity, select the menu icon, then double-click on the identity that you with to authenticate as:

![MBEUG11](\data\assets\images\chunks\MBEUG11.png)

## Managing an Existing Identity

Select the menu icon then select the pencil icon next to the identity that you wish to manage:

![MBEUG12](\data\assets\images\chunks\MBEUG12.png)

If you have forgotten your PIN, select “Reset PIN”followed by “Yes, Reactivate it” to confirm that you wish to reset your PIN. You will then be sent a confirmation email and you can proceed with the standard registration workflow.  

If you want to remove your identity entirely from the machine - if, for example, you are giving your PC to someone else, simply select “Remove Identity” followed by “Yes, Remove it” to confirm.
