---
title: Media Transfer Protocol
author: PawelWMS
ms.author: pawelwi
ms.date: 12/06/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to enable the optional Media Transfer Protocol (MTP) feature to transfer files to and from your devices through USB.
keywords: windows iot, MTP, media transfer protocol, file transfer, devices
---

# Media Transfer Protocol
The Media Transfer Protocol (MTP) allows you to transfer files to and from your Windows 10 IoT Core device through USB. It allows access to the device's internal storage and the SD card, if present.

The feature is part of the IoT Core Kits, which can be downloaded and installed from the [Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/download/details.aspx?id=55031).

## How to install the MTP feature on a device running Windows 10 IoT Core

### Provisioning the device with required packages

1. Launch [PowerShell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md) and access your device running Windows 10 IoT Core.
2. From PowerShell or SSH, do the following:
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
The [USB registry settings](/windows-hardware/drivers/usbcon/usb-registry-settings-for-a-function-controller-driver) article explains the details of USB's configuration.

While you can modify the default USBFN configuration available under the `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN\Configurations\Default` key, it is recommended to define your own, as they will not get overwritten by system updates.

#### Creating a new USBFN configuration with the MTP interface

Follow these steps to add a new configuration with MTP:
1. Add a new key under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN\Configurations`. Example: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN\Configurations\MyConfiguration`.
2. Under the new key, create a `REG_MULTI_SZ` value `InterfaceList` equal to `MTP`.
3. Under the same key, create a `REG_BINARY` value `MSOSCompatIdDescriptor` equal to `2800000000010400010000000000000000014D545000000000000000000000000000000000000000`.
4. Under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN` add a new `REG_SZ` value `CurrentConfiguration` equal to the name of the newly created key. In this case, it would be `MyConfiguration`.
5. [**Optional**] Under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN` add a new `REG_DWORD` value `IncludeDefaultCfg` equal to 1. This will make the USB driver enumerate the default interfaces along with MTP.

> [!NOTE]
> If you are already using a custom configuration you will have to modify it instead of creating a new one.

#### Adding the MTP interface to an existing configuration

Follow these steps to add MTP to an existing USBFN configuration:
1. Find the current configuration by checking the `CurrentConfiguration` value under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN`. If the value is present, then the current configuration can be found under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN\Configurations\[CurrentConfiguration]`. Otherwise it is under `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\USBFN\Configurations\Default`.
2. Under the current configuration key, add `\0MTP` to the value of `InterfaceList`. The ***\0*** part is used as the type of `InterfaceList` is `REG_MULTI_SZ` and it requires this separator between values.
3. Modify the `MSOSCompatIdDescriptor` value to include the MTP's descriptor. In order to create a valid descriptor containing all interfaces currently under the `InterfaceList` value, please follow the instructions documentation available at the bottom of [this page](/previous-versions/gg463179(v=msdn.10)). *OS_Desc_CompatID.doc* gives an explanation of the descriptor's format and an example of including multiple interfaces in the descriptor. MTP's compatible and subcompatible IDs are also available on the same page and are used in one of the examples.

## How to include MTP in Your Custom FFU

1. Add **IOT_MTP** feature ID to the OEM Input file. This is an equivalent of following the steps from the "[**Provisioning the device with required packages**](#provisioning-the-device-with-required-packages)" section.
2. Make sure to apply the same registry changes as mentioned in the "[**Creating a new USBFN configuration with the MTP interface**](#creating-a-new-usbfn-configuration-with-the-mtp-interface)" section. Follow [these instructions](/windows-hardware/manufacture/iot/add-a-registry-setting-to-an-image) to learn how to apply registry changes to an FFU.
3. Create the image\FFU. Read [this article](/windows-hardware/manufacture/iot/create-a-basic-image) for instructions.

> [!WARNING]
> Modifying the default configuration should not be attempted through FFU customization. System-defined entries may be refreshed/changed by a system update and any custom settings will be lost.

## How to set up the MTP SD card filter

By default MTP will enumerate all of the contents of an SD card, if it is present on the device. It is possible, however, to limit this enumeration to a specific subfolder. In order to do so, you must add a registry value `MTPSDFolderFilter` under the registry key `HKEY_LOCAL_MACHINE\Software\Microsoft\MTP`.
The value is of type `REG_SZ` and should contain a relative path to the folder you would like MTP to enumerate. The folder will get automatically created if it does not already exist.

Sample paths:
- \FirstLevelDirectory;
- FirstLevelDirectory;
- \FirstLevelDirectory\SecondLevelDirectory;
- Never\Before\Created\Directory.

> [!WARNING]
> Do not use an absolute path containing the drive letter like `C:\Some\Folder\Path` - this might prevent the SD card from being enumerated.

See [this link](/windows-hardware/manufacture/iot/add-a-registry-setting-to-an-image) for details about customizing your image with specific registry entries.