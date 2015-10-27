---
content_type: Chunks
title: Docs M-Pin Core - M-Pin Core AWS - Getting Started Guide
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

This content is relevant only to the AWS distribution of M-Pin Core.

## Summary

This section provides instructions of how to quickly customize your M-Pin Core instance so that it can be used in your custom environment. The information applies to both Free-Tier and Enterprise-Tier instances.   
The content assumes your M-Pin Core instance has already been created and its demo application operates properly. (To verify proper operation sign in to the demo application as explained in M-Pin Core for AWS Product Access Instructions.)

### In this section:

[M-Pin Core Instance Configuration Overview](#part1)  
[Network Setup](#part2)
[RPS/RPA Overview](#part2a)  
[Proxy Configuration](#part2b)  
[Default Network Configuration](#part2c)

## M-Pin Core Instance Configuration Overview

Your M-Pin Core instance has its Customer-Side Modules – the M-Pin Server, the Relaying Party Service (RPS), and the Customer Distributed-Trust Authority (Customer D-TA) – deployed on the AMI. The remaining Modules – the MIRACL D-TA, the MIRACL D-TA Proxy, and the MIRACL API – run on MIRACL's infrastructure but are activated in the process of creating the instance. (For a conceptual explanation of the M-Pin Core architecture, refer to M-Pin Core Platform General Overview.)

After you create your M-Pin Core instance, you need to further configure its services according to the specifics of your particular deployment, integrate the M-Pin Pad into your application or web-page and set up your (Relying Party Application) RPA to work with M-Pin Core.

Here is an overview of what customizing your M-Pin Core instance is about:

*   Configuring M-Pin Core's Services, including:

*   Configuring M-Pin Core's Services Overview
*   RPS Configuration Options Reference
*   M-Pin Server Configuration Options Reference
*   D-TA (Customer) Configuration Options Reference
*   Integrating the M-Pin PIN Pad
*   Enabling the Mobile Authentication

For further configuring the services to cater for the specifics of your particular deployment, see the M-Pin Core Configuration Guide.

## Network Setup

### RPS/RPA Overview

The RPS and the RPA are basically two parts of the same - the Relying Party, as the RPS encapsulates and abstract some more specific functionality related to the M-Pin authentication scheme and protocol. Therefore, the RPS and the RPA need to exchange some private messages, as both expose some API that should not be publicly accessible.The RPS API consist of two types of requests:

1.  Public API - the URL's for the public API always start with the /rps prefix (customizable). Examples GET /rps/clientSettings, PUT /rps/user
2.  Private API - API that should be exposed only to another M-Pin Services as the RPA or the M-Pin Server. The URL's for those requests do not start with the /rps prefix. Examples: POST /user/<mpin-id>, PUT /token.

Since the RPS should not expose its Private API, it should be placed behind a proxy.

### Proxy Configuration

**RPS/RPA Proxy and D-TA Proxy**
Do not confuse this proxy with the D-TA Proxy. The D-TA Proxy is part of the MIRACL-hosted services and doesn't exist at the Customer side.

**RPA serving as a proxy**
This is the default and the simpler option, but not necessarily the best one for a real deployment. The RPA is the only service that is "exposed" to the world. It forwards to the RPS only the requests starting with the /rps prefix and handles all the rest by itself. If the RPS and the RPA run on the same machine (the default), the RPS could listen only to the loopback network interface, which limits the possible attack vectors.

**Dedicated proxy**
This option implies deploying of a dedicated proxy (as Nginx), which should be configured to forward all the requests with prefix /rps to the RPS, and all the rest - to the RPA. Both, the RPS and the RPA should not listen to "public" network interfaces. If they are deployed on the same machine with the dedicated proxy and the rest of the customer-hosted services (M-Pin Server, D-TA) , then they might listen to the loopback network interface only.

### Default Network Configuration

By default, all the services, including the demo RPA, are installed on a single machine. The installation process itself is detailed further in this document. The services are configured as follows:

*   **Demo RPA** - listens on loopback (127.0.0.1) network interface, on port 8005\. Communicates with the RPS over http://127.0.0.1:8011\. The RPA is proxying requests starting with the rps prefix to the RPS
*   **RPS** – listens on loopback (127.0.0.1) network interface, on port 8011\. Communicates with the RPA over http://127.0.0.1:8005
*   **M-Pin Server** – listens on loopback (127.0.0.1) network interface, on port 8002\. Communicates with the RPS over http://127.0.0.1:8011 and with the D-TA over http://127.0.0.1:8001
*   **Customer D-TA** – listens on loopback (127.0.0.1) network interface, on port 8001