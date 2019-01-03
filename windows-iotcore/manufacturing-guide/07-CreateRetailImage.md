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


> [!IMPORTANT]
> If you have more than one custom application that you are including in your retail image, signing them individually with your retail certificate will cause verification collisions when you boot up your image on your device. This will prevent your apps from running properly. Follow the steps in the **Properly Signing and Including Your Applications** section to create a separate Feature .CAB file that contains your retail certificate, to include in your retail image.

3. Minimize the included Windows IoT Core features. You also want to remove any test applications that are included (by default) with test images for Windows IoT Core. This includes the IoT Core default application (aka. Bertha), along with any other developer tools or testing features. You can do this by using [Remove-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Remove-IoTProductFeature.md):

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


> [!NOTE]
> Please use the `-SkipCert` parameter if you have more than one application that is signed with the same certificate. This will ensure that the certificate is not added more than once to the image (which can cause verification problems when booting up the device).


## Creating a Package for Including your Retail Certificate
If you have more than one application that you signed with the same certificate, you need to create a dedicated .CAB file that contains only your retail certificate file. Including this in your retail image *once* (instead of in each application CAB file) ensures that Windows IoT Core properly installs your retail certificate on your device.

> [!NOTE]
> You can skip this section if you only have one application to include in your retail image.

1. Create a new folder called **Appx.Certificates** under the **C:\iot-adk-addonkit\Source-< arch>\Packages\\** directory. In our example, we created this folder under **C:\iot-adk-addonkit\Source-arm\Packages\\**.
2. Create a **customizations.xml** file and edit it to look like below, replacing **HelloWorld.cer** with the name of your retail certificate:

   ```XML
   <?xml version="1.0" encoding="utf-8" ?>
      <WindowsCustomizations>
        <PackageConfig xmlns="urn:schemas-Microsoft-com:Windows-ICD-Package-Config.v1.0">
          <ID>{c3b3273a-1aef-4367-a8d9-228fe15cce84}</ID>
          <Name>Certificates</Name>
          <Version>1.1.0.0</Version>
          <OwnerType>OEM</OwnerType>
          <Rank>0</Rank>
        </PackageConfig>
        <Settings xmlns="urn:schemas-microsoft-com:windows-provisioning">
          <Customizations>
            <Common>
              <Certificates>
                <RootCertificates>
                  <RootCertificate CertificateName="HelloWorld" Name="HelloWorld">
                    <CertificatePath>HelloWorld.cer</CertificatePath>
                  </RootCertificate>
                </RootCertificates>
              </Certificates>
            </Common>
          </Customizations>
        </Settings>
      </WindowsCustomizations>
   ```

3. Copy your retail certificate .CER file to this directory.
4. Create a **Appx.Certificates.wm.xml** file and edit it to look like this:

   ```XML
   <?xml version="1.0" encoding="utf-8"?>
   <identity xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    name="Certificates"
    namespace="Appx"
    owner="$(OEMNAME)"
    legacyName="$(OEMNAME).Appx.Certificates" xmlns="urn:Microsoft.CompPlat/ManifestSchema.v1.00">
       <onecorePackageInfo
        targetPartition="MainOS"
        releaseType="Production"
        ownerType="OEM" />
       <files>
           <file
            destinationDir="$(runtime.windows)\Provisioning\Packages"
            source="$(BLDDIR)\ppkgs\Appx.Certificates.ppkg"
            name="Appx.Certificates.ppkg" />
       </files>
   </identity>
   ```

. From **IoT Core Powershell Environment**, you can now build the package into a .CAB file (using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md))

        ```powershell
        New-IoTCabPackage Appx.Certificates
        (or) buildpkg Appx.Certificates
        ```

    This will build the package into a .CAB file under the `Workspace\Build\<arch>\pkgs` subdirectory in the ADK Toolkit files. 

6. Add the Feature ID using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md):

  ```powershell
  Add-IoTProductFeature <product name> Retail APPX_CERTIFICATES -OEM
  or addfid <product name> Retail APPX_CERTIFICATES -OEM
  ```

  This adds a FeatureID called **APPX_CERTIFICATES** to the specified product's Retail OEMInput XML file (`C:\MyWorkspace\Source-arm\<product name>\RetailOEMInput.xml` file).


## Build the Retail Image Files
Once we have all the custom application packages signed properly, we can now build the Windows IoT Core retail image. Please verify that you have the retail code-signing certificate installed on your PC prior to following these steps:

1. Set the IoT Signature to include details about your certificate and cross-certificate. This is done using [Set-IoTSignature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Set-IoTSignature.md):

    ```powershell
    Set-IoTSignature /ac `"C:\Certs\DigiCert High Assurance EV Root CA.crt"` /s my /i `"DigiCert EV Code Signing CA (SHA2)"` /n `"MySubjectText"` /fd SHA256
    ```

   Please note the .CRT file is the cross-root certificate file.


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

6. If you re-signed the .CAB files from Step 5, copy the re-signed .CAB files to the `C:\IoT-ADK-AddOnToolkit\Build\<arch>\pkgs`, overwriting the existing files. In our example, these files are copied to `C:\IoT-ADK-AddOnToolkit\Build\arm\pkgs`.
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
    xcopy C:\BSP.OUT\*.cab C:\IoT-ADK-AddOnToolkit\Build\arm\pkgs\*.cab
    New-IoTFFUImage <product name> Retail
    ```
