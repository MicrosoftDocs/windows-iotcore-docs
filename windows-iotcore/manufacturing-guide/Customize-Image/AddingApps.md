---
title: Adding an App to a Windows IoT Core Image
author: lmaung
ms.author: Lwin Maung
ms.date: 03/21/2019 
ms.topic: article 
description: Description on how to add an App to a Windows IoT Core Image
keywords: Windows 10 IoT Core, images
---

# Adding an App to a Windows IoT Core Image
We are now going to take an app (like the IoT Core sample [Hello World!](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld) app), package it up and create a new Windows IoT Core image that you can load onto your device. 

Please note that this process is identical for both background and foreground apps. The only difference to be aware of is that only one foreground app can be selected as the startup app, and all other installed apps will run as background apps.

## Goals
* Create a custom Universal Windows Platform (UWP) application that will be installed on a device
* Package the UWP application so it can be included in an FFU image
* Modify IoT Addon Kit project configuration files to include your UWP application package
* Build and deploy an FFU image that contains your UWP app package

## Prerequisites/Requirements
Please make sure you've created a basic image from [Creating a Basic IoT Core Image](../Create-IoT-Image/CreateBasicImage.md) previously. For this example, we have created a basic image with the Qualcomm DragonBoard called *TestDragonBoardProduct*.


You will need the following tools installed to complete this section:
* **Visual Studio**. This is needed to create the UWP application that will be added to the custom FFU image.
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.

    > [!NOTE]
    > The version of ADK used must match the version of IoT Core Packages used below.

* **[Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore)** for your specific architecture. These provide the IoT Core packages and feature manifest files needed to build custom Windows IoT images for the specific architecture (ARM, ARM64, x86, x64).
* **[IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)**. These provide the sample scripts and base structure for building custom Windows IoT Core images.
* **IoT Core Powershell Environment**. This is included with the Windows ADK and is the Powershell commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* A text editor like **Notepad** or **VS Code**.

## Supported Application Types
Windows IoT Core supports the following application types:

### Universal Windows Platform (UWP) Apps
IoT Core is a UWP centric OS and UWP apps are its primary app type.

Universal Windows Platform (UWP) is a common app platform across all version of Windows 10, including Windows 10 IoT Core. UWP is an evolution of Windows Runtime (WinRT). You can find more information and an overview to UWP on [docs.microsoft.com](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide).

### Traditional UWP Apps
UWP apps just work on IoT Core, just as they do on other Windows 10 editions. A simple, blank Xaml app in Visual Studio will properly deploy to your IoT Core device just as it would on a phone or Windows 10 PC. All of the standard UWP languages and project templates are fully supported on IoT Core.

There are a few additions to the traditional UWP app-model to support IoT scenarios and any UWP app that takes advantage of them will need the corresponding information added to their manifest. In particular the "iot" namespace needs to be added to the manifest of these standard UWP apps.

Inside the attribute of the manifest, you need to define the iot xmlns and add it to the IgnorableNamespaces list. The final xml should look like this:

```xml
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:iot="http://schemas.microsoft.com/appx/manifest/iot/windows10"
  IgnorableNamespaces="uap mp iot">
```

### Background Apps
In addition to the traditional UI apps, IoT Core has added a new UWP app type called "Background Applications". These applications do not have a UI component, but instead have a class that implements the "IBackgroundTask" interface. They then register that class as a "StartupTask" to run at system boot. Since they are still UWP apps, they have access to the same set of APIs and are supported from the same language. The only difference is that there is no UI entry point.

Each type of IBackgroundTask gets its own resource policy. This is usually restrictive to improve battery life and machine resources on devices where these background apps are secondary components of foreground UI apps. On IoT devices, Background Apps are often the primary function of the device and so these StartupTasks get a resource policy that mirrors foreground UI apps on other devices.

You can find in-depth information on Background apps on [MSDN](https://docs.microsoft.com/windows/iot-core/develop-your-app/backgroundapplications).

### Non-UWP (Win32) Apps
IoT Core supports certain traditional Win32 app types such as Win32 Console Apps and NT Services. These apps are built and run the same way as on Windows 10 Desktop. Additionally, there is an IoT Core C++ Console project template to make it easy to build such apps using Visual Studio.

There are two main limitations on these non-UWP applications:

1. *No legacy Win32 UI support*: IoT Core does not contain APIs to create classic (HWND) Windows. Legacy methods such as CreateWindow() and CreateWindowEx() or any other methods that deal with Windows handles (HWNDs) are not available. Subsequently, frameworks that depend on such APIs including MFC, Windows Forms and WPF, are not supported on IoT Core.
2. *C++ Apps Only*: Currently, only C++ is supported for developing Win32 apps on IoT Core.

### App Service
App services are UWP apps that provide services to other UWP apps. They are analogous to web services, on a device. An app service runs as a background task in the host app and can provide its service to other apps. For example, an app service might provide a bar code scanner service that other apps could use. App services let you create UI-less services that apps can call on the same device, and starting with Windows 10, version 1607, on remote devices. Starting in Windows 10, version 1607, you can create app services that run in the same process as the host app.

Additional information regarding creating a background app service as well as consuming the service from a uwp apps (as well as background tasks/services) can be found [here] (https://docs.microsoft.com/en-us/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service)

# Extend your app with services, extensions, and packages

There are many technologies in Windows 10 for extending and componentizing your app. This table should help you determine which technology you should use depending on requirements. It is followed by a brief description of the scenarios and technologies.

| Scenario                           | Resource package   | Asset package      | Optional package   | Flat bundle        | App Extension      | App service        | Streaming Install  |
|------------------------------------|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|
| Third-party code plug-ins            |                    |                    |                    |                    | :heavy_check_mark: |                    |                    |
| In-proc code plug-ins              |                    |                    | :heavy_check_mark: |                    |                    |                    |                    |
| UX Assets (strings/images)         | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| On demand content <br/> (e.g. additional Levels) |      |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| Separate licensing and acquisition |                    |                    | :heavy_check_mark: |                    | :heavy_check_mark: | :heavy_check_mark: |                    |
| In-app acquisition                 |                    |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    |                    |
| Optimize install time              | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| Reduce disk footprint              | :heavy_check_mark: |                    | :heavy_check_mark: |                    |                    |                    |                    |
| Optimize packaging                 |                    | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    |                    |                    |
| Reduce publishing time             | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    |                    |                    |




## Create an Appx Package
The first step is to create a **Universal Windows Platform (UWP)** application that will run on the IoT device. You may skip this section if you've already created and tested your UWP application.

1. Create a UWP application. This can be any app designed for IoT Core and saved as an Appx package. For our example, we are using the IoT Core sample [Hello World!](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld) app
2. In Visual Studio, save your application as an Appx package. This is done by clicking **Project > Store > Create App Packages > I want to Create Packages for Sideloading > Next** 
3. Select **Output Location** as C:\DefaultApp (or any other local filepath that doesn't include spaces)
4. Select **Generate app bundle:** Never
5. Click **Create**

![Dashboard screenshot](../../media/ManufacturingGuide/CreateAppxPackage.jpg)

   Visual Studio creates the Appx package files in your specified location, for the architecture(s) you selected (ARM, x86, x64). In our example, this file is *C:\Dev\OpenSource\ContosoApp\ContosoApp\AppPackages\ContosoApp_1.0.0.0_ARM_Debug_Test\ContosoApp_1.0.0.0_ARM_Debug.appx* (for ARM architecture).
   

## Package the Appx
The next step is to package the Appx file, which will allow you to customize it and build it using the Windows ADK (when you build the FFU image).

1. Open `IoTCorePShell.cmd`. It should prompt you to run as an administrator.
2. Create the package for your Appx by using [Add-IoTAppxPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTAppxPackage.md). Replace the file path location and package name with your Appx package. In our example, the command is as follows:

  ```powershell
     Add-IoTAppxPackage "C:\Dev\OpenSource\ContosoApp\ContosoApp\AppPackages\ContosoApp_1.0.0.0_ARM_Debug_Test\ContosoApp_1.0.0.0_ARM_Debug.appx" fga Appx.ContosoApp
     (or) newAppxPkg "C:\Dev\OpenSource\ContosoApp\ContosoApp\AppPackages\ContosoApp_1.0.0.0_ARM_Debug_Test\ContosoApp_1.0.0.0_ARM_Debug.appx" fga Appx.ContosoApp
  ```


> [!NOTE]
> The *fga* parameter indicates the Appx file is a foreground application. If you specify your package as a background application (with the *bga* parameter) and have no other foreground applications in the image, the system will get stuck when booting up (displays a spinner indefinitely).

The *Appx.HelloWorldApp* is the name of the Appx file for referencing in the Windows ADK XML files when building the FFU image (you can call this whatever is appropriate for your scenario).

Be aware that if your Appx has dependencies you will need the *Dependencies* subdirectory to be present in the same location as your Appx when you run this command. Failure to include this will result in errors when you build your FFU image.

3. From **IoT Core Powershell Environment**, you can now build the package into a .CAB file (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md))

        ```powershell
        New-IoTCabPackage Appx.ContosoApp
        (or) buildpkg Appx.ContosoApp
        ```

    This will build the package into a .CAB file under the `Workspace\Build\<arch>\pkgs` subdirectory in the ADK Toolkit files. In our example, this file is located in *C:\IoT\Workspaces\ContosoWS\Build\arm\pkgs\Contoso.Appx.ContosoApp.cab*.

## Update Project Configuration Files
You can now update your product configuration files to include your app in the FFU image build. 

1. Add the Feature ID for your app package using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md):

```powershell
Add-IoTProductFeature ProductX Test APPX_CONTOSOAPP -OEM
or addfid ProductX Test APPX_CONTOSOAPP -OEM
```


  This adds a FeatureID called **APPX_HELLOWORLDAPP** to the specified product's Test OEMInput XML file (`C:\IoT\Workspaces\ContosoWS\Source-arm\<product name>\TestOEMInput.xml` file).

## Build and Test Image

From IoT Core Powershell Environment, get your environment ready to create products by building all of the packages in the working folders (using New-IoTCabPackage):

```powershell
New-IoTCabPackage All
(or) buildpkg all
```

Build the FFU image again, as specified in [Creating a Basic IoT Core Image](../Create-IoT-Image/CreateBasicImage.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

```powershell
New-IoTFFUImage ProductX Test
(or)buildimage ProductX Test 
```

Once the FFU file has been built (it should now include your app), you can flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](../Create-IoT-Image/FlashingImage.md).

## Next Steps
[Creating a Provisioning Package](CreateProvisioningPackage.md)

