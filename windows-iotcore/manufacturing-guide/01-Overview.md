--- 
title: Get Started Overview
author: johnadali, lmaung
ms.author: johnadali, lmaung
ms.date: 09/05/2018 
ms.topic: article 
description: Overview for Windows IoT Core Manufacturing Guide.
keywords: Windows 10 IoT Core, 
--- 

# IoT Core Manufacturing Guide

Thinking about mass-producing devices running Windows 10 IoT Core? Use this guide and the [Windows ADK IoT Core Add-ons](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-adk-addons) to create images that you can quickly flash onto new devices.

You can create **test images** which include tools for quickly accessing and modifying devices. Test images are great for:

* Developers, hardware vendors and manufacturers (OEMs) who are trying out new device designs.
* Hobbyists and organizations that are creating devices designed to run in non-networked or controlled network environments.

You can create **retail images**, which can be made more secure for public or corporate networks while still receiving updates.

You can add customizations, including apps, settings, hardware configurations and board support packages (BSPs).

For OEM-style images, you'll wrap your customizations into package (.cab) files. Packages let OEMs, ODMs (Original Device Manufacturers), developers, and Microsoft work together to help deliver security and feature updates to your devices without stomping on each other's work.

## Outline
* [01-Overview(this doc)](01-Overview.md)
* [02-Concepts and Terminology](02-ConceptsTerminology.md)
* [03-Get the tools needed to create Windows IoT Core Images](03-ToolsNeeded.md)
* [04-Creating a Basic Windows IoT Core Image](04-CreateBasicImage.md)
* [05-Flashing a Windows IoT Core Image](05-FlashingImage.md)
* [06-Customizing a Windows IoT Core Image](06-CustomizeImageOverview.md)
    * [06a-Adding an App to an image](06a-AddingApps.md)
    * [06b-Creating a Provisioning Package](06b-CreateProvisioningPackage.md)
    * [06c-Adding file(s) and registry settings to an image](06c-AddFileRegistrySettings.md)
    * [06d-Adding a driver to an image](06d-AddingDrivers.md)
* 07-Creating a Retail Windows IoT Core Image


## Next Steps
[Concepts and Terminology](02-ConceptsTerminology.md)

## Related Topics

* [Build a prototype](../GetStarted.md)
* [Learn about Windows IoT Core](https://developer.microsoft.com/en-us/windows/iotcore)
* [IoT Core Developer Resources](https://developer.microsoft.com/en-us/windows/iot)
* [What's in the Windows ADK IoT Core Add-ons](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-adk-addons)
* [IoT Core feature list](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-feature-list)
* [IoT Core Add-ons command-line options](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-adk-addons-command-line-options)
