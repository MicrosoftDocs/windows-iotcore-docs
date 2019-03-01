---
title: Get Started Overview
author: johnadali
ms.author: johnadali

ms.date: 09/05/2018 
ms.topic: article 
description: Overview for Windows IoT Core Manufacturing Guide.
keywords: Windows 10 IoT Core, 
---

# IoT Core Manufacturing Guide

Thinking about mass-producing devices running Windows 10 IoT Core? Use this guide and the [Windows ADK IoT Core Add-ons](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons) to create images that you can quickly flash onto new devices.

You can create **Test images** which include tools for quickly accessing and modifying devices. Test images are great for:

* Developers, hardware vendors and manufacturers (OEMs) who are trying out new device designs.
* Hobbyists and organizations that are creating devices designed to run in non-networked or controlled network environments.

You can create **Retail images**, which can be made more secure for public or corporate networks while still receiving updates.

You can add customizations, including apps, settings, hardware configurations and board support packages (BSPs).

For OEM-style images, you'll wrap your customizations into package (.cab) files. Packages let OEMs, ODMs (Original Device Manufacturers), developers, and Microsoft work together to help deliver security and feature updates to your devices without stomping on each other's work.

This guide is created so that you can follow step by step to create an Windows IoT Core image from scratch for mass production. It might be a good idea to start with the **Concepts and Terminology** page to understand the image creation process as well as terminology or naming convensions being used in this guide.

## Outline
* [01-Manufacturing Guide Overview(this document)](GuideOverview.md)
* [02-Concepts and Basics](Concepts-Terms-Basics/Concepts-Terms-Basics.md)
   * [Concepts and Terminology](Concepts-Terms-Basics/ConceptsTerminology.md)
   * [Get the tools needed to create Windows IoT Core Images](Concepts-Terms-Basics/ToolsNeeded.md)
   * [Board Support Packages](Concepts-Terms-Basics/BoardSupportPackages.md)
* [03-Create IoT Core Image](Create-IoT-Core-Image/Create-IoT-Core-Image).md
  * [Creating a Basic Windows IoT Core Image](04-CreateBasicImage.md)
  * [Flashing a Windows IoT Core Image](05-FlashingImage.md)
* [04-Customizing a Windows IoT Core Image](06-CustomizeImageOverview.md)
    * [Adding an App to an image](06a-AddingApps.md)
    * [Creating a Provisioning Package](06b-CreateProvisioningPackage.md)
    * [Adding file(s) and registry settings to an image](06c-AddFileRegistrySettings.md)
    * [Adding a driver to an image](06d-AddingDrivers.md)
* [05-Creating a Retail Windows IoT Core Image](07-CreateRetailImage.md)
* [06-Building Secure Devices with Windows 10 IoT Core](08-BuildingSecureDevices.md)
    * [Secure Boot, BitLocker, and Device Guard](08a-SecureBootBitLockerDeviceGuard.md)
    * [Using the Unified Write Filter](08b-UnifiedWriteFilter.md)
    * [Implementing a Trusted Platform Module](08c-ImplementingTPM.md)
* 07-Debugging
* [08-IoT Core Services](09-IoTCoreServices.md)
    * [Device Update Center](09a-SettingUpDeviceCenter.md)

## Next Steps
[Concepts and Terminology](02-ConceptsTerminology.md)

## Related Topics 

* [Build a prototype](../GetStarted.md)
* [IoT Core Developer Resources](https://developer.microsoft.com/en-us/windows/iot)
* [What's in the Windows ADK IoT Core Add-ons](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons)
* [IoT Core feature list](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-feature-list)
* [IoT Core Add-ons command-line options](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons-command-line-options)
