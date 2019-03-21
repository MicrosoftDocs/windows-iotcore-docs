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

One of the ultimate goals for creating an IoT image for a device is so that you can eventually have a mass-produced IoT device. 
The following checklist and guide will assist you in creating your first test image of Window IoT Core in the platform of your choosing:

---
1. We will split the tasks into multiple sections.
2. We will be using Snapdragon 410C as an example for this walkthrough. Feel free to substitute the device as needed.
3. We will use the product name "**ProductX**" in this walkthrough.

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
    new-ws C:\IoT\iot-adk-addonkit\Workspace\ContosoWS Contoso Arm
    ```

 - [ ] For subsequent visits, use this:
  
    ``` powershell
    (or) open-ws C:\IoT\iot-adk-addonkit\Workspace\ContosoWS
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
    Add-IoTProduct ProductX QCDB410C
    (or) newproduct ProductX QCDB410C
    ```
    Sample **SMBIOS**
* **System OEM Name:** Contoso
* **System Family Name:** ContosoHub
* **System SKU Number:** AI-001
* **Baseboard Manufacturer:** Arrows
* **Baseboard Product:** DragonBoard 410c

### Create a test Image
Build your first test FFU image with the following command:
- [ ] Create Test FFU
 
    ``` powershell
    New-IoTFFUImage ProductX Test
    (or)buildimage ProductX Test 
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
Opening workspace : C:\IoT\Workspaces\ContosoWS\IoTWorkspace.xml
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
PS C:\IoT\iot-adk-addonkit\Workspace>new-ws c:\IoT\Workspaces\ContosoWS Contoso ARM
New IoTWorkSpace available at c:\IoT\Workspaces\ContosoWS for ARM
Opening workspace : C:\IoT\WorkSpaces\ContosoWS\IoTWorkspace.xml
Corekit found OK
ADK_VERSION : 10.0.17763.1
IOTCORE_VER : 10.0.17763.107
BSP_VERSION : 10.0.0.0
ADDONKITVER : 6.0.190116.1218
HostOS Info : Microsoft Windows 10 Enterprise - 10.0.17763 - en-US
IOTWKSPACE  : C:\IoT\WorkSpaces\ContosoWS
OEM_NAME    : Contoso
BSP_ARCH    : ARM
BSPPKG_DIR  : C:\IoT\WorkSpaces\ContosoWS\Build\ARM\pkgs
MSPKG_DIR   : C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail\ARM\fre
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
PS C:\IoT\WorkSpaces\BSWDemo>Import-QCBSP c:\Temp\db410c_bsp_mar2019.zip C:\IoT\BSPs\QCDB410C -ImportBSP
Processing C:\Dev\OpenSource\iot-adk-addonkit\Workspace\Source-ARM\BSP\QCDB410C
No .pkg.xml files found in C:\IoT\Workspaces\ContosoWS\Source-ARM\BSP\QCDB410C.
Warning: %BLD_DIR%\MergedFMs\OEMCommonFM.xml already defined
Warning: %BLD_DIR%\MergedFMs\OEMFM.xml already defined
Warning: %BLD_DIR%\MergedFMs\OEMCommonFM.xml already defined
Warning: %BLD_DIR%\MergedFMs\OEMFM.xml already defined
BSP copy completed
Extracting DB410c_BSP/prebuilt/8016/cabfiles/DevicePlatformID/8016/SBC/Qualcomm.QC8916.OEMDevicePlatform.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/mtp/Qualcomm.QC8916.qcAlsCalibrationMTP.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/mtp/Qualcomm.QC8916.qcAlsPrxAPDS9900.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/mtp/Qualcomm.QC8916.qcMagAKM8963.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/mtp/Qualcomm.QC8916.qcTouchScreenRegsitry1080p.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/OEM.HalExtensions.UpdateOS.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/production/Qualcomm.QC8916.UEFI_PRODUCTION.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8016.AMSSPeriImage.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.ABD.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.ADCM.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.AudioDeviceDriver.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.bam_dmux.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.BCryptCipher_KM.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.direct3dum11.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.HalExtQCTimer.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.HalExtQCWdogTimer.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.hwnhaptics.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.hwnled.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.ipc_router.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.MemRes_ModemLite.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.OEMAutobrightness.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.PhoneRadioRevision_8916.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.pil.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QC_PEP.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcAccGyroMPU6050.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcadc.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcBattMiniclass.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcBattMngr.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcbluetooth.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qccdi.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QCCI.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qccomposite.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcdx11compiler.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcdxdriver.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcEhciFilter.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcfmminiport.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcfmtransport.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcFocalTechTouch.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcgnss.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcgpio.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qci2c.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcimssink.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcimssrc.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcKmdBam.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QCListenSoundModel.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcLTECoexMgr.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcPmic.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcPmic3P.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcPmicApps.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcPmicGpio.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QCSI.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcspi.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcspmi.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcSynapticsTouch.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcUrsFilter.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcVidEncmftH263.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcVidEncmftH264.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QcVidEncMftMPEG4.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcvidencum.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qcvss.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QHEE.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qmux.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QSEE.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.QSOCKET.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.qualcomm_uart.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.remotefs.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.RPEN.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.RPM.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.SBL1.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.scm.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.smbios_cfg.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.smd.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.smmu.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.ssd.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.ssm.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.subsys.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.TouchDetectionDriver.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.TrEE.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.TZAPPS.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.UEFI.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.UsbFnFilter.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.WCNSSPeriImage.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.WINSECAPP.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.wlan.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/Qualcomm.QC8916.wlan_caps.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/qwpct/Qualcomm.QC8916.DPP.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/sbc/Qualcomm.M8016SOC_SBC.acpi.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/sbc/Qualcomm.QC8916_SBC.ACSP.cab
Extracting DB410c_BSP/prebuilt/8016/cabfiles/sbc/Qualcomm.QC8916_SBC.qcaud.cab
Extracting DB410c_BSP/prebuilt/8016/DevicePlatformID/8016/SBC/Qualcomm.QC8916.OEMDevicePlatform.cab
BSP import completed
IoTCorePShell ARM 10.0.0.0 Test
PS C:\IoT\Workspaces\ContosoWS>buildpkg QCDB410c
Processing Custom.SMBIOS.wm.xml
Processing QCDB410C.DeviceLayout.wm.xml
Processing QCDB410C.DeviceLayout-R.wm.xml
Processing QCDB410C.DevicePlatform-R.wm.xml
True
IoTCorePShell ARM 10.0.0.0 Test
PS C:\IoT\Workspaces\ContosoWS>New-IoTCabPackage All
Processing Device.SystemInformation.wm.xml
Processing DeviceLayout.GPT4GB.wm.xml
Processing DeviceLayout.GPT8GB-R.wm.xml
Processing DeviceLayout.MBR4GB.wm.xml
Processing DeviceLayout.MBR8GB-R.wm.xml
Processing Registry.Version.wm.xml
Processing OEM.Sample.wm.xml
Processing Custom.SMBIOS.wm.xml
Processing QCDB410C.DeviceLayout.wm.xml
Processing QCDB410C.DeviceLayout-R.wm.xml
Processing QCDB410C.DevicePlatform-R.wm.xml
True
IoTCorePShell ARM 10.0.0.0 Test
PS C:\IoT\Workspaces\ContosoWS>Add-IoTProduct ProductX QCDB410c

cmdlet Add-IoTProduct at command pipeline position 1
Supply values for the following parameters:
OemName: Contoso
FamilyName: ContosoHub
SkuNumber: AI-001
BaseboardManufacturer: Arrows
BaseboardProduct: DragonBoard 410c
Creating ProductX Product with BSP QCDB410c
Creating C:\IoT\Workspaces\ContosoWS\Source-ARM\Products\ProductX\prov\customizations.xml...
Creating C:\IoT\Workspaces\ContosoWS\Source-ARM\Products\ProductX\ProductXSettings.xml...
Product Config file : C:\IoT\Workspaces\ContosoWS\Source-ARM\Products\ProductX\ProductXSettings.xml
DeviceInventory file : C:\IoT\Workspaces\ContosoWS\Source-ARM\Products\ProductX\IoTDeviceModel_ProductX.xml
OS Version           : 10.0.17763.253
BSP Version          : 10.0.0.0
DeviceInventory created
IoTCorePShell ARM 10.0.0.0 Test
PS C:\IoT\Workspaces\ContosoWS>New-IoTFFUImage ProductX

cmdlet New-IoTFFUImage at command pipeline position 1
Supply values for the following parameters:
Config: ^X
IoTCorePShell ARM 10.0.0.0 Test
PS C:\IoT\Workspaces\ContosoWS>New-IoTFFUImage ProductX Test
ADK_VERSION : 10.0.17763.1
IOTCORE_VER : 10.0.17763.253
BSP_VERSION : 10.0.0.0
ADDONKITVER : 6.0.190116.1218
HostOS Info : Microsoft Windows 10 Enterprise - 10.0.17763 - en-US
Validating product feature ids
Reading feature ids in C:\IoT\Workspaces\ContosoWS\Source-ARM\BSP\QCDB410C\Packages\QCDB410CFM.xml
Reading feature ids in C:\IoT\Workspaces\ContosoWS\Source-ARM\BSP\QCDB410C\Packages\QCDB410CTestFM.xml
Reading feature ids in C:\IoT\Workspaces\ContosoWS\Common\Packages\OEMCommonFM.xml
Reading feature ids in C:\IoT\Workspaces\ContosoWS\Source-ARM\Packages\OEMFM.xml
Checking Microsoft features in OEMInput file..
Checking OEM features in OEMInput file..
Building product specific packages
Processing Registry.Version.wm.xml
Processing Custom.Cmd.wm.xml
Processing Provisioning.Auto.wm.xml
Using custom SMBIOS settings
Processing Custom.SMBIOS.wm.xml
True
Building FM files..
Exporting OEM FM files..
Processing OEMFMList..
Exporting QCDB410c BSP FM files
Processing QCDB410cFMFileList.xml
Creating Image..
See C:\IoT\Workspaces\ContosoWS\Build\ARM\ProductX_Test.log for progress
This will take a while...
ThreadId164476 ERROR: Error : ImageCommon!BuildCompDB: Some Conditional Features have been defined and determined to apply but the corresponding Feature is missing:
ThreadId164476 ERROR:   Error : FeatureID=OEM_SMBIOS_DEFAULT FMID=QCDB410C
Build Completed. See C:\IoT\Workspaces\ContosoWS\Build\ARM\ProductX\Test\Flash.ffu
True
IoTCorePShell ARM 10.0.0.0 Test


```
