---
content_type: Chunks
title: Docs MIRACL M-Pin SSO
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Summary

![M-Pin Core](/img/1-m-pin-sso.png "M-Pin Core")

This section provides a conceptual overview M-Pin SSO Platform, its components, services, and operation. It is a good place to start if you are new to M-Pin SSO and want to find out what it is and how it works.

### In this section:

*   [M-Pin SSO General Overview](#chap1)
*   [M-Pin Services Run by MIRACL](#chap2)

*   [M-Pin SSO Services Run by MIRACL](#chap21)
*   [M-Pin SSO Services Run by MIRACL Customers](#chap22)

*   [M-Pin Authentication Protocol Overview](#chap3)

*   [Zero-Knowledge Proof Protocol Concept Overview](#chap31)
*   [M-Pin Protocol Background](#chap32)
*   [The M-Pin Protocol in a Few Sentences](#chap33)

*   [Distributed Trusted Authorities (D-TAs) Overview](#chap4)

*   [Trusted Authority (TA) Concept Overview](#chap41)
*   [M-Pin Platform's Distributed Trusted Authority Architecture Overview](#chap42)
*   [MIRACL D-TA Operation](#chap43)
*   [MIRACL D-TA Privacy And Security](#chap44)

*   [M-Pin Clients Overview](#chap5)
*   [M-Pin User Setup Overview](#chap6)
*   [M-Pin Authentication Overview](#chap7)

## M-Pin SSO General Overview

M-Pin SSO is an extension of the M-Pin Strong Authentication Platform that is compatible with SAML federated and RADIUS authenticated applications.

For SAML-federated applications, M-Pin SSO produces a SAML token, as the result of an M-Pin Strong Authentication based on patented M-Pin Protocol. This allows an end-user to authenticate with M-Pin and gain access to SAML-federated applications associated with M-Pin SSO. Examples of applications compatible with M-Pin SSO are Amazon AWS, Dropbox, Salesforce.

For Radius authenticated applications, M-Pin SSO generates a one-time password (OTP) as the result of a successful M-Pin Strong Authentication. The end-user can access a RADIUS-authenticated application associated with M-Pin SSO using that OTP as their password for the single application login. Examples of Radius authenticated applications are VPN clients, Remote Desktop and Virtual Desktop applications.

M-Pin SSO is distributed through AWS Marketplace as a server product, and it includes a web-based administrator console and end-user interfaces for the actual user authentication.

**The M-Pin SSO Authentication Platform is based on:**

*   M-Pin Protocol: A zero-knowledge proof authentication protocol, based on elliptic curve cryptography that delivers multi-factor authentication between M-Pin Clients and Servers. The M-Pin Protocol is proprietary of MIRACL.
*   M-Pin Server: An open source server written in Python, designed for Linux OS, but can run on Windows as well. M-Pin Server eliminates the threat of password or credential database breaches, as it stores no password or authentication credentials which internal or external actors can compromise.
*   M-Pin Client Software: The open source software application, available for JavaScript or smartphone operating systems (iOS, Android, Windows Phone), that provides the UI and performs the authentication protocol against M-Pin Server. MPin Client software works in any HTML5 enabled browser, and authenticates users into a browser session on the same device. As part of the client software offering, the M-Pin Mobile is a web app compatible with HTML5 enabled mobile browsers, and provides hands-off access to a second device browser session while performing the user authentication from the mobile app – this is referred to as "Global Authenticator mode" and eliminates the threat of host based malware stealing user login details.
*   MIRACL's Distributed Trusted Authority (D-TA) Architecture: An advancement in elliptic curve cryptography that results in eliminating single points of compromise at MIRACL and its customers, without affecting the privacy of MIRACL customers or the security efficacy of the system. The D-TA architecture enables MIRACL customers to gain the benefits of MIRACL's enhanced security posture without having to invest in the infrastructure or personnel to maintain it.

As part of the Distributed Trusted Authority Architecture, several services are split between MIRACL and its customer:

## M-Pin SSO Services

### M-Pin SSO Services Run by MIRACL

*   **D-TA** - Distributed Trusted Authority Service, managed by MIRACL. It is responsible for generating Client and Server Key Shares as well as Time Permit Shares. Each customer's D-TA instance is isolated and unique to each customer, and its cryptographic Master Key is protected with encryption keys housed in FIPS 140-2 Level 3 hardware security models.
*   **D-TA Proxy** – It proxies request to the D-TA from the customer's applications (RSA/S), validating RPS signatures and provides security to the D-TA. The D-TA Proxy is public facing, while the D-TA is never publicly accessible.
*   **MIRACL API** - Additional services for customer/application registration

### M-Pin SSO Services Run by MIRACL Customers

M-Pin Server – A drop-in replacement for password-based authentication applicable for any online service or system that removes the risk of password database breaches entirely. The M-Pin Server includes the following modules:

*   **AML IdP **– Security Assertions Markup Language Identity Provider. It is the service that generates the SAML identity assertion to be consumed by SAML federated applications.
*   **RADIUS Service **– it is the service against which the RADIUS federated application authenticates its end users
*   **Web Server** - serves up the M-Pin PIN pad for SAML and RADIUS federated authentication, and also displays the resulting one-time password specifically for Radius authentication.
*   **M-Pin Clients** - all the client side services, providing the user interface and the cryptographic functions on the end user's device. For M-Pin SSO they are all already embedded in the web pages distributed with the package

## M-Pin Authentication Protocol Overview

This page provides a very brief summary of the M-Pin Authentication Protocol. If you need a more detailed explanation, refer to our [M-Pin: A Multi-Factor Zero Knowledge Authentication Protocol](/downloads/pdfs/crypto-labs/CertiVox_Labs_mpin.pdf) white paper.

### Zero-Knowledge Proof Protocol Concept Overview

A [zero-knowledge proof](http://en.wikipedia.org/wiki/Zero-knowledge_proof) protocol is a method by which one party (the prover) can prove to another party (the verifier) that a given statement is true, without conveying any additional information apart from the fact that the statement is indeed true. Proving that one possesses certain knowledge is, in most cases, trivial if one is allowed to simply reveal that knowledge; the challenge is proving that one has such knowledge without revealing it or without revealing anything else.

### M-Pin Protocol Background

The M-Pin Protocol is the first productized zero-knowledge proof protocol to hit mainstream adoption. While M-Pin is a relatively new product and service, the M-Pin Protocol was first introduced in academic circles over a decade ago by Dr. Michael Scott, MIRACL's chief cryptographer, and has been sited over three thousand times in cryptographic research since initial publication. To date, no known theoretical or practical attacks exist against it.

For more information on the M-Pin Protocol in general, refer to the M-Pin cryptographic white papers available on the [MIRACL website](http://www.certivox.com) in the [MIRACL Research](/crypto-labs) section.

### The M-Pin Protocol in a Few Sentences

The M-Pin Authentication Protocol is a zero-knowledge proof authentication protocol using proven, strong, standards-based elliptic curve cryptography:

*   M-Pin Server and M-Pin Client Keys are issued according to elliptic curve cryptography principles, and the server can tell whether a client key comes from the right elliptic curve set
*   M-Pin Server can prove who a user is without having to store a client credential on a server, or in a database (like passwords currently are)
*   Credentials (M-Pin Client Keys) are NEVER exchanged (encrypted or unencrypted) between a user and the M-Pin Server
*   M-Pin Server Key compromise doesn't reveal anything about users or their credentials, eliminating scenarios like password database breaches
*   The code that manipulates the M-Pin Client Key (a user's credential) runs in the user's browser or app, therefore no separate hardware tokens or software installations are required.

The picture below represents schematically the operation of the M-Pin Authentication Protocol – a cryptographic zero-knowledge proof, challenge-response authentication protocol built on standards-based elliptic curve cryptography.

![1-m-pin-authentication-overlay](/img/1-m-pin-authentication-overlay.jpg)

## Distributed Trusted Authorities (D-TAs) Overview

### Trusted Authority (TA) Concept Overview

The concept of Trusted Authority (TA) is very familiar in the Public Key Infrastructure (PKI) paradigm, where a central Certification Authority (CA) is responsible for verifying all the requests, and for issuing valid credentials (in this case Digital Certificates) to associate to private/public key pairs, using its root, or master key. One big weakness of the PKI paradigm is that the CA is a single point of trust, and failure, and its reliability is strongly dependent on how the CA maintains and securely stores its master key.

Many organizations are realizing that by using the services of a 3rd party certificate authority, or any security vendor that holds a root key, or seed value, they are placing an inappropriate level of trust and leaking personally identifiable information about end users that may violate regulatory standards and put their organization at risk.

### M-Pin Platform's Distributed Trusted Authority Architecture Overview

The M-Pin Strong Authentication Platform's Distributed Trusted Authority architecture has been designed to address these weaknesses.

The M-Pin Platform's architecture is designed to distribute the single point of compromise between MIRACL and its customers. For this reason, M-Pin TA is split into two Distributed TAs: MIRACL D-TA and Customer D-TA. Each MIRACL customer runs its own D-TA, and for each Customer D-TA, MIRACL runs a corresponding MIRACL D-TA. The two D-TAs do not communicate in any way.

MIRACL hosts a dedicated D-TA for each paying customer.

The picture below represents schematically the Distributed Trust Authorities and demonstrates how this distributed architecture removes insider threats and single points of compromise.

![2-DTA-nodes-overlay](/img/2-DTA-nodes-overlay.jpg)

### MIRACL D-TA Operation

The MIRACL D-TA issues:

*   One share of the server key to customers, to be used when setting up M-Pin Server
*   One share of the client key to customers' clients, issued when an end user registers
*   One share of the time permit to customers' clients, issued when an end user authenticates

All the above elements are needed to perform the M-Pin Authentication, together with a correspondent share issued by the M-Pin Server deployed, owned and managed by MIRACL customers.

### MIRACL D-TA Privacy And Security

MIRACL personnel is never exposed to the unencrypted Master Key inside of the customer's D-TA service at MIRACL. The Master Key of each Enterprise-Tier Customer is housed in each distinct D-TA Service is cryptographically protected with FIPS 140-2 Level 3 hardware security module. Because the D-TA architecture removes the single point of compromise, in order to have a security breach equivalent to a PKI root key breach or 2FA seed value breach, both Master Keys inside the D-TA services, at MIRACL and MIRACL's customer, must be compromised.

Customers gain the benefit of the security efficacy achieved using FIPS validated hardware security modules, without having to invest in resources or infrastructure to maintain this level of security. MIRACL houses its D-TA infrastructure at ISO/IEC 27001 certified data center locations in the European Union for resiliency and high availability, offering 100% uptime of its D-TA service.

Additionally, when the MIRACL API receives a request for a M-Pin Client Key share, the request is made in a cryptographically secured manner, in which the identity of the end user, which is bound to the requested M-Pin Client Key, is hashed through a one-way function, so that MIRACL never receives any personally identifiable information about who our customer's end users are.

As an example, user John Doe may have 3 M-Pin Client Keys issued, one for each device he owns. MIRACL has no way to ascertain the identity of the M-Pin Client Keys (that they belong to John Doe) or that they are related to any one identity whatsoever.

## M-Pin Clients Overview

The M-Pin Client software is responsible for M-Pin User Setup, performing the M-Pin Authentication Protocol against the server and handling of the M-Pin Client Keys and MPin Tokens. The M-Pin Client software contains the "PIN Pad" UI that guides the end user through the various workflows including setup, authentication and Global Authenticator mode. The M-Pin Client software is available as:

*   A JavaScript application suitable for desktop applications
*   An HTML5 "web app" which can be deployed to any smart device capable of running a browser. This enables enterprises and ISVs to deploy the M-Pin web app onto their user's devices without having to create a native app and deploy it via a workflow with an app store. An HTML5 web app can simply be deployed over a publicly accessible URL.

## M-Pin User Setup Overview

M-Pin adds multi-factor authentication to its zero-knowledge proof protocol by splitting the M-Pin Client Key into, at a minimum, two parts; an M-Pin Token, so that it is no longer representative of the end user's identity, and a low entropy PIN or passphrase:

*   End users choose their PIN - nobody else knows it, it's not stored anywhere
*   Programmatically, the PIN is "extracted" from the M-Pin Client Key, and ONLY the resulting token (M-Pin Token) is stored in the browser, locked to the domain of the issuer, or stored in secured storage within an app
*   Neither the PIN, nor the M-Pin Token, or the combination of the two is ever exchanged between client and server; this is the benefit of zero-knowledge proof protocols

The picture below represents schematically the M-Pin User Setup process – splitting the M-Pin Client Key into an M-Pin Token and PIN or other factors.

![3-m-pin-setup-overlay](/img/3-m-pin-setup-overlay.jpg)

## M-Pin Authentication Overview

To successfully authenticate with M-Pin, an end user must have access to two factors:

*   The token in the browser or application: "something you have"
*   The PIN number: "something you know"

The level of security is the same used in payment systems by the coupling of credit/debit cards and PIN numbers. M-Pin is arguably more secure, as the client key and the PIN are never stored. M-Pin is an online authentication protocol, it is impossible to mount an offline attack, and so the configurable number of incorrect attempts can result in the revocation of an M-Pin Client Key according the security guidelines set by an application.

To enable revocation of users who have already been issued with a valid client key, M-Pin introduces the concept of Time Permits. Before the actual authentication protocol is started, the end user must request a valid Time Permit. If no valid Time Permit is available, the M-Pin protocol simply doesn't start, and the authentication cannot be performed.

The picture below represents schematically the M-Pin Authentication – recombining from PIN/Passphrase + M-Pin Token and optionally additional factors.

![4-m-pin-login-overlay](/img/4-m-pin-login-overlay-235200-edited.jpg)
