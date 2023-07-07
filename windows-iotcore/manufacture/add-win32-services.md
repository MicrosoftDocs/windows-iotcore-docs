---
title: Lab 1f Add Win32 services to an image
description: To get started, we will create a basic Windows 10 IoT Core (IoT Core) image, flash it to a micro SD card, and put it into a device to make sure that everything is working properly. (add-win32-services)
ms.date: 10/15/2018
ms.topic: article
---

# Lab 1f: Add Win32 services to an image

Windows 10 IoT Core supports adding a Win32 NT Service to your image.

## Prerequisites/Requirements

Make sure you've created a basic image from  [Create a basic image](create-a-basic-image.md). 

You will need the following tools installed to complete this section:

* Windows Assessment and Deployment Kit (Windows ADK)

> [!NOTE]
> The version of ADK used must match the version of IoT Core Packages used below.

* Windows 10 IoT Core Packages
* IoT Core PowerShell Environment
* IoT Core ADK Add-Ons
* A text editor like Notepad or VS Code

## Add a Win32 Service app to package build
In order to include your Win32 Service App in the FFU image build process, you first must add the .EXE file so that it can be packaged up (using `buildpkg`).

1. Create a subdirectory for your Win32 Service App under `C:\IoT\Workspaces\ContosoWS\Source-<arch>\Packages`. This will contain the XML and EXE files to include when building the image. For example, refer to the **AzureDM.Services** subdirectory at `C:\IoT\Workspaces\ContosoWS\Source-<arch>\Packages\AzureDM.Services` for a working example.

2. Create an XML file titled `<your Win32 Service App Name>.wm.xml` in the subdirectory you created from Step #1. This file will specify how the package will be built. Here is an example of what that file should look like (you would replace the appropriate entries with your Win32 Service App information):


```xml
<?xml version="1.0" encoding="utf-8"?>
<identity xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
name="Services"
namespace="AzureDM"
owner="$(OEMNAME)"
legacyName="$(OEMNAME).<your Win32 Service App Name>.Services" xmlns="urn:Microsoft.CompPlat/ManifestSchema.v1.00">
<onecorePackageInfo
targetPartition="MainOS"
releaseType="Production"
ownerType="OEM" />
<files>
<file
destinationDir="$(runtime.system32)"
source="<your Win32 Service App Name executable filename>" />
</files>
<service
name="<your Win32 Service App Name>"
start="auto"
type="win32OwnProcess"
objectName="LocalSystem"
errorControl="normal"
displayName="<your Win32 Service App Display Name>"
description="<your Win32 Service App Description>"
imagePath="<path and file name of your Win32 Service App>">
<failureActions
resetPeriod="86400">
<actions>
<action
type="restartService"
delay="1000" />
<action
type="restartService"
delay="1000" />
<action
type="restartService"
delay="1000" />
<action
type="none"
delay="0" />
</actions>
</failureActions>
</service>
</identity>
```

> [!NOTE]
> The `<service>` area in the XML file specifies Win32 Service-specific information. If you are adding a Win32 application (like a console app), this section can be omitted.

3. Add your EXE file to the subdirectory from Step #1. This is your Win32 Service application executable.

## Package the Win32 Service App
The next step is to package the Win32 Service App file, which will allow you to build it using the Windows ADK (when you build the FFU image).

1. Open `IoTCorePShell.cmd` from your workspace. It should prompt you to run as an administrator.
2. Build the package into a .CAB file (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md))

``` powershell
New-IoTCabPackage <your Win32 Service App Name>
(or) buildpkg <your Win32 Service App Name>
```

This will build the package into a .CAB file under the `\Build\<arch>\pkgs` subdirectory in your workspace.

## Update Project Configuration Files
You can now update your product configuration files to include your app in the FFU image build. 

1. Add the Feature ID for your app package using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md), replacing `<your Win32 service app name>` with an identifier for your Win32 service app:

``` powershell
Add-IoTProductFeature <product name> Test <your Win32 service app name> -OEM
or addfid <product name> Test <your Win32 service app name> -OEM
```

This adds a FeatureID corresponding to the identifier you chose for your Win32 service app.

## Build and Test Image

Build the FFU image again, as specified in [Create a Basic IoT Core Image](create-a-basic-image.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

``` powershell
New-IoTFFUImage ProductX Test
(or)buildimage ProductX Test 
```

Once the FFU file has been built (it should now include your app), you can flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](./create-a-basic-image.md#flash-a-windows-iot-core-image).

## Next Steps
[Lab 1g: Build a retail image](./build-retail-image.md)
