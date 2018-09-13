--- 
title: Create your first IoT Core Image
author: jadali, lmaung
ms.author: jadali, lmaung
ms.date: 09/05/2018 
ms.topic: article 
description: 
keywords: Windows 10 IoT Core, 
--- 

# Create a basic image
## Image Types
You can create **test images**, which include tools for quickly accessing and modifying devices. Test images are great for: 
* Developers, hardware vendors, and manufacturers (OEMs) who are trying out new device designs. 
* Hobbyists and organizations that are creating devices designed to run in non-networked or controlled network environments. 

You can create **retail images**, which can be made more secure for public or corporate networks while still receiving updates. 
You can add customizations, including apps, settings, hardware configurations, and board support packages (BSPs). 
For OEM-style images, you’ll wrap your customizations into package (.cab) files. Packages let OEMs, ODMs, developers, and Microsoft work together to help deliver security and feature updates to your devices without stomping on each other's work.

## Creation process terms and their roles
There are a few terms that we should familiarize ourselves with before we create our first image since we will be referring to these names and terms through out the process. 
### Packages 
Packages are the logical building blocks of IoT Core. They contain all the files, libraries, registry settings, executables, and data on the device. From device drivers to system files, every component must be contained in a package. This modular architecture allows for precise control of updates: a package is the smallest serviceable unit on the device. 
Each package contains: 
* The contents of the package, such as a signed driver binary or a signed appx binary. 
* A package definition (.pkg.xml) file specifies the contents of the package and where they should be placed in the final image. See %SRC_DIR%\Packages\ directory for various samples of package files. 
* A signature. This can be a test or retail certificate. 

The **pkggen** tool combines these items into signed packages. Our samples include scripts: **createpkg**, and **createprovpkg**, which call *pkggen* to create packages for our drivers, apps, and settings. 
The process is similar to that used by Windows 10 Mobile. To learn more about creating packages, see Creating mobile packages.

## Feature manifests (FMs) 
After you've put everything into packages, you'll use FM files to list which of your packages belong in the final image. 

You can use as many FMs into an image as you want. In this guide, we refer to the following FMs: 
* **OEMFM.xm**l includes features an OEM might add to a device, such as the app and a provisioning package. 
* **BSPFM.xml** includes features that a hardware manufacturer might use to define a board. For example, *OEM_RPi2FM.xml* includes all of the features used for the *Raspberry Pi 2*. 

The process is similar to that used by Windows 10 Mobile. To learn more, see Feature manifest file contents. 
You'll list which of the features to add by using these tags: 
* \<BasePackages\>: Packages that you always included in your images, for example, your base app. 
* <Features>\<OEM>: Other individual packages that might be specific to a particular product design. 

The Feature Merger tool generates the required feature identifier packages that are required for servicing the device. Run this tool whenever any changes are made to the FM files. After you change OEM FM or OEM COMMON FM files, run Buildfm oem. After you change bspfm files, run buildfm bsp **< bspname >**.

## Creating the image: ImgGen and image configuration file (OEMInput.xml) 
To create the final image, you'll use the imggen tool with an image configuration file, OEMInput.xml file. 

These are the same tools used to create Windows 10 Mobile images. To learn more, see OEMInput file contents. 

The image configuration file lists: 
* The feature manifests (FMs) and the packages that you want to install from each one. 
* An SoC chip identifier, which is used to help set up the device partitions. The supported values for socare defined in the corresponding bspfm.xml, under <devicelayoutpackages>. 
* A Device identifier, which is used to select the device layout. The supported values for device are defined in the corresponding bspfm.xml, under <oemdeviceplatformpackages>. 
* The ReleaseType (either Production or Test). 

    Retail builds: We recommend creating retail images early on in your development process to verify that everything will work when you are ready to ship. 

    * These builds contain all of the security features enabled. 
    * To use this build type, all of your code must be signed using retail (not test) code signing certificates. 
    *  For a sample, see %SRC_DIR%\Products\SampleA\RetailOEMInput.xml.

    Test builds: Use these to try out new versions of your apps and drivers created by you and your hardware manufacturer partners. 
        
    * These builds have some security features disabled, which allows you to use either test-signed or production-signed packages.
    * These builds also include developer tools such as debug transport, SSH, and PowerShell, that you can use to help troubleshoot issues. 
    * For a sample, see %SRC_DIR%\Products\SampleA\TestOEMInput.xml. 

> |             | Retail Builds  |  Test Builds  |
> |-------------|----------|---------|
> | Image Release Type | ReleaseType: <b>Production</b> | ReleaseType: <b>Test</b>
> | Package Release Type | Only Production Type packages are supported | Both Production Type or Test Type are supported
> | Test-signed packages | Not supported | Supported<p>IOT_ENABLE_TESTSIGNING feature must be included
> | Code integrity check | Supported. By default, this is enabled. | Supported. By default, no policy is enforced.

## Board Support Packages 
Board Support Packages contain a set of software, drivers, and boot configurations for a particular board, typically supplied by a board manufacturer. The board manufacturer may periodically provide updates for the board, which your devices can receive and apply 

# Creation of a test image 
To get started, we'll create a basic Windows 10 IoT Core (IoT Core) image, flash it to a device (or micro SD card), and put it into a device to make sure that everything's working properly. 

We'll create a product folder that represents our first design. For our first product design, we'll customize just enough for the IoT core device to boot up and run the built-in OOBE app, which we should be able to see on an HDMI-compatible monitor. 

To make running these commands easier, we will use the IoT Core shell, which presets several frequently-used paths and variables.

## Set your OEM Name (one-time only)
Open the file **C:\IoT-ADK-AddonKit\Tools\setOEM.cmd** in Notepad, and modify it with your company name. We've added this variable to help you create packages with names that are easy to differentiate from those provided from other manufacturers you're working with. Only alphanumeric characters are supported in the OEM_NAME as this is used as a prefix for various generated file names.

    set OEM_NAME=Fabrikam

## Choosing architecture, test certificates 
1. In Windows Explorer, go to the folder where you installed the IoT Core ADK Add-Ons, for example, **C:\IoT-ADK-AddonKit**, and open **IoTCoreShell.cmd**. It should prompt you to run as an administrator. 

    The new value for OEM_NAME should appear when you start the tool. 

    Troubleshooting: Error: "The system cannot find the path specified". If you get this, right-click the icon and modify the path in "Target" to the location you've chosen to install the tools. 
2. At the **Set Environment for Architecture** prompt, select 1 for ARM, 2 for x86, or 3 for x64, based on the architecture for the boards that you'll be developing. For example, press **1** to create an image that's compatible with the Raspberry Pi 2 or Raspberry Pi 3, or press **2** to create an image that's compatible with the Minnowboard Max. 

    The launch tool sets the default architecture, and sets a version number for the design, which you can use for future updates. The first version number defaults to 10.0.0.0. 
    
    (Why a four-part version number? Learn about versioning schemes in Update requirements) 

## Install certificates 
From the IoT Core Shell, install the test certificates, which you'll use to sign your test binaries. You'll only need to do this the first time you install the IoT ADK Add-on Kit. 

    installoemcerts 

## Building BSPs 
See BoardSupportPackage.md page

## Build Packages 
From the IoT Core Shell, get your environment ready to create products by building all of the packages in the working folders. 
    
    buildpkg All 

## Create a test project 
From the IoT Core Shell, create a new product folder that uses the Rpi2 BSP. This folder represents a new device we want to build, and contains sample customization files that we can use to start our project. 

    newproduct ProductA rpi2 

The BSP name is the same as the folder name for the BSP. You can see which BSPs are available by looking in the **C:\IoT-ADK-AddonKit\Source-\< arch >\BSP** folders. 

This creates the folder: **C:\IoT-ADK-AddonKit\Source-< arch >\Products\\ProductA**. 

## Build an image 
Eject any removable storage drives, including the Micro SD card and any USB flash drives. 

From the IoT Core Shell, build a flashable test image using the default files. Test images include additional tools, and you can create test images using either signed or unsigned test packages. 

    buildimage ProductA test 

This builds an FFU file with your basic image at **C:\IoT-ADK-AddonKit\Build\< arch >\ProductA\Test**.

## Commands Used
      set OEM_NAME=Fabrikam
      installoemcerts 
      buildpkg all
      newproduct NameOfImage ProductType(BSP Type)
      buildimage NameOfImage Test(for Test)
  
