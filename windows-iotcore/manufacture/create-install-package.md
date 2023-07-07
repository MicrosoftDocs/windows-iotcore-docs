---
author: parameshbabu
description: 'Learn how to set up your environment and create and install packages for Windows IoT Core.'
ms.assetid: d9a50f87-e8c0-48da-89e7-0cdd542ce053
MSHAttr: 'PreferredLib:/library'
title: 'Create and Install a Package'
ms.author: pabab
ms.date: 10/15/2018
ms.topic: article
ms.custom: RS5
---


# Create and install a package
[Packages](./iot-core-manufacturing-guide.md#packages) are the building blocks of Windows 10 IoT Core. From device drivers to system files, every component must be packaged to install on a device. Packages are the smallest servicable units on the device.

## Step 1: Get set up

### Install the tools

1. [Windows Assessment and Deployment Kit(Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
2. [IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)

### Set up your environment

* Launch `IoTCorePShell.cmd` ( this one launches in the elevated prompt )
* Create a new workspace using `new-ws C:\MyWorkspace <oemname> <arch>`

To create your own image (FFU), follow the steps outlined in the ["Create a basic image" lab in the IoT Manufacturing guide](./create-a-basic-image.md).

## Step 2: Create a new package
1. Create a **package definition xml file** (.wm.xml file), and specify the files and reg keys you want to add. 
      Learn more at [Windows Universal OEM Package Schema](./package-schema.md).

2. Build the package: `buildpkg filename.wm.xml`. The .cab file will be created in the build directory `<workspace>\Build\<arch>\pkgs`.

### Create a package with files and reg keys
Below is an example for specifying files and reg keys.

```xml
<?xml version="1.0" encoding="utf-8"?>
<identity xmlns:xsd="http://www.w3.org/2001/XMLSchema" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    name="SUBNAME" namespace="COMPNAME" owner="Contoso" legacyName="Contoso.COMPNAME.SUBNAME" 
    xmlns="urn:Microsoft.CompPlat/ManifestSchema.v1.00">
    <onecorePackageInfo
        targetPartition="MainOS"
        releaseType="Production"
        ownerType="OEM" />
    <regKeys>
        <regKey
            keyName="$(hklm.software)\Contoso\Test">
            <regValue name="StringValue" type="REG_SZ" value="Test string" />
            <regValue name="DWordValue" type="REG_DWORD" value="0x12AB34CD" />
            <regValue name="BinaryValue" type="REG_BINARY" value="12ABCDEF" />
        </regKey>
        <regKey
            keyName="$(hklm.software)\Contoso\EmptyKey" />
    </regKeys>
    <files>
        <file
            destinationDir="$(runtime.system32)"
            source="filename.txt" />
        <file
            destinationDir="$(runtime.bootDrive)\OEMInstall"
            source="filename2.txt"
            name="filename2.txt" />
    </files>
</identity>
```

### Create an Appx package

Use [Add-IoTAppxPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTAppxPackage.md) to generate the .wm.xml file for a given appx file. This tool expects the appx dependencies in the sub directory named "dependencies" in the folder containing the appx file.

```PowerShell
Add-IoTAppxPackage HelloWorld.appx fga Appx.HelloWorld
(or) newappxpkg HelloWorld.appx fga Appx.HelloWorld
New-IoTCabPackage Appx.HelloWorld
(or) buildpkg Appx.HelloWorld
```

`fga` sets the appx as the foreground startup app, `bgt` sets the appx as the background task and `none` skips startup configuration.
For older commandline tool, see [newappxpkg.cmd](https://github.com/ms-iot/iot-adk-addonkit/tree/17134/Tools/newappxpkg.cmd)

See [Appx.IoTCoreDefaultApp](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/Packages/Appx.IoTCoreDefaultApp/) as an example.

When you have to install multiple applications signed with same certificate, you can add the certificate along with one app and for the remaining apps, you can skip adding the certificate using the skipcert flag.

```PowerShell
newappxpkg AnotherApp.appx none Appx.AnotherApp skipcert
```

See also

* [Lab 1b: Add an app to your image](./deploy-your-app-with-a-standard-board.md)


### Create a driver package

The driver package contains the references (InfSource) to the Inf file for the driver. You can author the driver .wm.xml file manually or use [Add-IoTDriverPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTDriverPackage.md) that generates package xml based on the input inf file.

```PowerShell
Add-IoTDriverPackage C:\Mydriver\GPIO.inf MyDriver.GPIO
(or) newdrvpkg C:\Mydriver\GPIO.inf MyDriver.GPIO
New-IoTCabPackage MyDriver.GPIO
(or) buildpkg MyDriver.GPIO
```
For the older commandline tool, use [inf2cab.cmd](https://github.com/ms-iot/iot-adk-addonkit/tree/17134/Tools/inf2cab.cmd) creates the package xml file and also builds the cab file directly by invoking `buildpkg.cmd` internally.

> [!NOTE]
> Windows IoT Core supports Universal Inf only.

See also

* [Sample Driver Package](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/BSP/CustomRpi2/Packages/CustomRPi2.GPIO)

## Step 3: Install on device
---
* Connect to the device ([using SSH](/windows/iot-core/connect-your-device/SSH) or [using Powershell](/windows/iot-core/connect-your-device/powershell))
* Copy the `<filename>.cab` file to the device to a directory say C:\OemInstall
* Initiate staging of the package using `applyupdate -stage C:\OemInstall\<filename>.cab`. Note that this step is be repeated for each package, when you have multiple packages to install.
* Commit the packages using `applyupdate -commit`.
> [!NOTE]
> You can also install the cab using **Windows Update > CAB Install** option in Windows Device Portal.
The device will reboot into the update OS (showing gears) to install the packages and will reboot again to main OS. This process can take a few minutes.