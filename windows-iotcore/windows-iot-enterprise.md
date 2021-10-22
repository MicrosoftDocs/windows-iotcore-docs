---
title: Overview of Windows 10 IoT Enterprise
ms.date: 12/01/2020
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn about what Windows 10 IoT Enterprise is and what you can do with it.
keywords: Windows 10 IoT Enterprise, Enterprise, binary, Windows
---

# An overview of Windows 10 IoT Enterprise

## What is Windows 10 IoT Enterprise?
Windows 10 IoT Enterprise is a full version of Windows 10 that delivers enterprise manageability and security to IoT solutions. Windows 10 IoT Enterprise shares all the benefits of the world-wide Windows ecosystem. It is a binary equivalent to Windows 10 Enterprise, so you can use the same familiar development and management tools as client PCs and laptops.  However, when it comes to licensing and distribution, the desktop version and IoT versions differ. Note that Windows 10 IoT Enterprise offers both Long-term Servicing Channel (LTSC) and Semi-Annual Channel (SAC) options. OEMs can choose the version they require for their devices.

## Getting started

In order to start your journey in manufacturing with Windows 10 IoT Enterprise, you'll need to reach out to a [Windows IoT distributor](https://aka.ms/IoTDistributorList).

You can also try the Windows 10 IoT Enterprise [90 day evaluation](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise).

From there, you can learn how to manufacture with Windows 10 IoT Enterprise with our [the Windows 10 IoT Enterprise Manufacturing Guide](/windows-hardware/manufacture/desktop/iot-ent-overview).

## Fixed purpose devices

> [!TIP]
> See your licensing agreement for complete guidance on all Windows 10 IoT Enterprise usage scenarios. If you do not have this licensing agreement, ask the OEM you work with for the commercial agreement.

Windows is well known as the operating systems on laptop and desktops used by consumers and businesses world-wide.  What is less well known is that for years, Windows has also powered many ATM machines, point-of-sale terminals, industrial automation systems, thin clients, medical Devices, digital signage, kiosks, and other fixed purpose devices.  Windows 10 IoT Enterprise allows you to build fixed purpose devices with specific allowances and restrictions in the license agreement.  

A fixed purpose device differs from a general purpose device in the following ways:  
* The device is locked down to a single application or fixed set of applications through the Assigned Access or Shell Launcher features.  
* The device experience is immediate when the customer powers-on. This is achieved by configuring the device image to skip the normal Windows out-of-box experiences.
* Keyboards, USB ports, and device policies are locked down to constrain the device to be used only in its fixed purpose.  
* The OEM licenses the device to the user with the software attached to the device as a complete product and passes through specific Windows terms in their own agreements.
* The OEM provides the customer support for their complete product, including the functions performed by the operating system.

## Long-term Servicing Channel (LTSC)

Specialized systems, such as PCs that control medical equipment, point-of-sale systems, and ATMs, often require a longer servicing option because of their purpose. These devices typically perform a single important task and don’t need feature updates as frequently as other devices in the organization. It’s more important that these devices be kept as stable and secure as possible than that they be up to date with UI changes. The LTSC servicing model prevents Windows 10 IoT Enterprise LTSC devices from receiving the usual feature updates and provides only quality updates to ensure that device security stays up to date. With this in mind, quality updates are still immediately available to Windows 10 IoT Enterprise LTSC clients, but customers can choose to defer them by using one of the servicing tools mentioned in the Servicing tools section.

Microsoft makes available a new Windows 10 IoT Enterprise LTSC release approximately every three years. Each Windows 10 IoT Enterprise LTSC release is its own SKU and contains all the new capabilities and support updates included in the Windows 10 IoT Enterprise features updates since the previous LTSC release. To access these feature updates, a new Windows 10 IoT Enterprise LTSC SKU license must be purchased. For example, to get access to the new security, deployment, and management updates and features released since the launch of Windows 10 IoT Enterprise 2016 LTSC, a license for Windows 10 IoT Enterprise 2019 LTSC must be purchased, and an update applied to the device.

* [Learn more about LTSC](/windows/deployment/update/waas-overview#long-term-servicing-channel)

> [!NOTE]
> Due to the long life of the LTSC releases and the benefit of remaining on a specific release for 10 years, an upgrade fee will be charged for customers moving from one LTSC release to another.

## Long-Term Support Silicon Details

The Windows 10 IoT Enterprise 2019 release will be an LTSC release. See [here](/windows/whats-new/ltsc) for a general description of Windows 10 LTSC and other channels available. You can find details on processor support for each edition and channel of Windows 10 [here](/windows-hardware/design/minimum/windows-processor-requirements#windows-iot-enterprise--embedded-processor-table).

## Helpful resources
> [!NOTE]
> Additional resources may be available from your distributor to explain Windows EPKEA OEM Activation and provide guidance in generating your manufacturing-ready Windows IoT Enterprise [WIM](/previous-versions/msdn10/dd861280(v=msdn.10)) device image.

* [Customizations for enterprise desktop](/windows-hardware/customize/enterprise/enterprise-custom-portal)
* [Unified Write Filter for Windows 10](/windows-hardware/customize/enterprise/unified-write-filter)
* [Assigned Access for Enterprise & Pro](/windows-hardware/customize/enterprise/assigned-access)
* [Shell Launcher for Enterprise and Education editions](/windows-hardware/customize/enterprise/shell-launcher)
* [Lockdown resources](/windows-hardware/customize/enterprise/create-a-kiosk-image)
* [Enabling Embedded Mode and using Background Tasks on Windows IoT Enterprise](/windows/iot-core/develop-your-app/embeddedmode)
* [Configure Windows telemetry in your organization](/windows/configuration/configure-windows-telemetry-in-your-organization)
* [Configure kiosk and shared devices running Windows desktop editions](/windows/configuration/kiosk-shared-pc)
* [Desktop manufacturing](/windows-hardware/manufacture/desktop/)