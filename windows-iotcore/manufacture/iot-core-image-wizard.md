---
author: EliotSeattle
description: Describes the IoT Core Image Wizard, a tool built using the Windows 10 IoT Core (IoT Core) ADK Add-Ons. 
MSHAttr: 'PreferredLib:/library'
title: IoT Core Image Wizard
ms.date: 11/06/2018
ms.topic: article
ms.custom: RS5
---

# IoT Core Image Wizard (Preview release)

The IoT Core Image Wizard is a GUI tool that uses the [IoT Core Add-ons Powershell Commands](iot-core-adk-addons-command-line-options.md).
Using the IoT Core Image Wizard simplifies the process of creating your first image for your device.

## Download link

Download the [IoT Core Image Wizard](https://go.microsoft.com/fwlink/?linkid=2044446).

## Setup instructions

1. Download the zip file
2. Extract to a folder
3. See the readme.md in the extracted files for the prerequisites
4. Starting with the Windows 10 October 2018 Update, you use the RSAT: Server Manager optional feature. Older versions of Windows 10 use the matching [package](https://www.microsoft.com/en-us/download/details.aspx?id=45520)
5. Once prerequisites are installed, go to the extracted files' folder and run IoTCoreImageWizard.exe

## November 2018 Preview release notes

- Only supports creating a new workspace.  Cannot open/edit a workspace.  Use the [Powershell Commands](iot-core-adk-addons-command-line-options.md) to open/edit a workspace.
- Just debug configurations of image builds.  If you need to build retail images, use the [Powershell Commands](iot-core-adk-addons-command-line-options.md).
- Errors with creating a recovery image.  Make sure the OS version matches or is newer than the kits' version.  Also, all the kits need to be the same version.

## Related topics

[IoT Core Add-ons](iot-core-adk-addons.md)

[IoT Core Add-ons Powershell Commands](iot-core-adk-addons-command-line-options.md)

[IoT Core manufacturing guide](iot-core-manufacturing-guide.md)
