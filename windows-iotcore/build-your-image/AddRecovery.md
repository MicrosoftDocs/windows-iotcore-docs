---
title: Add a recovery mechanism to an IoT Core image
author: parameshbabu
ms.author: pabab
ms.date: 10/03/2017
ms.topic: article
description: Learn how to add a recovery mechanism to your IoT Core image. 
keywords: windows iot, image creation, windows iot, recovery
---

# Add a recovery mechanism to your image

You can add a recovery mechanism to your image with **WinPE** as a Safe OS and **WIM files** as Recovery SW from recovery partition, using the steps provided below.

See [Windows 10 IoT Core Recovery](../commercialize-your-device/Recovery.md) for the details on the possible mechanisms.

## Step 1 : Update device layout with recovery partition

In the devicelayout.xml file, you add a new partition **MMOS** with the following attributes
- FAT32 filesystem
- Atleast 2GB size ( to accomodate WinPE wim and recovery wims)
- Partition type 
    - GPT : {ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}
    - MBR : 0x07

Sample xml snippet given below for a GPT device (assumes a sector size of 512)

```xml
<Partition>
    <Name>MMOS</Name>
    <FileSystem>FAT32</FileSystem>
    <TotalSectors>4096000</TotalSectors>
    <Type>{ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}</Type>
</Partition>
```
See also [QCDB410C device layout](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Source-arm/BSP/QCDB410C/Packages/QCDB410C.DeviceLayout-R/DeviceLayout.xml)

Sample xml snippet given below for an MBR device

```xml
<Partition>
    <Name>MMOS</Name>
    <FileSystem>FAT32</FileSystem>
    <TotalSectors>4096000</TotalSectors>
    <Type>0x07</Type>
</Partition>
```
See also [MBR 8GB Recovery device layout](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/DeviceLayout.MBR8GB-R/DeviceLayout.xml)

## Step 2 : Configure BCD settings
In this step, the newly added MMOS partition is defined as a bootable partition in the BCD settings and the recovery sequence is enabled and configured to boot into this partition. These settings are available in the below given packages that you can readily use. Select GPT or MBR packages based on your device.

- [Recovery.GPT-BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.GPT-BCD) package
- [Recovery.MBR-BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.MBR-BCD) package
    - Recovery.BCD.xml declares the MMOS partition availability.
- [Recovery.GPT-BcdEdit](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.GPT-BcdEdit) package
- [Recovery.MBR-BcdEdit](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.MBR-BcdEdit) package
    - Recovery.BcdEdit.cmd enables recovery sequence and configures to boot into the MMOS partition.

## Step 3 : Prepare WinPE image 
Windows 10 ADK Release 1709 contains the Windows 10 Preinstall Environment for all architectures (x86/amd64 and arm).
In this WinPE, you add the following

- Recovery scripts used for recovery process on device
    - `startnet.cmd`, `startnet_recovery.cmd`: predefined scripts from the templates directory (see [templates\recovery](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Templates/recovery)).
    - config files : generated files based on the device layout, placed at `Build\<arch>\<bspname>\recovery`.
- Recovery customizations files (optional)
    - `RecoveryGUI.exe` : Optional simple UI to hide the recovery shell prompt on the device. The recoveryGUI.exe can be a C++ application built for the target CPU or a .NET Framework 4 Windows from application. Newwinpe.cmd will have to be modified to add .NET Framework 4 capabilities to the WinPE image.
    - `pre_recovery_hook.cmd` and `post_recovery_hook.cmd`: optional hooks to add additional actions before and after recovery process. 
    - Place these files in `Source-<arch>\bsp\<bspname>\WinPEExt\recovery` folder.

- BSP drivers (optional)
    - You may need to add bsp drivers to winpe image to boot/write to storage, on your device platform.
    - Place the required drivers in `Source-<arch>\bsp\<bspname>\WinPEExt\drivers` folder.

You can create the WinPE image for the bsp with the above contents using the below command in IoTCoreShell
``` 
newwinpe.cmd <bspname> <socname>
```
This script will output the winpe at  `Build\<arch>\<bspname>\winpe.wim`.



## Step 4 : Update Feature manifest file and OEMInputFile
- Update the **\<bspname\>FM.xml** with the following changes (see [QCDB410CFM.xml sample](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Source-arm/BSP/QCDB410C/Packages/QCDB410CFM.xml))

    - Include the new device layout package, specifying new SOC name, *QC8016-R* in the example below .
    
      ```xml
        <DeviceLayoutPackages>
            <PackageFile SOC="QC8016-R" Path="%PKGBLD_DIR%" Name="%OEM_NAME%.QCDB410C.DeviceLayout-R.cab" />
            <PackageFile SOC="QC8016" Path="%BSPPKG_DIR%" Name="Qualcomm.QC8916.DeviceLayout.cab" />
        </DeviceLayoutPackages>    
        ```

- Update the **\<productname\>/TestOEMInput.xml** (and RetailOEMInput.xml) with the following changes (see [Recovery sample](https://github.com/ms-iot/iot-adk-addonkit/blob/develop/Source-arm/Products/RecoverySample/TestOEMInput.xml))

    - Specify the SOC name as defined in the \<bspname\>FM.xml

        ```xml
        <SOC>QC8016-R</SOC>
        ```

    - Include the RECOVERY_BCD feature in the OEM section

        ```xml
        <OEM>
        ...
        <Feature>RECOVERY_BCD</Feature>
        ...
        </OEM>
        ```

- Update the `oemcustomization.cmd` to invoke the `Recovery.BcdEdit.cmd`

    ```
        REM The below should be called on every boot
        if exist C:\RecoveryConfig\Recovery.BcdEdit.cmd (
            call C:\RecoveryConfig\Recovery.BcdEdit.cmd
        )
    ```

## Step 5 : Build the image

- `buildpkg.cmd all` - to build all packages.

- `buildrecovery.cmd <productname> Test` (or Retail) - to build the image. This will build the following
    - winpe image for the specified device layout
    - regular FFU (`Flash.ffu`)
    - extract the required recovery files
    - update the FFU with the recovery files and save as `Flash_Recovery.ffu`


