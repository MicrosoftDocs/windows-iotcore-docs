---

description: 'The Windows 10 IoT Core ADK Add-Ons include tools to help you customize and create new images for your devices with the apps, board support packages (BSPs), drivers, and Windows features that you choose, and a sample structure you can use to quickly create new images.'
ms.assetid: 26cfbad0-9528-4f89-a174-f198ece325d4
MSHAttr: 'PreferredLib:/library'
title: 'Windows ADK IoT Core Add-ons: contents'

ms.date: 10/15/2018
ms.topic: article


---

# Windows ADK IoT Core Add-ons: contents

The [Windows 10 IoT Core ADK Add-Ons](https://go.microsoft.com/fwlink/?LinkId=735028) include OEM-specific tools to create images for your IoT Core devices with your apps, board support packages (BSPs), settings, drivers, and features.

This kit 
- makes IoT Core image creation process easy and simple
- enables creation of multiple images/image variants easily
- provides automation support for nightly builds 


The [IoT Core manufacturing guide](iot-core-manufacturing-guide.md) walks you through building images with these tools.

## Key XML definitions

- Package definitions (*.wm.xml) : defines a component package
- Provisioning definitions (customizations.xml) : source file for provisioning settings
- Feature manifests (*FM.xml) : defines feature composition and feature IDs
- Feature manifest List (*FMList.xml) : enumerates the FM files 
- Product definitions (*OEMInputFile.xml) : specifies the product composition with the Microsoft features and OEM features included in the product

| Name | Filename.ext | ADK tool | build command | Output |
|-----|----|----|---|---|
| Package  | *.wm.xml  | `pkggen.exe` | `New-IoTCabPackage (buildpkg)`   | *.cab  |
| Provisioning  | customizations.xml  | `icd.exe`  | `New-IoTProvisioningPackage (buildppkg)`   | *.ppkg | 
| Feature manifest  | *FM.xml  | `featuremerger.exe` `imageapp.exe`  | -  | - | 
| Feature manifest list | *FMList.xml  | `featuremerger.exe`  | `New-IoTFIPPackage (buildfm)`  | MergerdFM/*FM.xml , *FIP.cab  |
| Product  | *OEMInputFile.xml  | `imageapp.exe`  | `New-IoTFFUImage (buildimage)`  | *.ffu |

## Code Architecture

- Root folder
    - IoTCorePShell.cmd: Launches the IoT Core Powershell
    - README.md: Version info, links to documentation
- Scripts
    - This contains helper powershell scripts and sample build scripts.
- Tools
    - IoTCoreImaging, containing the powershell module and scripts. See [IoT Core Add-ons Powershell tools](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/README.md#supported-functionality-listing)
    - README.md : Documentation on the powershell tools
- Workspace 
    - IoTWorkspace.xml
        - XML file containing the workspace configuration information such as supported architecture, security settings etc.
    - Build
        - This is the output directory where the build contents are stored. It starts as empty.
    - Common/Packages
        - Architecture *independent*, platform *independent* packages
        - OEMCommonFM.xml - feature manifest file that enumerates common packages and defines common features.
    - Source-\<arch\>
        - Packages
            - Architecture *specific*, platform *independent* packages
            - OEMFM.xml - the feature manifest file that enumerates arch specific packages and defines arch specific features.
            - OEMFMList.xml - enumeration of OEM FM files. 
        - BSP
            - \<bspname\>/Packages
                -  Architecture *specific*, platform *specific* packages
                - \<bspname\>FM.xml - feature manifest that enumerates the bsp packages and defines supported device layouts and features
                - \<bspname\>FMList.xml - enumeration of BSP FM files.
            - \<bspname\>/OemInputSamples
                - sample oeminput files demonstrating how to use the bsp, these files are used as templates in `Add-IoTProduct (newproduct)`
        - Products
            - architecture specific named products


## Sample packages
Sample packages are provided in the iot-adk-addonkit that can be used as a reference or as is in your image, if it meets your needs. Few of such packages are listed here.

### Common Packages 

| Package Name | Description |
| ----- | ----- |
| Registry.Version  |  Package containing registry settings with product and version information. |
|  DeviceLayout.GPT4GB | Package with [GPT drive/partition layout](device-layout.md) for UEFI-based devices with 4GB drives.  |
|  DeviceLayout.GPT8GB-R | Package with GPT drive/partition layout for UEFI-based devices with 8GB drives with recovery partition.  |
|  DeviceLayout.MBR4GB | Package with MBR drive/partition layout for legacy BIOS-based devices with 4GB drives.  |
|  DeviceLayout.MBR8GB-R | Package with MBR drive/partition layout for legacy BIOS-based devices with 8GB drives with recovery partition.  |


### Applications and Services packages

| Package Name | Description |
| ----- | ----- |
| Appx.IoTCoreDefaultApp | Foreground apps package containing [IoTCoreDefaultApp](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/IoTCoreDefaultApp), see [description](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/IoTCoreDefaultApp).  |
| Appx.IoTOnboardingTask | Background apps package containing [IoTOnboardingTask](https://github.com/microsoft/Windows-iotcore-samples/tree/master/Samples/IoTOnboarding), see [description](https://github.com/microsoft/Windows-iotcore-samples/tree/master/Samples/IoTOnboarding).  |
| AzureDM.Services | Service package contaiing Azure Device Management |

### <span id="BSP"></span><span id="bsp"></span>BSP
Source files to create board support packages (BSPs). 

Some BSPs are included in each folder as a start. You can [create your own BSPs](create-a-new-bsp.md) based on these packages.

### Driver packages

| Package Name | Description |
| ----- | ----- |
| Drivers.GPIO | Sample package for adding a driver. |

### <span id="Products"></span><span id="products"></span><span id="PRODUCTS"></span>Products

Source file for product configurations. Use our samples (SampleA, SampleB) or [create your own](iot-core-manufacturing-guide.md).

| Product | Description |
| ----- | ----- |
| SampleA | Product with Microsoft provided features / apps |
| SampleB | Product using OEM Apps and OEM drivers |
| SingleLangSample | Product with single non english language support |
| MultiLangSample  | Product with multiple language support |
| SecureSample  | Product using security features  |
| RecoverySample  | Product using recovery mechanism   |

## <span id="related_topics"></span>Related topics

[IoT Core manufacturing guides](iot-core-manufacturing-guide.md)

[IoTCore Servicing](/windows-hardware/service/iot/)

[IoT Core feature list](iot-core-feature-list.md)

[IoT Core Image Wizard](iot-core-image-wizard.md)
