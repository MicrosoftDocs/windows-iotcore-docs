---
title: UEFI Requirements 
author: parameshbabu
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
description: Learn the UEFI requirements for Windows 10 IoT Core OS.
keywords: windows iot, image creation, image customizations, OEM customizations, UEFI
---

# UEFI Requirements

The UEFI requirements for IoT Core are similar to other windows editions like desktop. See [UEFI in Windows](https://docs.microsoft.com/windows-hardware/drivers/bringup/uefi-in-windows) for details and specifically see [UEFI requirements for Windows editions on SoC platforms](https://docs.microsoft.com/windows-hardware/drivers/bringup/uefi-requirements-that-apply-to-all-windows-platforms). 

## ACPI Design

See [Windows ACPI design guide for SoC platforms](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-acpi-design-guide-for-soc-platforms) for the details on the ACPI requirements for IoT Core.

## Replacing Windows Boot Logo

There are multiple ways to replace the boot logo that is displayed by the BIOS or UEFI:

* One way is to license the UEFI, or pay a board manufacturer vendor to do so, and make changes directly to the UEFI source code.
* Alternatively, on devices whose UEFI implementation supports signed loadable UEFI drivers there is a sample [here](https://github.com/Microsoft/MS_UEFI/tree/share/MsIoTSamples) that shows how to build a driver that replaces the boot logo and supply a BGRT table to bootmgr so that the Windows boot process leaves your logo in place during boot instead of replacing it with the Windows logo.

## SMBIOS settings

Minimum required SMBIOS settings are described in [OEM License Requirements](OEMLicenseRequirements.md).

## I/O Bus Access

Windows IoT Core and IoT Enterprise allow for user applications to interface with system I/O pins. To enable this, specific configuration is required in the ASL table. Read [Enable user mode access on Windows 10 IoT Core](https://docs.microsoft.com/windows/uwp/devices-sensors/enable-usermode-access) for more information.

## Recovery Trigger

Review [Windows 10 IoT Core Recovery Options](Recovery.md) and if you require hardware trigger to get into recovery mode, you may require to implement this in the UEFI apps and invoke recovery by setting the required bootsequence before windows boots.

The bootsequence required to boot into the recovery OS is given below

```
bcdedit /set {bootmgr} bootsequence {a5935ff2-32ba-4617-bf36-5ac314b3f9bf}
```
