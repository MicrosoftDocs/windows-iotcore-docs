---
title: Creating a Retail IoT Core Image
author: johnadali
ms.author: johnadali
ms.date: 10/05/2018 
ms.topic: article 
description: Steps to create a retail Windows IoT Core image
keywords: Windows 10 IoT Core, 
---

# Creating a Retail IoT Core Image
We will detail the steps needed to create a retail Windows IoT Core image and flash it onto a specific hardware device.

## Goals
* Create a project using Windows ADK Toolkit that can be used to create Windows IoT Core images
* Add a custom application to a Windows IoT Core retail image
* Build a Full Flashable Update (FFU) file for a Windows IoT Core retail image

## Prerequisites/Requirements
Please make sure you've created a basic test image from [Creating a Basic IoT Core Image](04-CreateBasicImage.md) previously. For this example, we have created a basic image with the Qualcomm DragonBoard called *TestDragonBoardProduct*.

You will need the following tools installed to complete this section:
* A retail [code-signing](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate) certificate. For the kernel driver signing, a Standard code-signing certificate is sufficient. You will require an EV certificate to access the Device Update Center in Hardware Dev Center portal.
* A [Cross-Signing certificate](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing) that matches the CA of your retail code-signing certificate.
* **Visual Studio**. This is needed to create the UWP application that will be added to the custom FFU image, as well as properly signing the application with your retail code-signing certificate.
* **[Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)**. This provides the OEM-specific tooling and files to create and customize images for Windows IoT Core.
* **IoT Core Powershell Environment**. This is included with the Windows ADK and is the Powershell commandline window interface where you execute commands to build custom FFU images for Windows IoT Core.
* A text editor like **Notepad** or **VS Code**.


## Modify Project Configuration Files
Follow the steps below to add any custom applications or provisioning packages you want to add to the retail image. For our example, we are modifying the project files for our Qualcomm DragonBoard project called *TestDragonBoardProduct*.

1. To add a custom application, you should follow the instructions listed in [Adding an App to an image](06a-AddingApps.md). However, you would specify `Retail` instead of `Test` when executing the [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md) command, as shown here:

    ```powershell
    Add-IoTProductFeature <product name> Retail APPX_HELLOWORLDAPP -OEM
    or addfid <product name> Retail APPX_HELLOWORLDAPP -OEM
    ```

    This adds a FeatureID called **APPX_HELLOWORLDAPP** to the specified product's Retail OEMInput XML file (`C:\MyWorkspace\Source-arm\<product name>\RetailOEMInput.xml` file).

2. Minimize the included Windows IoT Core features. You also want to remove any test applications that are included (by default) with test images for Windows IoT Core. This includes the IoT Core default application (aka. Bertha), along with any other developer tools or testing features. You can do this by using [Remove-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Remove-IoTProductFeature.md):

    ```powershell
    Remove-IoTProductFeature <product name> Test IOT_BERTHA
    or removefid <product name> Test IOT_BERTHA
    ```

## Properly Signing and Including Your Applications
If you have one or more custom applications that you want to include in your Windows IoT Core retail image, you need to verify that these applications are signed properly when including them in your retail image. Follow these steps for each application you want to include in your image. Please note that you can skip Steps 8 and 9 if you only have one application to include.

1. Install your retail code-signing certificate on your technician PC.
2. Open your custom application **in Visual Studio** and open the **Package.appxmanifest** file.
3. Click on the **Packaging** tab and click on **Choose Certificate...** button.

   ![Dashboard screenshot](../media/ManufacturingGuide/RetailImageAppxCertSelection1.jpg)

4. The dialog displayed will show what certificate is being used for code-signing. Click on the **Configure Certificate...** dropdown and select **Pick from certificate store...**:

   ![Dashboard screenshot](../media/ManufacturingGuide/RetailImageAppxCertSelection2.jpg)


5. Choose your retail code-signing certificate when prompted and click **OK**.
6. Save your project in **Visual Studio** and then build your Appx package. Please note that you should be prompted for your password for your retail code-signing certificate when building this package.
7. Once the Appx file is built, run the following command in **IoT Core Powershell Environment**:

  ```powershell
     Add-IoTAppxPackage "C:\Users\jadali\Desktop\HelloWorld\CS\AppPackages\HelloWorld_1.0.0.0_ARM_Debug.appx" fga Appx.HelloWorldApp
     (or) newAppxPkg "C:\Users\jadali\Desktop\HelloWorld\CS\AppPackages\HelloWorld_1.0.0.0_ARM_Debug.appx" fga Appx.HelloWorldApp
  ```


## Build the Retail Image Files
Once we have all the custom application packages signed properly, we can now build the Windows IoT Core retail image. Please verify that you have the retail code-signing certificate installed on your PC prior to following these steps:

1. Set the IoT Signature to include details about your certificate and cross-certificate. This is done by modifying the `IoTWorkspace.xml` file, located in your workspace (e.g. C:\MyWorkspace):

    ```XML
    <!--Specify the retail signing certificate details, Format given below -->
    <RetailSignToolParam>/s my /i "Issuer" /n "Subject" /ac "C:\CrossCertRoot.cer" /fd SHA256</RetailSignToolParam>
    ```

2. Run **IoT Core Powershell Environment** as an administrator.
3. Set the environment for retail signing. This is done with [Set-IoTRetailSign](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Set-IoTRetailSign.md):

    ```powershell
    Set-IoTRetailSign On
    (or) retailsign on 
    ```

4. Build the packages:

    ```powershell
    New-IoTCabPackage All
    (or) buildpkg all 
    ```

5. Once all the package .CAB files are built, you should verify that each of these files is properly signed with the retail certificate. If some are still signed with the test certificates (this usually happens if you use your technician PC for building both test and retail images), you can re-sign these files using [Redo-IoTCabSignature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Redo-IoTCabSignature.md):

    ```powershell
    Redo-IoTCabSignature  C:\BSP.IN C:\BSP.OUT
    (or) re-sign.cmd C:\BSP.IN C:\BSP.OUT 
    ```

   This takes the .CAB files from `c:\BSP.IN`, re-signs them with the retail certificate and copies them to the `c:\BSP.OUT` directory.

6. If you re-signed the .CAB files from Step 5, copy the re-signed .CAB files to the `C:\MyWorkspace\Build\<arch>\pkgs`, overwriting the existing files. In our example, these files are copied to `C:\MyWorkspace\Build\arm\pkgs`.
7. Build your retail image by running the following command:

    ```powershell
    New-IoTFFUImage <product name> Retail
    (or)buildimage <product name> Retail 
    ```

8. You can then flash the retail image as described in [Flashing a Windows IoT Core Image](05-FlashingImage.md).

## Commands Used
Listed here are the commands (in order) for creating a retail IoT Core image. Please note that your retail code-signing certificate should be installed first, and it may prompt you for the certificate password when re-signing the .CAB files. 

    ```powershell
    Set-IoTRetailSign On
    New-IoTCabPackage All
    Redo-IoTCabSignature  C:\BSP.IN C:\BSP.OUT
    xcopy C:\BSP.OUT\*.cab C:\MyWorkspace\Build\arm\pkgs\*.cab
    New-IoTFFUImage <product name> Retail
    ```
