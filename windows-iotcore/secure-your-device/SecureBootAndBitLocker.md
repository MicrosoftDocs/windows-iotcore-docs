---
title: Enabling Secure Boot, BitLocker, and Device Guard on Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to enable Secure Boot, BitLocker, and Device Guard on Windows 10 IoT Core
keywords: windows iot, secure boot, BitLocker, device guard, security, turnkey security
---

# Enabling Secure Boot, BitLocker, and Device Guard on Windows 10 IoT Core

## Introduction  
With the release of Creators Update, Windows 10 IoT Core improves its security feature offerings to include UEFI Secure Boot, BitLocker Device Encryption and Device Guard.  These will allow device builders in creating fully locked down Windows IoT devices that are resilient to many different types of attacks.  Together, these features provide the optimal protection that ensures that a platform will launch in a defined way, while locking out unknown binaries and protecting user data through the use of device encryption.  

### Secure Boot
UEFI Secure Boot is the first policy enforcement point, located in UEFI.  It restricts the system to only allow execution of binaries signed by a specified authority. This feature prevents unknown code from being executed on the platform and potentially weakening the security posture of it. 

### BitLocker Device Encryption
Windows 10 IoT Core also implements a lightweight version of BitLocker Device Encryption, protecting IoT devices against offline attacks.  This capability has a strong dependency on the presence of a TPM on the platform, including the necessary preOS protocol in UEFI that conducts the necessary measurements. These preOS measurements ensure that the OS later has a definitive record of how the OS was launched; however, it does not enforce any execution restrictions.
> [!TIP]
> BitLocker functionality on Windows 10 IoT Core allows for automatic encryption of NTFS-based OS volume while binding all available NTFS data volumes to it.  For this, it’s necessary to ensure that the EFIESP volume GUID is set to _C12A7328-F81F-11D2-BA4B-00A0C93EC93B_.  

### Device Guard on Windows IoT Core
Most IoT devices are built as fixed-function devices.  This implies that device builders know exactly which firmware, operating system, drivers and applications should be running on a given device.  In turn, this information can be used to fully lockdown an IoT device by only allowing execution of known and trusted code.  Device Guard on Windows 10 IoT Core can help protect IoT devices by ensuring that unknown or untrusted executable code cannot be run on locked-down devices.

## Locking-down IoT Devices
In order to lockdown a Windows IoT device, the following considerations must be made.
 
### UEFI Platform & Secure Boot
In order to leverage Device Guard capabilities, it is necessary to ensure that the boot binaries and UEFI firmware are signed and cannot be tampered with.  UEFI Secure Boot is the first policy enforcement point, located in UEFI.  It prevents tampering by restricting the system to only allow execution of boot binaries signed by a specified authority. Additional details on Secure Boot, along with key creation and management guidance, is available [here](https://technet.microsoft.com/en-us/library/dn747883.aspx).

### Configurable Code Integrity (CCI)
Code Integrity (CI) improves the security of the operating system by validating the integrity of a driver or application each time it is loaded into memory. CI contains two main components - Kernel Mode Code Integrity (KMCI) and User Mode Code Integrity (UMCI).  

Configurable Code Integrity (CCI) is a feature in Windows 10 that allows device builders to lockdown a device and only allow it to run and execute code that is signed and trusted.  To do so, device builders can create a code integrity policy on a 'golden' device (final release version of hardware and software) and then secure and apply this policy on all devices on the factory floor.  

To learn more about deploying code integrity policies, auditing and enforcement, check out the latest technet documentation [here](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/deploy-code-integrity-policies-steps).

## Turnkey Security on IoT Core
To facilitate easy enablement of key secrutiy features on IoT Core devices, Microsoft is providing a turnkey 'Security Package' that allows device builders to build fully locked down IoT devices.  This package will help with:
* Provisioning Secure Boot keys and enabling the feature on supported IoT platforms
* Setup and configuration of device encryption using BitLocker 
* Initiating device lockdown to only allow execution of signed applications and drivers

### Pre-requisites:
* A PC running Windows 10 Enterprise
* [Windows 10 SDK](https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk) - Required for Certificate Generation 
* [Windows 10 ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) - Required for CAB generation
* Reference platform - release hardware with shipping firmware, OS, drivers and applications will be required for final lockdown

### Development IoT Devices 
Windows 10 IoT Core works with various silicons that are utilized in hundreds of devices. Of the [suggested IoT development devices](../learn-about-hardware/suggestedboards.md), the following provide firmware TPM functionality out of the box, along with Secure Boot, Measured Boot, BitLocker and Device Guard capabilities:
* Qualcomm DragonBoard 410c

    In order to enable Secure Boot, it may be necessary to provision RPMB. Once the eMMC has been flashed with Windows 10 IoT Core (as per instructions [here](https://developer.microsoft.com/en-us/windows/iot/getstarted), press [Power] + [Vol+] + [Vol-] simultaneously on the device when powering up and select "Provision RPMB" from the BDS menu. *Please note that this is an irreversible step.*
* Intel MinnowBoardMax 

    For Intel's MinnowBoard Max, firmware version must be 0.82 or higher (get the [latest firmware](https://firmware.intel.com/projects/minnowboard-max)). To enable TPM capabilities, power up board with a keyboard & display attached and press F2 to enter UEFI setup. Go to _Device Manager -> System Setup -> Security Configuration -> PTT_ and set it to _&lt;Enable&gt;_. Press F10 to save changes and proceed with a reboot of the platform.

> [!NOTE]
> Raspberry Pi 2 nor 3 do not support TPM and so we cannot configure Lockdown scenarios.

### Generate Lockdown Packages

1. Download the [DeviceLockDown Script](https://github.com/ms-iot/security/tree/master/TurnkeySecurity) package, which contains all of the additional tools and scripts required for configuring and locking down devices
2. Start an Administrative PowerShell (PS) console on your Windows 10 PC and navigate to the location of the downloaded script.
3. Mount your reference hardware platform (running the unlocked image) to your PC via network share using `net use \\a.b.c.d\c$ /user:username password`
4. Generate keys for your device using `.\GenerateKeys.ps1 -OemName '<your oem name>' -outputPath '<output directory>'`
    * The keys and certificates are generated in the specified output folder with appropriate suffix.
    * **Secure your generated keys** as the device will trust binaries signed with these keys only after lockdown.
    * You may skip this step and use the pre-generated keys for testing only
5. Configure _settings.xml_
   * General section : Specify the package directories
    * Tools section : Set the path for the tools
      - Windows10KitsRoot `(e.g. <Windows10KitsRoot>C:\Program Files (x86)\Windows Kits\10\</Windows10KitsRoot>)`
      - WindowsSDKVersion `(e.g. <WindowsSDKVersion>10.0.15063.0</WindowsSDKVersion>)`
        - SDK version installed on your machine is under `C:\Program Files (x86)\Windows Kits\10\`
    * SecureBoot section : Specify which keys to use for secure boot (PK and SB keys)
    * BitLocker section : Specify a certificate for Bitlocker data recovery (DRA key)
    * SIPolicy section : Specify certs that should be trusted
      * ScanPath : Path of the device for scanning binaries , `\\a.b.c.d\C$`
      * Update   : Signer of the SIPolicy (PAUTH keys)
      * User     : User mode certificates (UMCI keys) 
      * Kernel   : Kernel mode certificates (KMCI keys)
    * Packaging : Specify the settings for the package generation

> [!IMPORTANT]
> In order to assist with testing during the initial development cycle, Microsoft has provided pre-generated keys and certificates where appropriate.  This implies that Microsoft Test, Development and Pre-Release binaries are considered trusted.  During final product creation and image generation, be sure to remove these certifcates and use your own keys to ensure a fully locked down device.
  
6. Execute the following commands to generate required packages:
    * `Import-Module .\IotDeviceGuardPackage.psm1`
    * `New-IotDeviceGuardPackage -ConfigFileName .\settings.xml`
  
### Test Lockdown packages
You can test the generated packages by manually installing them on a unlocked device by the following steps

1. Flash the device with the unlocked image (image used for scanning in earlier step).
2. Connect to the device ([using SSH](../connect-your-device/SSH.md) or using [Powershell](../connect-your-device/PowerShell.md))
3. Copy the following .cab files to the device under a directory e.g. `c:\OemInstall`
    * OEM.Custom.Cmd.cab
    * OEM.Security.BitLocker.cab
    * OEM.Security.SecureBoot.cab
    * OEM.Security.DeviceGuard.cab
4. Initiate staging of the generated packages by issueing the following commands:
    * `applyupdate -stage c:\OemInstall\OEM.Custom.Cmd.cab`
      - If you are using custom image, then you will have to *skip* this file and manually edit the `c:\windows\system32\oemcustomization.cmd` with the contents available in `Output\OEMCustomization\OEMCustomization.cmd` file.
    * `applyupdate -stage c:\OemInstall\OEM.Security.BitLocker.cab`
    * `applyupdate -stage c:\OemInstall\OEM.Security.SecureBoot.cab`
    * `applyupdate -stage c:\OemInstall\OEM.Security.DeviceGuard.cab`
5. Finally, commit the packages via: 
    * `applyupdate -commit`
6. The device will reboot into update OS (showing gears) to install the packages and will reboot again to main OS.  Once the device reboots back into MainOS, Secure Boot will be enabled and SIPolicy should be engaged.
7. Reboot the device again to activate the Bitlocker encryption.
8. Test the security features
    * SecureBoot: try `bcdedit /debug on` , you will get an error stating that the value is protected by secure boot policy
    * BitLocker: Run `fvecon -status c:`, you will get the status mentioning *On, Encrypted, Has Recovery Data (external key), Has TPM Data, Secure, Boot Partition, Used Space Only*
    * DeviceGuard : Run any unsigned binary or a binary signed with certificate not in the SIPolicy list and confirm that it fails to run.

### Generate Lockdown image
After validating that the lockdown packages are working as per the settings defined earlier, you can then include these packages into the image by following the below given steps. Read [IoT manufacturing guide](https://aka.ms/iotcoreguide) for custom image creation instructions.

1. In the iot-adk-addonkit directory, update the following files from the generated output directory above
    * SecureBoot : `Copy ..\Output\SecureBoot\*.bin  ..\iot-adk-addonkit\Common\Packages\Security.SecureBoot`
      * SetVariable_db.bin
      * SetVariable_kek.bin
      * SetVariable_pk.bin
    * BitLocker : `Copy ..\Output\Bitlocker\*.* ..\iot-adk-addonkit\Common\Packages\Security.Bitlocker`      
      * DETask.xml
      * Security.Bitlocker.pkg.xml
      * setup.bitlocker.cmd
    * DeviceGuard : `Copy ..\Output\DeviceGuard\*.*  ..\iot-adk-addonkit\Common\Packages\Security.DeviceGuard`     
      * SIPolicyOn.p7b
      * SIPolicyOff.p7b
  
2. Add RetailOEMInput.xml and TestOEMInput.xml under the ProductName directory with lockdown package feature ID
    * `<Feature>Sec_BitLocker</Feature>`
    * `<Feature>Sec_SecureBoot</Feature>`
    * `<Feature>Sec_DeviceGuard</Feature>`
3. Re-generate Image
    * `buildpkg all` (this generates new lockdown packages based on above policy files)
    * `buildimage ProductName test(or)retail`  (this generates new Flash.ffu)
4. Flash the device with this new Flash.ffu and validate the security features.

See [SecureSample](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Source-arm/Products/SecureSample) as an example of a lockdown dragon board configuration.


### Developing with CodeSigning Enforcement Enabled
Once the packages are generated and lockdown is activated, any binaries introduced into the image during development will need to be signed appropriately. Ensure that your user-mode binaries are signed with the key  _.\Keys\ ***-UMCI.pfx_. For kernel-mode signing, such as for drivers, you’ll need to specify your own signing keys and make sure that they are also included in the SIPolicy above.


### Unlocking Encrypted Drives  
During development and testing, when attempting to read contents from an encrypted device offline (e.g. SD card for MinnowBoardMax or DragonBoard's eMMC through USB mass storage mode), 'diskpart' may be used to assign a drive letter to MainOS and Data volume (let's assume v: for MainOS and w: for Data).
The volumes will appear locked and need to be manually unlocked. This can be done on any machine that has the OEM-DRA.pfx certificate installed (included in the [DeviceLockDown sample](https://github.com/ms-iot/security/tree/master/TurnkeySecurity)). Install the PFX and then run the following commands from an administrative CMD prompt:

* `manage-bde -unlock v: -cert -cf OEM-DRA.cer`
* `manage-bde -unlock w: -cert -cf OEM-DRA.cer`

If the contents need to be frequently accessed offline, BitLocker autounlock can be set up for the volumes after the initial unlock using the following commands:

* `manage-bde -autounlock v: -enable`
* `manage-bde -autounlock w: -enable`

### Disabling BitLocker  
Should there arise a need to temporarily disable BitLocker, initate a remote PowerShell session with your IoT device and run the following command: `sectask.exe -disable`.  
**Note:** Device encryption will be re-enabled on subsequent device boot unless the scheduled encryption task is disabled.
