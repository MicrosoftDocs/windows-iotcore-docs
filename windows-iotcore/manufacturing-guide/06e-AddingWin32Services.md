---
title: Adding a Win32 Service App to a Windows IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 12/6/2018 
ms.topic: article 
description: Description on how to add a Win32 Service to a Windows IoT Core Image
keywords: Windows 10 IoT Core, images
---

# Adding a Win32 NT Service to a Windows IoT Core Image
Windows 10 IoT Core supports adding a Win32 NT Service to your image.

## Goals
* Package a Win32 Service application so it can be included in an FFU image
* Modify IoT Addon Kit project configuration files to include your Win32 Service application package
* Build and deploy an FFU image that contains your Win32 NT Service package

## Prerequisites/Requirements
Please make sure you've created a basic image from [Creating a Basic IoT Core Image](04-CreateBasicImage.md) previously. For this example, we have created a basic image with the Qualcomm DragonBoard called *TestDragonBoardProduct*.


You will need the following tools installed to complete this section:
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.

    > [!NOTE]
    > The version of ADK used must match the version of IoT Core Packages used below.

* **[Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore)** for your specific architecture. These provide the IoT Core packages and feature manifest files needed to build custom Windows IoT images for the specific architecture (ARM, ARM64, x86, x64).
* **[IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)**. These provide the sample scripts and base structure for building custom Windows IoT Core images.
* **IoT Core Powershell Environment**. This is included with the Windows ADK and is the Powershell commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* A text editor like **Notepad** or **VS Code**.


## Add Win32 Service App to Package Build
In order to include your Win32 Service App in the FFU image build process, you first must add the .EXE file so that it can be packaged up (using `buildpkg`).

1. Create a subdirectory for your Win32 Service App under `iot-adk-addonkit/Workspace/Source-<arch>/Packages`. This will contain the XML and EXE files to include when building the image. For example, refer to the **AzureDM.Services** subdirectory at `iot-adk-addonkit/Workspace/Source-<arch>/Packages/AzureDM.Services` for a working example.

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

1. Open `IoTCorePShell.cmd`. It should prompt you to run as an administrator.
2. Build the package into a .CAB file (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md))

        ```powershell
        New-IoTCabPackage Appx.HelloWorldApp
        (or) buildpkg Appx.HelloWorldApp
        ```

    This will build the package into a .CAB file under the `Workspace\Build\<arch>\pkgs` subdirectory in the ADK Toolkit files.

## Update Project Configuration Files
You can now update your product configuration files to include your app in the FFU image build. 

1. Add the Feature ID for your app package using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md), replacing `<your Win32 service app name>` with an identifier for your Win32 service app:

```powershell
Add-IoTProductFeature <product name> Test <your Win32 service app name> -OEM
or addfid <product name> Test <your Win32 service app name> -OEM
```

  This adds a FeatureID corresponding to the identifier you chose for your Win32 service app to the `C:\iot-adk-addonkit-master\Workspace\Source-arm\Packages\OEMFM.xml` file (under the OEM Features section).

## Build and Test Image

Build the FFU image again, as specified in [Creating a Basic IoT Core Image](04-CreateBasicImage.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

```powershell
New-IoTFFUImage <product name> Test
(or)buildimage <product name> Test 
```

Once the FFU file has been built (it should now include your app), you can flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](05-FlashingImage.md).

## Next Steps
[Creating a Retail Image](07-CreateRetailImage.md)

