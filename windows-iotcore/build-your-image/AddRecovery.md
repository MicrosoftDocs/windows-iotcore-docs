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

You can add a recovery mechanism to your image with **WinPE** as a Safe OS and **wim files** as Recovery SW from recovery partition, using the steps provided below.

See [Windows 10 IoT Core Recovery](../commercialize-your-device/Recovery.md) for the details on the possible mechanisms.

## Step 1 : Create WinPE image 
Windows 10 ADK Release 1709 contains the Windows 10 Preinstall Environment for all architectures (x86/amd64 and arm).

In this WinPE, you add the following

- Recovery scripts (see [template\recovery](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Templates/recovery))
    - startnet.cmd, startnet_recovery.cmd and diskpart txt files - the scripts that perform the actual recovery process
- Recovery UI (optional)
    - Optional recoveryUI.exe can be added and launched from startnet.cmd to hide the recovery shell
- Bsp drivers (optional)
    - You may need to add bsp drivers to winpe image to boot/write to storage. 

You can create the WinPE image with these scripts and drivers in the IoTCoreShell using 
``` 
newwinpe.cmd <bspname> C:\bspdrivers
```
This script will create **Recovery.WinPE** directory under \<bspname\>/Packages directory with the following files

- Recovery.WinPE.wm.xml : package definition file
- startrecovery.cmd : script that launchs the recovery from MainOS ( for system reset )
- winpe.wim : wim file with the recovery scripts and drivers included

## Step 2 : Update device layout with Recovery partition

In the devicelayout.xml file, you add a new partition **MMOS** with the following attributes
- FAT32 filesystem
- Atleast 2GB size ( to accomodate WinPE wim and recovery wims)
- Partition type 
    - GPT : {ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}
    - MBR : 0x07

Sample xml snippet given below for a GPT device

```xml
    <Partition>
      <Name>MMOS</Name>
      <FileSystem>FAT32</FileSystem>
      <TotalSectors>4096000</TotalSectors>
      <Type>{ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}</Type>
    </Partition>
```
See also [QCDB410C device layout](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/BSP/QCDB410C/Packages/QCDB410C.DeviceLayout-R/DeviceLayout.xml)

## Step 3 : Configure BCD settings
The newly added MMOS partition needs to be defined as a bootable partition in the BCD settings and the recovery sequence needs to be enabled and configured to boot into this partition.

- [Recovery.GPT-BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.GPT-BCD) package
    - Recovery.BCD.xml declares the MMOS partition availability. Use this package as is (no changes required)
- [Recovery.GPT-BcdEdit](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Recovery.GPT-BcdEdit) package
    - Recovery.BcdEdit.cmd enables recovery sequence and configures to boot into the MMOS partition. Use this package as is (no changes required)


## Step 4 : Update Feature manifest file and OEMInputFile
- Update the **\<bspname\>FM.xml** with the following changes (see [QCDB410CFM.xml sample](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/BSP/QCDB410C/Packages/QCDB410CFM.xml))

    - Include the newly defined Recovery.WinPE package and define a feature id say RECOVERY_WINPE
     - ```xml
        <PackageFile Path="%PKGBLD_DIR%" Name="%OEM_NAME%.Recovery.WinPE.cab">
            <FeatureIDs>
            <FeatureID>RECOVERY_WINPE</FeatureID>
            </FeatureIDs>
        </PackageFile>
       ```
    - Include the new device layout package, specifying new SOC id.
     - ```xml
        <DeviceLayoutPackages>
            <PackageFile SOC="QC8016" Path="%BSPPKG_DIR%" Name="Qualcomm.QC8916.DeviceLayout.cab" />
            <PackageFile SOC="QC8016-R" Path="%PKGBLD_DIR%" Name="%OEM_NAME%.bspname.DeviceLayout-R.cab" />
        </DeviceLayoutPackages>    
        ```
- Update the **\<productname\>/TestOEMInput.xml** (and RetailOEMInput.xml) with the following changes (see [Recovery sample](https://github.com/ms-iot/iot-adk-addonkit/blob/develop/Source-arm/Products/RecoverySample/TestOEMInput.xml)

    - Specify the SOC name as defined in the \<bspname\>FM.xml
 ```xml
        <SOC>QC8016-R</SOC>
 ```
    - Include the RECOVERY_WINPE and RECOVERY_BCD feature in the OEM section
 ```xml
        <OEM>
        ...
        <Feature>RECOVERY_WINPE</Feature>
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

- `buildpkg.cmd all` - to build all packages 
    - if you have already built all packages before this change, you can also use `buildbsp \<bspname\>`, followed by `buildfm bsp \<bspname\>`
- `buildrecovery.cmd \<productname\> Test` (or retail) - to build the image
    - this will build the regular FFU first (`Flash.ffu`) , mount the ffu to extract the wim files and store them to the recovery partition, and save the modified ffu as `Flash_Recovery.ffu`

