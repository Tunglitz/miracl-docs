---
content_type: Chunks
title: Docs MIRACL M-Pin Core Access
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---
This content is relevant to the AWS distribution of M-Pin Core.

### Summary

This section explains how to access the demo application of a newly created M-Pin Core instance. It assumes that your instance has been created successfully and is currently running. Note that the demo application has no real functionality and serves only to verify the instance the M-Pin service are on and operational; if you want to configure your M-Pin Core System, refer to the M-Pin Core user documentation.

### In This Section

*   [Introduction](#introduction)
*   [Accessing the Demo and Testing It](#demo)
*   [Accessing the Documentation](#docs)

## Introduction

Once your M-Pin Core instance launches, it is fully functional with all its services up and running. There is also a demo application with which you can verify the proper operation of the instance.

**Note:**

If you have created an Enterprise -Tier instance of M-Pin Core, there will be about 15 minutes of lag time before the instance becomes operational. This is because the address of the dedicated MIRACL D-TA needs to be propagated through the DNS servers over the world. Free-Tier instances of M-Pin Core are operational immediately upon creation.

## Accessing the Demo and Testing It

To access your M-Pin Core demo application and test its functionality:

*   (_Conditional_) If you hadn't enabled HTTP access when you created the M-Pin Core instance, **enable HTTP access to port 80** now (from your AWS EC2 management console).

*   With your browser, **access the M-Pin Core demo application** at this URL:  
     http://HOST
    _Public DNS_ or _Public IP_ address of your M-Pin Core instance. (The _Public DNS_ or _Public IP_ of the instance can be found on your AWS EC2 management console.)

The page will display the M-Pin PIN Pad:

![core-access1](\data\assets\images\chunks\core-access1.png)

*   Follow the instructions in the PIN Pad to **create your access PIN and sign in to the demo application**.

##  Accessing the Documentation

For your M-Pin Core instance to became useful, you need to customize it to make it work with your own application or web site. For customization instructions, see the following documents:

*   **[M-Pin Core for AWS Getting Started Guide](url here)**
*   [**M-Pin Core Configuration Guide**](url here)
