---
title: IoT Core Introduction
author: lmaung
ms.author: lmaung

ms.date: 10/1/2018 
ms.topic: article 
description: Windows IoT Core Introduction
keywords: Windows 10 IoT Core, 
---

# What is Windows 10 IoT?
Windows 10 IoT is a member of the Windows 10 family that brings enterprise-class power, security and manageability to the Internet of Things.  It leverages Windows' embedded experience, ecosystem and cloud connectivity, allowing organizations to create their Internet of Things with secure devices that can be quickly provisioned, easily managed, and seamlessly connected to an overall cloud strategy.  

## Windows 10 IoT Editions
Windows 10 IoT comes in two editions.  Windows 10 IoT Core is the smallest member of the Windows 10 operating system family.  While only running a single app, it still has the manageability and security expected from Windows 10.  By contrast, Windows 10 IoT Enterprise is a full version of Windows 10 with specialized features to create dedicated devices locked down to a specific set of applications and peripherals. 

## What is Windows 10 IoT Core
Windows IoT Core is a version of Windows 10 that is optimized for smaller devices with or without a display that run on both ARM and x86/x64 devices browser.

Windows 10 IoT Core supports a variety of peripheral interfaces and protocols, including support for common busses like I2C, UART, USB, and more.

## Why do you want to use IoT Core?
Windows 10 IoT Core allows for you to get your device to market quicker while leveraging on enterprise-class security and managebility. Additionally, IoT Core allows to integrate with latest state of the art Ai/ML features to create devices that are intelligent on the edge of the cloud while integrating with cloud infrastructes and offerings.

*As long as you have Board Support Package drivers.

## How to create Windows IoT Core Image 
Follow instructions and directions on this [IoT Core Manufacturing Guide](GuideOverview.md) to create Test, and Retail IoT Core images for mass-production of IoT devices.

If you have prior knowledge of image creation and just want to quickly go through a checklist based guide to create a test image, follow this [quick start guide](QuickStartGuide.md)

---
## Differences between Windows 10 IoT Core and Windows 10 IoT Enterprise

While Windows 10 IoT Core and Windows 10 IoT Enterprise are similar in name, there are differences in what they offer as well as what they support. Below is a feature list that highlights edition differences.

> |             | Windows 10 IoT Core  |  Windows 10 IoT Enterprise  |
> |-------------|----------|---------|
> | User experience | One UWP app in the foreground at a time (see [IoT Shell documentation](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/iotcoreshell) for app backstack handling) with supporting background apps and services. | Traditional Windows Shell with Advanced Lockdown Features |
> | Headless supported | Yes | Yes |
> | App architecture supported | UWP UI only | Full Windows UI support (e.g. UWP, WinForms, etc) |
> | Cortana | [*Cortana SDK*](https://developer.microsoft.com/en-us/cortana/devices) | Yes |
> | Domain join | AAD only | AAD and Traditional Domain |
> | Management | MDM | MDM |
> | Device Security Technologies | [TPM](https://docs.microsoft.com/windows/iot-core/secure-your-device/tpm), [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/windows/iot-core/secure-your-device/securebootandbitlocker), and Device Health Attestation | [TPM](https://docs.microsoft.com/windows/iot-core/secure-your-device/tpm), [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/windows/iot-core/secure-your-device/securebootandbitlocker) and Device Health Attestation |
> | CPU Architecture support | x86, x64, and ARM | x86 and x64 |
> | Licensing | Online Licensing Agreement and Embedded OEM Agreements, Royalty-free | Direct and Indirect Embedded OEM Agreements |
> | Usage scenarios | [Digital Signage](https://www.microsoft.com/en-us/windowsforbusiness/digital-signage), Smart Building, IoT Gateway, HMI, Smart Home, Wearables | Industry Tablets, POS, Kiosk, [Digital Signage](https://www.microsoft.com/en-us/windowsforbusiness/digital-signage), ATM, Medical Devices, Manufacturing Devices, Thin Client |

For minimum requirement details, please visit [the Windows Hardware site](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview).
