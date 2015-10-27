---
content_type: Chunks
title: Docs M-Pin SSO - M-Pin SSO AWS 3.3 Release Notes
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Release notes for:

M-Pin SSO for AWS v 3.3

## Official Release Date:

11th November 2014

## What’s new:

*   First public release of the new M-Pin SSO Server
*   Currently available only as AMI's on AWS
*   Available as both Free & Enterprise tier AMI's
*   One-time-password generation for RADIUS clients (previously available in M-Pin Arion) is now merged into the M-Pin SSO product

## Supported Platforms:

Amazon EC2, Amazon EBS

## Minimum System Requirements:

t2.small EC2 instance

## Amazon AWS Marketplace Links:

[M-Pin SSO Server for Strong Authentication - Free Tier AMI](https://aws.amazon.com/marketplace/pp/B00PB4WX64)
[M-Pin SSO Server for Strong Authentication - Enterprise Tier AMI](https://aws.amazon.com/marketplace/pp/B00PB4X0SY)

## Distribution of Enterprise-Tier server keys:

Free tier credentials.json will automatically be downloaded and installed when launching the M-Pin SSO Free-tier AMI
Enterprise tier credentials.json will automatically be downloaded and installed when launching the M-Pin SSO Enterprise-tier AMI

## Upgrade instructions from free tier to enterprise tier:

If you wish to upgrade from the free tier to the enterprise tier, please launch a new instance of the M-Pin SSO Enterprise tier AMI.

If you do not wish to lose the configuration of your free tier instance, please contact your MIRACL representative for instructions on how to perform a true upgrade from the free tier to the enterprise tier.

## Bugs fixed:

n/a (first release of M-Pin SSO Server on AWS)

## Known Bugs:

The mobile application is not currently supported on Windows Mobile
There are additionally some known bugs running M-Pin-In-Browser in the desktop version of Internet Explorer 10 or higher (earlier versions are not supported) that are currently being resolved by MIRACL.

## Documentation:

[AWS Product Access Instructions](/docs/m-pin-sso/access)

[M-Pin SSO Server Getting Started Guide](/docs/m-pin-sso/m-pin-sso-for-aws-getting-started-guide)

[M-Pin SSO Server Configuration Guide](/docs/m-pin-sso/m-pin-sso-configuration-guide)
