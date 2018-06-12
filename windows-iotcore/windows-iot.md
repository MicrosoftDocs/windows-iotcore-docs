---
title: Overview of Windows 10 IoT 
author: saraclay
ms.author: saclayt
ms.date: 01/30/2018
ms.topic: article
description: Learn about what Windows 10 IoT is and what you can do with it.
keywords: Windows 10 IoT Enterprise, Windows 10 IoT Core, headless, speech, features, binary edition, editions 
---

# An overview of Windows 10 IoT 

## What is Windows 10 IoT?
Windows 10 IoT is a member of the Windows 10 family that brings enterprise-class power, security and manageability to the Internet of Things.  It leverages Windows' embedded experience, ecosystem and cloud connectivity, allowing organizations to create their Internet of Things with secure devices that can be quickly provisioned, easily managed, and seamlessly connected to an overall cloud strategy.  

## Windows 10 IoT Editions
Windows 10 IoT comes in two editions.  Windows 10 IoT Core is the smallest member of the Windows 10 operating system family.  While only running a single app, it still has the manageability and security expected from Windows 10.  By contrast, Windows 10 IoT Enterprise is a full version of Windows 10 with specialized features to create dedicated devices locked down to a specific set of applications and peripherals. 

## Differences between Windows 10 IoT Core and Windows 10 IoT Enterprise

While Windows 10 IoT Core and Windows 10 IoT Enterprise are similar in name, there are differences in what they offer as well as what they support. Below is a feature list that highlights edition differences.

> |             | Windows 10 IoT Core  |  Windows 10 IoT Enterprise  |
> |-------------|----------|---------|
> | User experience | Single UWP app running at startup with supporting background apps and services. | Traditional Windows Shell with Advanced Lockdown Features |
> | Headless supported | Yes | Yes |
> | App architecture supported | UWP only | UWP and Win32 |
> | Cortana | [*Cortana SDK*](https://developer.microsoft.com/en-us/cortana/devices) | Yes |
> | Domain join | AAD only | AAD and Traditional Domain |
> | Management | MDM | MDM |
> | Device Security Technologies | [TPM](https://docs.microsoft.com/en-us/windows/iot-core/secure-your-device/tpm), [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/en-us/windows/iot-core/secure-your-device/securebootandbitlocker), and Device Health Attestation | TPM, [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/en-us/windows/iot-core/secure-your-device/securebootandbitlocker), Defender ATP, and Device Health Attestation |
> | CPU Architecture support | x86, x64, and ARM | x86 and x64 |
> | Licensing | Online Licensing Agreement and Embedded OEM Agreements, Royalty-free | Direct and Indirect Embedded OEM Agreements |
> | Usage scenarios | [Digital Signage](https://www.microsoft.com/en-us/windowsforbusiness/digital-signage), Smart Building, IoT Gateway, HMI, Smart Home, Wearables | Industry Tablets, POS, Kiosk, [Digital Signage](https://www.microsoft.com/en-us/windowsforbusiness/digital-signage), ATM, Medical Devices, Manufacturing Devices, Thin Client |

For minimum requirement details, please visit [the Windows Hardware site](https://docs.microsoft.com/en-us/windows-hardware/design/minimum/minimum-hardware-requirements-overview).


## Helpful resources
* [Windows 10 IoT Enterprise](windows-iot-enterprise.md)
* [Windows 10 IoT Core](windows-iot-core.md)