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
The Media Transfer Protocol (MTP) allows you to transfer files to and from your Windows 10 IoT Core device through USB. It allows access to the device's internal storage and the SD card, if present.

The feature is part of the IoT Core Kits, which can be downloaded and installed from the [Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/download/details.aspx?id=55031).

## How to install the MTP feature on a device running Windows 10 IoT Core

### Provisioning the device with required packages

1. Launch [Powershell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md) and access your device running Windows 10 IoT Core.
2. From Powershell or SSH, do the following:
    1. Create a temporary folder on the target machine (e.g. `C:\MTPTemp`).
    2. Based on your device's architecture, copy the following packages from your PC (`C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail\<arch>\fre`) to `C:\MTPTemp`:
        * `Microsoft-OneCoreUAP-Mtp-UserService-Package.cab`
        * `Microsoft-OneCoreUAP-Mtp-UserService-Package_Lang_en-US.cab`
        * `Microsoft-WindowsStorSvc-API-Schema-Extension-Package.cab`
        * `Microsoft-WindowsStorSvc-API-Schema-Extension-Package_Lang_en-US.cab`
    3. Run these commands from `C:\MTPTemp` to install the packages to your IoT device's system image:
        * `ApplyUpdate.exe -stage Microsoft-OneCoreUAP-Mtp-UserService-Package.cab`
        * `ApplyUpdate.exe -stage Microsoft-OneCoreUAP-Mtp-UserService-Package_Lang_en-US.cab`
        * `ApplyUpdate.exe -stage Microsoft-WindowsStorSvc-API-Schema-Extension-Package.cab`
        * `ApplyUpdate.exe -stage Microsoft-WindowsStorSvc-API-Schema-Extension-Package_Lang_en-US.cab`
        * `ApplyUpdate.exe -commit`
3. The device will boot to the Update OS, install the MTP feature, and reboot to the MainOS.

### Enabling the MTP USB interface

Once the device comes back to the MainOS, the USBFN configuration still needs to be updated to include MTP. In order to do that, you will need to add MTP to the interfaces enumerated by USBFN.
The [USB registry settings](https://docs.microsoft.com/en-us/windows-hardware/drivers/usbcon/usb-registry-settings-for-a-function-controller-driver) article explains the details of USB's configuration.

Follow these steps to append the current configuration with MTP:
1. Find the current configuration's registry key: check if the registry value `CurrentConfiguration` is present under the `HKEY_LOCAL_MACHINE\CurrentControlSet\Control\USBFN\Configurations` registry key. If so, your current configuration is present under `HKEY_LOCAL_MACHINE\CurrentControlSet\Control\USBFN\Configurations\[CurrentConfiguration]`.
Otherwise, the current configuration is present under `HKEY_LOCAL_MACHINE\System\ControlSet001\Control\USBFN\Configurations\Default`.
2. Append `MTP` to the current `InterfaceList` registry value present under your USBFN configuration.
NOTE: that value is of type `REG_MULTI_SZ`, so you will actually have to append `\0MTP` to the existing value if the `InterfaceList` value already has some entries.
If `InterfaceList` value is not present, create a new one containing only `MTP`.
3. Add the MTP's Microsoft OS compatible descriptor to the `MSOSCompatIdDescriptor` value under your USBFN configuration.
In order to create a valid descriptor containing all interfaces currently under the `InterfaceList` value (that now includes MTP after finishing the previous point), please follow the instructions available [here](https://msdn.microsoft.com/en-us/windows/hardware/gg463179.aspx).
If MTP is the only interface under `InterfaceList` please use the value `2800000000010400010000000000000000014D545000000000000000000000000000000000000000`.

## How to include MTP in Your Custom FFU

1. Add **IOT_MTP** feature ID to the OEM Input file
2. Create the image\FFU. Read [this article](https://docs.microsoft.com/windows-hardware/manufacture/iot/create-a-basic-image) for instructions.
NOTE: make sure to apply the same changes to the device's USBFN configuration as mentioned in the previous section.

## How to setup the MTP SD card filter

By default MTP will enumerate all of the contents of an SD card, if it is present on the device. It is possible, however, to limit this enumeration to a specific subfolder. In order to do so, you must add a registry value `MTPSDFolderFilter` under the registry key `HKEY_LOCAL_MACHINE\Software\Microsoft\MTP`.
The value is of type `REG_SZ` and should contain a relative path to the folder you would like MTP to enumerate. The folder will get automatically created if it does not already exist.

Sample paths:
- \FirstLevelDirectory;
- FirstLevelDirectory;
- \FirstLevelDirectory\SecondLevelDirectory;
- Never\Before\Created\Directory.

**NOTE**: do NOT use an absolute path containing the drive letter like `C:\Some\Folder\Path` - this might prevent the SD from being enumerated.

See [this link](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/add-a-registry-setting-to-an-image) for details about customizing your image with specific registry entries.