---
content_type: Chunks
title: Docs M-Pin Core - M-Pin SSO Configuration Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Summary

This content explains how to configure AWS and Dropbox as SAML2 Service Providers to authenticate through your M-Pin SSO Platform.

## In this section

[Configuring an AWS Service Provider](#part1)

[Overview](#part1a)
[Details](#part1b)

[Configuring a Dropbox Service Provider](#part2)

[Overview](#part2a)
[Details](#part2b)

## Configuring an AWS Service Provider

### Configuring an AWS Service Provider Overview

Following are the main steps to configuring an AWS Service provider with M-Pin SSO. For the full detailed procedure, see [Configuring an AWS Service Provider Details.](#part1)

1.  In your AWS account, **declare an Identity Provider and a Role for that Provider**, using the SAML2 Identity Provider metadata of your M-Pin SSO System.
2.  In your M-Pin SSO web management interface, **create an AWS profile** using the declared Identity Provider and Role.

### Configuring an AWS Service Provider Details

Following is the detailed procedure to configuring an AWS Service Provider with M-Pin SSO.

1.  **Declare an Identity Provider and a Role for that Provider** in AWS.

    In your AWS account, declare an Identity Provider and a Role for accessing that Provider, using the SAML2 Identity Provider metadata of your M-Pin SSO System.

    Settings:

    *   **Identity Provider name** – must be unique within your AWS account
    *   **Identity Provider type** – SSL
    *   **Role type** – Identity Provider Access, Web Single Sign-On (WebSSO) access to SAML providers
    *   **SAML2 Identity Provider metadata URL**

    http://HOST/idp/saml2/metadata

    where HOST is the Public DNS or Public IP address of your M-Pin SSO instance

    For details on how to perform this step, refer to AWS user documentation.

2.  **Create an AWS Profile** in M-Pin SSO.

In the web management interface of your M-Pin SSO system, create an AWS profile using the newly declared Identity Provider and Role. To do this:

1.  On the _Dashboard_ page, _Integration_ panel, _AWS profiles_ row, **select the Add button**.

    ![SSOCG1](\data\assets\images\chunks\SSOCG1.png)

    This will display the Add AWS profiles page.

    ![SSOCG2](\data\assets\images\chunks\SSOCG2.png)

2.  **Fill in the Profile’s fields** and then **save the profile**.

Settings:

*   **Name** _(Required)_ – Name of the profile
*   **AWS Role** _(Required)_ – the Role you created in step 1
*   **AWS Account Number** _(Required)_ – the unique account number of your AWS account
*   **AWS Provider** _(Required)_ – the Identity Provider you created in step 1
*   **LDAP Profile** _(Optional)_ – if you have LDAP profiles configured, they will be available in this drop-down

After saving, the profile will display on the AWS Profiles page.

## ![SSOCG3](\data\assets\images\chunks\SSOCG3.png)
Configuring a Dropbox Service Provider

### Configuring a Dropbox Service Provider Overview

Following are the main steps to configuring a Dropbox Service provider with M-Pin SSO. For the full detailed procedure, see [Configuring a Dropbox Service Provider Details.](#part2b)

1.  In your Dropbox account, **declare the end point URL for your M-Pin SSO System and your SSL key**.
2.  In your M-Pin SSO web management interface, **create a Dropbox profile**.

### Configuring a Dropbox Service Provider Details

Following is the detailed procedure to configuring an AWS Service Provider with M-Pin SSO.

1.  **Declare the end point URL for your M-Pin SSO System and your SSL key** in your Dropbox account, SSO settings.

    The M-Pin SSO end point URL is

    http://HOST/idp/saml2/sso

    where HOST is the Public DNS or Public IP address of your M-Pin SSO instance.  
    For details on how to perform this step, refer to Dropbox user documentation.

2.  **Create a Dropbox Profile** in M-Pin SSO.

In the web management interface of your M-Pin SSO system, create a Dropbox profile. To do this:

1.  On the _Dashboard_ page, _Integration_ panel, _Dropbox_ profiles row, **select the Add button**.

    ![SSOCG4](\data\assets\images\chunks\SSOCG4.png)

    This will display the Add Dropbox profiles page.

    ![SSOCG5](\data\assets\images\chunks\SSOCG5.png)

2.  **Fill in the Profile’s fields** and then **save the profile**.

Settings:

*   **Name** _(Required)_ – name of the profile
*   **SSL Key** _(Required)_ – paste or upload your SSL key
*   **LDAP Profile** _(Optional)_ – if you have LDAP profiles configured, they will be available in this drop-down.

After saving, the profile will display on the _Dropbox profiles_ page.
