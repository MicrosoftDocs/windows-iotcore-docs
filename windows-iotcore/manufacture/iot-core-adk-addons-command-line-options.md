---

description: 'These tools are part of the Windows 10 IoT Core (IoT Core) ADK Add-Ons, in the \\Tools folder. To learn more about these tools, see What''s in the Windows ADK IoT Core Add-ons.'
ms.assetid: ae043bb0-656e-4439-bdbe-a8d370629ab7
MSHAttr: 'PreferredLib:/library'
title: 'IoT Core Add-ons command-line options'

ms.date: 10/15/2018
ms.topic: article


---

# IoT Core Add-ons Powershell Commands

> [!NOTE]
> IoT Core Add-ons command-line is deprecated. Refer to [IoT Core Add-ons command-line options](https://github.com/ms-iot/iot-adk-addonkit/tree/17134/Docs/iot-core-adk-addons-command-line-options.md) for the old list of commands.

The Powershell version of the [Windows 10 IoT Core (IoT Core) ADK Add-Ons](https://github.com/ms-iot/iot-adk-addonkit/tree/master) supports the following commands. These are part of the powershell module [IoTCoreImaging](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging). To learn more about these tools, see [What's in the Windows ADK IoT Core Add-ons](iot-core-adk-addons.md).

## Powershell Commands with Alias

### [Add-IoTAppxPackage (newappxpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTAppxPackage.md#Add-IoTAppxPackage)

Adds an Appx package directory to the workspace and generates the required wm.xml and customizations.xml files

### [Add-IoTBitLocker](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTBitLocker.md#Add-IoTBitLocker)

Generates the Bitlocker package (Security.BitLocker) contents based on the workspace specifications.

### [Add-IoTBSP (newbsp)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTBSP.md#Add-IoTBSP)

Generates a BSP directory under Source-arch\BSP\ using a BSP directory template.

### [Add-IoTCEPAL (addcepal)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTCEPAL.md#Add-IoTCEPAL)

Chain CEPALFM.xml into the IoT Core packaging process for a specific product

### [Add-IoTCommonPackage (newcommonpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTCommonPackage.md#Add-IoTCommonPackage)

Adds a common(generic) package directory to the workspace and generates the required wm.xml file.

### [Add-IoTDeviceGuard](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTDeviceGuard.md#Add-IoTDeviceGuard)

Generates the device guard package (Security.DeviceGuard) contents based on the workspace specifications.

### [Add-IoTDirPackage (adddir)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTDirPackage.md#Add-IoTDirPackage)

Adds the directory contents into a IoT file package definition.

### [Add-IoTDriverPackage (newdrvpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTDriverPackage.md#Add-IoTDriverPackage)

Adds a driver package directory to the workspace and generates the required wm.xml file.

### [Add-IoTEnvironment (addenv)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTEnvironment.md#Add-IoTEnvironment)

Adds a new architecture to the workspace

### [Add-IoTFilePackage (addfile)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTFilePackage.md#Add-IoTFilePackage)

Adds a file package directory to the workspace and generates the required wm.xml file.

### [Add-IoTProduct (newproduct)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTProduct.md#Add-IoTProduct)

Generates a new product directory under Source-arch\Products\.

### [Add-IoTProductFeature (addfid)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md#Add-IoTProductFeature)

Adds feature id to the specified product's oeminput xml file.

### [Add-IoTProvisioningPackage (newprovpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTProvisioningPackage.md#Add-IoTProvisioningPackage)

Adds a provisioning package directory to the workspace and generates the required wm.xml file, customizations.xml file and the icdproject file.

### [Add-IoTRegistryPackage (addreg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTRegistryPackage.md#Add-IoTRegistryPackage)

Adds a registry package directory to the workspace and generates the required wm.xml file.

### [Add-IoTSecureBoot](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTSecureBoot.md#Add-IoTSecureBoot)

Generates the secure boot package (Security.SecureBoot) contents based on the workspace specifications. If Test is specified, then it includes test certificates from the specification.

### [Add-IoTSecurityPackages](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTSecurityPackages.md#Add-IoTSecurityPackages)

Creates the security packages based on the settings in workspace configuration.

### [Add-IoTSignature (signbinaries)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTSignature.md#Add-IoTSignature)

Signs the files with the certificate selected via Set-IoTSignature

### [Add-IoTZipPackage (addzip)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTZipPackage.md#Add-IoTZipPackage)

Adds the zip file contents into a IoT file package definition.

### [Convert-IoTPkg2Wm (convertpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Convert-IoTPkg2Wm.md#Convert-IoTPkg2Wm)

Converts the existing pkg.xml files to wm.xml files.

### [Copy-IoTBSP (copybsp)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Copy-IoTBSP.md#Copy-IoTBSP)

Copies a BSP folder to the destination workspace from a source workspace or a source bsp directory.

### [Copy-IoTOEMPackage (copypkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Copy-IoTOEMPackage.md#Copy-IoTOEMPackage)

Copies an OEM package to the destination workspace from a source workspace.

### [Copy-IoTProduct (copyproduct)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Copy-IoTProduct.md#Copy-IoTProduct)

Copies a product folder to the destination workspace from a source workspace.

### [Dismount-IoTFFUImage (ffud)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Dismount-IoTFFUImage.md#Dismount-IoTFFUImage)

Dismounts the mounted ffu image and saves it as a new ffu if an ffuname is specified.

### [Export-IoTDeviceModel (exportidm)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Export-IoTDeviceModel.md#Export-IoTDeviceModel)

Exports the DeviceModel XML file required to register the device in the Device Update Center portal.

### [Export-IoTDUCCab (exportpkgs)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Export-IoTDUCCab.md#Export-IoTDUCCab)

Exports the update cab file required to upload on the Device Update Center

### [Export-IoTFFUAsWims (ffue)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Export-IoTFFUAsWims.md#Export-IoTFFUAsWims)

Extracts the mounted partitions as wim files

### [Get-IoTFFUDrives (ffugd)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Get-IoTFFUDrives.md#Get-IoTFFUDrives)

Returns a hashtable of the drive letters of the mounted partitions

### [Get-IoTProductFeatureIDs (gpfids)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Get-IoTProductFeatureIDs.md#Get-IoTProductFeatureIDs)

Returns the list of supported feature IDs in the Windows 10 IoT Core OS release defined in the workspace.

### [Get-IoTProductPackagesForFeature (gpfidpkgs)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Get-IoTProductPackagesForFeature.md#Get-IoTProductPackagesForFeature)

Returns the list of supported feature IDs in the Windows 10 IoT Core OS release defined in the workspace.

### [Get-IoTWorkspaceBSPs (gwsbsps)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Get-IoTWorkspaceBSPs.md#Get-IoTWorkspaceBSPs)

Returns the list of BSP names in the workspace.

### [Get-IoTWorkspaceProducts (gwsproducts)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Get-IoTWorkspaceProducts.md#Get-IoTWorkspaceProducts)

Returns the list of product names in the workspace.

### [Import-IoTBSP (importbsp)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTBSP.md#Import-IoTBSP)

Imports a BSP folder in to the current workspace from a source workspace or a source bsp directory or a source zip file.

### [Import-IoTCEPAL (importcepal)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTCEPAL.md#Import-IoTCEPAL)

Import a flat release directory and prepare for packaging into IoT Core

### [Import-IoTCertificate](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTCertificate.md#Import-IoTCertificate)

Imports an certificate and adds to the Workspace security specification.

### [Import-IoTDUCConfig (importcfg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTDUCConfig.md#Import-IoTDUCConfig)

Imports the Device Update Center Configuration files into the product directory

### [Import-IoTOEMPackage (importpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTOEMPackage.md#Import-IoTOEMPackage)

Imports an OEM package in to the current workspace from a source workspace.

### [Import-IoTProduct (importproduct)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-IoTProduct.md#Import-IoTProduct)

Imports a product folder in to the current workspace from a source workspace.

### [Import-PSCoreRelease (importps)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-PSCoreRelease.md#Import-PSCoreRelease)

Import Powershell Core Release into your workspace and update the wm xml files.

### [Import-QCBSP](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-QCBSP.md#Import-QCBSP)

Import QC BSP into your workspace and update the bsp files as required by the latest tools.

### [Install-IoTOEMCerts](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Install-IoTOEMCerts.md#Install-IoTOEMCerts)

Installs the OEM certs (pfx files) in the certs\private folder

### [Mount-IoTFFUImage (ffum)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Mount-IoTFFUImage.md#Mount-IoTFFUImage)

Mounts the specifed FFU, parses the device layout and assigns drive letters for the partitions with file system defined.

### [New-IoTCabPackage (buildpkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md#New-IoTCabPackage)

Creates a Cab package file for the specified wm.xml file or the wm.xml files in the specified directory.

### [New-IoTDeviceLayout](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTDeviceLayout.md#New-IoTDeviceLayout)

Factory method to create a new object of class IoTDeviceLayout

### [New-IoTFFUCIPolicy (ffus)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTFFUCIPolicy.md#New-IoTFFUCIPolicy)

This function scans the mounted FFU Main OS partition and creates a CI policy.

### [New-IoTFFUImage (buildimage)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md#New-IoTFFUImage)

Creates the IoT FFU image for the specified product / configuration. Returns boolean true for success and false for failure.

### [New-IoTFIPPackage (buildfm)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTFIPPackage.md#New-IoTFIPPackage)

Creates Feature Identifier Packages (FIP packages) for the given feature manifest files and updates the feature manifest files with the generated FIP packages. Returns boolean true for success and false for failure.

### [New-IoTFMXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTFMXML.md#New-IoTFMXML)

Factory method to create a new object of class IoTFMXML

### [New-IoTInf2Cab (inf2cab)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTInf2Cab.md#New-IoTInf2Cab)

Creates a cab file for the given inf.

### [New-IoTOEMCerts](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTOEMCerts.md#New-IoTOEMCerts)

Generates the required OEM certificates.

### [New-IoTOemInputXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTOemInputXML.md#New-IoTOemInputXML)

Factory method to create a new object of class IoTOemInputXML

### [New-IoTProduct](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTProduct.md#New-IoTProduct)

Factory method to create a new object of class IoTProduct

### [New-IoTProductSettingsXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTProductSettingsXML.md#New-IoTProductSettingsXML)

Factory method to create a new object of class IoTProductSettingsXML

### [New-IoTProvisioningPackage (buildppkg)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTProvisioningPackage.md#New-IoTProvisioningPackage)

Creates a .ppkg file from the customizations.xml input file. Returns a boolean indicating success or failure.

### [New-IoTProvisioningXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTProvisioningXML.md#New-IoTProvisioningXML)

Factory method to create a new object of class IoTProvisioningXML

### [New-IoTRecoveryImage (buildrecovery)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTRecoveryImage.md#New-IoTRecoveryImage)

Creates recovery ffu from a regular ffu

### [New-IoTWindowsImage (newwinpe)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWindowsImage.md#New-IoTWindowsImage)

Builds a WinPE image with relevant drivers and recovery files

### [New-IoTWMWriter](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWMWriter.md#New-IoTWMWriter)

Factory method, returing the IoTWMWriter class object used to write namespace.name.wm.xml file.

### [New-IoTWMXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWMXML.md#New-IoTWMXML)

Factory method to create a new object of class IoTWMXML

### [New-IoTWorkspace (new-ws)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWorkspace.md#New-IoTWorkspace)

Creates a new IoTWorkspace xml and the directory structure at the specified input directory.

### [New-IoTWorkspaceXML](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTWorkspaceXML.md#New-IoTWorkspaceXML)

Creates a new IoTWorkspaceXML object

### [Open-IoTWorkspace (open-ws)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Open-IoTWorkspace.md#Open-IoTWorkspace)

Opens the IoTWorkspace xml at the specified input directory and sets up the environment with those settings.

### [Redo-IoTCabSignature (re-signcabs)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Redo-IoTCabSignature.md#Redo-IoTCabSignature)

Resigns the cab file and its contents / cat files with the certificate set in the environment.

### [Redo-IoTWorkspace (migrate)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Redo-IoTWorkspace.md#Redo-IoTWorkspace)

Updates an old iot-adk-addonkit folder with required xml files to make it a proper workspace.

### [Remove-IoTProductFeature (removefid)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Remove-IoTProductFeature.md#Remove-IoTProductFeature)

Removes feature id from the specified product's oeminput xml file.

### [Set-IoTCabVersion (setversion)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Set-IoTCabVersion.md#Set-IoTCabVersion)

Sets the version to be used in the Cab package creation.

### [Set-IoTEnvironment (setenv)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Set-IoTEnvironment.md#Set-IoTEnvironment)

Sets the environment variables as per requested architecture

### [Set-IoTRetailSign (retailsign)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Set-IoTRetailSign.md#Set-IoTRetailSign)

Sets the signing certificate to the retail cert or test cert.

### [Set-IoTSignature (setsignature)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Set-IoTSignature.md#Set-IoTSignature)

Sets the signing related env vars with the cert information provided.

### [Test-IoTCabSignature (checkcab)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTCabSignature.md#Test-IoTCabSignature)

Checks if the cab file and its contents are properly signed.

### [Test-IoTCerts (tcerts)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTCerts.md#Test-IoTCerts)

Checks if the certs in the workspace folder are all valid.

### [Test-IoTFeatures (tfids)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTFeatures.md#Test-IoTFeatures)

Validates if all features specified in the specified product/config oeminputxml are defined. This returns boolean true for success and false for failure.

### [Test-IoTPackages (tpkgs)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTPackages.md#Test-IoTPackages)

Validates if all packages required for the specified product/config image creation are available and properly signed. This returns boolean true for success and false for failure.

### [Test-IoTRecoveryImage (verifyrecovery)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTRecoveryImage.md#Test-IoTRecoveryImage)

Validates if the recovery wim files are proper in the recovery ffu

### [Test-IoTSignature (checksign)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Test-IoTSignature.md#Test-IoTSignature)

Checks if the file is properly signed.

## Related topics

[IoT Core Add-ons](iot-core-adk-addons.md)

[IoT Core manufacturing guide](iot-core-manufacturing-guide.md)
