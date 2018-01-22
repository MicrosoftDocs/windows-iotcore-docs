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
Before reaching out to an Embedded/IoT Distributor, we recommend working with one of [these devices](https://solutionsdirectory.intel.com/solutions-directory/processors/736/processors/766/processors/782/processors/788/processors/869/processors/879/processors/883/processors/888/processors/1053/processors/1058/processors/1103/processors/1107/processors/1110/processors/1117/processors/1133/processors/1135/processors/1139/processors/1141/processors/1175/processors/1192/processors/1344/processors/1348/processors/1349/processors/1371/processors/1392/processors/1729/processors/2284).  You can load your PC or recommended device with an [evaluation copy](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise) of Windows 10 Enterprise in order to begin prototyping right away.

In order to start your journey in manufacturing with Windows 10 IoT Enterprise, you will need to reach out to a distributor from [this list](http://wincom.blob.core.windows.net/documents/Windows_IoT_Distributor_Information.pdf). 

## Fixed purpose devices 

> [TIP]
> See your licensing agreement for complete guidance on all Windows IoT Enterprise usage scenarios.

The Windows IoT Enterprise edition is licensed to allow you to build fixed purpose devices like Thin Clients, ATM Machines, Point-of-Sale Terminals, Industrial Automation Systems, etc.  There are specific allowances and restrictions in the license agreement. 

In general a fixed purpose device differs from a general purpose device in the following ways:  
* The device is locked down to a single application or fixed set of applications through the Assigned Access or Shell Launcher features.  
* The device powers-on immediately to the experience when recieved by the end-customer. This is achieved by configuring the device image to skip the normal Windows out-of-box experiences.
* Keyboards, USB ports, and device policies are locked down to constrain the device to be used only in its fixed purpose.  
* The OEM licenses the device to the user with the software attached to the device as a complete product and passes through specific Windows terms in thier own agreements.

## Differences between Windows 10 IoT Core and Windows 10 IoT Enterprise
While Windows 10 IoT Core and Windows 10 IoT Enterprise are similar in name, there are differences in what they offer as well as what they support. Below is a feature list that highlights edition differences.

For minimum requirement details, please visit [the Windows Hardware site](https://docs.microsoft.com/en-us/windows-hardware/design/minimum/minimum-hardware-requirements-overview).

> |             |  IoT Core  |  IoT Enterprise  |
> |-------------|----------|---------|
> | User experience | Single UWP app running at startup with supporting background apps and services. | Traditional Windows Shell with Advanced Lockdown Features |
> | Headless supported | Yes | Yes |
> | App architecture supported | UWP only | UWP and Win32 |
> | Cortana | *Cortana SDK* | Yes |
> | Domain join | AAD only | AAD and Traditional Domain |
> | Management | MDM | MDM |
> | Device Security Technologies | TPM, Secure Boot, BitLocker, Device Health Attestation, and Device Guard for IoT | TPM, Secure Boot, BitLocker, Device Guard, Defender ATP, and Device Health Attestation |
> | CPU Architecture support | x86, x64, and ARM | x86 and x64 |
> | Licensing | Online Licensing Agreement and Embedded OEM Agreements, Royalty-free | Direct and Indirect Embedded OEM Agreements |
> | Usage scenarios | Digital Signage, Smart Building, IoT Gateway, HMI, Smart Home, Wearables | Industry Tablets, POS, Kiosk, Digital Signage, ATM, Medical Devices, Manufacturing Devices, Thin Client |

## Helpful resources
> [!NOTE]
> Additional resources may be available from you distributor to explain Windows EPKEA OEM Activation and provide guidance in generating your manufacturing-ready Windows IoT Enterprise [WIM](https://msdn.microsoft.com/en-us/library/windows/desktop/dd861280.aspx) device image.

* [Desktop manufacturing](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/)
* [Unified Write Filter for Windows 10](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/unified-write-filter)
* [Assigned Access for Enterprise & Pro](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/assigned-access)
* [Shell Launcher for Enterprise and Education editions](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/shell-launcher)
* [Lockdown resources](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/create-a-kiosk-image) 
* [Enabling Embedded Mode and using Background Tasks on Windows IoT Enterprise](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/embeddedmode)
* [Configure Windows telemetry in your organization](https://docs.microsoft.com/en-us/windows/configuration/configure-windows-telemetry-in-your-organization )
* [Configure kiosk and shared devices running Windows desktop editions](https://docs.microsoft.com/en-us/windows/configuration/kiosk-shared-pc)
