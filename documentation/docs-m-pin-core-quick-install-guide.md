---
content_type: Chunks
title: Docs M-Pin Core Quick Install Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Summary

This section provides instruction of how to install and deploy M-Pin Core. The information applies to both Free-Tier and Enterprise-Tier installations. The content covers also switching from the Free-Tier to the Enterprise-Tier infrastructure of M-Pin Core.

### In this section:

*   [Installation and Deployment Overview](#installationanddeployment)
*   [Installing M-Pin Services](#installingmpin)
*   [Network Setup](#network)
*   [Installing M-Pin Core](#installingcore)

## Installation and Deployment Overview

To install and deploy M-Pin Core means to unpack and deploy its Customer-Side Modules   – the M-Pin Server, the Relaying Party Service (RPS), and the Customer Distributed-Trust Authority (Customer D-TA) – on your infrastructure and to make sure the respective services run and provide proper communication across components. The remaining Modules – the MIRACL D-TA, the MIRACL D-TA Proxy, and the MIRACL API – are not installed in the technical sense as they are not Customer-Side (they run on MIRACL’s infrastructure) but are activated in this process. (For a conceptual explanation of the M-Pin Core architecture, refer to M-Pin Core Platform General Overview.)

The M-Pin Core components can reside all on a single machine (one-tier deployment) or one or more of them can be deployed on individual machines (distributed one- or two-tier deployments). The Free-Tier version of M-Core is deployed automatically via a script on a single machine and also runs a demo Relying Party Application (RPA).

If you want to create a distributed deployment, you need to first run this script and install the Free-Tier version on every machine of your deployment configuration and then disable the unnecessary services on each of the machine. For example, if a machine is supposed to run the M-Pin Server only, you need to disable respectively the Relaying Party Service (RPS) and the Client Distributed-Trust Authority (D-TA) services leaving only the M-Pin Server running (The script installs and runs all three services.)

**Tip:**
You can create any type of deployment using the free version on M-Pin Core – in this regard, there is no difference between the Free-Tier and Enterprise-Tier versions. This allows you to fully test your M-Pin Core system in your real-life environment, configured exactly as it should operate, prior to committing to the Enterprise-Tier version of the product.

After you deploy your M-Pin Core, you need to further configure its services according to the specifics of your particular deployment, integrate the M-Pin Pad into your application or web-page and set up your RPA to work with M-Pin Core.

Switching from the free to the production version of M-Pin Core is done by replacing the Free-Tier version Security Credentials with the Enterprise-Tier version Credentials provided by MIRACL upon purchase. (With distributed deployments, you need to do this on every machine of the deployment set.) There is no separate installation and deployment for the production version: you can only “upgrade” to it by installing the fee version first and then just changing the Security Keys.

To proceed with your M-Pin Core installation:

*   Decide on the desired deployment architecture.
*   Install the necessary M-Pin Services on each machine of the deployment. After this step, you’ll have the proper M-Pin Services running on the respective machines as necessary.
*   For further configuring the services to cater for the specifics of your particular deployment, see the [M-Pin Core Configuration Guide](/docs/m-pin-core/m-pin-core-config-guide). There, you will find topics on:
*   Configuring M-Pin Core's Services, including:
*   Configuring M-Pin Core's Services Overview
*   RPS Configuration Options Reference
*   M-Pin Server Configuration Options Reference
*   D-TA (Customer) Configuration Options Reference

*   Integrating the M-Pin PIN Pad
*   Enabling the Mobile Authentication

## Installing M-Pin Services

### Network Setup

There are few network setup considerations that should take place. By default, all the Customer-hosted services are installed on the same machine for several reasons:

*   Simplicity
*   Ease of deployment
*   Communication between the different services could be done on the loopback network interface without going on the wire.

The RPS and the RPA are basically two parts of the same - the Relying Party, as the RPS encapsulates and abstract some more specific functionality related to the M-Pin authentication scheme and protocol. Therefor, the RPS and the RPA need to exchange some private messages, as both expose some API that should not be publicly accessible.
The RPS API consist of two types of requests:

1.  Public API - the URL's for the public API always start with the /rps prefix (customizable). Examples GET /rps/clientSettings, PUT /rps/user
2.  Private API - API that should be exposed only to another M-Pin Services as the RPA or the M-Pin Server. The URL's for those requests do not start with the /rps prefix. Examples: POST /user/<mpin-id>, PUT /token.

Since the RPS should not expose its Private API, it should be placed behind a proxy.

### Other Considerations

**Proxy**
Do not confuse this proxy with the D-TA Proxy. The D-TA Proxy is part of the MIRACL-hosted services and doesn't exist at the Customer side.

**RPA serving as a proxy**
This is the default and the simpler option, but not necessarily the best one for a real deployment. The RPA is the only service that is "exposed" to the world. It forwards to the RPS only the requests starting with the /rps prefix and handles all the rest by itself. If the RPS and the RPA run on the same machine (the default), the RPS could listen only to the loopback network interface, which limits the possible attack vectors.

**Dedicated proxy**
This option implies deploying of a dedicated proxy (as Nginx), which should be configured to forward all the requests with prefix /rps to the RPS, and all the rest - to the RPA. Both, the RPS and the RPA should not listen to "public" network interfaces. If they are deployed on the same machine with the dedicated proxy and the rest of the customer-hosted services (M-Pin Server, D-TA) , then they might listen to the loopback network interface only.  

Please take into account the proxy considerations when considering the deployment options below.

### Deployment Types

**One-Tier Deployment**
Deploying M-Pin Core on a single machine is the default. Since the RPS need to communicate "privately" with the rest of the services (RPA, D-TA, M-Pin Server), this option allows communication to happen without being sent over wire, and thus being more secure. The RPS and the D-TA might listen to loopback network interface only. The M-Pin Server has to have its authentication endpoints "exposed", but the M-Pin Protocol that takes place on those endpoint, is safe without being secured by additional means.

**Distributed Deployment**
This option implies that one or more of the M-Pin Services are deployed on separated machines. In this case, a VPN should be setup and all the machines that host the M-Pin Services should communicate securely inside this VPN. A publicly facing dedicated proxy (https://certivox.org/display/ENG/M-Pin+v0.3+-+Installation%2C+Configuration+and+Maintenance#M-Pinv0.3-Installation,ConfigurationandMaintenance-Dedicatedproxy) might be deployed to propagate the requests to the services inside the VPN and the services should be configured to listen only on the relevant network interface(s).

Since the RPS, the M-Pin Server and the D-TA all communicate between each-other, if they are deployed on separate machines they should communicate over the private network. Moreover, it is recommended to additionally secure the communication between using HTTPS/SSL. Since our Python services do not support HTTPS requests, additional proxy should be deployed together with each service, so the proxy "terminates" the HTTPS connection and communicates with the corresponding M-Pin service over HTTP on an the machine's loopback interface.

A possible scenario is that the RPS, M-Pin Server and D-TA will run on one machine, as originally installed, but the actual RPA (which might be a heavy and complex web application) will run on another machine(s). In such a case, again a VPN should be setup around those machines and a proper proxy should be deployed in front to propagate the requests to the RPA, RPS and M-Pin Server.

### Default Network Configuration

By default, all the services, including the demo RPA, are installed on a single machine. The installation process itself is detailed further in this document. The services are configured as follows:

*   **Demo RPA** - listens on loopback (127.0.0.1) network interface, on port 8005\. Communicates with the RPS over *http://127.0.0.1:8011\. The RPA is proxying requests starting with the rps prefix to the RPS
*   **RPS** - listens on loopback (127.0.0.1) network interface, on port 8011\. Communicates with the RPA over *http://127.0.0.1:8005
*   **M-Pin Server** - listens on loopback (127.0.0.1) network interface, on port 8002\. Communicates with the RPS over *http://127.0.0.1:8011 and with the D-TA over http://127.0.0.1:8001
*   **Customer D-TA** - listens on loopback (127.0.0.1) network interface, on port 8001

**NOTE:**
This configuration allows the Demo RPA to be opened from a browser that is running on the local machine only.

## Installing M-Pin Core

The initial installation on a Linux machine is as simple as running a command in the command prompt:

python -c "$(curl -fsSL https://mpin.certivox.net/v3/install)"

Following is a sample output:

MIRACL M-Pin v0.3.2 server installation.
Build d616c9c (2014-10-07T16:11:23Z)
Checking machine hardware... x86_64
Checking platform system... Linux
Checking python version... 2.7
Using python executable... /usr/bin/python
Finding the python shared library... libpython2.7.so.1.0
Enter the installation path [/opt/mpin]:
Installation path: /opt/mpin
Downloading components [6/6]... Done
Installing M-Pin... Done
Running tests... Pass
Getting Community D-TA keys... Done
M-Pin Server has been installed into the following folder /opt/mpin.
For a list of helpful commands, type ./mpin --help.
For helpful resources, please visit miracl.com.

### IMPORTANT INFORMATION:

*   Each M-Pin Platform utilizes two Distributed Trust Authority (D-TA) Services.
*   Dual D-TA Services insure no single point of compromise.
*   Each D-TA Service has its own root key and operates independently.
*   Each D-TA Service issues a 'share' of an M-Pin Key to clients and servers.
*   Clients and servers assemble whole M-Pin Keys from these shares.
*   Only M-Pin Clients and Servers ever possess a whole, complete M-Pin Key.
*   The first D-TA Service exists as part of this M-Pin Server installation.
*   This is your D-TA Service, exclusively under your control.
*   The second D-TA Service is the Community D-TA operated by MIRACL.
*   The Community D-TA Service at MIRACL is a free of charge, fair-use service.
*   Use it for testing and development, not for production.
*   For production deployments, purchase an M-Pin Service Plan at miracl.com.
*   An M-Pin Service Plan includes:

*   Dedicated D-TA Service instance at MIRACL, replacing the Community D-TA
*   Individual root key secured with FIPS 140-2 Level 3 HSMs
*   Support, 100% uptime service level, monitoring, and unlimited use

**NOTE:** For security reasons, it is not possible to migrate M-Pin Keys with shares issued from a Community D-TA to a dedicated D-TA Service.
Please see miracl.com for more information.

Note that the actual link for the installation script might be a subject to change.