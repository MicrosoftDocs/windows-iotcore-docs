---
author: parameshbabu
description: 'Learn how to use board supported packages in order to start assembling and manufacturing your device.'
title: 'BSP for Hardware'
ms.author: pabab
ms.date: 10/15/2018
ms.topic: article
ms.custom: RS5
---

# IoT Core Board Supported Packages (BSP)

Board Support Packages (BSP) is a collection of drivers/settings required to run IoT Core on a hardware platform. These are provided by the hardware vendors/silicon vendors. The BSP also includes a set of device drivers that are specific to the components/silicon used in the board, mostly in the form of .inf files and their associated .sys/.dll files.

Listed below are the steps required to extract the BSP files for specific manufacturers. You will need these files extracted properly before you ca nbuild a FFU image file. Then, you'll learn how to create your own BSP by following the steps listed in [Lab 2](./create-a-new-bsp.md).

## Raspberry Pi BSP

1. Create RPi_BSP.zip following the build instructions at [rpi-iotcore github](https://github.com/ms-iot/rpi-iotcore#build-the-drivers).
    * For quick prototyping, you can download this [prebuilt RPi_BSP.zip](https://github.com/ms-iot/iot-adk-addonkit/releases/download/17134_v5.3/RPi_BSP.zip) to a local directory such as `C:\Downloads\RPi_BSP.zip`
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
> You are required to rebuild the kernel.img with proper SMBIOS values to meet [Device Update Center](/windows-hardware/service/iot/using-device-update-center#step-2-create-a-new-product) requirements. See [UEFI Customisations](https://github.com/ms-iot/rpi-iotcore#uefi-customisations) for more details.

## Intel BSPs

### BSP Links

| Chipset          | Download Link          |
|--------------- |--------------------- |
| Intel® Atom™ Processor E3800 Product Family and Intel® Celeron® Processor N2807/N2930/J1900  | [Download](https://downloadcenter.intel.com/download/25618) Intel® Embedded Drivers for Microsoft Windows® 10 IoT Core (32-bit and 64-bit) MR1 |
|Intel Atom® Processor E3900 Series, and Intel® Pentium® and Celeron® Processor N- and J-Series (Apollo Lake)| [Download](https://www.intel.com/content/dam/www/public/us/en/zip/atom-e3900-board-support-package-iot-platforms.zip?asset=14806) Software Package: Intel Atom® E3900 SoC Family—Board Support Package (BSP) for Windows* 10 IoT Core 32-bit and 64-bit Platforms |
|Intel® Pentium® and Celeron® Processor N3000 Product Families, and Intel® Atom™ x5-E8000 Processor | [Download](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html) Board Support Package for Intel Atom® Processor Windows* 10 IoT Core 32-bit and 64-bit Platforms |
|Intel® Atom™ x5-E8000 Processor and Intel® Atom™ x5-Z8350 Processor| Contact your Intel representative |

### Instructions to use

Follow the steps below to use this BSP with the Windows 10 ADK release 1809 (17763) with iot-adk-addonkit version 6.0.

1. Download the BSP package and install
2. Launch IoTCorePShell and create/open your workspace

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

## Qualcomm BSPs

### DragonBoard 410C

DragonBoard drivers are available at [DragonBoard 410C Software](https://developer.qualcomm.com/hardware/dragonboard-410c/software) under the *Windows 10 IoT Core* section.

Steps to import the drivers :

1. Download the `Windows 10 IoT Core Board Support Package` to a folder such as `C:\Downloads\*_db410c_BSP.zip`.
2. Launch IoTCorePShell, and create/open your workspace

    ``` powershell
    new-ws C:\MyWorkspace <oemname> arm
    (or) open-ws C:\MyWorkspace
    ```

3. Import the bsp using [Import-QCBSP](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Import-QCBSP.md) and build using

    ``` powershell
    Import-QCBSP "C:\Downloads\*_db410c_BSP.zip" C:\prebuilt\DB410c_BSP -ImportBSP
    buildpkg QCDB410C
    ```

    Set `<BSPPkgDir>` setting in the IoTWorkspace.xml to `C:\prebuilt\DB410c_BSP`

## NXP BSPs

See [Window 10 IoT Core and NXP i.MX SoCs](/windows/iot-core/learn-about-hardware/iotnxp) for information on the NXP BSP access and Ecosystem resources.

## Other helpful resources

* [Windows ADK IoT Core Add-Ons Overview](./iot-core-adk-addons.md)
* [IoT Core Add-Ons Powershell Commands](./iot-core-adk-addons-command-line-options.md)
* [IoT Core feature list](./iot-core-feature-list.md)
* [Channel9 Video on Manufacturing Guide](https://channel9.msdn.com/events/Build/2017/B8085)