---
content_type: Chunks
title: Docs M-Pin Core - Technologies and 3rd Party Software
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## General

This document describes the technologies and 3rd party software used by the different components of the M-Pin solution. It is targeted at Technical Staff - Developers, DevOps System Administrators, System Integrators, and QA personnel.

## System Overview

The M-Pin System consists of Client (front-end) and two groups of Services (back-end) - Customer-hosted Services and MIRACL-hosted Services.

### Client

*   Browser PIN Pad - The Client which runs on the end-user's Browser.
*   Mobile App - The Client which runs on the end-user's Mobile Device. It is also sometimes referred to as Mobile PIN Pad.

### Customer-hosted Services

*   M-Pin Server - The Authentication Server against which End-Users authenticate. The Client (PIN Pad) performs the "M-Pin Dance" against the M-Pin server in order to authenticate an End-User.
*   D-TA - Distributed Trusted Authority Service, managed by the Customer. Responsible to generate Client and Server Secret Shares as well as Time Permit Shares
*   RPS - Relying Party Service. Implements the M-Pin Protocol and Workflows on behalf of the Customer. The RPS serves as an abstraction layer between the specific implementation of the M-Pin Protocol and the RPA.
*   RPA - Relying Party Application. This is the Application to which end-users are authenticated through the M-Pin System. *This application is implemented/managed by the Customer and is strictly specific for each different Customer.*

### MIRACL-hosted Services

*   D-TA - Distributed Trusted Authority Service, managed by MIRACL. Responsible for generating Client and Server Secret Shares as well as Time Permit Shares.
*   D-TA Proxy - Proxies request to the D-TA, validating RPS signatures. The D-TA Proxy is public-facing, while the D-TA should not be publicly accessible.
*   Time Permits Service - A service responsible to publish Time Permits to an online storage (CDN), such as AWS S3.
*   Registration Service - A service that handles new Customer registration.

## Technologies

[missing table]

* - Additional Linux distributions might be supported as well, but they were not tested

## 3rd Party Components

[missing table]


