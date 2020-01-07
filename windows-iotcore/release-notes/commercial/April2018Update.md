---
title: April 2018 Update - Build 17134
ms.date: 05/01/2018
ms.topic: article
description: Learn about what's new in the April 2018 Update for Windows 10 IoT.
keywords: Windows IoT, April 2018 Update, release notes
---

# April 2018 Update Release Notes for Windows 10 IoT
Build Number 17134. May 2018

Windows 10 IoT enables development of embedded or dedicated-purpose devices and is the choice for OEMs and developers building Windows solutions for smart devices.

This document provides information that supplements other content and documentation for this release of Windows 10 IoT.

## Privacy Statement

The privacy statement for this version of the Windows operating system can be viewed at [https://go.microsoft.com/fwlink/?LinkId=521839](https://go.microsoft.com/fwlink/?LinkId=521839).

## What's New in April 2018 Update
* The [Visual Studio Test Platform](https://blogs.msdn.microsoft.com/devops/2017/02/12/evolving-the-visual-studio-test-platform-part-4-together-in-the-open/) that ships with [Visual Studio 15.6 RTW](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes#Win10_IoT_Core_Testing_Support) now supports testing on Windows 10 IoT Core. When [writing unit tests](https://blogs.msdn.microsoft.com/devops/2018/03/07/devops-for-iot-with-win10-iot-core-uwp-and-vsts/) for a project in Visual Studio 2017 which targets Windows 10 IoT Core, developers can now execute those unit tests remotely on the device directly from Visual Studio instead of having to deploy tests to the device and run them manually.
* Developers can leverage the capabilities in the [Windows AI Platform](https://blogs.windows.com/buildingapps/2018/03/07/ai-platform-windows-developers/) on Windows 10 IoT to create more intelligent devices and accelerate ML model evaluation using CPU or GPU.
* OEMs looking to bring a voice-enabled device to market quickly can integrate Cortana support into their device using the [preview of the Cortana Devices SDK](https://www.aka.ms/cortanadevices).
* OEMs can leverage the rich set of CSPs available on Windows to perform remote configuration and management of devices at scale using [Azure IoT Device Management](https://github.com/ms-iot/iot-core-azure-dm-client). This new sample implementation combines a local client, cloud service, and management portal, enabling IoT operators to perform device management at cloud scale.
* With this release, you can write [UWP console apps](https://docs.microsoft.com/windows/uwp/launch-resume/console-uwp) that run in a console host, such as a command console or PowerShell. UWP console apps can also use Win32 APIs available to UWP apps and can be published and updated through the Microsoft Store.
* We've added a new [Miracast feature package](https://docs.microsoft.com/windows/iot-core/connect-your-device/miracast) for IoT Core along with a [set of casting APIs](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicMediaCasting) to enable a device to act as a Miracast transmitter or receiver.
* We've added support for the [Bluetooth A2DP-SRC](https://docs.microsoft.com/windows/iot-core/connect-your-device/bluetooth) profile which allows a device to act as an audio source for Bluetooth streaming, including remote control capabilities over Bluetooth using the AVRCP profile.
* One of our most popular Qualcomm boards, the DragonBoard 410c, has become far easier to flash with this release. Using the latest version of the [Windows 10 IoT Core Dashboard](https://docs.microsoft.com/windows/iot-core/connect-your-device/iotdashboard), simply connect the board, put it into flash mode, and [flash the device](https://developer.microsoft.com/en-us/windows/iot/getstarted/prototype/setupdevice) directly from the dashboard.
* For finding and connecting to WiFi networks, we've updated the [WiFi Connector sample](https://github.com/Microsoft/Windows-iotcore-samples/blob/develop/Samples/WiFiConnector/CS) to be on par with the netcmd command which was previously deprecated. This sample uses the [WiFiAdapter APIs](https://docs.microsoft.com/uwp/api/Windows.Devices.WiFi.WiFiAdapter) to manage wireless network connections and adapters.
* We have new time-related APIs for automatically setting the system clock to the [local time](https://docs.microsoft.com/uwp/api/windows.system.datetimesettings.setsystemdatetime) and [time zone](https://docs.microsoft.com/uwp/api/windows.system.timezonesettings.autoupdatetimezoneasync#Windows_System_TimeZoneSettings_AutoUpdateTimeZoneAsync_Windows_Foundation_TimeSpan_) based on device location, enabling OEMs to create a more streamlined out of box experience.
* We have new language APIs for setting the preferred user [language](https://docs.microsoft.com/uwp/api/windows.system.userprofile.globalizationpreferences.trysetlanguages#Windows_System_UserProfile_GlobalizationPreferences_TrySetLanguages_Windows_Foundation_Collections_IIterable_System_String__), [region](https://docs.microsoft.com/uwp/api/windows.system.userprofile.globalizationpreferences.trysethomegeographicregion#Windows_System_UserProfile_GlobalizationPreferences_TrySetHomeGeographicRegion_System_String_), default [speech](https://docs.microsoft.com/uwp/api/windows.media.speechrecognition.speechrecognizer.trysetsystemspeechlanguageasync) language, and default [voice](https://docs.microsoft.com/uwp/api/windows.media.speechsynthesis.speechsynthesizer.trysetdefaultvoiceasync).
* With a new [MTP feature package](https://github.com/PawelWMS/windows-iotcore-docs/blob/MTP_Optional_Feature_Instructions/windows-iotcore/connect-your-device/MTP.md), you can transfer files to and from a Windows 10 IoT Core device over USB using the Media Transfer Protocol (MTP). This includes files located on the device's internal storage and SD card, if present.
* We've published a new [sample on GitHub](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/Azure/IoTHubClients) and [Channel 9 video](https://channel9.msdn.com/Shows/Internet-of-Things-Show/Connecting-Windows-IoT-Devices-To-IoT-Central) showing how easy it is to get a Windows 10 IoT device integrated into Azure IoT Central. We've also updated our documentation to describe [how to connect devices](https://docs.microsoft.com/azure/iot-central/howto-connect-windowsiotcore) running Windows 10 IoT Core to Azure IoT Central.

## Improvements in Assigned Access
* We've added support for multiple screens for digital signage use cases.
* The Enrollment Status page now includes the ability to ensure all MDM configurations are enforced on the device prior to entering assigned access.
* We've added the ability to configure and run Shell Launcher in addition to existing UWP Store apps.
* Devices using assigned access can be configured to automatically enter a desired state after a reboot using a simplified process for creating and configuring an auto-logon account.
* For multi-user devices, instead of specifying every user, it’s now possible to assign different assigned access configurations to Azure AD groups or Active Directory groups.
* To help with troubleshooting, you can now view error reports generated if an assigned access-configured app has issues.

## Features in Preview for Dev and Test Scenarios
* Device Update Center [Preview] allows OEMs to globally manage their apps and push updates for the operating system, apps, settings, and files from the cloud to devices to keep them up to date and secure.
* Support for hosting [Nano Server Containers](https://docs.microsoft.com/virtualization/windowscontainers/about/index) on 64-bit editions of Windows 10 IoT Core and Enterprise, enabling applications and their data can be isolated from each other and quickly moved from development to production or cloud to the edge.
* Windows Device Health Attestation [Preview] service uses hardware features and cloud services to provide tamper proofing and remote attestation of device health based on hardware-level metrics and attested data.
* [Azure IoT Edge](https://azure.microsoft.com/campaigns/iot-edge/) on Windows IoT [Preview] allows IoT solutions to orchestrate intelligence between the cloud and edge devices to ensure applications and services can act on IoT data wherever it makes the most sense.
* Azure IoT Hub [Device Provisioning Service [Preview]](https://blogs.windows.com/buildingapps/2017/10/05/windows-10-iot-enables-complete-iot-lifecycle/) enables Windows 10 IoT devices to be created with a common image during manufacturing and configured to connect automatically at first boot to Azure IoT Hub to retrieve device-specific provisioning information.

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

## Additional Information
* Based on the recent Intel announcement to stop producing the Intel Joule platform, FFUs for Intel Joule were discontinued in the previous release. Customers evaluating Intel Joule should identify an alternative platform using one of the other supported SoCs - see [Suggested Boards and SoCs](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/suggestedboards) for a list.

## Known Issues
* F5 driver deployment from Visual Studio does not work on Windows 10 IoT Core. Drivers must be manually copied and registered on the device.
* Devices that were installed via NOOBS cannot run the bcdedit tool to enable the kernel debugger.
* The Windows IoT Remote client does not work for Raspberry Pi. Use a board with accelerated graphics such as Minnowboard Max or Dragonboard or attach a monitor for local display.
