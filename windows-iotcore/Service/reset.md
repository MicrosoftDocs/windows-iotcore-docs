---
author: parameshbabu
description: 'Learn about device reset and how it works for Windows 10 IoT Core devices..'
ms.assetid: d8298c99-6fa7-4825-a0b8-181b99e40975
MSHAttr: 'PreferredLib:/library/windows/hardware'
title: Windows 10 IoT Core Reset
ms.author: pabab
ms.date: 10/15/2018
ms.topic: article
ms.custom: RS5
---

# Windows 10 IoT Core Reset

Device reset is a process to restore the device to its initial conditions (with all user data removed). This is useful when you want to wipe out the user data/ enterprise provisioning data and bring the device back to its pristine state. This feature is supported from Windows 10 IoT Core, version 1809.

> [!NOTE]
> Device reset is supported in IoT Core only when the device guard security feature is enabled. For more information on device guard, see [Enabling Secure Boot, BitLocker, and Device Guard on Windows 10 IoT Core](/windows/iot-core/secure-your-device/securebootandbitlocker).

## Device Reset functionality

Device reset includes the following key operations:

- Formats the data partition (all data stored there are lost)
  - OEM custom packages **should not** store files/data in the data partition if they want to use device reset.
- Restores all registry settings to the initial values specified in the packaging
- Removes extraneous files in the Main OS partition excluding the files specified in the packaging
- Restores Microsoft Store Apps to the version packaged in the image (via ppkg)
  - Store apps updates performed via the Microsoft Store will be reverted back
- All changes to BCD settings performed at run-time will **remain intact**.
- All OS/OEM updates applied to the device will **remain intact**
  - Note that this is the main difference between the Reset and Recovery process. The Recovery process will also roll back the updates and put the device back to the factory condition.

## Reset using MDM

Device reset can be triggered using the [RemoteWipe CSP](/windows/client-management/mdm/remotewipe-csp).

IoT Core supports only **doWipe** node in this CSP.

## Reset using Azure DM

Device reset can also be triggered using the Azure Device Management using [Remote Wipe API](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/remote-wipe.md).

The reset through this API performs additional functionality such as **resetting the TPM**.
