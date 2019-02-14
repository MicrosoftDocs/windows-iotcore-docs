---
title: IoT Core Quick Start Guide
author: lmaung
ms.author: lmaung

ms.date: 2/14/2019 
ms.topic: article 
description: Windows IoT Core Quick Start Guide
keywords: Windows 10 IoT Core, 
---

# Quick Start Guide and Check List

One of the ultimate goals for creating an IoT image for a device is so that you can have a eventually have a mass produced IoT device. 
The following checklist and guide will assist you in creating your first test image of Window IoT Core in the platform of your choosing:

---
We will split the tasks into multiple sections.

## Tools
### Gather and download neccessary Tools
- [ ] [Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK) 
- [ ] [Windows PE add-on for the ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install#winADK)
- [ ] [Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore) 
- [ ] [IoT Core ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/) (Recommand that you clone this)
- [ ] [Windows 10 IoT Core Dashboard](http://go.microsoft.com/fwlink/p/?LinkId=708576)

### Gather BSP
 You will need to decide on your IoT Core Board of choice. You will only need to aquire BPS for the board or architecture of your choosing. 
 * DragonBoard 410C
- [ ] [DragonBoard 410C](https://developer.qualcomm.com/hardware/dragonboard-410c/software) 
- [ ] [DragonBoard 410C](https://developer.qualcomm.com/hardware/dragonboard-410c/software) 
 * Raspberry Pi (2/3)
- [ ] [RPi_BSP.zip](https://github.com/ms-iot/iot-adk-addonkit/releases/download/17134_v5.3/RPi_BSP.zip)
> [!NOTE]
> Raspberry Pi BSP driver sources are available at [ms-iot/bsp](https://github.com/ms-iot/bsp)
> Pi 3B+ has a different BSP from 2/3
 * Intel Boards (Pick one from list below)
- [ ] [Intel® Atom™ Processor E3800 Product Family and Intel® Celeron® Processor N2807/N2930/J1900](https://downloadcenter.intel.com/download/25618)
- [ ] [Intel Atom® Processor E3900 Series, and Intel® Pentium® and Celeron® Processor N- and J-Series (Apollo Lake)](https://downloadcenter.intel.com/download/25618)
- [ ] [Intel® Pentium® and Celeron® Processor N3000 Product Families, Intel® Atom™ x5-E8000 Processor, and Intel® Atom™ x5-Z8350 Processor](https://www.intel.com/content/www/us/en/embedded/products/braswell/software-and-drivers.html)

### Create Workspace
 After unzipping the IoT Core ADK Add-On Package to a directory of your choosing on your technician computer, run the following command line from console. Powershell window will open up. Depending on the architecutre of your choosing, you will have to use one arm, x86, or x64 as your system architecture.
 
 ``` powershell
    c:\<unzip folder>iot-adk-addonkit\IoTCorePShell.cmd
 ```
 
 - [ ] Once the Powershell window opens, you can type in the following command (if this is your first time)
    
``` powershell
    new-ws C:\MyWorkspace <oemname> <arch>
```

 - [ ] For subsequent visits, use this:
  
``` powershell
    (or) open-ws C:\MyWorkspace
```
### Import BSP
 Import the BPS of your choice and build the package of the BSP
 - [ ] DragonBoard 401C
 
    ``` powershell
    Import-QCBSP "C:\Downloads\db410c_BSP.zip" C:\prebuilt\DB410c_BSP -ImportBSP
    buildpkg QCDB410C
    ```
    
- [ ] Raspberry Pi


    ``` powershell
    Import-IoTBSP RPi2 C:\Downloads\RPi_BSP.zip
    (or) importbsp RPi2 C:\Downloads\RPi_BSP.zip
    buildpkg RPi2
    ```

- [ ] Intel

    ``` powershell
    Import-IoTBSP <bspname> "C:\Program Files (x86)\Intel IoT\Source-<arch>"
    buildpkg <bspname>
    ```

### Build all packages
- [ ] Rebuild packages with the following command
 
    ``` powershell
    New-IoTCabPackage All
    (or) buildpkg all 
    ```
### Create a Product
At this point, create a new product with the command listed below: You will be prompted to enter SMBIOS information.
- [ ] Create new product
 
    ``` powershell
    Add-IoTProduct ProductA QCDB410C
    (or) newproduct MyProductA QCDB410C
    ```
    Sample **SMBIOS**
* **System OEM Name:** Accolade Industries
* **System Family Name:** AccoladeHub
* **System SKU Number:** AIHub-001
* **Baseboard Manufacturer:** Arrows
* **Baseboard Product:** Dragonboard 410C

### Create a test Image
Build your first test FFU image with the following command:
- [ ] Create Test FFU
 
    ``` powershell
    New-IoTFFUImage <product name> Test
    (or)buildimage <product name> Test 
    ```
 
 ### Flash the FFU
 
