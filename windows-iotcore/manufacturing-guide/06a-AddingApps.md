--- 
title: Adding an App to a Windows IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 09/20/2018 
ms.topic: article 
description: Description on how to add an App to a Windows IoT Core Image
keywords: Windows 10 IoT Core, 
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
Please make sure you've created a basic image from [Creating a Basic IoT Core Image](04-CreateBasicImage.md) previously. For this example, we have created a basic image with the Qualcomm DragonBoard called *TestDragonBoardProduct*.


You will need the following tools installed to complete this section:
* **Visual Studio**. This is needed to create the UWP application that will be added to the custom FFU image.
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.
* **[Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore)** for your specific architecture. These provide the IoT Core packages and feature manifest files needed to build custom Windows IoT images for the specific architecture (ARM, ARM64, x86, x64).
* **[IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/)**. These provide the sample scripts and base structure for building custom Windows IoT Core images.
* **Iot Core Shell**. This is included with the Windows ADK and is the commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* A text editor like **Notepad** or **VS Code**.


## Create an Appx Package
The first step is to create a **Universal Windows Platform (UWP)** application that will run on the IoT device. You may skip this section if you've already created and tested your UWP application.

1. Create a UWP application. This can be any app designed for IoT Core and saved as an Appx package. For our example, we are using the IoT Core sample [Hello World!](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld) app
2. In Visual Studio, save your application as an Appx package. This is done by clicking **Project > Store > Create App Packages > I want to Create Packages for Sideloading > Next** 
3. Select **Output Location** as C:\DefaultApp (or any other local filepath that doesn't include spaces)
4. Select **Generate app bundle:** Never
5. Click **Create**

![Dashboard screenshot](../media/ManufacturingGuide/CreateAppxPackage.jpg)

   Visual Studio creates the Appx package files in your specified location, for the architecture(s) you selected (ARM, x86, x64). In our example, this file is *C:\Users\jadali\Desktop\HelloWorld\CS\AppPackages\HelloWorld_1.0.0.0_ARM_Debug.appx* (for ARM architecture).
   

## Package the Appx
The next step is to package the Appx file, which will allow you to customize it and build it using the Windows ADK (when you build the FFU image).

1. Open **IoT Core Shell** as an administrator
2. Create the package for your Appx by using [Add-IoTAppxPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTAppxPackage.md). Replace the file path location and package name with your Appx package. In our example, the command is as follows:

  ```powershell
     Add-IoTAppxPackage "C:\Users\jadali\Desktop\HelloWorld\CS\AppPackages\HelloWorld_1.0.0.0_ARM_Debug.appx" fga Appx.HelloWorldApp
     (or) newAppxPkg "C:\Users\jadali\Desktop\HelloWorld\CS\AppPackages\HelloWorld_1.0.0.0_ARM_Debug.appx" fga Appx.HelloWorldApp
  ```

Please note that the *fga* parameter indicates the Appx file is a foreground application. Also, the *Appx.HelloWorldApp* is the name of the Appx file for referencing in the Windows ADK XML files when building the FFU image (you can call this whatever is appropriate for your scenario).

Also be aware that if your Appx has dependencies you will need the *Dependencies* subdirectory to be present in the same location as your Appx when you run this command. Failure to include this will result in errors when you build your FFU image.

3. From **IoT Core Shell**, you can now build the package into a .CAB file (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md))

        ```powershell
        New-IoTCabPackage Appx.HelloWorldApp
        (or) buildpkg Appx.HelloWorldApp
        ```

    This will build the package into a .CAB file under the **Build\\< arch >\pkgs** subdirectory in the ADK Toolkit files. In our example, this file is located in *C:\IoT-ADK-AddOnToolkit\Build\ARM\pkgs\Contoso.Appx.HelloWorldApp.cab*.

    This also adds a FeatureID called **APPX_HELLOWORLDAPP** to the `C:\MyWorkspace\Source-< arch>\Packages\OEMFM.xml` file.

## Update Project Configuration Files
You can now update your product configuration files to include your app in the FFU image build. 

1. Add the Feature ID for your app package using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md):

```powershell
Add-IoTProductFeature <product name> Test APPX_HELLOWORLDAPP -OEM
or addfid <product name> Test APPX_HELLOWORLDAPP -OEM
```

2. Remove the sample test apps **IOT_BERTHA** using [Remove-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Remove-IoTProductFeature.md):
```powershell
Remove-IoTProductFeature <product name> Test IOT_BERTHA
or addfid <product name> Test IOT_BERTHA
```

## Build and Test Image
Build the FFU image again, as specified in [Creating a Basic IoT Core Image](04-CreateBasicImage.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

    ```powershell
    New-IoTFFUImage <product name> Test
    (or)buildimage <product name> Test 
    ```
Once the FFU file has been built (it should now include your app), you can flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](05-FlashingImage.md).

## Next Steps
[Creating a Provisioning Package](06b-CreateProvisioningPackage.md)

