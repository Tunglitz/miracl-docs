---
content_type: Chunks
title: Docs MIRACL M-Pin Core
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Summary

![M-Pin Core](\data\assets\images\chunks\1-m-pin-core.png "M-Pin Core")

This section provides a conceptual overview of the M-Pin Core and its components, services, and operation. It is a good place to start if you are new to M-Pin Core and want to find out what it is and how it works.

### In this section:

*   [M-Pin Core General Overview](#chap1)

*   [M-Pin Core Key Elements](#chap11)
*   [M-Pin Core Services](#chap12)
*   [Services Run by MIRACL](#chap13)
*   [M-Pin Core Services Run by MIRACL Customers](#chap14)

*   [M-Pin Authentication Protocol Overview](#chap2)
*   [Distributed Trusted Authorities (D-TAs) Overview](#chap3)

*   [Trusted Authority (TA) Concept Overview](#chap31)
*   [M-Pin Platform's Distributed Trusted Authority Architecture Overview](#chap32)
*   [MIRACL D-TA Operation](#chap33)
*   [MIRACL D-TA Privacy and Security](#chap34)

*   [M-Pin User Setup Overview](#chap4)
*   [M-Pin Authentication Overview](#chap5)

## M-Pin Core General Overview

M-Pin Core is a client-server software for [strong authentication](http://en.wikipedia.org/wiki/Strong_authentication) over WebSocket and HTTP data transfer protocols. M-Pin Core provides a drop-in replacement for password-based authentication that is applicable to any online system or service. The M-Pin Core is based on the M-Pin Strong Authentication Platform which is an identity-based cryptosystem that uses elliptic curve cryptography to fix the fundamental design flaws that affect all PKI and two-factor authentication platforms; the inappropriate level of trust demanded by 3rd-party ISV security service providers, weak security efficacy of the products and services themselves and design flaws that leak personally identifiable information about end users to these 3rd-party services.  MIRACL supplies open source client and server software under the BSD-Clause 3 license and runs a cryptographic service, called the Distributed Trusted Authority, which issues shares of M-Pin Keys to clients and servers deployed on the platform.

### M-Pin Core Key Elements

**The M-Pin Core key elements include: **

*   **M-Pin Protocol**: A zero-knowledge proof authentication protocol, based on elliptic curve cryptography that delivers multi-factor authentication between the M-Pin Clients and the M-Pin Authentication Server. The M-Pin Protocol is proprietary of MIRACL.
*   **M-Pin Authentication Server**: An open source server written in Python, designed for Linux OS, but can run on Windows as well. The Authentication Server eliminates the threat of password or credential database breaches, as it stores no password or authentication credentials which internal or external actors can compromise.
*   **Pin-In-Browser**: The open source software client application, available for JavaScript or smartphone operating systems (iOS, Android, Windows Phone), that provides the UI and performs the authentication protocol against M-Pin Authentication Server. The Pin-In-Browser software works in any HTML5-enabled browser, and authenticates users into a browser session on the same device. As part of the client software offering, the M-Pin Mobile is a web app compatible with HTML5 enabled mobile browsers, and provides hands-off access to a second device browser session while performing the user authentication from the mobile app – this is referred to as "Global Authenticator mode" and eliminates the threat of host based malware stealing user login details.
*   **MIRACL's Distributed Trusted Authority (D-TA) Architecture**: An advancement in elliptic curve cryptography that results in eliminating single points of compromise at MIRACL and its customers, without affecting the privacy of MIRACL customers or the security efficacy of the system. The D-TA architecture enables MIRACL customers to gain the benefits of MIRACL's enhanced security posture without having to invest in the infrastructure or personnel to maintain it.

### M-Pin Core Services

As part of the Distributed Trusted Authority Architecture, several services (components) are split between MIRACL and the Customer.

### Services Run by MIRACL

*   **D-TA** - Distributed Trusted Authority Service, managed by MIRACL. It is responsible for generating Client and Server Key Shares as well as Time Permit Shares. Each customer's D-TA instance is isolated and unique to each customer, and its cryptographic Master Key is protected with encryption keys housed in FIPS 140-2 Level 3 hardware security models.
*   **D-TA Proxy** – proxies requests to the D-TA from the Customer's Relying Party Applications (RSA's), validating Relying Party Service's (RPS's) signatures and provides security to the D-TA. The D-TA Proxy is public facing, while the D-TA is never publicly accessible.
*   **MIRACL API** - Additional services for customer/application registration.

### M-Pin Core Server Services Run by MIRACL Customers

*   **M-Pin Core Server** – A drop-in replacement for password-based authentication applicable for any online service or system that removes the risk of password database breaches entirely. The M-Pin Authentication Server includes the following modules:

*   **M-Pin Authentication Server**  – the server against which end-users authenticate using M-Pin Protocol
*   **D-TA** – Distributed Trusted Authority Service managed by the Customer and it is responsible for generating Client and Server Key Shares, as well as Time Permit Shares.
*   **RPS** – Relying Party Service. It is the service that the customer's application will communicate with to perform the M-Pin authentication for your end users.
*   **RPA** – Relying Party Application. It is the customer's application to which end users are authenticated using M-Pin. This application is implemented and managed by each MIRACL customer and is specific for each different customer.

*   **M-Pin Core Clients** – These are the client side-services, providing the user interface and the cryptographic functions on the end user's device.

*   **PIN Pad UI** - The PIN Pad is a JavaScript UI software component that should be served and integrated with a customer's application. The PIN Pad encapsulates all the operations and logic in order to register and authenticate an end-user.
*   **Pin-In-Browser** – A JavaScript application served by an endpoint in a customer's application. The Pin-In-Browser does not require any integration. It carries out the operations needed to register and authenticate an end-user to a browser session on a secondary device, enabling out-of-band authentication. The code can also be embedded into an HTML5 web app.
*   **Pin-In-Mobile** – Open source cryptographic libraries written in native smartphone OS that are used by M-Pin Customers to embed M-Pin Mobile App functionality into their own native smartphone OS application. These libraries handles the client aspects of the M-Pin Protocol.

## M-Pin Authentication Protocol Overview

This page provides a very brief summary of the M-Pin Authentication Protocol. If you need a more detailed explanation, refer to our [M-Pin: A Multi-Factor Zero Knowledge Authentication Protocol](\data\assets\downloads\pdfs\crypto-labs\CertiVox_Labs_mpin.pdf) white paper.

### Zero-Knowledge Proof Protocol Concept Overview

A [zero-knowledge proof](http://en.wikipedia.org/wiki/Zero-knowledge_proof) protocol is a method by which one party (the prover) can prove to another party (the verifier) that a given statement is true, without conveying any additional information apart from the fact that the statement is indeed true. Proving that one possesses certain knowledge is, in most cases, trivial if one is allowed to simply reveal that knowledge; the challenge is proving that one has such knowledge without revealing it or without revealing anything else.

### M-Pin Protocol Background

The M-Pin Protocol is the first productized zero-knowledge proof protocol to hit mainstream adoption. While M-Pin is a relatively new product and service, the M-Pin Protocol was first introduced in academic circles over a decade ago by Dr. Michael Scott, MIRACL's chief cryptographer, and has been sited over three thousand times in cryptographic research since initial publication. To date, no known theoretical or practical attacks exist against it.

For more information on the M-Pin Protocol in general, refer to the M-Pin cryptographic white papers available on the [MIRACL website](http://www.certivox.com/) in the [MIRACL Labs](/crypto-labs) section.

### The M-Pin Protocol in a Few Sentences

**The M-Pin Authentication Protocol is a zero-knowledge proof authentication protocol using proven, strong, standards-based elliptic curve cryptography:**

*   M-Pin Server Keys and M-Pin Client Keys are issued according to elliptic curve cryptography principles, and the server can tell whether a client key comes from the right elliptic curve set
*   The M-Pin Authentication Server can prove who a user is without having to store a client credential on a server, or in a database (like passwords currently are)
*   Credentials (M-Pin Client Keys) are NEVER exchanged (encrypted or unencrypted) between a user and the M-Pin Authentication Server
*   An M-Pin Server Key compromise doesn't reveal anything about users or their credentials, eliminating scenarios like password database breaches
*   The code that manipulates the M-Pin Client Key (a user's credential) runs in the user's browser or app, therefore no separate hardware tokens or software installations are required.

The picture below represents schematically the operation of the M-Pin Authentication Protocol – a cryptographic zero-knowledge proof, challenge-response authentication protocol built on standards-based elliptic curve cryptography.

![1-m-pin-authentication-overlay](\data\assets\images\chunks\1-m-pin-authentication-overlay.jpg)

## Distributed Trusted Authorities (D-TAs) Overview

### Trusted Authority (TA) Concept Overview

The concept of Trusted Authority (TA) is very familiar in the Public Key Infrastructure (PKI) paradigm, where a central Certification Authority (CA) is responsible for verifying all the requests, and for issuing valid credentials (in this case Digital Certificates) to associate to private/public key pairs, using its root, or master key. One big weakness of the PKI paradigm is that the CA is a single point of trust, and failure, and its reliability is strongly dependent on how the CA maintains and securely stores its master key.

Many organizations are realizing that by using the services of a 3rd party certificate authority, or any security vendor that holds a root key, or seed value, they are placing an inappropriate level of trust and leaking personally identifiable information about end users that may violate regulatory standards and put their organization at risk.

### M-Pin Platform's Distributed Trusted Authority Architecture Overview

The Distributed Trusted Authority architecture of the M-Pin Strong Authentication Platform ("M-Pin Platform" for short) has been designed to address these weaknesses.

The picture below represents schematically the M-Pin Strong Authentication Platform – all components reside in the MIRACL customer environment, with the exception of the MIRACL run D-TA service, which issues key shares' to customer.

![7-m-pin-platform](\data\assets\images\chunks\7-m-pin-platform.jpg)

The M-Pin Platform's architecture is designed to distribute the single point of compromise between MIRACL and its customers. For this reason, M-Pin TA is split into two Distributed TAs: MIRACL D-TA and Customer D-TA. Each MIRACL customer runs its own D-TA, and for each Customer D-TA, MIRACL runs a corresponding MIRACL D-TA. The two D-TAs do not communicate in any way.

MIRACL hosts a dedicated D-TA for each paying customer.

The picture below represents schematically the Distributed Trust Authorities and demonstrates how this distributed architecture removes insider threats and single points of compromise.

![2-DTA-nodes-overlay](\data\assets\images\chunks\2-DTA-nodes-overlay.jpg)

### MIRACL D-TA Operation

The MIRACL D-TA issues:

*   One share of the M-Pin Server Key to Customers, to be used when setting up M-Pin Core
*   One share of the M-Pin Client Key to Customers' clients, issued when an end user registers
*   One share of the Time Permit to Customers' clients, issued when an end user authenticates

All the above elements are needed to perform the M-Pin Authentication, together with a correspondent share issued by the M-Pin Core deployed, owned and managed by MIRACL customers.

### MIRACL D-TA Privacy and Security

MIRACL personnel is never exposed to the unencrypted Master Key inside of the customer's D-TA service at  MIRACL. The Master Key of each Enterprise-Tier Customer is housed in each distinct D-TA Service is cryptographically protected with FIPS 140-2 Level 3 hardware security module. Because the D-TA architecture removes the single point of compromise, in order to have a security breach equivalent to a PKI root key breach or 2FA seed value breach, both Master Keys inside the D-TA services, at MIRACL and MIRACL's customer, must be compromised.

Customers gain the benefit of the security efficacy achieved using FIPS validated hardware security modules, without having to invest in resources or infrastructure to maintain this level of security. MIRACL houses its D-TA infrastructure at ISO/IEC 27001 certified data center locations in the European Union for resiliency and high availability, offering 100% uptime of its D-TA service.

Additionally, when the MIRACL API receives a request for a M-Pin Client Key share, the request is made in a cryptographically secured manner, in which the identity of the end user, which is bound to the requested M-Pin Client Key, is hashed through a one-way function, so that MIRACL never receives any personally identifiable information about who our customer's end users are.

As an example, user John Doe may have three M-Pin Client Keys issued, one for each device he owns. MIRACL has no way to ascertain the identity of the M-Pin Client Keys (that they belong to John Doe) or that they are related to any one identity whatsoever.

## M-Pin User Setup Overview

M-Pin adds multi-factor authentication to its zero-knowledge proof protocol by splitting the M-Pin Client Key into, at a minimum, two parts; an M-Pin Token, so that it is no longer representative of the end user's identity, and a low entropy PIN or passphrase:

*   End users choose their PIN - nobody else knows it, it's not stored anywhere
*   Programmatically, the PIN is "extracted" from the M-Pin Client Key, and ONLY the resulting token (M-Pin Token) is stored in the browser, locked to the domain of the issuer, or stored in secured storage within an app
*   Neither the PIN, nor the M-Pin Token, or the combination of the two is ever exchanged between client and server; this is the benefit of zero-knowledge proof protocols

The picture below represents schematically the M-Pin User Setup process – splitting the M-Pin Client Key into an M-Pin Token and PIN or other factors.

![3-m-pin-setup-overlay](\data\assets\images\chunks\3-m-pin-setup-overlay.jpg)

## M-Pin Authentication Overview

To successfully authenticate with M-Pin, an end user must have access to two factors:

*   The token in the browser or application: "something you have"
*   The PIN number: "something you know"

The level of security is the same used in payment systems by the coupling of credit/debit cards and PIN numbers. M-Pin is arguably more secure, as the client key and the PIN are never stored. M-Pin is an online authentication protocol, it is impossible to mount an offline attack, and so the configurable number of incorrect attempts can result in the revocation of an M-Pin Client Key according the security guidelines set by an application.

To enable revocation of users who have already been issued with a valid client key, M-Pin introduces the concept of Time Permits. Before the actual authentication protocol is started, the end user must request a valid Time Permit. If no valid Time Permit is available, the M-Pin protocol simply doesn't start, and the authentication cannot be performed.

The picture below represents schematically the M-Pin Authentication – recombining from PIN/Passphrase + M-Pin Token and optionally additional factors.

![4-m-pin-login-overlay](http://cdn2.hubspot.net/hub/230906/file-2142907027-jpg/Images-cos/diagrams/4-m-pin-login-overlay-235200-edited.jpg)
