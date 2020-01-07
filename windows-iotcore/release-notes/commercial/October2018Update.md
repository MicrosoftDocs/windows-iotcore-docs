---
title: October 2018 Update - Build 17763
ms.date: 10/02/2018
ms.topic: article
description: Learn about what's new in the October 2018 Update for Windows.
keywords: Windows IoT, October 2018 Update, release notes
---

# October 2018 Update Release Notes for Windows 10 IoT
Build Number 17763. October 2018

> [!IMPORTANT]
> If you're using the [October 2018 Update](https://docs.microsoft.com/windows/iot-core/release-notes/commercial/october2018update), please use the [October Update (with January servicing pack, build 17763.253)](https://docs.microsoft.com/windows/iot-core/release-notes/commercial/17763) release instead. We have found that there are known issues that affect users of the October 2018 Update. 

Windows 10 IoT enables development of embedded or dedicated-purpose devices and is the choice for OEMs and developers building Windows solutions for smart devices.

This document provides information that supplements other content and documentation for this release of Windows 10 IoT.

## Privacy Statement

The privacy statement for this version of the Windows operating system can be viewed at [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).

## What's New in October 2018 Update

_Windows 10 IoT Enterprise & Windows 10 IoT Core_
* The Windows 10 IoT October 2018 Update will have 10 years of support for both IoT Core and IoT Enterprise.
* [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/quickstart) is a fully managed service that delivers cloud intelligence locally by deploying and running artificial (AI) workloads, Azure services, and custom logic directly on Windows 10 IoT devices.
* [Windows Machine Learning](https://docs.microsoft.com/windows/ai/) allows developers to use pretrained machine learning models in their applications. These models are typically trained in the cloud to be evaluated at the edge. Local evaluation on devices running Windows 10 IoT helps mitigate concerns of connectivity, bandwidth, and data privacy.  

_Windows 10 IoT Core_
* [Windows 10 IoT Core Services](https://docs.microsoft.com/windows-hardware/manufacture/iot/iotcoreservicesoverview) subscription is now generally available. This subscription comes with three main benefits including 10 years of OS support, update control with the [Device Update Center](https://docs.microsoft.com/windows-hardware/service/iot/using-device-update-center), and Device Health Attestation (DHA).
* To meet growing customer and partner demand for silicon diversity, Microsoft, in close partnership with NXP, have added support for NXP i.MX 6, 7, and 8M series processors to Windows 10 IoT Core. 
* Qualcomm and Microsoft have created a solution that combines Windows 10 IoT Enterprise with Snapdragon processors to build devices that consume less power, are always connected and wake instantly. Long battery life enables dedicated devices like mobile POS and line-of-business tablets to last a full day of heavy use. 
* [The Windows 10 IoT Core Default App](https://docs.microsoft.com/windows/iot-core/develop-your-app/iotcoredefaultapp) has more features that users can leverage for their own applications, especially when bringing their devices to market. These features include weather, inking capabilities, audio capabilities. 
* If you are building an open retail device for commercial deployment to a "specific/limited installation" (i.e. factory or retail store) where the end-user does the final configuration and you document your customers that they must [obtain a certificate for WDP and install it on both WDP and connecting browsers and passwords are changed on WDP](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-ssl), then using WDP in this narrow commercial instance is acceptable. Retail images in this scenario should still not include IOT_TOOLKIT, but should use the IOT_WEBBEXTN package to pull in WDP. 
* Limpet.exe is now available as an [open source project](https://github.com/ms-iot/azure-dm-client). To make testing easier, we have a non-signed, pre-built version of Limpet.exe available and can be downloaded right from WDP. Learn more about this feature from the [Windows Device Portal documentation](https://docs.microsoft.com/windows/iot-core/manage-your-device/deviceportal).  
* With RS5, developers are now able to flash custom FFUs onto their device using the Dashboard. This can be done with either the DragonBoard 410C or NXP. Learn more and get started [here](https://docs.microsoft.com/windows/iot-core/tutorials/quickstarter/devicesetup).
* Windows 10 IoT Core now uses the same touch keyboard components as the desktop edition of Windows which allows for features like dictation mode, the entire set of Windows keyboard language layouts, and more. This new update also includes supprt for emoticons, most input "scopes", and better multi-lang support. Learn how to leverage these features [here](https://docs.microsoft.com/windows/iot-core/develop-your-app/onscreenkeyboard).
* Learn how to [configure your device to allow to be turned off](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/wakeontouch) while not in use and to be turned on when a user touches a screen.
* Bluetooth A2DP-SINK is now optionally supported (e.g. Allows playback from remote source such as iPhone to IoT device) and Bluetooth A2DP-SRC is now an optional package (was available by default in the April 2018 Release). You can control Bluetooth A2DP-SRC and A2DP-SINK profile preferences when both profiles are present and when pairing with another device that also supports both. 
* By design, Windows 10 IoT Core does not display an application frame around an application’s window – in order words, an application is shown as full screen. But with this release, developers have the option of [configuring title bars](https://docs.microsoft.com/windows/iot-core/develop-your-app/signindialogtitlebars).
* Bus tools that allow you to interact with Gpio, I2c, Spi and UART are now available in [our samples repository](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/BusTools). These tools will run on any edition of Windows including Windows 10 IoT Core and Windows Enterprise. 
* [The Windows.System.Update Namespace API](https://docs.microsoft.com/uwp/api/windows.system.update) enables calls for interactive control of system updates. This namespace is only available for Windows 10 IoT Core.
* If you're looking to use IoT Central as part of a Windows 10 IoT solution, you can now prepare and [connect a Windows 10 IoT Core device to your Azure IoT Central application](https://docs.microsoft.com/azure/iot-central/howto-connect-windowsiotcore). 
* The release for the Raspberry Pi 3B+ (the downloadable ISO can be found [here](https://go.microsoft.com/fwlink/?LinkID=708576)) is a technical preview and there is currently no timeline for a release version. For a better evaluation experience and fr any commercial products, please use the Raspberry Pi 3B or other devices with supported Intel, Qualcomm or NXP SoCs. 

## IoT Enterprise Manufacturing Guide

* A new manufacturing guide for Windows 10 IoT Enterprise is [now available](https://docs.microsoft.com/windows-hardware/manufacture/desktop/iot-ent-overview). 

## Improvements in Assigned Access 

_Windows 10 IoT Enterprise_

* Kiosks and digital signs are often place in public places where issues are widely seen by people. With built-in status reporting, device management systems are automatically made aware of problems and can issue corrective actions like restarting the device or dispatching a service technician. 
* Reducing deployment and management costs are key drivers of ROI. Windows 10 IoT Enterprise has improved features for configuring a kiosk experience via a new wizard in the Settings app, managing multi-app kiosks and tailoring the [Microsoft Edge browser experience for kiosk devices](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy).
* While device builders have great flexibility to configure Assigned Access using provisioning packages, the Settings app, and mobile device management systems, some customers still need more. [Using a new set of Assigned Access APIs](https://docs.microsoft.com/uwp/api/windows.system.userprofile.assignedaccesssettings), developers can now configure Assigned Access programmatically from within their applications.
* With the October 2018 release, customers can specify an auto-launch experience as part of the multi-app assigned access configuration so the end user can always have a default primary app experience.
* You can control what the user sees from the moment the device is turned on until it's powered off. Starting by showing your logo instead of the Windows logo at boot, or auto-restart apps without error messages after an app crash, a system issue or a power interruption. 
* You can use the Unified Write Filter (UWF) feature to build a "read-only" device that returns to a known state after a power cycle by keeping disk changes in memory instead of writing them to disk. You can also combine UWF with the Hibernate Once, Resume Many (HORM) feature to resume to a predefined session. 


## More Management Support

_Windows 10 IoT Enterprise_
* Azure IoT Hub offers lightweight device management features and an extensibility model that enable device and cloud developers to build robust device management solutions. Integration with [Azure IoT Device Management](https://docs.microsoft.com/windows/iot-core/manage-your-device/azureiotdm) is now available for both Windows 10 IoT Core and Enterprise. 

_Windows 10 IoT Core_
* Enterprises that use [Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) for their device management can now manage Windows 10 IoT Core devices alongside their Windows 10 IoT Enterprise devices and other managed devices. This gives operators a consistent way to manage Windows 10 IoT devices using the same management interface and controls. 


## Windows 10 IoT Core Reference Images
___ 
* Minnowboard Max
  * Processor: Intel Atom E3825
  * Architecture: x86

* Raspberry Pi 3 Model B
  * Processor: Broadcom BCM2837
  * Architecture: ARM

* DragonBoard 410c
  * Processor: Qualcomm Snapdragon 410
  * Architecture: ARM
  * BSP Version: 2120.0.0.0


## Known Issues
* F5 driver deployment from Visual Studio does not work on Windows 10 IoT Core. Drivers must be manually copied and registered on the device.
* Devices that were installed via NOOBS cannot run the bcdedit tool to enable the kernel debugger.
* The Windows IoT Remote client does not work for Raspberry Pi. Use a board with accelerated graphics such as Minnowboard Max or Dragonboard or attach a monitor for local display.
