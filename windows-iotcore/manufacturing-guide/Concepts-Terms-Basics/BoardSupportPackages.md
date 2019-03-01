---
title: Board Support Packages
author: johnadali
ms.author: johnadali
ms.date: 09/16/2018 
ms.topic: article 
description: Listing and description of different supported BSPs.
keywords: Windows 10 IoT Core, 
---

# Board Support Packages

A Board Support Package (BSP) is a collection of drivers/settings required to run IoT Core on a hardware platform. These are provided by the hardware/silicon vendors. The BSP also included a set of device drivers that are specific to the components/silicon used in the board, mostly in the form of .inf files and their associated .sys/.dll files.

Listed below are the steps required to extract the BSP files for specific manufacturers. You will need these files extracted properly before you can build an FFU image file. Please see [04-Creating a Basic IoT Core Image](04-CreateBasicImage.md) after you successfully follow the steps below with the BSP files you are building an image for.


## Qualcomm
### DragonBoard 410c
DragonBoard drivers are available at [DragonBoard 410C Software](https://developer.qualcomm.com/hardware/dragonboard-410c/software) under `Windows 10 IoT Core` section as `Windows 10 IoT Core Board Support Package`.

Steps to import the drivers :

1. Download the `Windows 10 IoT Core Board Support Package` to a folder say, `C:\Downloads\db410c_BSP.zip`<p>You may need to sign up for an account in order to get access. Launch IoTCorePShell, and create/open your workspace

    ``` powershell
    new-ws C:\MyWorkspace <oemname> arm
    (or) open-ws C:\MyWorkspace
    ```

3. Import the bsp using [Import-QCBSP](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Import-QCBSP.md) and build using

    ``` powershell
    Import-QCBSP "C:\Downloads\db410c_BSP.zip" C:\prebuilt\DB410c_BSP -ImportBSP
    buildpkg QCDB410C
    ```

    Set `<BSPPkgDir>` setting in the `C:\MyWorkspace\IoTWorkspace.xml` to `C:\prebuilt\DB410c_BSP`
        
## Raspberry Pi BSP

1. Download [RPi_BSP.zip](https://github.com/ms-iot/iot-adk-addonkit/releases/download/17134_v5.3/RPi_BSP.zip) to a local directory, say `C:\Downloads\RPi_BSP.zip`
2. Launch [IoTCorePShell](https://github.com/ms-iot/iot-adk-addonkit) and create or open a workspace using

    ``` powershell
    new-ws C:\MyWorkspace <oemname> arm
    (or) open-ws C:\MyWorkspace
    ```

3. Import the bsp using [Import-IoTBSP](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Import-IoTBSP.md) and build using

    ``` powershell
    Import-IoTBSP RPi2 C:\Downloads\RPi_BSP.zip
    (or) importbsp RPi2 C:\Downloads\RPi_BSP.zip
    buildpkg RPi2
    ```

> [!NOTE]
> Raspberry Pi BSP driver sources are available at [ms-iot/bsp](https://github.com/ms-iot/bsp)


## Intel BSPs

### BSP Links

| Chipset          | Download Link          |
|--------------- |--------------------- |
| Intel® Atom™ Processor E3800 Product Family and Intel® Celeron® Processor N2807/N2930/J1900  | [Download](https://downloadcenter.intel.com/download/25618) Intel® Embedded Drivers for Microsoft Windows® 10 IoT Core (32-bit and 64-bit) MR1 |
|Intel Atom® Processor E3900 Series, and Intel® Pentium® and Celeron® Processor N- and J-Series (Apollo Lake)| [Download](https://downloadcenter.intel.com/download/25618) Software Package: Intel Atom® E3900 SoC Family—Board Support Package (BSP) for Windows* 10 IoT Core 32-bit and 64-bit Platforms |
|Intel® Pentium® and Celeron® Processor N3000 Product Families, Intel® Atom™ x5-E8000 Processor, and Intel® Atom™ x5-Z8350 Processor| [Download](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html) Board Support Package for Intel Atom® Processor Windows* 10 IoT Core 32-bit and 64-bit Platforms |

### Instructions to use

Follow the steps below to use this BSP with the Windows 10 ADK release 1809 (17763) with iot-adk-addonkit version 6.0.

1. Download the BSP package and install
2. Launch IoTCorePShell, and create/open your workspace

    ``` powershell
    new-ws C:\MyWorkspace <oemname> arm
    (or) open-ws C:\MyWorkspace
    ```

3. Set the source location, either the installed directory or the zip file path 

    ``` powershell
    $Source = "C:\Program Files (x86)\Intel IoT\Source-<arch>"
    (or) 
    $Source = "C:\Downloads\IntelBSP.zip"
    ```

4. Import the bsp using [Import-IoTBSP](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Import-IoTBSP.md) and build using

    ``` powershell
    Import-IoTBSP <bspname> $Source
    (or) importbsp <bspname> $Source
    buildpkg <bspname>
    ```
5. if the above commands does not work, you can skip the step 3, and combine the step 3 and 4 into a single step as follows:

    ``` powershell
    Import-IoTBSP <bspname> "C:\Program Files (x86)\Intel IoT\Source-<arch>"
    (or) importbsp <bspname> "C:\Program Files (x86)\Intel IoT\Source-<arch>"
    buildpkg <bspname>
    ```
