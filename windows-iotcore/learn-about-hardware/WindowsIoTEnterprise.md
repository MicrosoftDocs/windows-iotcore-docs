---
title: Overview of Windows 10 IoT Enterprise
author: saraclay
ms.author: saclayt
ms.date: 01/18/2017
ms.topic: article
description: Learn about what Windows 10 IoT Enterprise is and what you can do with it.
keywords: windows 10 IoT Enterprise, Enterprise, binary, Windows
---

# An overview of Windows 10 IoT Enterprise

## What is Windows 10 IoT Enterprise?
Windows 10 IoT Enterprise is a full version of Windows 10 that delivers enterprise manageability and security to IoT solutions. It is a binary equivalent to Windows 10 Enterprise, so if you already know how Windows 10 Enterprise works, a lot of that knowledge is transferrable to Windows 10 IoT Enterprise. However, when it comes to licensing and distribution, the desktop version and IoT version differ. 

## Getting Started 
Before reaching out to an Embedded/IoT Distributor, we recommend working with one of the following devices:
Jason to fill in

In order to start your journey in manufacturing with Windows 10 IoT Enterprise, you will need to reach out to a distributor from [this list](http://wincom.blob.core.windows.net/documents/Windows_IoT_Distributor_Information.pdf). We recommend contacting Avnet or Arrow as they have prior experience with Windows 10 IoT Enterprise.

## Fixed purpose devices 
Jason to fill in

## Differences between Windows 10 IoT Core and Windows 10 IoT Enterprise
While Windows 10 IoT Core and Windows 10 IoT Enterprise are similar in name, there are quite a few differences in what they offer as well as what they support. Below is a feature list that highlights editions differences.

For minimum requirement details, please visit [the Windows Hardware site](https://docs.microsoft.com/en-us/windows-hardware/design/minimum/minimum-hardware-requirements-overview).

> |             |  IoT Core  |  IoT Enterprise  |
> |-------------|----------|---------|
> | User experience | Single UWP app running at startup with supporting background apps and services. | Traditional Windows Shell with Advanced Lockdown Features |
> | Headless supported | Yes | Yes |
> | App architecture supported | UWP only | UWP and Win32 |
> | Cortana | Yes (display required) | Yes |
> | Domain join | AAD only (RS3) | AAD and Traditional Domain |
> | Management | MDM | MDM and Traditional Agent Based (e.g. SCCM) |
> | Device Security Technologies | TPM, Secure Boot, BitLocker and Device Guard | TPM, Secure Boot, BitLocker, Device Guard, Defender ATP, and Device Health Attestation |
> | CPU Architecture support | x86, x64, and ARM | x86 and x64 |
> | Licensing | Online licensing terms agreement and Embeded OEM Agreements, Royalty-free | Direct and indirect Embedded OEM Agreements |
> | Usage scenarios | Digital signage, smart building, IoT Gateway, HMI, smart home devices, wearables | Industry tablets, POS, kiosk, digital signage, ATM, medical devices, manufacturing devices, Thin client |

## Helpful resources
* [Desktop manufacturing](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/)
* [Unified Write Filter for Windows 10](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/unified-write-filter)
* [Assigned Access for Enterprise & Pro](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/assigned-access)
* [Shell Launcher for Enterprise and Education editions](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/shell-launcher)
* [Lockdown resources](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/create-a-kiosk-image) 
* [Configure Windows telemetry in your organization](https://docs.microsoft.com/en-us/windows/configuration/configure-windows-telemetry-in-your-organization )
* [Configure kiosk and shared devices running Windows desktop editions](https://docs.microsoft.com/en-us/windows/configuration/kiosk-shared-pc)
