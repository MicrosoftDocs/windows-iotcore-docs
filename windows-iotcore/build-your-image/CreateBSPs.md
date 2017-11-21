---
title: Creating Board Supported Packages (BSP)
author: parameshbabu
ms.author: pabab
ms.date: 08/22/2017
ms.topic: article
description: Learn how to create board supported packages in order to start assembling and manufacturing your device.
keywords: windows iot, image creation, bsp, windows iot, board supported package 
---

# Create Board Supported Packages (BSP)
Board Support Packages (BSP) is a collection of drivers/settings required to run IoT Core on a hardware platform. These are provided by the hardware vendors/silicon vendors.

There are two steps to creating your own BSP:

* First, find where you can get BSPs for supported platforms **below**.
* Second, learn how to create your own BSP by following the steps listed in the [IoT Manufacturing guide](https://docs.microsoft.com/windows-hardware/manufacture/iot/create-a-new-bsp).

> [!NOTE]
> You can copy the bsp cab files to a folder, say `C:\MyBSPs\`, and `set BSPPKG_DIR=C:\MyBSPs\` in the IoTCoreShell to use these files in the imaging process.

## Raspberry Pi BSP
Raspberry drivers are available at [ms-iot/bsp](https://github.com/ms-iot/bsp).

Steps to create the drivers :

1. Check out [ms-iot/bsp](https://github.com/ms-iot/bsp) project.
2. Build the bcm2386 solution (Release or Debug)
    * You can also download the prebuilt binaries from [rpibsp.zip](https://github.com/ms-iot/iot-adk-addonkit/releases/download/RPiBSP/rpibsp.zip). 
3. Launch [IoTCoreShell](https://github.com/ms-iot/iot-adk-addonkit), select arm

    * In ms-iot/bsp project folder, run `tools\binexport.cmd Release (or) Debug C:\RPiBSP` to export the binaries to `C:\RPiBSP` folder. If you are using prebuilt binaries, you can skip this step and unzip the binaries to `C:\RPiBSP`.
    * Run `C:\RPiBSP\build.cmd` to create the cabs in the build output folder (`iot-adk-addonkit\Build\arm\pkgs`)
    * Run `buildpkg all` to process all cab files

> [!NOTE]
> To build a retail image, you will need to rerun the build.cmd to sign the bsp driver binaries with cross certificates. See IoT Core Manufacturing Guide for detailed instructions.

## Intel BSPs

### Bay Trail

[Bay Trail](https://www.intel.com/content/www/us/en/embedded/products/bay-trail/overview.html) drivers are available at [IO Drivers](https://downloadcenter.intel.com/download/25618), [Graphics drivers](https://downloadcenter.intel.com/download/25606)

Steps to create the drivers :

1. Download the drivers
2. Copy the cab files to the build output folder (`iot-adk-addonkit\Build\x86\pkgs`)
3. Launch IoTCoreShell, select x86

    * Run `buildpkg all` to process all cab files

You can also recreate the cab files with the below script, the cab files will be created in the build output folder
(set the DIR_ROOT value appropriately).

1. Launch IoTCoreShell, select x86
2. Create .cmd file copy below snippet and run from above launch shell window.

    ```
    @echo off

    setlocal
    set DIR_ROOT=D:\IntelBSP\BYT\333669_002_bsp_windows_10_iot_core-32_bit
    set OEM_NAME=Intel
    set SIGNFILES=None
    call inf2cab.cmd %DIR_ROOT%\Drivers\x86\GPIO\iaiogpio.inf BYT.GPIO
    call inf2cab.cmd %DIR_ROOT%\Drivers\x86\HSUART\iaiouart.inf BYT.UART
    call inf2cab.cmd %DIR_ROOT%\Drivers\x86\I2C\iaioi2c.inf BYT.I2C
    call inf2cab.cmd %DIR_ROOT%\Drivers\x86\SPI\iaiospi.inf BYT.SPI

    set DIR_ROOT=D:\IntelBSP\BYT\INTEL_HDGraphics_Win10IoTCore_v36.19.0_1227_PV
    call inf2cab.cmd %DIR_ROOT%\emgd_gfx_36_19_0_1227\igdlh.inf GFX.Build1227
    endlocal
    ```

### Apollo Lake / Braswell / Cherry trail

The BSP supporting Apollo Lake is available at [Apollo Lake BSP](https://www.intel.com/content/www/us/en/embedded/products/apollo-lake/technical-library.html).

The BSP supporting Braswell/Cherry trail are available at [Braswell BSP](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html).

> [!TIP]
> The published BSP works with Windows 10 ADK release 1703 (15063).

Follow the steps below to use this BSP with the Windows 10 ADK release 1709 (16299) with iot-adk-addonkit version 4.0 or later.

1. Download the BSP package and install 
2. Copy files from `C:\Program Files (x86)\Intel IoT\Source-<arch>` to `iot-adk-addonkit\Source-<arch>` 
3. Launch IoTCoreShell, select arch (x64 / x86) as required 
4. In the IoTCoreShell, run the below command to convert the BSP files to latest format and build
    * run `.\bsptools\<bspname>\convert.cmd`
    * `buildbsp <bspname>`

### Joule

Joule drivers are available at [Joule BSP](https://downloadcenter.intel.com/download/26797/Windows-10-IoT-Core-Files-for-Intel-Joule-Compute-Module).

Steps to create the drivers :

1. Download the Intel5xx_WinIoT_*_BSP.zip 
2. Copy the Intel5xx folder from the zip file to (`iot-adk-addonkit\Source-x64\BSP\`)
3. Launch IoTCoreShell, select x64

    * Run `buildpkg all` to create all cab files, including the Joule BSP cab files. 
    * Alternatively you can use `buildbsp Intel5xx` to build Joule BSP cabs only. 

The files will be available in the build output folder (`iot-adk-addonkit\Build\x64\pkgs`) 


## Qualcomm BSPs

### DragonBoard 410C

DragonBoard drivers are available at [DragonBoard 410C Software](https://developer.qualcomm.com/hardware/dragonboard-410c/software) under *Windows 10 IoT Core* section.

Steps to create the drivers :

1. Download the *_db410c_BSP.zip and extract to a folder say `C:\download\DB410c_BSP`
2. Launch IoTCoreShell, select arm

    * Run `.\bsptools\QCDB410C\export.cmd C:\download\DB410c_BSP C:\MyBSPs\QCDB410C` to export the required bsp cab files to a directory say `C:\MyBSPs\QCDB410C`.
    * `set BSPPKG_DIR=C:\MyBSPs\QCDB410C` to specify the location of the bsp cabs. See the BSPFM.xml file for the cab files it looks for in `BSPPKG_DIR`.
    * Run `buildpkg all` to create the oem packages
    * Run `buildimage <productname> <test> or <retail>` to build the image 

## Other helpful resources

* [Windows ADK IoT Core Add-Ons Overview](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-adk-addons)
* [IoT Core Add-Ons command-line options](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/iot/iot-core-adk-addons-command-line-options)
* [IoT Core feature list](https://docs.microsoft.com/windows-hardware/manufacture/iot/iot-core-feature-list)
* [Channel9 Video on Manufacturing Guide](https://channel9.msdn.com/events/Build/2017/B8085)
