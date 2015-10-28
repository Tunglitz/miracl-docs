---
content_type: Chunks
title: Docs M-Pin Core - M-Pin OTP End-User Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

As well as generating SAML tokens for SAML-compliant service providers, the M-Pin SSO Server can also be configured to generate One-Time-Passwords (OTPs) to use in RADIUS client applications. This guide is aimed at users of the M-Pin SSO Server whose administrators have configured the SSO server to generate OTPs.

The registration, authentication and account management workflows for the OTP generator of the M-Pin SSO Server are similar to those of M-Pin Core with the exception that instead of logging you into a service, an OTP is displayed instead. This OTP is then used as the password for authenticating into your RADIUS client application - for more details on how to perform this step, you will need to contact your system administrator. Note that you must use the OTP within the time limit set by your system administrator (typically 99 seconds). The countdown underneath the OTP tells you how much time you have left.  

## Generating OTPs using M-Pin-In-Browser

Your system administrator will give you the link to the OTP generating site. Users who wish to use the browser on their own PC to generate OTPs should read the [M-Pin-In-Browser End User Guide](/docs/m-pin-core/mpin-in-browser-end-user-guide). The workflows described in that document are identical to the OTP generation workflows with the exception that in the 'Authentication' section of this guide, after entering your PIN, instead of logging into a service, the OTP is displayed in your browser:

![MOTPEUG1](\data\assets\images\chunks\MOTPEUG1.png)

## Generating OTPs using M-Pin-In-Mobile

Users who wish to use their mobile to generate OTPs should read the [M-Pin-In-Mobile End User Guide](/docs/m-pin-core/mpin-in-mobile-end-user-guide). Your system administrator will give you the link to the OTP generating site. The workflows described in that document are identical to the OTP generation workflow except for the “Authentication” workflow which for OTP generation is as follows.   

Once you have registered the M-Pin-In-Mobile app for the OTP site, you will immediately see the PIN pad asking for your PIN (the screen asking for an access number is not required for OTP generation). When you have entered your PIN, the OTP will be displayed:

![MOTPEUG2](\data\assets\images\chunks\MOTPEUG2.jpe)
