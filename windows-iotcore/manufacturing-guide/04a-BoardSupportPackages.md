--- 
title: Board Support Packages
author: John Adali, Lwin Maung, Concurrency
ms.author: John Adali, Lwin Maung, Concurrency
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

2. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to import the required BSP .CAB files into your workspace (for example, C:\MyWorkspace\BSPDIR).

        ```powershell
        importbsp "C:\Temp\db410c_bsp.zip"
        ```
        
## Raspberry Pi
Drivers for the Raspberry Pi are located at [ms-iot/bsp](https://github.com/ms-iot/bsp). Note that these files can be used for Raspberry Pi 2 or 3.

1. Download the **RPi_bsp.zip** file to the Technician PC

2. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to import the required BSP .CAB files into your workspace (for example, C:\MyWorkspace\BSPDIR).

        ```powershell
        importbsp "C:\Temp\RPi_bsp.zip"
        ```

## Intel
### Apollo Lake / Braswell / Cherry Trail
The BSP supporting Apollo Lake is available at [Apollo Lake BSP](https://www.intel.com/content/www/us/en/embedded/products/apollo-lake/technical-library.html).

The BSP supporting Braswell/Cherry Trail are available at [Braswell BSP](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html).

1. Download the **atom-e3900-board-support-package-iot-platforms.zip** file to the Technician PC

2. Launch the `IoTCoreShell.cmd` shell and select the *ARM* architecture. Run the following command to import the required BSP .CAB files into your workspace (for example, C:\MyWorkspace\BSPDIR).

        ```powershell
        importbsp "C:\Temp\atom-e3900-board-support-package-iot-platforms.zip"
        ```
