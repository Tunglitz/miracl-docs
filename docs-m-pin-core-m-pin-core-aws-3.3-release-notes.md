---
content_type: Chunks
title: Docs M-Pin Core - M=Pin Core AWS 3.3 Release Notes
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Release notes for:

M-Pin Core for AWS v 3.3

## Official Release Date:

11th November 2014

## What’s new:

*   First preview version of the new M-Pin API
*   High availability support using Redis key-value store
*   Communication between the M-Pin Server, DTA & RPS services are now signed
*   First public release of M-Pin Core on the AWS Marketplace

## Supported Platforms:

Amazon EC2, Amazon EBS

## Minimum System Requirements:

t2.micro EC2 instance

## Source Code:

We will be releasing the source code for the M-Pin services, PIN pad & mobile client application shortly on the [MIRACL GitHub](https://github.com/miraclhq) page.

## Amazon AWS Marketplace Links:

[M-Pin Core Server for Strong Authentication - Free Tier AMI](https://aws.amazon.com/marketplace/pp/B00PB4WZ4O)
[M-Pin Core Server for Strong Authentication - Enterprise Tier AMI](https://aws.amazon.com/marketplace/pp/B00PB4X3D6)

## Distribution of Enterprise-Tier server keys:

Free tier credentials.json will automatically be downloaded and installed when launching the M-Pin Core Free-tier AMI

Enterprise tier credentials.json will automatically be downloaded and installed when launching the M-Pin Core Enterprise-tier AMI

## Upgrade instructions from free tier to enterprise tier:

If you wish to upgrade from the free tier to the enterprise tier, please launch a new instance of the M-Pin Core Enterprise tier AMI.

If you do not wish to lose the configuration of your free tier instance, please contact your MIRACL representative for instructions on how to perform a true upgrade from the free tier to the enterprise tier.

## Bugs fixed:

n/a - first release of M-Pin Core for AWS

## Known Bugs

The mobile application is not currently supported on Windows Mobile.
There are additionally some known bugs running M-Pin-In-Browser in the desktop version of Internet Explorer 10 or higher (earlier versions are not supported) that are currently being resolved by MIRACL.

## Documentation:

[AWS Product Access Instructions](http://www.certivox.com/docs/m-pin-core/access)
[M-Pin Core Configuration Guide](/docs/m-pin-core/m-pin-core-config-guide)
