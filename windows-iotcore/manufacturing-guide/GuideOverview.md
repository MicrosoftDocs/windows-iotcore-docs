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
* [03-Create IoT Core Image](Create-IoT-Image/Create-IoT-Core-Image.md)
  * [Creating a Basic Windows IoT Core Image](Create-IoT-Image/CreateBasicImage.md)
  * [Flashing a Windows IoT Core Image](Create-IoT-Image/FlashingImage.md)
* [04-Customizing a Windows IoT Core Image](Customize-Image/CustomizeImageOverview.md)
    * [Adding an App to an image](Customize-Image/AddingApps.md)
    * [Creating a Provisioning Package](Customize-Image/CreateProvisioningPackage.md)
    * [Adding file(s) and registry settings to an image](Customize-Image/AddFileRegistrySettings.md)
    * [Adding a driver to an image](Customize-Image/AddingDrivers.md)
    * [Adding Win32 services](Customize-Image/AddingWin32Services.md)
* [05-Creating a Retail Windows IoT Core Image](Create-Retail-Image/CreateRetailImage.md)
    * [Maunfacturing Checklist](Create-Retail-Image/ManufacturingCheckList.md)
    * [Testing Retail Image](Create-Retail-Image/Test-Retail-Image.md)
* [06-Building Secure Devices with Windows 10 IoT Core](Secure-IoT-Core/BuildingSecureDevices.md)
    * [Secure Boot, BitLocker, and Device Guard](Secure-IoT-Core/SecureBootBitLockerDeviceGuard.md)
    * [Using the Unified Write Filter](Secure-IoT-Core/UnifiedWriteFilter.md)
    * [Implementing a Trusted Platform Module](Secure-IoT-Core/ImplementingTPM.md)
* [07-IoT Core Services](IoT-Core-Services/IoTCoreServices.md)
    * [Device Update Center](IoT-Core-Services/SettingUpDeviceCenter.md)
* [08-Debugging on IoT Core](Debugging-IoT-Core)

## Next Steps
[Concepts and Terminology](02-ConceptsTerminology.md)

## Related Topics 

* [Build a prototype](../GetStarted.md)
* [IoT Core Developer Resources](https://developer.microsoft.com/en-us/windows/iot)
* [What's in the Windows ADK IoT Core Add-ons](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons)
* [IoT Core feature list](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-feature-list)
* [IoT Core Add-ons command-line options](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons-command-line-options)
