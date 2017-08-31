---
title: Create and Install a package
author: parameshbabu
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
ms.prod: Windows
ms.technology: IoT
description: How to create and install packages for IoT Core.
keywords: windows iot, package creation, package installation
---

# Create and install a package
[Packages](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/iot/iot-core-manufacturing-guide#Packages) are the logical building blocks of IoT Core. From device drivers to system files, every component must be contained in a package. This is the smallest servicable unit on the device.

## Step 1: Get set up

### Install the tools

1. [Windows Assessment and Deployment Kit(Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit#winADK)
2. [IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)
3. [Windows Driver Kit (WDK)](https://developer.microsoft.com/en-us/windows/hardware/windows-driver-kit)

### Set up your environment

* Edit `\IoT-ADK-AddonKit\Tools\setOEM.cmd` to set the OEM_NAME
* Launch `IoTCoreShell.cmd` ( this one launches in the elevated prompt )
* Select the required architecture in the `Set Environment for Architecture` prompt
* Install test signing certificates using `InstallOEMCerts` . This is required *only once* for the PC.

To create your own image (FFU), [follow the steps outlined in the "Create a basic image" lab in the IoT Manufacturing guide. (https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/create-a-basic-image).

## Step 2: Create a new package
1. Create a **package definition xml file** (.pkg.xml file), and specify the files and reg keys you want to add.
      Learn more at [Specifying components in a package](https://msdn.microsoft.com/en-us/library/dn789218) and [Elements and Attributes of a package](https://msdn.microsoft.com/en-us/library/dn756796)

2. Build the package: `buildpkg.cmd filename.pkg.xml`. The .cab file will be created in the build directory `\IoT-ADK-AddonKit\Build\<arch>\pkgs`.

### Create a package with files and reg keys
Below is an example for specifying files and reg keys.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="urn:Microsoft.WindowsPhone/PackageSchema.v8.00"
   Owner="OEMName"           OwnerType="OEM"
   ReleaseType="Test"        Platform="PlaformName"
   Component="ComponentName" SubComponent="SubName">
   <Components>
      <OSComponent>
         <Files>
            <File Source="$(_RELEASEDIR)\test_file1.dll"/>
            <File Source="$(_RELEASEDIR)\toBeRenamed.dat"
               DestinationDir="$(runtime.system32)\test" Name="test.dat"/>
         </Files>
         <RegKeys>
            <RegKey KeyName="$(hklm.software)\OEMName\test">
               <RegValue Name="StringValue" Value="Test string" Type="REG_SZ"/>
               <RegValue Name="DWordValue" Value="12AB34CD" Type="REG_DWORD"/>
               <RegValue Name="BinaryValue" Value="12,AB,CD,EF" Type="REG_BINARY"/>
            </RegKey>
            <RegKey KeyName="$(hklm.software)\OEMName\EmptyKey"/>
         </RegKeys>
      </OSComponent>
   </Components>
</Package>
```

### Create an Appx package

Use [appx2pkg.cmd tool](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/appx2pkg.cmd) to generate the .pkg.xml file for a given appx file. This tool expects the appx dependencies in the sub directory named "dependencies" in the folder containing the appx file.

You can also create the Appx component directly in the IoTCoreShell, using the following steps

    > newappxpkg HelloWorld.appx fga Appx.HelloWorld
    > buildpkg Appx.HelloWorld

`fga` sets the appx as the foreground startup app, `bgt` sets the appx as the background task and `none` skips startup configuration.

See [Appx.IoTCoreDefaultApp](https://github.com/ms-iot/iot-adk-addonkit/blob/develop/Source-arm/Packages/Appx.IoTCoreDefaultApp/) as an example.

When you have to install multiple applications signed with same certificate, you can add the certificate along with one app and for the remaining apps, you can skip adding the certificate using the skipcert flag.

    > newappxpkg AnotherApp.appx none Appx.AnotherApp skipcert

See also

* [Lab 1b: Add an app to your image](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/iot/deploy-your-app-with-a-standard-board)


### Create a driver package

The driver package contains the references (InfSource) to the Inf file for the driver and also lists all the files referenced in the Inf file. You can author the driver .pkg.xml file manually or use [inf2pkg.cmd tool](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/inf2pkg.cmd) that generates package xml based on the input inf file.

[`inf2cab.cmd` tool](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/inf2cab.cmd) creates the package xml file and also builds the cab file directly by invoking `buildpkg.cmd` internally.

> [!NOTE]
> Windows IoT Core supports Universal Inf only.

See also

* [Sample Driver Package](https://github.com/ms-iot/iot-adk-addonkit/blob/develop/Source-arm/BSP/CustomRpi2/Packages/CustomRPi2.GPIO/CustomRPi2.GPIO.pkg.xml)

## Step 3: Install on device
---

* Connect to the device ([using SSH](../connect-your-device/SSH.md) or [using Powershell](../connect-your-device/powershell.md))
* Copy the <filename>.cab file to the device to a directory say C:\OemInstall
* Initiate staging of the package using `applyupdate -stage C:\OemInstall\<filename>.cab`. Note that this step is be repeated for each package, when you have multiple packages to install.
* Commit the packages using `applyupdate -commit`.

The device will reboot into the update OS (showing gears) to install the packages and will reboot again to main OS. This process can take a few minutes.
