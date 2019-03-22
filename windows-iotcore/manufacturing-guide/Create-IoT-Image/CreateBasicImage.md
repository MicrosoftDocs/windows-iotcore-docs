---
title: Creating a Basic IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 09/05/2018 
ms.topic: article 
description: Steps to create a basic Windows 10 IoT Core image
keywords: Windows 10 IoT Core, 
---

# Creating a Basic IoT Core Image
To get started, we will detail the steps needed to create a basic Windows 10 IoT Core image and flash it onto a specific hardware device.

**Note**
1. The sample below uses 'C:\IoT\Workspaces\ContosoWS' as workspace.
2. Contoso is the OEM name.
3. ProductX is used as a sample product.

## Goals
* Create a project using ADK Add-ons that can be used to create Windows 10 IoT Core images
* Build a Full Flashable Update (FFU) file for a Windows 10 IoT Core test image

## Prerequisites / Requirements
Make sure your technician PC has the necessary tools installed prior to creating an IoT Core image. 

See [Get the tools needed to create Windows 10 IoT Core images](../Concepts-Terms-Basics/ToolsNeeded.md) for details.

You will need the following tools installed to complete this section:
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows 10 IoT Core

    > [!NOTE]
    > The version of ADK used must match the version of IoT Core Packages used below.

* **[Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore)** for your specific architecture. These provide the IoT Core packages and feature manifest files needed to build custom Windows IoT images for the specific architecture (ARM, ARM64, x86, x64).
* **[IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)**. These provide the sample scripts and base structure for building custom Windows 10 IoT Core images.
* **IoT Core Powershell Environment**. This is part of with the ADK Add-on  and is the Powershell command line interface where you execute commands to build custom FFU images for Windows 10 IoT Core.
* A text editor like **Notepad** or **VS Code**.

## Create a Workspace
1. In Windows Explorer, go to the folder where you installed the IoT Core ADK Add-Ons, for example, `C:\IoT-ADK-AddonKit`, and open `IoTCorePShell.cmd`. It should prompt you to run as an administrator.

   This will load the powershell module and also check the versions of the ADK, IoT Core kit. This will also check for the test certificates in the certificate store and if not present, install them automatically.

   If you receive the error "The system cannot find the path specified", right-click the icon and modify the path in "Target" to the location you've chosen to install the tools.

2. In the **IoT Core Powershell Environment**, create a new workspace (for example, `C:\Myworkspace`) with an OEM name of `Contoso` for the architecture `arm` using [New-IoTWorkspace](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTWorkspace.md)

    ```powershell
    New-IoTWorkspace C:\IoT\Workspaces\ContosoWS Contoso arm
    (or) new-ws C:\IoT\Workspaces\ContosoWS Contoso arm
    ```

   **IoT Core supports four architects, x64, x86, arm and arm64.** 

   Only alphanumeric characters are supports in the OEM name as this is used as a prefix for various generated file names.

   This generates the `IoTWorkspace.xml` file and sets a version number for the design, which you can use for future updates. The first version number defaults to 10.0.0.0. (Why a four-part version number? Learn about versioning schemes in [Update requirements](https://docs.microsoft.com/windows-hardware/service/mobile/update-requirements)).

   The required packages such as Registry.Version, Custom.Cmd and Provisioning.Auto will be imported into the workspace automatically.

## Building BSP

The next step is to take the Board Support Package files and extract/build their .CAB files to include in the FFU file. There are some differences in the steps to do this for the different BSPs, so please visit the appropriate section for the hardware device you are working with.

[Adding a Board Support Package](../Concepts-Terms-Basics/BoardSupportPackages.md)

## Build Packages 
From IoT Core Powershell Environment, get your environment ready to create products by building all of the packages in the working folders (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md)):

```powershell
New-IoTCabPackage All
(or) buildpkg all 
```
    > [!NOTE]
    > If you get SignTool errors when building the packages in Test mode, please run installoemcerts.cmd to install the test certificates on your Technician PC.

## Create a Product

From **IoT Core Powershell Environment**, create a new product folder that uses the BSP you are working with. This folder represents a new device we want to build an image for, and contains sample customization files that we can use to start our project. For example, to create a product folder called `ProductA` that uses the Raspberry Pi 2 or 3 BSP , execute the following command (using [Add-IoTProduct](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProduct.md)):

```powershell
Add-IoTProduct ProductX QCDB410C
(or) newproduct ProductX QCDB410C
```

You will be prompted to enter the **SMBIOS** information, such as Manufacturer Name (OEM Name), Family, SKU, BaseboardManufacturer, and BaseboardProduct. Here are some example values:

* **System OEM Name:** Contoso
* **System Family Name:** ContosoHub
* **System SKU Number:** AI-001
* **Baseboard Manufacturer:** Arrows
* **Baseboard Product:** DragonBoard 410c

The BSP name is the same as the folder name for the BSP. You can see which BSPs are available by looking in the `C:\IoT\WorkSpaces\ContosoWS\Source-<arch>\BSP` folders. 

In the example above, this creates the folder: `C:\IoT\WorkSpaces\ContosoWS\Source-arm\Products\ProductX`.

## OemCustomization.cmd File
Every image includes a file `oemcustomization.cmd` which will run on every boot up of your device. You have the ability to modify this file to customize what executes on boot up. This file is located under `C:\IoT\WorkSpaces\ContosoWS\Source-arm\Products\ProductX` in this example. The contents of the file is as follows:
```
@echo off
REM OEM Customization Script file
REM This script if included in the image, is called everytime the system boots.

reg query HKLM\Software\IoT /v FirstBootDone >nul 2>&1

if %errorlevel% == 1 (
    REM Enable Administrator User
    net user Administrator p@ssw0rd /active:yes
    if exist C:\Data\oobe (
        call folderpermissions.exe 'C:\Data\oobe -e'
    )
REM - Enable the below if you need secure boot/bitlocker
REM Enable Secureboot
REM if exist c:\IoTSec\setup.secureboot.cmd  (
REM    call c:\IoTSec\setup.secureboot.cmd
REM )

REM Enable Bitlocker
REM if exist c:\IoTSec\setup.bitlocker.cmd  (
REM    call c:\IoTSec\setup.bitlocker.cmd
REM )
    reg add HKLM\Software\IoT /v FirstBootDone /t REG_DWORD /d 1 /f >nul 2>&1
)

REM The below should be called on every boot
if exist C:\RecoveryConfig\Recovery.BcdEdit.cmd (
    call C:\RecoveryConfig\Recovery.BcdEdit.cmd
)

REM Set the crashdump file locations to data partition, set on every boot.
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl" /v DedicatedDumpFile /t REG_SZ /d C:\Data\DedicatedDumpFile.sys /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl" /v DumpFile /t REG_SZ /d C:\Data\MEMORY.DMP /f
```

> [!NOTE]
> Please be aware that security features like BitLocker and SecureBoot are disabled by default for a custom test image. If you wish to include these features (in a retail image) you can uncomment out the appropriate lines in the file, prior to building your image.

> [!NOTE]
> Please be aware that the commands in this file run with local system privilege.


## Build an image 
Eject any removable storage drives, including the microSD card and any USB flash drives. 

Build the FFU image file by entering the following command in IoT Core Powershell Environment (using [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md)):

```powershell
New-IoTFFUImage ProductX Test
(or)buildimage  ProductX Test 
```

This builds an FFU image file with your basic image at **C:\MyWorkspace\Build\\< arch >\\< product name >\Test**. This test image will include additional tools that can be used for debugging purposes. Building the final FFU file will take around 10-30 minutes to complete.

To direct all output to console instead of log file, add `-Verbose` flag.  eg.
```powershell
New-IoTFFUImage -Verbose ProductX Test
```

## Adding a Recovery Mechanism

You can add a recovery mechanism to your image with WinPE as a Safe OS and WIM files as Recovery SW from recovery partition, using the steps provided below.

See [Windows 10 IoT Core Recovery](https://docs.microsoft.com/en-us/windows-hardware/service/iot/recovery) for the details on the possible mechanisms.

**Step 1 : Update device layout with recovery partition**
TODO: Point them to recovery partition file (QCDB lives in Common/Packages folder)
Workspace/Common/Packages (-Rs) - This is general
END TODO

In the `devicelayout.xml` file, you add a new partition **MMOS** with the following attributes:

* FAT32 filesystem
* Atleast 2GB size ( to accommodate WinPE wim and recovery wims)
* Partition type
    * GPT : {ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}
    * MBR : 0x07

Sample xml snippet given below for a GPT device (assumes a sector size of 512)

```xml
<Partition>
    <Name>MMOS</Name>
    <FileSystem>FAT32</FileSystem>
    <TotalSectors>4096000</TotalSectors>
    <Type>{ebd0a0a2-b9e5-4433-87c0-68b6b72699c7}</Type>
</Partition>
```

See also [QCDB410C device layout](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Workspace/Source-arm/BSP/QCDB410C/Packages/QCDB410C.DeviceLayout-R/DeviceLayout.xml)

Sample xml snippet given below for an MBR device

```xml
<Partition>
    <Name>MMOS</Name>
    <FileSystem>FAT32</FileSystem>
    <TotalSectors>4096000</TotalSectors>
    <Type>0x07</Type>
</Partition>
```

See also [MBR 8GB Recovery device layout](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Workspace/Common/Packages/DeviceLayout.MBR8GB-R/DeviceLayout.xml)

**Step 2 : Configure BCD settings**

In this step, the newly added MMOS partition is defined as a bootable partition in the BCD settings and the recovery sequence is enabled and configured to boot into this partition. These settings are available in the below given packages that you can readily use. Select GPT or MBR packages based on your device.

* [Recovery.GPT-BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Common/Packages/Recovery.GPT-BCD) package
* [Recovery.MBR-BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Common/Packages/Recovery.MBR-BCD) package
    * Recovery.BCD.xml declares the MMOS partition availability
* [Recovery.GPT-BcdEdit](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Common/Packages/Recovery.GPT-BcdEdit) package
* [Recovery.MBR-BcdEdit](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Common/Packages/Recovery.MBR-BcdEdit) package
    * Recovery.BcdEdit.cmd enables recovery sequence and configures to boot into the MMOS partition

**Step 3 : Prepare WinPE image**

Windows 10 ADK Release 1709 contains the Windows 10 Preinstall Environment for all architectures (x86/amd64 and arm). For Windows 10 ADK Release 1809, you will need to install the **Windows PE add-on for ADK**. In this WinPE, you add the following:

* Recovery scripts used for recovery process on device
    * `startnet.cmd`, `startnet_recovery.cmd`: predefined scripts from the templates directory (see [templates\recovery](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Templates/recovery)).
    * config files : generated files based on the device layout, placed at `Build\<arch>\<bspname>\recovery`

* Recovery customizations files (optional)
    * `RecoveryGUI.exe` : Optional simple UI to hide the recovery shell prompt on the device. The recoveryGUI.exe can be a C++ application built for the target CPU or a .NET Framework 4 Windows from application. Newwinpe.cmd will have to be modified to add .NET Framework 4 capabilities to the WinPE image
    * `pre_recovery_hook.cmd` and `post_recovery_hook.cmd`: optional hooks to add additional actions before and after recovery process
    * Place these files in `Source-<arch>\bsp\<bspname>\WinPEExt\recovery` folder
* BSP drivers (optional)
    * You may need to add BSP drivers to winpe image to boot/write to storage, on your device platform.
    * Place the required drivers in `Source-<arch>\bsp\<bspname>\WinPEExt\drivers` folder.

You can create the WinPE image for the BSP with the above contents using the [New-IoTWindowsImage](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWindowsImage.md) command in **IoT Core Powershell Environment**.

```powershell
New-IoTWindowsImage ProductX <config>
(or) newwinpe ProductX <config>
```

This script will output the winpe at `Build\<arch>\<product>\<config>\winpe.wim`.

**Step 4 : Update Feature manifest file and OEMInputFile**

Update the **`<bspname>FM.xml`** with the following changes (see [QCDB410CFM.xml sample](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/BSP/QCDB410C/Packages/QCDB410CFM.xml))

* Include the new device layout package, specifying new SOC name, *QC8016-R* in the example below:

```xml
  <DeviceLayoutPackages>
      <PackageFile SOC="QC8016-R" Path="%PKGBLD_DIR%" Name="%OEM_NAME%.QCDB410C.DeviceLayout-R.cab" />
      <PackageFile SOC="QC8016" Path="%BSPPKG_DIR%" Name="Qualcomm.QC8916.DeviceLayout.cab" />
  </DeviceLayoutPackages>    
```

* Update the **`<productname>/TestOEMInput.xml`** (and RetailOEMInput.xml) with the following changes (see [Recovery sample](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/Products/RecoverySample/TestOEMInput.xml))

    * Specify the SOC name as defined in the <bspname>FM.xml

    ```xml
    <SOC>QC8016-R</SOC>
    ```

    * Include the RECOVERY_BCD feature in the OEM section

    ```xml
    <OEM>
    ...
    <Feature>RECOVERY_BCD</Feature>
    ...
    </OEM>
    ```

Update the `oemcustomization.cmd` file to invoke the `Recovery.BcdEdit.cmd`

```
    REM The below should be called on every boot
    if exist C:\RecoveryConfig\Recovery.BcdEdit.cmd (
        call C:\RecoveryConfig\Recovery.BcdEdit.cmd
    )
```

**Step 5 : Build the recovery image using [New-IoTRecoveryImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTRecoveryImage.md)**

```powershell
# Build all packages
New-IoTCabPackage All
(or) buildpkg All
# Build the product image
New-IoTFFUImage ProductX <config>
(or) buildimage ProductX <config>
# Build the recovery image
New-IoTRecoveryImage ProductX <config>
(or) buildrecovery ProductX <config>
```
This will generate the recovery file as Flash_Recovery.ffu


## Commands Used
Listed here are the commands (in order) for creating a basic IoT Core image. 

```powershell
New-IoTWorkspace C:\IoT\Workspaces\ContosoWS Contoso arm
New-IoTCabPackage All
Add-IoTProduct ProductX ARM
New-IoTFFUImage ProductX Test
```

## Examples 
### Raspberry Pi 2 or 3
The following is assumed in these steps:

1. OEM Name is **Contoso**.
2. Workspace is created at C:\IoT\Workspaces\ContosoWS.
3. Product name is **MyIoTDevice**.

```powershell
New-IoTWorkspace C:\IoT\Workspaces\ContosoWS Contoso arm
New-IoTCabPackage All
Add-IoTProduct MyIoTDevice RPi2
New-IoTFFUImage MyIoTDevice Test
```
      
### DragonBoard 410C
The following is assumed in these steps:

1. OEM Name is **Contoso**.
2. Product name is **MyIoTDevice**.
3. BSP files for the DragonBoard 410c are located at **C:\BSPs\DB410c_BSP**.

```powershell
New-IoTWorkspace C:\IoT\Workspaces\ContosoWS Contoso arm
New-IoTCabPackage All
Add-IoTProduct MyIoTDevice QCDB410C
New-IoTFFUImage MyIoTDevice Test
```
      
### Apollo Lake / Braswell / Cherry Trail
The following is assumed in these steps:

1. OEM Name is **Contoso**.
2. Product name is **MyIoTDevice**.
3. Architecture is set to **x64**.
4. Braswell CPU/board is used for this.
5. BSP files for Apollo Lake / Braswell / Cherry Trail are located at **C:\iot-adk-addonkit\Source-x64\BSP**.
6. These are the commands for Braswell. Replace with **APLx64** or **CHTx64** for Apollo Lake or Cherry Trail, respectively.

```powershell
New-IoTWorkspace C:\IoT\Workspaces\ContosoWS Contoso x64
New-IoTCabPackage All
Add-IoTProduct MyIoTDevice BSWx64
New-IoTFFUImage MyIoTDevice Test
```

## Next Steps
[Flashing a Windows 10 IoT Core Image](FlashingImage.md)

