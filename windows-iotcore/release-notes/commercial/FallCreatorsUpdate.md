---
title: Fall Creators Update - Build 16299
author: danharman
ms.author: dan.harman
ms.date: 10/12/2017
ms.topic: article
description: Learn about what's new in the Fall Creators Update for Windows 10 IoT.
keywords: Windows IoT, Fall Creators Update, release notes
---

# Fall Creators Update Release Notes for Windows 10 IoT
Build Number 16299. October 2017

Windows 10 IoT enables development of embedded or dedicated-purpose devices and is the choice for OEMs and developers building Windows solutions for smart devices.

This document provides information that supplements other content and documentation for this release of Windows 10 IoT.

To download this latest build as well as packages, please visit the [Windows Insider Preview Downloads page](https://www.microsoft.com/en-us/software-download/windowsiot).

## Privacy Statement

The privacy statement for this version of the Windows operating system can be viewed at [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).

## What's New in Fall Creators Update
* [.NET for UWP apps](https://msdn.microsoft.com/library/windows/apps/xaml/mt185501.aspx?f=255&mspperror=-2147217396), the set of managed types that can be used to build Universal Windows Platform apps using C# or Visual Basic, has been augmented with [thousands of new APIs](https://blogs.msdn.microsoft.com/dotnet/2017/08/25/uwp-net-standard-2-0-preview/) to make it compliant with .NET Standard 2.0.
* Updated language support on Windows 10 IoT Core including English (en-US and en-GB), French (fr-FR and fr-CA), Spanish (es-ES and es-MX), and Simplified Chinese (zh-CN). You can create FFUs supporting multiple languages - see [MultiLangSample](https://github.com/ms-iot/iot-adk-addonkit/tree/develop/Source-arm/Products/MultiLangSample) and [SingleLangSample](https://github.com/ms-iot/iot-adk-addonkit/tree/develop/Source-arm/Products/SingleLangSample) for more information.
* Support for [Emergency Management Services](https://technet.microsoft.com/library/cc736319(v=ws.10).aspx) on Windows 10 IoT Core.
* Improved [ink support](https://docs.microsoft.com/windows/uwp/input-and-devices/pen-and-stylus-interactions) on Windows 10 IoT Core. With a compatible pen digitizer, you can now utilize DirectInk APIs for highlighter, pencil, and vector-based ink. We've also added XAML ink controls for UWP, including InkCanvas and InkToolbar, which enable stencils like rulers and protractors, and multi-modal interactions such as simultaneous pen and touch on compatible hardware. Smart Ink features such as ink recognition and ink analysis are not supported.
* Additional support for controlling line displays including customization of the cursor style, brightness, blink rate, and character sets. We've also added support for custom glyphs, transaction descriptors, and marquee mode for scrolling text.
* On Windows 10 IoT Enterprise, we've enabled access to industry standard buses like GPIO, I2C, SPI, and UART from user mode through the [Windows.Devices APIs](https://docs.microsoft.com/windows/uwp/devices-sensors/enable-usermode-access).
* [Assigned Access](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps) is a feature in Windows 10 IoT Enterprise which lets you restrict a specific user account to using only one Universal Windows app. We've expanded Assigned Access support to allow running multiple UWP and Win32 apps in a lockdown experience and manage those settings from the cloud.
* You can change the system language using IoTSettings.exe or new APIs. For details, see the language configuration section of the [Command Line Utils](https://docs.microsoft.com/windows/iot-core/develop-your-app/multilang) and [Language Support](https://docs.microsoft.com/windows/iot-core/develop-your-app/multilang) documentation.
* Updates to Raspberry Pi UEFI to enable Boot Volume Monitor.
* Added SMSC network driver to all architectures of Windows 10 IoT Core.
* Enabled [exclusive-mode audio streams](https://msdn.microsoft.com/library/windows/desktop/dd370844(v=vs.85).aspx) for audio endpoint devices on Windows 10 IoT Core.
* Added new APIs in WinRT for setting the system date and time on Windows 10 IoT Core.
* Added support for [Universal BSP (wm.xml)](https://docs.microsoft.com/windows-hardware/manufacture/iot/create-packages). Use the iot-adk-addonkit v4.0 with the current version of the ADK.
* Added language selection and localized layouts to On-Screen Keyboard. For more details, see  [On-Screen Keyboard Layouts](https://docs.microsoft.com/windows/iot-core/develop-your-app/onscreenkeyboardlayouts).

## Features in Preview for Dev and Test Scenarios
* Component Update Service [Preview] allows OEMs to globally manage their apps and push updates for the operating system, apps, settings, and files from the cloud to devices to keep them up to date and secure.
* Support for hosting [Nano Server Containers](https://docs.microsoft.com/virtualization/windowscontainers/about/index) on 64-bit editions of Windows 10 IoT Core and Enterprise, enabling applications and their data can be isolated from each other and quickly moved from development to production or cloud to the edge.
* Windows Device Health Attestation [Preview] service uses hardware features and cloud services to provide tamper proofing and remote attestation of device health based on hardware-level metrics and attested data.
* [Azure IoT Edge](https://azure.microsoft.com/campaigns/iot-edge/) on Windows IoT [Preview] allows IoT solutions to orchestrate intelligence between the cloud and edge devices to ensure applications and services can act on IoT data wherever it makes the most sense.
* Azure IoT Hub [Device Provisioning Service [Preview]](https://blogs.windows.com/buildingapps/2017/10/05/windows-10-iot-enables-complete-iot-lifecycle/) enables Windows 10 IoT devices to be created with a common image during manufacturing and configured to connect automatically at first boot to Azure IoT Hub to retrieve device-specific provisioning information.
* [Azure IoT Device Management [Preview]](https://docs.microsoft.com/windows/iot-core/manage-your-device/AzureIoTDM) enables IoT operators to manage device configuration such as installed applications, Windows updates, certificates, and network settings remotely from the cloud.

## Windows 10 IoT Core Reference Images
___ 
* Minnowboard Max
  * Processor: Intel Atom E3825
  * Architecture: x86
  * BSP Version: 10.0.4.0
* Raspberry Pi 3
  * Processor: Broadcom BCM2837
  * Architecture: ARM
  * BSP Version: 10.0.16248.1001
* DragonBoard 410c
  * Processor: Qualcomm Snapdragon 410
  * Architecture: ARM
  * BSP Version: 2112.0.0.0

## Additional Information
* Based on the recent Intel announcement to stop producing the Intel Joule platform, FFUs for Intel Joule are discontinued in this release. Customers evaluating Intel Joule should identify an alternative platform using one of the other supported SoCs - see [Suggested Boards and SoCs](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/suggestedboards) for a list.
* The IOT_WEBB_EXTN feature has been refactored to remove the onboarding feature which is now available as IOT_ONBOARDING_APP. With this update, the onboarding feature will be removed and devices using this feature should be reflashed to get this feature again.

## Known Issues
* F5 driver deployment from Visual Studio does not work on Windows 10 IoT Core. Drivers must be manually copied and registered on the device.
* The Windows IoT Remote client does not work for Raspberry Pi. Use a board with accelerated graphics such as Minnowboard Max or Dragonboard or attach a monitor for local display.
