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
- [ ] [DragonBoard 410C Windows 10 IoT Core Board Support Package](https://developer.qualcomm.com/hardware/dragonboard-410c/software) 
- [ ] [DragonBoard 410C Windows 10 IoT Core Update Tool (32/64 bit)](https://developer.qualcomm.com/hardware/dragonboard-410c/software) 
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
 - [ ] [Dragon Board Instructions](https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/fabricam/windows-iotcore/manufacturing-guide/05-FlashingImage.md#DragonBoard)
 
 - [ ] [Flashing Raspberry Pi using Windows IoT Core Dashboard](https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/fabricam/windows-iotcore/manufacturing-guide/05-FlashingImage.md#RaspberryPi)
 
 - [ ] [Creating Windows PE Bootable drive to flash Intel based IoT Devices](https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/fabricam/windows-iotcore/manufacturing-guide/05-FlashingImage.md#Intel)


-----
 ### Example Powershell Screen Output
 
 This example shows a **BSWx64** image built from scratch with all steps shown. The workspace is located at **c:\IoT\WorkSpaces**. 
 
 ``` powershell

Loading IoTCoreImaging module..
arm IoT Core kit found.
x86 IoT Core kit found.
x64 IoT Core kit found.
arm64 IoT Core kit found.
Test certs installed
Opening workspace : C:\IoT\iot-adk-addonkit\Workspace\IoTWorkspace.xml
Corekit found OK
ADK_VERSION : 10.0.17763.1
IOTCORE_VER : 10.0.17763.107
BSP_VERSION : 10.0.0.0
ADDONKITVER : 6.0.190116.1218
HostOS Info : Microsoft Windows 10 Enterprise - 10.0.17763 - en-US
IOTWKSPACE  : C:\IoT\iot-adk-addonkit\Workspace
OEM_NAME    : Contoso
BSP_ARCH    : arm
BSPPKG_DIR  : C:\IoT\iot-adk-addonkit\Workspace\Build\arm\pkgs
MSPKG_DIR   : C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail\arm\fre
IoTCorePShell arm 10.0.0.0 Test
PS C:\IoT\iot-adk-addonkit\Workspace>new-ws C:\IoT\WorkSpaces\BSWDemo TestDevice x64
New IoTWorkSpace available at C:\IoT\WorkSpaces\BSWDemo for x64
Opening workspace : C:\IoT\WorkSpaces\BSWDemo\IoTWorkspace.xml
Corekit found OK
ADK_VERSION : 10.0.17763.1
IOTCORE_VER : 10.0.17763.107
BSP_VERSION : 10.0.0.0
ADDONKITVER : 6.0.190116.1218
HostOS Info : Microsoft Windows 10 Enterprise - 10.0.17763 - en-US
IOTWKSPACE  : C:\IoT\WorkSpaces\BSWDemo
OEM_NAME    : TestDevice
BSP_ARCH    : amd64
BSPPKG_DIR  : C:\IoT\WorkSpaces\BSWDemo\Build\amd64\pkgs
MSPKG_DIR   : C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail\amd64\fre
Copying Registry.Version
Copying Custom.Cmd
Copying Provisioning.Auto
Copying OEM.Sample
Copying Device.SystemInformation
Copying DeviceLayout.GPT4GB
Copying DeviceLayout.GPT8GB-R
Copying DeviceLayout.MBR4GB
Copying DeviceLayout.MBR8GB-R
Workspace ready!
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>Import-IoTBSP BSWx64 "C:\Program Files (x86)\Intel IoT\Source-x64\BSP\"
Processing C:\Program Files (x86)\Intel IoT\Source-x64\BSP\\BSWx64
Warning:   Replacing Intel.BSW64.DeviceLayout with %OEM_NAME%.BSW64.DeviceLayout
Warning:   Replacing Intel.BSW64.GFX with %OEM_NAME%.BSW64.GFX
Warning:   Replacing Intel.BSW64.OEMDevicePlatform with %OEM_NAME%.BSW64.OEMDevicePlatform
BSP copy completed
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>buildpkg BSWx64
Processing BSW64.DeviceLayout.wm.xml
Processing BSW64.GFX.wm.xml
Processing BSW64.GPIO.wm.xml
Processing BSW64.I2C.wm.xml
Processing BSW64.OEMDevicePlatform.wm.xml
Processing BSW64.SystemInformation.wm.xml
Processing BSW64.UART.wm.xml
True
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>New-IoTCabPackage All
Processing Device.SystemInformation.wm.xml
Processing DeviceLayout.GPT4GB.wm.xml
Processing DeviceLayout.GPT8GB-R.wm.xml
Processing DeviceLayout.MBR4GB.wm.xml
Processing DeviceLayout.MBR8GB-R.wm.xml
Processing Registry.Version.wm.xml
Processing OEM.Sample.wm.xml
Processing BSW64.DeviceLayout.wm.xml
Processing BSW64.GFX.wm.xml
Processing BSW64.GPIO.wm.xml
Processing BSW64.I2C.wm.xml
Processing BSW64.OEMDevicePlatform.wm.xml
Processing BSW64.SystemInformation.wm.xml
Processing BSW64.UART.wm.xml
True
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>Add-IoTProduct IoTProductA BSWx64

cmdlet Add-IoTProduct at command pipeline position 1
Supply values for the following parameters:
OemName: Contoso
FamilyName: DeviceFamily-1
SkuNumber: SKU-001
BaseboardManufacturer: Intel
BaseboardProduct: BSW-Ax5-Z8350
Creating IoTProductA Product with BSP BSWx64
Creating C:\IoT\WorkSpaces\BSWDemo\Source-x64\Products\IoTProductA\prov\customizations.xml...
Creating C:\IoT\WorkSpaces\BSWDemo\Source-x64\Products\IoTProductA\IoTProductASettings.xml...
Product Config file : C:\IoT\WorkSpaces\BSWDemo\Source-x64\Products\IoTProductA\IoTProductASettings.xml
DeviceInventory file : C:\IoT\WorkSpaces\BSWDemo\Source-x64\Products\IoTProductA\IoTDeviceModel_IoTProductA.xml
OS Version           : 10.0.17763.107
BSP Version          : 10.0.0.0
DeviceInventory created
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>New-IoTFFUImage IoTProductA Test
ADK_VERSION : 10.0.17763.1
IOTCORE_VER : 10.0.17763.107
BSP_VERSION : 10.0.0.0
ADDONKITVER : 6.0.190116.1218
HostOS Info : Microsoft Windows 10 Enterprise - 10.0.17763 - en-US
Validating product feature ids
Reading feature ids in C:\IoT\WorkSpaces\BSWDemo\Source-x64\BSP\BSWx64\Packages\BSWx64FM.XML
Reading feature ids in C:\IoT\WorkSpaces\BSWDemo\Common\Packages\OEMCommonFM.xml
Reading feature ids in C:\IoT\WorkSpaces\BSWDemo\Source-x64\Packages\OEMFM.xml
Checking Microsoft features in OEMInput file..
Warning: IOT_APPLICATIONS is not defined
Warning: IOT_CORTANA is not defined
Warning: IOT_DISABLE_UMCI is not defined
Warning: IOT_GENERIC_POP is not defined
Warning: IOT_NETCMD is not defined
Checking OEM features in OEMInput file..
Building product specific packages
Processing Registry.Version.wm.xml
Processing Custom.Cmd.wm.xml
Processing Provisioning.Auto.wm.xml
Building FM files..
Exporting OEM FM files..
Processing OEMFMList..
Exporting BSWx64 BSP FM files
Processing BSWx64FMFileList.xml
Creating Image..
See C:\IoT\WorkSpaces\BSWDemo\Build\amd64\IoTProductA_Test.log for progress
This will take a while...
Build Completed. See C:\IoT\WorkSpaces\BSWDemo\Build\amd64\IoTProductA\Test\Flash.ffu
True
IoTCorePShell amd64 10.0.0.0 Test
PS C:\IoT\WorkSpaces\BSWDemo>


```
