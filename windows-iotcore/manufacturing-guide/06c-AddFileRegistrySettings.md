---
title: Adding files and registry settings to a Windows IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 09/26/2018 
ms.topic: article 
description: Description on how to add files and registry settings to a Windows IoT Core Image
keywords: Windows 10 IoT Core, 
---

# Adding file(s) and registry settings to a Windows IoT Core Image
We will create some test files and registry keys to a Windows IoT Core image, and package them up so that they can be serviced after they are distributed to your customers. Since files and registry keys that you add to your image are often not specific to an architecture, we recommend creating a common package that you can use across all of your device architectures.

## Goals
* Create a package that contains registry and file settings for your device
* Package the registry/file settings package so it can be included in an FFU image
* Modify IoT Addon Kit project configuration files to include your registry/file settings package
* Build and deploy an FFU image that contains your registry/file settings package

## Prerequisites/Requirements
Please make sure you've created a basic image from [Creating a Basic IoT Core Image](04-CreateBasicImage.md) previously. For this example, we have created a basic image with the Qualcomm DragonBoard called *TestDragonBoardProduct*.

You will need the following tools installed to complete this section:
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.
* **Iot Core Shell**. This is included with the Windows ADK and is the commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* **[Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore)** for your specific architecture. These provide the IoT Core packages and feature manifest files needed to build custom Windows IoT images for the specific architecture (ARM, ARM64, x86, x64).
* **[IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)**. These provide the sample scripts and base structure for building custom Windows IoT Core images.
* A text editor like **Notepad** or **VS Code**.

## Create your test files
Create a few sample text files using Notepad and add some random text so that these files are not empty. For our example, we have created two files titled **TestFile1.txt** and **TestFile2.txt**.



## Build a Package for Test Files
1. Open the IoT Core Shell: run C:\MyWorkspace\IoTCorePShell.cmd as an administrator and create a File package using [Add-IoTFilePackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTFilePackage.md):

```powershell
# Array of files with destinationDir, Source and destinationFilename
$myfiles = @(
    ("`$(runtime.system32)","C:\Temp\TestFile1.txt", ""),        
    ("`$(runtime.bootDrive)\OEMInstall","C:\Temp\TestFile2.txt", "TestFile2.txt")
    )
Add-IoTFilePackage Files.Configs $myfiles
```

This creates a new folder at `C:\MyWorkspace\Common\Packages\Files.Configs`.

This also adds a FeatureID called **FILES_CONFIGS** to the `C:\MyWorkspace\Common\Packages\OEMCOMMONFM.xml` file.

Variables like `$(runtime.system32)` are defined in `C:\Program Files (x86)\Windows Kits\10\Tools\bin\i386\pkggen.cfg.xml`.

2. Create a Registry package using [Add-IoTRegistryPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTRegistryPackage.md):

```powershell
# Array of files with destinationDir, Source and destinationFilename
$myregkeys = @(
    ("`$(hklm.software)\`$(OEMNAME)\Test","StringValue", "REG_SZ", "Test string"),
    ("`$(hklm.software)\`$(OEMNAME)\Test","DWordValue", "REG_DWORD", "0x12AB34CD")
    )
Add-IoTRegistryPackage Registry.Settings $myregkeys
```

This creates a new folder at `C:\MyWorkspace\Common\Packages\Registry.Settings`.

This also adds a FeatureID **REGISTRY_SETTINGS** to the `C:\MyWorkspace\Common\Packages\OEMCOMMONFM.xml` file.

3. Build the packages using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md). (The `buildpkg All` command builds everything in the source folders):

```powershell
New-IoTCabPackage Files.Configs
(or) buildpkg Files.Configs
New-IoTCabPackage Registry.Settings
(or) buildpkg Registry.Settings
```

The package is built and is available at `C:\MyWorkspace\Build\<arch>\pkgs`.

## Update the project's configuration files
Update the product test configuration to include the features using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md):

```powershell
Add-IoTProductFeature ProductB Test FILES_CONFIGS -OEM
(or) addfid ProductB Test FILES_CONFIGS -OEM
Add-IoTProductFeature ProductB Test REGISTRY_SETTINGS -OEM
(or) addfid ProductB Test REGISTRY_SETTINGS -OEM
```
## Build and Test Image
Build the FFU image again, as specified in [Creating a Basic IoT Core Image](04-CreateBasicImage.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

    ```powershell
    New-IoTFFUImage <product name> Test
    (or)buildimage <product name> Test 
    ```
Once the FFU file has been built, you can flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](05-FlashingImage.md).

## Verify Files and Registry Keys Added
In order to verify that the files were added on the device, do the following:

1. Connect both your technician PC and the device to the same ethernet network.

   For our example, the Qualcomm DragonBoard has wireless capability, so we connected to a wireless access point that has internet access, and was on the same network as the technician PC. For devices that have an ethernet jack, plug an ethernet cable into that jack and into the technician PC (or a router switch that is on the same network as the technician PC). 

2. On the test app note the IP address of the device. For example, 10.100.0.100.
3. On the technician PC, open File Explorer and type in the IP address of the device with a \\\ prefix and \c$ suffix.

        \\10.100.0.100\c$

4. Check that the files exist on the device. for our example, look for:

        \\10.100.0.100\c$\Windows\system32\TestFile1.txt
        \\10.100.0.100\c$\OEMInstall\TestFile2.txt

For verifying registry keys, follow these steps:

1. On the technician PC, connect to your device using an SSH client such as [PuTTY](https://www.putty.org/). For example, use the IP address and port 22 to connect to the device. Then login using the Administrator account and password. (To learn more, see [SSH](https://docs.microsoft.com/windows/iot-core/connect-your-device/SSH)).

    > [!NOTE]
    > When using SSH to connect to your device, you will be prompted for credentials for IoT Core. Please use *Administrator* and *p@ssw0rd* as the Username and Password to login to the device (unless you changed the credentials previously). 

2. From the command line in the SSH client, query the system for the registry key. In our example, this command was executed to check the existence of the registry key:

        reg query HKLM\Software\Contoso\Test

   The SSH client should display your test values.

   a. Alternatively, you can use the **Run Command** in Windows Device Portal for your connected device to run the `reg query` command.

   ![Dashboard screenshot](../media/ManufacturingGuide/WindowsDevicePortalRunCommand.jpg)

   The Output window should display your test values.

## Next Steps
[Adding a driver to an image](06d-AddingDrivers.md)

