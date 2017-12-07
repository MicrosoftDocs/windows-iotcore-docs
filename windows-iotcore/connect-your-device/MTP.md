---
title: Media Transfer Protocol
author: PawelWMS
ms.author: pawelwi
ms.date: 12/06/2017
ms.topic: article
description: Learn how to enable the optional Media Transfer Protocol (MTP) feature to transfer files to and from your devices through USB.
keywords: windows iot, MTP, media transfer protocol, file transfer, devices
---

# Media Transfer Protocol
The Media Transfer Protocol (MTP) allows you to transfer files to and from your Windows 10 IoT Core device through USB. It allows access to the device's internal storage and a SD card, if present.

The feature is part of the IoT Core Kits, which can be downloaded and installed from the [Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/download/details.aspx?id=55031).

## How to Install MTP on a device running Windows 10 IoT Core

* Launch [Powershell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md) and access your device running Windows 10 IoT Core.
* From Powershell or SSH, do the following:
  * Create a temporary folder on the target machine (e.g. ```C:\MTPTemp```).
  * Based on your device architecture, copy the following packages from your PC (`C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail\<arch>\fre\`) to `C:\MTPTemp`:
    * Microsoft-OneCoreUAP-Mtp-UserService-Package.cab
    * Microsoft-OneCoreUAP-Mtp-UserService-Package_Lang_en-US.cab
    * Microsoft-WindowsStorSvc-API-Schema-Extension-Package.cab
    * Microsoft-WindowsStorSvc-API-Schema-Extension-Package_Lang_en-US.cab
  * Run these commands to install the packages to your IoT device system image:
    * `ApplyUpdate.exe -stage Microsoft-OneCoreUAP-Mtp-UserService-Package.cab`
    * `ApplyUpdate.exe -stage Microsoft-OneCoreUAP-Mtp-UserService-Package_Lang_en-US.cab`
    * `ApplyUpdate.exe -stage Microsoft-WindowsStorSvc-API-Schema-Extension-Package.cab`
    * `ApplyUpdate.exe -stage Microsoft-WindowsStorSvc-API-Schema-Extension-Package_Lang_en-US.cab`
    * `ApplyUpdate.exe -commit`
* The device will boot to the Update OS, install the MTP feature, and reboot to the MainOS.
* Once the device comes back to the MainOS, the USBFN configuration still needs to be update to include MTP.

## How to include MTP in Your Custom FFU 


* Add **IOT_MTP** feature ID to the OEM Input file 
* Create the image\FFU. Read [Create a basic image](https://docs.microsoft.com/windows-hardware/manufacture/iot/create-a-basic-image) for instructions.
NOTE: Make sure to make the same changes to the device's USBFN configuration as mentioned in the previous section.
* Make sure the image
