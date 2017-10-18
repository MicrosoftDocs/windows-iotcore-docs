---
title: Create and Install a package
author: parameshbabu
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
description: Learn how to set up your environment and create and install packages for Windows IoT Core.
keywords: windows iot, package creation, package installation
---

# Create and install a package
[Packages](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-manufacturing-guide#Packages) are the logical building blocks of IoT Core. From device drivers to system files, every component must be contained in a package. This is the smallest servicable unit on the device.

## Step 1: Get set up

### Install the tools

1. [Windows Assessment and Deployment Kit(Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
2. [IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)

### Set up your environment

* Edit `\IoT-ADK-AddonKit\Tools\setOEM.cmd` to set the OEM_NAME
* Launch `IoTCoreShell.cmd` ( this one launches in the elevated prompt )
* Select the required architecture in the `Set Environment for Architecture` prompt
* Install test signing certificates using `InstallOEMCerts` . This is required *only once* for the PC.

To create your own image (FFU), follow the steps outlined in the ["Create a basic image" lab in the IoT Manufacturing guide](https://docs.microsoft.com/windows-hardware/manufacture/iot/create-a-basic-image).

## Step 2: Create a new package
1. Create a **package definition xml file** (.wm.xml file), and specify the files and reg keys you want to add. 
      Learn more at [Windows Universal OEM Package Schema](https://docs.microsoft.com/windows-hardware/manufacture/iot/package-schema).

2. Build the package: `buildpkg.cmd filename.wm.xml`. The .cab file will be created in the build directory `\IoT-ADK-AddonKit\Build\<arch>\pkgs`.

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

Use [newappxpkg.cmd](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/newappxpkg.cmd) to generate the .wm.xml file for a given appx file. This tool expects the appx dependencies in the sub directory named "dependencies" in the folder containing the appx file.

    newappxpkg HelloWorld.appx fga Appx.HelloWorld
    buildpkg Appx.HelloWorld

`fga` sets the appx as the foreground startup app, `bgt` sets the appx as the background task and `none` skips startup configuration.

See [Appx.IoTCoreDefaultApp](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/Packages/Appx.IoTCoreDefaultApp/) as an example.

When you have to install multiple applications signed with same certificate, you can add the certificate along with one app and for the remaining apps, you can skip adding the certificate using the skipcert flag.

    newappxpkg AnotherApp.appx none Appx.AnotherApp skipcert

See also

* [Lab 1b: Add an app to your image](https://docs.microsoft.com/windows-hardware/manufacture/iot/deploy-your-app-with-a-standard-board)


### Create a driver package

The driver package contains the references (InfSource) to the Inf file for the driver and also lists all the files referenced in the Inf file. You can author the driver .wm.xml file manually or use [inf2pkg.cmd](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/inf2pkg.cmd) that generates package xml based on the input inf file.

[inf2cab.cmd](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/inf2cab.cmd) creates the package xml file and also builds the cab file directly by invoking `buildpkg.cmd` internally.

> [!NOTE]
> Windows IoT Core supports Universal Inf only.

See also

* [Sample Driver Package](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/BSP/CustomRpi2/Packages/CustomRPi2.GPIO)

## Step 3: Install on device
---

* Connect to the device ([using SSH](../connect-your-device/SSH.md) or [using Powershell](../connect-your-device/powershell.md))
* Copy the <filename>.cab file to the device to a directory say C:\OemInstall
* Initiate staging of the package using `applyupdate -stage C:\OemInstall\<filename>.cab`. Note that this step is be repeated for each package, when you have multiple packages to install.
* Commit the packages using `applyupdate -commit`.

> [!NOTE]
> You can also install the cab using **Windows Update > CAB Install** option in Windows Device Portal.

The device will reboot into the update OS (showing gears) to install the packages and will reboot again to main OS. This process can take a few minutes.
