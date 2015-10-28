---
content_type: Chunks
title: Docs M-Pin Core - M-Pin Understanding D-TA
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

The concept of Trusted Authority (TA) is very familiar in the Public Key Infrastructure (PKI) paradigm, where a central Certification Authority (CA) is responsible for verifying all the requests, and for issuing valid credentials (in this case Digital Certificates) to associate to private/public key pairs. One big weakness of the PKI paradigm is that the CA is a single point of trust, and its reliability is strongly dependent on how the CA maintains and securely stores their private keys.

M-Pin is completely different.

M-Pin architecture is designed to distribute the trust between MIRACL and its customers. For this reason, M-Pin TA is split into two Distributed TAs: MIRACL D-TA and Customer D-TA. Each MIRACL customer runs its own D-TA, and for each Customer D-TA, MIRACL runs a corresponding MIRACL D-TA. The two D-TAs don't need to communicate in any way.

## AWS Infrastructure

AWS Infrastructure, also referred to as MIRACL Infrastructure, is deployed on AWS Cloud Computing infrastructure, and it provides distribution of trust for all MIRACL’s customers.

MIRACL hosts a dedicated D-TA and a dedicated D-TA Proxy for each customer.  

The MIRACL D-TA issues:

*   one share of the server secret to customers, to be used when setting up M-Pin Server
*   one share of the client secret to customers’ clients, issued when an end user registers
*   one share of the time permit to customers’ clients, issued when an end user authenticates

All the above elements are needed to perform the M-Pin Authentication, together with a correspondent share issued by the M-Pin Server deployed, owned and managed by the customers.. 

The following diagram shows at a high level how key shares are distributed to both the M-Pin Server & Clients from the two D-TA's:

![2-DTA-nodes-overlay](\data\assets\images\chunks\/2-DTA-nodes-overlay.jpg)

## Infrastructure architecture and deployment

D-TAs are not directly accessible by any entity but its D-TA Proxy. The Proxy receives and processes all the external requests, and forwards the relevant ones to the D-TA. The D-TA Proxy also serves the response to the requests from the D-TA proxy to any entitled external entity.

All the requests to a D-TA Proxy are signed by the legitimate customer M-Pin keys, so that only the entitled entities can reach a D-TA Proxy, namely the customer’s relying party application(s) and the customer’s clients.

## Separation of duties

D-TA and D-TA Proxy deployed on AWS infrastructure are built as closed LXC containers and cannot be accessed by MIRACL DevOps or by any other MIRACL employee at any time after creation. No one has access to those containers, and no one can access the D-TA master secret, which is contained in the D-TA memory only.

All the procedures to create the containers are automated, and the procedures to resume an existing D-TA, for disaster recovery purposes only, are performed using encrypted passphrases automatically generated. Access to those passphrases and their usage is thoroughly logged, and the logs are protected and maintained by AWS as per AWS compliance statements.

## Data obfuscation

Although MIRACL issues shares of cryptographic parameters to their customers and their customers’ end users, data on end users are completely obfuscated to MIRACL and MIRACL employees at any level. MIRACL is only able to see and collect info for billing and analytics purposes, and those data are limited to:

*   Number of total client secret shares generated per customer
*   Number of total time permits issued per customer

MIRACL is not able to retrieve any info beyond the data listed above. In particular, MIRACL cannot see directly or recover information about the following:

*   How many unique end users a customer has enrolled
*   How many unique users are active
*   What usernames the end users are submitting as M-Pin Identities
*   What services the customer offers and the end users access
*   How many devices have been enrolled per unique user or per customer

## High Availability

AWS Infrastructure is configured to provide high availability to MIRACL customers.

D-TA and D-TA Proxy instances are deployed in High Availability mode across two availability zones on AWS: EU Ireland Zone A and Zone B.

HA across different regions is available on request only, for customers who specifically need it.

## Customer D-TA

The Customer D-TA is distributed with the M-Pin installation package, and by default it runs as a separate service on M-Pin Authentication Server.
