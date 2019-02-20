---
title: Creating a Provisioning Package for a Windows IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 09/20/2018 
ms.topic: article 
description: Description on how to create a provisioning package for a Windows IoT Core Image
keywords: Windows 10 IoT Core, 
---

# Creating a Provisioning Package for a Windows IoT Core Image
A provisioning package allows you to apply customization settings over an existing Windows IoT Core installation image. We will describe the steps required to create a provisioning package that you can apply to your Windows 10 IoT Core FFU images.

## Goals
* Create a provisioning package that contains customizations for your device
* Package the provisioning package so it can be included in an FFU image
* Modify IoT Addon Kit project configuration files to include your provisioning package customizations
* Build and deploy an FFU image that contains your provisioning package customizations

## Prerequisites/Requirements
Please make sure you've created an image with your custom App from [06a-Adding an App to an image](06a-AddingApps.md) previously. For this example, we have created an image with the Qualcomm DragonBoard called *TestDragonBoardProduct* that contains the sample app [Hello World!](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld).

You will need the following tools installed to complete this section:
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.
* **Windows Configuration Designer**. Part of the Windows ADK, this provides tooling to create custom provisioning packages for Windows IoT Core devices.
* **IoT Core Powershell Environment**. This is included with the Windows ADK and is the Powershell commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* A text editor like **Notepad** or **VS Code**.

## Install Windows Configuration Designer
We will be using **Windows Configuration Designer (WCD)** to create a provisioning package for our IoT Core image. Windows Configuration Designer allows you to create provisioning packages, which are used to configure devices running Windows 10 IoT Core.

Windows Configuration Designer comes with the **Windows ADK Toolkit** and should have been installed to the Technician PC previously. If not, please run the install for the Windows ADK Toolkit and make sure you have the **Configuration Designer** selection checked for installation.

![Dashboard screenshot](../media/ManufacturingGuide/WindowsADKSetup.jpg)

## Create WCD Project for a Provisioning Package
In order to create a provisioning package for your device, we need to create a project in **Windows Configuration Designer**. Once we have this project, we can specify the configuration customizations we want included in our FFU image.

1. From your Technician PC, run **Windows Imaging and Configuration Designer**.
2. Create a new project by clicking **File > New Project**. For our example, we created a project called *TestProvPackage*.
3. Select **Provisioning Package** and click **Next**.
4. On the **Choose which settings to view and configure** page, select **Windows 10 IoT Core**. Click **Next**.

   ![Dashboard screenshot](../media/ManufacturingGuide/ProvPackage1.jpg)

5. At the **Import a provisioning package(optional)** page, leave the entry blank and click **Finish**.
6. Add a sample setting. For our example, we will specify a default startup app that executes when the IoT Core device is booted up.
   
   a. Change the **View** dropdown under **Available Customizations** to *Common IoT Settings*.

   b. Expand the **Runtime settings > Startup App > Default** node.

   c. Enter the [Application User Model ID (AUMID)](https://docs.microsoft.com/windows/configuration/find-the-application-user-model-id-of-an-installed-app) of the app you want to be the default startup app. For our example, this value is *HelloWorld_1w720vyc4ccym!App*.

   ![Dashboard screenshot](../media/ManufacturingGuide/ProvPackage2.jpg)
   
   d. Save the project.

7. Export the provisioning package.

   a. Click **Export > Provisioning Package**. An export dialog will appear. You can modify the **Name**, **Version** and **Rank** field, as well as the **Owner**. Select *OEM* for **Owner** and click **Next**.

   ![Dashboard screenshot](../media/ManufacturingGuide/ProvPackage3.jpg)

   b. Under **Select security details for the provisioning package**, uncheck the **Encrypt package** and **Sign package** checkboxes. Click **Next**.

   c. Click **Build** to build the provisioning package. A dialog listing the output location will appear when the export is complete. Click **Finish**.

8. Create a provisioning package using [Add-IoTProvisioningPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProvisioningPackage.md):

```powershell
Add-IoTProvisioningPackage Prov.TestProvPackage "C:\Users\<username>\Documents\Windows Imaging and Configuration Designer (WICD)\TestProvPackage\TestProvPackage.ppkg"
(or) newprovpkg Prov.TestProvPackage "C:\Users\<username>\Documents\Windows Imaging and Configuration Designer (WICD)\TestProvPackage\TestProvPackage.ppkg"
```
This creates a new folder at `C:\MyWorkspace\Common\Packages\Prov.TestProvPackage`.
This also adds a FeatureID called **PROV_TESTPROVPACKAGE** to the `C:\MyWorkspace\Common\Packages\OEMCOMMONFM.xml` file.

## Build and Test Image
Build the FFU image again, as specified in [Creating a Basic IoT Core Image](04-CreateBasicImage.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command:

    ```powershell
    New-IoTFFUImage <product name> Test
    (or)buildimage <product name> Test 
    ```
Once the FFU file has been built and you flash it to your hardware device as specified in [Flashing a Windows IoT Core Image](05-FlashingImage.md), your provisioning package customizations should be applied when you power up the device. In our example, the default app is the [Hello World!](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld) app and will run when the device is booted up.


## Next Steps
[Adding file(s) and registry settings to an image](06c-AddFileRegistrySettings.md)

