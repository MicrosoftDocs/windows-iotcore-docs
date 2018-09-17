--- 
title: Board Support Packages
author: jadali, lmaung
ms.author: jadali, lmaung
ms.date: 09/16/2018 
ms.topic: article 
description: Listing and description of different supported BSPs.
keywords: Windows 10 IoT Core, 
--- 

# Board Support Packages

A Board Support Package (BSP) is a collection of drivers/settings required to run IoT Core on a hardware platform. These are provided by the hardware/silicon vendors. The BSP also included a set of device drivers that are specific to the components/silicon used in the board, mostly in the form of .inf files and their associated .sys/.dll files.

Listed below are the steps required to extract the BSP files for specific manufacturers. You will need these files extracted properly before you can build an FFU image file. Please see [Creating a Basic IoT Core Image](CreateBasicImage.md) after you successfully follow the steps below with the BSP files you are building an image for.


## Qualcomm
### DragonBoard 410c
The BSP files are available at [DragonBoard 410c Software](https://developer.qualcomm.com/hardware/dragonboard-410c/software) under the *Windows IoT Core* section. You will need to export the files from the zip file, using the `export.cmd` file (via the `IoTCoreShell.cmd` shell).

1. Download the **db410c_bsp.zip** file from Qualcomm to the Technician PC

2. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to export the required BSP .CAB files to a local file directory (for example **C:\BSPs\DB410c_BSP**).

        C:\iot-adk-addonkit\Tools\bsptools\QCDB410C\export.cmd C:\BSPs\DB410c_BSP
        
## Raspberry Pi
1. Download the BSP zipfile located [here](https://github.com/ms-iot/iot-adk-addonkit/releases/download/RPiBSP/rpibsp.zip) and extract the zipfile to a local directory on the technician PC (for example, **C:\BSPs\rpibsp**).
2. Launch IoT Core Shell and select the **ARM** architecture. 
3. Run the following command from the directory you extracted the BSP files to (for example, **C:\BSPs\rpibsp**). This will build the .CAB files and place them in the **\Build\arm\pkgs** subdirectory under where you installed the Windows ADK Toolkit.

        C:\BSPs\rpibsp\build.cmd 

## Intel
### Apollo Lake / Braswell / Cherry trail
The BSP supporting Apollo Lake is available at Apollo Lake BSP.

The BSP supporting Braswell/Cherry trail are available at Braswell BSP.

Follow the steps below to use this BSP with the Windows 10 ADK release 1709 (16299) with iot-adk-addonkit version 4.0 or later.

1. Download the BSP package and install
2. Copy files from C:\Program Files (x86)\Intel IoT\Source-<arch> to iot-adk-addonkit\Source-<arch>
3. Launch IoTCoreShell, select arch (x64 / x86) as required
4. In the IoTCoreShell, run the below command to convert the BSP files to latest format and build
    * run .\bsptools\<bspname>\convert.cmd
    * buildbsp <bspname>
5. For serial support (FILL IN BLANK HERE with Win8 Drivers??)

### KabyLake



## OLD INFO (DELETE)
There are two steps to creating your own BSP:

First, find where you can get BSPs for supported platforms below.
Second, learn how to create your own BSP by following the steps listed in the IoT Manufacturing guide.

## Raspberry Pi BSP
Steps to create the drivers :

1. Check out ms-iot/bsp project.
2. Build the bcm2386 solution (Release or Debug)
    * You can also download the prebuilt binaries from rpibsp_wm.zip.
3. Launch IoTCoreShell, select arm
   * In ms-iot/bsp project folder, run tools\binexport.cmd Release (or) Debug C:\RPiBSP to export the binaries to C:\RPiBSP folder. If you are using prebuilt binaries, you can skip this step and unzip the binaries to C:\RPiBSP.
   * Run C:\RPiBSP\build.cmd to create the cabs in the build output folder (iot-adk-addonkit\Build\arm\pkgs)
   * Run buildpkg all to process all cab files

