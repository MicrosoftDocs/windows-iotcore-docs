---
title: October 2018 Update - Build 17763
author: saraclay
ms.author: saclayt
ms.date: 10/02/2018
ms.topic: article
description: Learn about what's new in the October 2018 Update for Windows.
keywords: Windows IoT, October 2018 Update, release notes
---

# October 2018 Update Release Notes for Windows 10 IoT
Build Number 17763. October 2018

Windows 10 IoT enables development of embedded or dedicated-purpose devices and is the choice for OEMs and developers building Windows solutions for smart devices.

This document provides information that supplements other content and documentation for this release of Windows 10 IoT.

## Privacy Statement

The privacy statement for this version of the Windows operating system can be viewed at [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).

## What's New in October 2018 Update
* [Windows 10 IoT Core Services](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iotcoreservicesoverview) subscription is now generally available. This subscription comes with three main benefits including 10 years of OS support, update control with the [Device Update Center](https://docs.microsoft.com/en-us/windows-hardware/service/iot/using-device-update-center), and Device Health Attestation (DHA).
* [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/quickstart) is a fully managed service that delivers cloud intelligence locally by deploying and running artificial (AI) workloads, Azure services, and custom logic directly on Windows 10 IoT devices.
* [Windows Machine Learning](https://docs.microsoft.com/windows/ai/) allows developers to use pretrained machine learning models in their applications. These models are typically trained in the cloud to be evaluated at the edge. Local evaluation on devices running Windows 10 IoT helps mitigate concerns of connectivity, bandwidth, and data privacy. 
* To meet growing customer and partner demand for silicon diversity, Microsoft, in close partnership with NXP, have added support for NXp i.mX 6, 7, and 8 series processors to Windows 10 IoT Core. 
* [The Windows 10 IoT Core Default App](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/iotcoredefaultapp) has more features that users can leverage for their own applications, especially when bringing their devices to market. These features include weather, inking capabilities, audio capabilities. 
* With RS5, developers are now able to flash custom FFUs onto their device using the Dashboard. This can be done with either the DragonBoard 410C or NXP. Learn more and get started [here](https://docs.microsoft.com/en-us/windows/iot-core/tutorials/quickstarter/devicesetup).
* Windows 10 IoT Core now uses the same touch keyboard components as the desktop edition of Windows which allows for features like dictation mode, the entire set of Windows keyboard language layouts, and more. Learn how to leverage these features [here](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/onscreenkeyboard).
* Learn how to [configure your device to allow to be turned off](https://docs.microsoft.com/en-us/windows/iot-core/learn-about-hardware/wakeontouch) while not in use and to be turned on when a user touches a screen.
* By design, Windows 10 IoT Core does not display an application frame around an application’s window – in order words, an application is shown as full screen. But with this release, developers have the option of [configuring title bars](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/signindialogtitlebars).
* [The Windows.System.Update Namespace API](https://docs.microsoft.com/en-us/uwp/api/windows.system.update) enables calls for interactive control of system updates. This namespace is only available for Windows 10 IoT Core.
* If you're looking to use IoT Central as part of a Windows 10 IoT solution, you can now prepare and [connect a Windows 10 IoT Core device to your Azure IoT Central application](https://docs.microsoft.com/en-us/azure/iot-central/howto-connect-windowsiotcore). 
* The release for the Raspberry Pi 3B+ (the downloadable ISO can be found [here](http://go.microsoft.com/fwlink/?LinkID=708576)) is a technical preview and there is currently no timeline for a release version. For a better evaluation experience and fr any commercial products, please use the Raspberry Pi 3B or other devices with supported Intel, Qualcomm or NXP SoCs. 


## Improvements in Assigned Access
* Kiosks and digital signs are often place in public places where issues are widely seen by people. With built-in status reporting, device management systems are auomatically made aware of problems and can issue corrective actions like restarting the device or dispatching a service technician. 
* Reducing deployment and management costs are key drivers of ROI. Windows 10 IoT Enterprise has improved features for configuring a kiosk experience via a new wizard in the Settings app, managing multi-app kiosks and tailoring the [Microsoft Edge browser experience for kiosk devices](https://docs.microsoft.com/en-us/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy).
* While device builders have great flexibility to configure Assigned Access using provisioning packages, the Settings app, and mobile device management systems, some customers still need more. [Using a new set of Assigned Access APIs](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.assignedaccesssettings), developers can now configure Assigned Access programmatically from within their applications.


## More Management Support
* Azure IoT Hub offers lightweight device management features and an extensibility model that enable device and cloud developers to build robust device management solutions. Integration with [Azure IoT Device Management](https://docs.microsoft.com/windows/iot-core/manage-your-device/azureiotdm) is now available for both Windows 10 IoT Core and Enterprise. 
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
  * BSP Version: 2118.0.0.0


## Known Issues
* F5 driver deployment from Visual Studio does not work on Windows 10 IoT Core. Drivers must be manually copied and registered on the device.
* Devices that were installed via NOOBS cannot run the bcdedit tool to enable the kernel debugger.
* The Windows IoT Remote client does not work for Raspberry Pi. Use a board with accelerated graphics such as Minnowboard Max or Dragonboard or attach a monitor for local display.
