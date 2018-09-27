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

Listed below are the steps required to extract the BSP files for specific manufacturers. You will need these files extracted properly before you can build an FFU image file. Please see [04-Creating a Basic IoT Core Image](04-CreateBasicImage.md) after you successfully follow the steps below with the BSP files you are building an image for.



## Qualcomm
### DragonBoard 410c
The BSP files are available at [DragonBoard 410c Software](https://developer.qualcomm.com/hardware/dragonboard-410c/software) under the *Windows IoT Core* section. You will need to export the files from the zip file, using the `export.cmd` file (via the `IoTCoreShell.cmd` shell).

1. Download the **db410c_bsp.zip** file from Qualcomm to the Technician PC

2. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to export the required BSP .CAB files to a local file directory (for example **C:\BSPs\DB410c_BSP**).

        C:\iot-adk-addonkit\Tools\bsptools\QCDB410C\export.cmd C:\BSPs\DB410c_BSP
        
## Raspberry Pi
Drivers for the Raspberry Pi are located at [ms-iot/bsp](https://github.com/ms-iot/bsp). Note that these files can be used for Raspberry Pi 2 or 3.

1. Clone or download the [ms-iot/bsp](https://github.com/ms-iot/bsp) project.
2. Build the **bcm2386** solution (release or debug).
3. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to export the required BSP .CAB files to a local file directory (for example **C:\BSPs\RPiBSP**). Note that `binexport.cmd` is located in the tools project folder of where you cloned/downloaded the [ms-iot/bsp](https://github.com/ms-iot/bsp) project.

        binexport.cmd Release C:\BSPs\RPiBSP
        or
        binexport.cmd Debug C:\BSPs\RPiBSP


4. Run the following command from the directory you extracted the BSP files to (for example, **C:\BSPs\rpibsp**). This will build the .CAB files and place them in the **\Build\arm\pkgs** subdirectory under where you installed the Windows ADK Toolkit.

        C:\BSPs\RPiBSP\build.cmd 

## Intel
### Apollo Lake / Braswell / Cherry Trail
The BSP supporting Apollo Lake is available at [Apollo Lake BSP](https://www.intel.com/content/www/us/en/embedded/products/apollo-lake/technical-library.html).

The BSP supporting Braswell/Cherry Trail are available at [Braswell BSP](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html).

Follow the steps below to extract and build the BSP files for the Intel hardware device you are working with.

1. Download the BSP package and install. By default, these files will be installed to **C:\Program Files (x86)\Intel IoT\Source-< arch >**
2. Copy files from **C:\Program Files (x86)\Intel IoT\Source-< arch >** to **C:\iot-adk-addonkit\Source-< arch >**
3. Launch **IoT Core Shell** and select architecture you are working with (x64 or x86)
4. Run the following commands to build the .CAB files and place them in the **\Build\\< arch >\pkgs** subdirectory under where you installed the Windows ADK Toolkit.
        
        run .\bsptools\<bspname>\convert.cmd
        buildbsp <bspname>

