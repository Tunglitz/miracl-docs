---
content_type: Chunks
title: Docs M-Pin Core - M-Pin Core 3.3 Release Notes
marketing_text:
tags: 
keywords: 
last_updated: October 21, 2015
summary: 
---

## Release notes for:

M-Pin Core v 3.3

## Official Release Date:

21st October 2014

## What’s new:

*   First preview version of the new M-Pin API
*   High availability support using Redis key-value store
*   Communication between the M-Pin Server, DTA & RPS services are now signed

## Supported Platforms:

The M-Pin installer should work on any modern Linux distribution (kernel 2.6 or higher) with Python 2.7\. The M-Pin server may also be installed on Mac OSX 10.6 or higher, but this configuration is not recommended for production use.
MIRACL has tested M-Pin on the following distributions:

*   Red Hat 6
*   Red Hat 7
*   Ubuntu 12+

## Minimum System Requirements:

*   300MHz x86 processor
*   192 MB of system memory (RAM)
*   1GB of disk space

## Production URL for the installation:

python -c "$(curl -fsSL [https://mpin.certivox.net/v3/install)"](https://mpin.certivox.net/v3/install)")

Please see the  [M-Pin Core Quick Installation Guide](https://certivox.org/display/MPINDOC/M-Pin+Core+Quick+Installation+Guide) for details on how to install and the [M-Pin Core Configuration Guide](https://certivox.org/display/MPINDOC/M-Pin+Core+Configuration+Guide) for details on how to configure the M-Pin server.

## Source Code:

We will be releasing the source code for the M-Pin services, PIN pad & mobile client application shortly on the [MIRACL GitHub](https://github.com/miraclhq) page

## Distribution of Enterprise-Tier server keys:

This release will automatically download and install the keys.json file for the free tier version of M-Pin Core. Please contact your MIRACL representative to obtain the keys for the Enterprise tier.

## Upgrade instructions from free tier to enterprise tier:

The new credentials.json file should be placed into the M-Pin installation directory (/opt/mpin/ by default) then the M-Pin services should be restarted.

## Bugs fixed:

n/a - first public release

## Known Bugs

The mobile application is not currently supported on Windows Mobile</span>

There are additionally some known bugs running M-Pin-In-Browser in the desktop version of Internet Explorer 10 or higher (earlier versions are not supported) that are currently being resolved by MIRACL.

## Documentation:

[M-Pin Core Quick Installation Guide ](/docs/m-pin-core/quick-install-guide)

[M-Pin Core Configuration Guide](/docs/m-pin-core/m-pin-core-config-guide)
