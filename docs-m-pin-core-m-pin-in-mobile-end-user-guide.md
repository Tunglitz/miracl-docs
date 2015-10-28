---
content_type: Chunks
title: Docs M-Pin Core - M-Pin Mobile End-User Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

M-Pin Core & M-Pin SSO users can authenticate into your services using either their browser or mobile phone. This guide is aimed at users who wish to use the mobile client, M-Pin-In-Mobile™. Please see the [M-Pin-In-Browser™ End User Guide](/docs/m-pin-core/mpin-in-browser-end-user-guide) for details on how to use the mobile client.

Note that this guide describes the default M-Pin workflow, but it is possible for this workflow to be customised, in which case you should contact your system administrator for details.

Also note that the workflow described below is for the case when you want to login to a site using your PC's browser, but wish to use your mobile device as the authentication. This is particularly useful when using a shared or untrusted PC as firstly you don't enter any credentials into the PC's browser which could be captured by malware, and secondly, you don't leave your identity on the PC.

## Registration

When you first visit a page that is protected by M-Pin using your PC's browser, you will see the M-Pin PIN pad as follows:

![MMEUG1](\data\assets\images\chunks\MMEUG1.png)

Select “Setup your phone”:

![MMEUG2](\data\assets\images\chunks\MMEUG2.png)

If your mobile phone has a QR code reader, you can use it to launch the M-Pin-In-Mobile site. If not, simply enter the URL below the QR code into the browser on your mobile phone:

![MMEUG3](\data\assets\images\chunks\MMEUG3.png)

Follow the instructions to add the M-Pin-In-Mobile app to your phone's home screen. Note that this step refers to running M-Pin-In-Mobile on an Apple iOS device. On other phones, instead of adding the app to your homescreen, simply bookmark the page in your phone's browser. Some other mobile browsers will then allow you to add an icon to this bookmark to your phone's home screen for easy access.

Now when you launch the app from your home screen, you will see the following screen:

![MMEUG4](\data\assets\images\chunks\MMEUG4.jpg)

Enter your email address and optionally change the “Device name” to something meaningful to yourself, e.g. “My Laptop”. Note that “Device Name” will only be visible if your system administrator has set up device revocation. If device revocation has been set up, this is the name you will need to provide to your system administrator if you want to revoke access from this device in the event that it is for example lost or stolen. Once you have entered the correct information, select “Setup M-Pin™”:

![MMEUG5](\data\assets\images\chunks\MMEUG5.jpg)

You should now receive an email with an activation link. Click the link in the email, then select “Confirm and activate” on the resulting web page. Note that you don't need to access the confirmation email and link on the same device that you are registering. Now you can select “I confirmed my email”. Note that if the email doesn't arrive, you can select “Resend confirmation email” to request that the email is resent to you.

Next, you will be asked to setup your PIN. Please ensure that nobody can see the PIN that you use either when setting it up or when using it, and we also strongly recommend that you don't write it down anywhere.

![MMEUG6](\data\assets\images\chunks\MMEUG6.jpg)

Enter you 4-digit PIN, then select “SETUP” to complete the registration process:

![MMEUG7](\data\assets\images\chunks\MMEUG7.jpg)

## Authentication

Now that you have registered your mobile device, you can select “Sign in with this M-Pin” and it will ask for an “access number”:

![MMEUG8](\data\assets\images\chunks\MMEUG8.jpg)

Now return to the PIN pad on your PC's browser and select “Sign in with Phone”:

![MMEUG9](\data\assets\images\chunks\MMEUG9.png)

Now you need to enter the 7-digit access number displayed on your PC's browser into the M-Pin-In-Mobile app. Note that this access number is only valid for 99 seconds and the countdown in the centre of the screen shows you how much time is left.

If you enter the access number incorrectly, you will see the following warning screen:

![MMEUG10](\data\assets\images\chunks\MMEUG10.jpg)

Please try again with the correct access number.
Once you have entered the access number into your phone, click “Next” and it will ask you to enter your personal PIN:

![MMEUG11](\data\assets\images\chunks\MMEUG11.jpg)

If you enter an incorrect PIN, you will see the following warning screen:

![MMEUG12](\data\assets\images\chunks\MMEUG12.jpg)

Please try again with the correct PIN. If you enter an incorrect PIN 3 times, you will see the following message and you will need to register again:

![MMEUG13](\data\assets\images\chunks\MMEUG13.jpg)

When you enter your correct PIN then select “Login”, you will be logged into the site on your PC's browser and you will see a confirmation screen on your mobile device:

![MMEUG14](\data\assets\images\chunks\MMEUG14.jpg)

Note that you can also log out of the session on your PC's browser by clicking “Sign out” on your mobile device.

## Adding A New Identity

If you use different identities to access your service, or if you are sharing your PC with another user, you can add additional identities to the PIN pad. Click the menu icon to the right of your identity to display the account management screen:

![MMEUG15](\data\assets\images\chunks\MMEUG15.jpg)

Select “Add new identity” and simply proceed setting up the identity as before.

## Selecting a Different Identity

When the PIN pad asks for your PIN, it also displays the identity that you are about to login as. If you wish to you another identity, select the menu icon, then click on the identity that you with to authenticate as:

![MMEUG16](\data\assets\images\chunks\MMEUG16.jpg)

## Managing an Existing Identity

Select the menu icon then select the pencil icon next to the identity that you wish to manage:

![MMEUG17](\data\assets\images\chunks\MMEUG17.jpg)

If you have forgotten your PIN, select “Reset PIN”followed by “Yes, Reactivate it” to confirm that you wish to reset your PIN. You will then be sent a confirmation email and you can proceed with the standard registration workflow.  

If you want to remove your identity entirely from the machine - if, for example, you are giving your PC to someone else, simply select “Remove Identity” followed by “Yes, Remove it” to confirm.
