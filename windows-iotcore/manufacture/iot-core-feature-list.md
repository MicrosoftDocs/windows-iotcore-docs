---

description: 'These are the features you can add to Windows 10 IoT Core images.'
title: 'IoT Core feature list'
ms.date: 10/15/2018
ms.topic: article


---

# IoT Core feature list

Here's the features you can add to Windows 10 IoT Core (IoT Core) images.

Add features using the OEMInput XML file. To learn more, see the [IoT Core manufacturing guide](iot-core-manufacturing-guide.md).

## Retail features defined by Microsoft

The following table describes the Microsoft-defined features that can be used by OEMs in the Features element in the **OEMInput** file for **Retail** build.

When creating images for your device, determine which features are required for your device.

### Features

| Features                        | Description                                                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **IOT\_EFIESP** | Boots the device using UEFI, required feature in all images. |
| **IOT\_UAP\_OOBE** | Includes the inbox OOBE app that is launched during the first boot and also during installation of apps, required feature in all images.|
| **IOT\_CRT140** | Adds CRT binaries, required feature in all images.|
| **IOT\_UNIFIED\_WRITE\_FILTER** | Adds [Unified Write Filter (UWF)](/windows/iot-core/secure-your-device/UnifiedWriteFilter) to protect physical storage media from data writes.|
| **IOT\_USBFN\_CLASS\_EXTENSION** | Adds USB function WDF class extension for USB function mode support.  |
| **IOT\_POWERSHELL** | Adds PowerShell (except for Arm64) and WinRM binares. **Recommended:** Add the [open source powershell](https://github.com/PowerShell/PowerShell/releases) version using [Import-PSCoreRelease (importps)](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Import-PSCoreRelease.md#Import-PSCoreRelease). You will still require IOT\_POWERSHELL feature to include WinRM binaries |
| **IOT\_ALLJOYN\_APP** | Adds the AllJoyn application, used for Headless ZwaveAdapterAppx. |
| **IOT\_ONBOARDING_APP** | Provides a means of setting up the device’s WiFi connection if no other WiFi profile was configured.  It places the WiFi adapter into a Soft-AP mode so a phone or other device can connect to it. |
| **IOT\_FONTS\_CHINESE\_EXTENDED** | Adds additional Chinese fonts.  |
| **IOT\_APP\_TOOLKIT** | Adds tools required for Appx installation and management.|
| **IOT\_FFU\_FLASHMODE** | Adds flashing mode support so that the device can be flashed using ffutool. Currently supported for arm only.  |
| **IOT\_MTP** | Adds Media transfer protocol support. See [MTP](/windows/iot-core/connect-your-device/mtp).  |
| **IOT\_MIRACAST\_RX_APP** | Adds Connect App that supports Miracast receive feature. Note that the underlying hw/drivers should support Miracast for this app to work. Currently supported for arm only.  |
| **IOT\_WEBB\_EXTN** | Adds [Windows Device Portal]( /windows/iot-core/manage-your-device/deviceportal). If you are building an open retail device for commercial deployment to a "specific/limited installation" (i.e. factory or retail store) where the end-user does the final configuration and you document your customers that they must **obtain a certificate for WDP and install it on both WDP and connecting browsers and passwords are changed on WDP**, then using WDP in this narrow commercial instance is acceptable.  |
| **IOT\_BLUETOOTH\_A2DP\_SINK** | Allows an audio device to play to the device. This is new in Windows 10, version 1809|
| **IOT\_BLUETOOTH\_A2DP\_SOURCE** | Allows the device to play to an external device (e.g. a Bluetooth speaker). This is available as a separate feature in Windows 10, version 1809. In Windows 10, version 1803, this was included in the image by default.  |
| **IOT\_BLUETOOTH\_HFP\_AUDIOGATEWAY** | HFP AudioGateway allows the device to serve as a gateway device for phone calls. An application can interact with the calling functions of a paired Bluetooth headset by using APIs under Windows.ApplicationModel.Calls, specifically the VoipPhoneCall class. . |
| **IOT\_HEADLESS\_CONFIGURATION** | Configures device to boot into Headless mode, where the UI stack is disabled and foreground apps will not launch |
| **IOT\_NARRATOR** | Adds support for the Windows 10 screen-reading functionality, Narrator. |
| **IOT\_OCR\_ALL\_LANGS** | Adds Optical Character Recognition (OCR) for all supported languages, including English |
| **IOT\_OCR\_EN\_US** | Adds Optical Character Recognition (OCR) support for English. Do not use with **IOT\_OCR\_ALL\_LANGS** |
| ~~IOT\_HWN\_CLASS\_EXTENSION~~ (Deprecated)   | Adds hardware notification WDF class extension for vibration API support.  Deprecated in Windows 10, version 1709, as this feature is added by default |
| ~~IOT\_NETCMD~~ (Deprecated) | Adds the command-line tool: netcmd.exe, used for configuring network connectivity. Deprecated in Windows 10, version 1803. The netcmd.exe will be removed when updating to version 1803. Use [Windows.Devices.WiFi.WiFiAdapter](/uwp/api/Windows.Devices.WiFi.WiFiAdapter) for managing Wifi. See [WiFi Connector](https://github.com/Microsoft/Windows-iotcore-samples/blob/master/Samples/WiFiConnector/CS/README.md#wifi-connector) example. |
| ~~IOT\_APPLICATIONS~~ (Deprecated)           | Deprecated in Windows 10, 1809 release along with IOT\_CORTANA feature. Adds Account Management host application, enables MSA sign-in. Required for Cortana.  |

### Settings

| Features                        | Description                                                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **IOT\_POWER\_SETTINGS** | Prevents the device from going to sleep due to inactivity. Required for x86/amd64 platforms. This feature supports Arm starting with Windows 10, Version 1703. |
| **IOT\_EFIESP\_BCD** | Sets boot configuration data (BCD) for GPT-based drives. Required for x86/amd64. MBR devices should use **IOT\_EFIESP\_BCD_MBR**.|
| **IOT\_EFIESP\_BCD_MBR** | Sets boot configuration data (BCD) for MBR-based drives.|
| **IOT\_SHELL\_HOTKEY\_SUPPORT** | Adds support to launch default app using a hotkey: [VK_LWIN (Left Windows key)](/windows/win32/inputdev/virtual-key-codes). |  
| **IOT\_SHELL\_ONSCREEN\_KEYBOARD** | Adds available on-screen keyboard.|
| **IOT\_SHELL\_ONSCREEN\_KEYBOARD\_FOLLOWFOCUS** | Enables on-screen keyboard to automatically appear when input field is focused. Requires **IOT\_SHELL\_ONSCREEN\_KEYBOARD**.  |
| **IOT\_DISABLEBASICDISPLAYFALLBACK** | Disables the inbox basic render driver. This feature should only be used with the Qualcomm DragonBoard (DB). |
| **IOT\_CRASHCONTROL\_SETTINGS** | Configures the device to auto reboot without showing blue screen (BSOD) when the device crashs. This also disables crashdump. [AutoReboot = 1 ; DisplayDisabled = 1 and CrashDumpEnabled = 0]. See [Crash settings](./oscustomizations.md#crash-settings) |
| **IOT\_SSH** | Enables Secure Shell (SSH) connectivity |
| ~~IOT\_GENERIC\_POP~~ (Deprecated)   | In Windows 10 1809, this is deprecated and the device will get OS only updates by default. Adds the Generic device targeting info for OS only Updates.  |

### Developer Tools

> [!IMPORTANT]
> The following developer features should not be used in **Retail** builds and in images for commercial devices. If you would still like to disable IOT_SIREP as a developer tool, however, please follow the instructions [here](/windows/iot-core/troubleshooting#sirep-test-service).

| Features                        | Description                                                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **IOT\_SIREP** | Enables SIREP service for TShell connectivity.|
| **IOT\_TOOLKIT** | Includes developer tools such as: Kernel Debug components, FTP, Network Diagnostics, basic device portal, and XPerf. This also relaxes the firewall rules and enables various ports.|
| **IOT\_NANORDPSERVER** | Adds [Remote Display packages](/windows/iot-core/manage-your-device/RemoteDisplay). Note: Remote Display is prerelease software intended for development and training purposes only.|
| **IOT\_BERTHA** | Adds a sample app: "Bertha". This app provides basic version info and connectivity status.|
| **IOT\_UAP\_DEFAULTAPP** | Adds a sample app, "Chucky". This app is similar to "Bertha".|
| **IOT\_FTSER2K\_MAKERDRIVER** | Adds the FTDI USB-to-Serial driver.|
| **IOT\_CP210x\_MAKERDRIVER**  | Adds drivers for SiliconLabs CP210x-based USB to Serial adapters.|
| **IOT\_DMAP\_DRIVER** | Adds DMAP drivers.|
| **IOT\_CONTAINERS** | Adds support for native [Nano Server Containers](/virtualization/windowscontainers/manage-containers/container-base-images#base-images-for-windows-insiders). These are supported on Intel 64-bit platforms (since Windows 10, version 1709) and ARM32 platform (since Windows 10, version 1809). |
| ~~IOT\_CORTANA~~ (Deprecated) | Deprecated in Windows 10, 1809 release. See Cortana SDK for including Cortana to your device. Adds Cortana feature. Requires **IOT\_APPLICATIONS** feature.        |
| ~~IOT\_CORTANA\_OBSCURELAUNCH~~ (Deprecated) | Deprecated in Windows 10, 1809 release along with IOT\_CORTANA feature. Enables running Cortana application on boot. This add-on causes Cortana to run in the background resulting in better response time for Cortana.  |

### Speech Data

| Features                       | Description                                                                         |
|--------------------------------|-------------------------------------------------------------------------------------|
| **IOT\_SPEECHDATA\_AR\_SA** | Adds speech data for Arabic (Saudi Arabia). |
| **IOT\_SPEECHDATA\_DE\_DE** | Adds speech data for German (Germany).|
| **IOT\_SPEECHDATA\_EL\_GR** | Adds speech data for Greek.|
| **IOT\_SPEECHDATA\_EN\_CA** | Adds speech data for English (Canada).|
| **IOT\_SPEECHDATA\_EN\_GB** | Adds speech data for English (UK).|
| **IOT\_SPEECHDATA\_ES\_ES** | Adds speech data for Spanish (Spain).|
| **IOT\_SPEECHDATA\_ES\_MX** | Adds speech data for Spanish (Mexico).|
| **IOT\_SPEECHDATA\_FR\_CA** | Adds speech data for French (Canada).|
| **IOT\_SPEECHDATA\_FR\_FR** | Adds speech data for French (France).|
| **IOT\_SPEECHDATA\_IT\_IT** | Adds speech data for Italian.|
| **IOT\_SPEECHDATA\_JA\_JP** | Adds speech data for Japanese. |
| **IOT\_SPEECHDATA\_KO\_KR** | Adds speech data for Korean. |
| **IOT\_SPEECHDATA\_NL\_NL** | Adds speech data for Dutch. |
| **IOT\_SPEECHDATA\_PL\_PL** | Adds speech data for Polish. |
| **IOT\_SPEECHDATA\_PT\_BR** | Adds speech data for Portuguese (Brazil). |
| **IOT\_SPEECHDATA\_PT\_PT** | Adds speech data for Portuguese (Portugal). |
| **IOT\_SPEECHDATA\_RO\_RO** | Adds speech data for Romanian. |
| **IOT\_SPEECHDATA\_RU\_RU** | Adds speech data for Russian. |
| **IOT\_SPEECHDATA\_ZH\_CN** | Adds speech data for Chinese (Mainland).|
| **IOT\_SPEECHDATA\_ZH\_HK** | Adds speech data for Chinese (Hong Kong SAR). Do not include **IOT_SPEECHDATA_ZH_TW**. |
| **IOT\_SPEECHDATA\_ZH\_TW** | Adds speech data for Chinese (Taiwan). Do not include **IOT_SPEECHDATA_ZH_HK**. |
| ~~IOT\_SPEECHDATA\_EN\_US~~ (Deprecated) | Deprecated in Windows 10, version 1607. Do not add this feature. The default image includes speech data for English (US).|

### Features in the IoT Core Add-Ons

> [!NOTE]
> The packages corresponding to these features are available in source in the iot-adk-addonkit. You can modify them to suit your requirements.

| Features                  | Description                                                          |
|---------------------------|----------------------------------------------------------------------|
| **CUSTOM\_CMD** | Feature to include the oemcustomization.cmd. This is product-specific and picks up the input file from product directory. OEM\_CustomCmd is the deprecated feature ID, can still be used for legacy builds. See [Runtime Customizations](./oscustomizations.md#runtime-customizations)|
| **CUSTOM_BCD** | Includes [BCD settings](./oscustomizations.md#bcd-settings) to suppress boot UX progress display and also enables flight sigining. Modify [Custom.BCD.xml](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Workspace/Common/Packages/Custom.BCD/Custom.BCD.xml) to remove flight signing. |
| **CUSTOM_OOBEAPP** | Includes customizations for the [OOBE App](./oscustomizations.md#oobe-app)  |
| **PROV\_AUTO** | Feature to [add a provisioning package to an image](add-a-provisioning-package-to-an-image.md). This is product specific and picks up the input ppkg file from the product directory OEM\_ProvAuto is the deprecated feature ID, can still be used for legacy builds. See [Runtime customizations](./oscustomizations.md#runtime-customizations)|
| **RECOVERY_BCD** | Includes recovery BCD settings for GPT devices. See [Add a recovery mechanism](recovery-mechanism.md)|
| **RECOVERY_BCD_MBR** | Includes recovery BCD settings for MBR devices. See [Add a recovery mechanism](recovery-mechanism.md)|
| **SEC_BITLOCKER** | Includes the configuration for Bitlocker |
| **SEC_SECUREBOOT** | Includes the retail configuration for Secure Boot |
| **SEC_SECUREBOOT_TEST** | Includes the test configuration for Secure Boot |
| **SEC_DEVICEGUARD** | Includes the retail configuration for DeviceGuard |
| **SEC_DEVICEGUARD_TEST** | Includes the test configuration for DeviceGuard |
| **SETTINGS_HOTKEY** | Feature  to demonstrate how to [add a registry setting to an image](add-a-registry-setting-to-an-image.md). Read [Switching between apps](/windows/iot-core/develop-your-app/iotcoreshell#switching-between-apps-with-hid-injection-keys) for more details.|

### Test features

The following table describes the Microsoft-defined test features that can be used by OEMs in the Features element in the **OEMInput** file for **Test** builds ONLY.

| Features                         | Description                                                                                                               |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **IOT\_BCD\_FLASHMODE\_SETTING** | Enables FFU flashing setting. |
| **IOT\_DISABLE\_TESTSIGNING**    | Disables runtime-installation of test-signed packages.|
| **IOT\_EFIESP\_TEST**            | UEFI packages required for booting test images. Should not be used with **IOT\_EFIESP**.|
| **IOT\_ENABLE\_ADMIN**           | Enables the Administrator account with default password 'p@ssw0rd'.|
| **IOT\_ENABLE\_TESTSIGNING**     | Enables run-time installation of test-signed packages. Allows test-signed drivers and (.appx) apps to run.|
| **IOT\_KD\_ON**                  | Enables Kernel Debugger|
| **IOT\_KDNETUSB\_SETTINGS**      | Includes all kernel debugger transports and enables KDNET over USB. The default debug transport settings for this feature are an IP address of &quot;1.2.3.4&quot;, a port address of &quot;50000&quot;, and a debugger key of &quot;4.3.2.1&quot;. To use the default IP address of 1.2.3.4, run VirtEth.exe with the /autodebug flag.  For example, to establish a kernel debugger connection to the phone, use the command:`Windbg -k net:port=50000,key=4.3.2.1`  **Note** Do not include either **IOT\_KDUSB\_SETTINGS** or **IOT\_KDNETUSB\_SETTINGS** if you need to enable MTP or IP over USB in the image. If the kernel debugger is enabled in the image and the debug transports are used to connect to the device, the kernel debugger has exclusive use of the USB port and prevents MTP and IP over USB from working.|
| **IOT\_KDSERIAL\_SETTINGS**      | Includes all kernel debugger transports and enables KDSERIAL with the following settings: 115200 Baud, 8 bit, no parity. These settings apply to x86 and amd64 platforms. Arm platforms use UEFI-defined serial transport settings.|
| **IOT\_KDUSB\_SETTINGS**         | Includes all kernel debugger transports and enables KDUSB. The default debug transport target name for this feature is **WOATARGET**. To establish a kernel debugger connection to the phone, use the command: `Windbg -k usb:targetname=WOATARGET`. **Note** Do not include either  **IOT_KDUSB_SETTINGS** or **IOT\_KDNETUSB\_SETTINGS** if you need to enable MTP or IP over USB in the image. If the kernel debugger is enabled in the image and the debug transports are used to connect to the device, the kernel debugger has exclusive use of the USB port and prevents MTP and IP over USB from working.|
| **IOT\_WDTF**                    | Includes components for Windows Driver Test Framework, required for HLK validation.|
| **IOT\_DIRECTX\_TOOLS**    | Adds DirectX tools.|
| **IOT\_UMDFDBG\_SETTINGS** | Includes user-mode driver framework debug settings.|
| ~~IOT\_DISABLE\_UMCI~~ (Deprecated)          | Disables the code integrity check. Deprecated in Windows 10, version 1709. |

## Features per release

The following table provides an overview of supported features per IoT Core OS release, listed in alphabetical order.

| Features                                         |1809 (17731.x)|1803 (17134.x)|1709 (16299.x)|1703 (15063.x)|1607 (14393.x)|
|--------------------------------------------------|:------------:|:------------:|:------------:|:------------:|:------------:|
| **IOT\_ALLJOYN\_APP**                            |x|x|x|x|x|
| ~~IOT\_APPLICATIONS~~ (Deprecated)               |N/A|x|x|x| |
| **IOT\_APP\_TOOLKIT**                            |x|x|x|x|x|
| **IOT\_BCD\_FLASHMODE\_SETTING**                 |x| | | | |
| **IOT\_BERTHA**                                  |x|x|x|x|x|
| **IOT\_BLUETOOTH\_A2DP\_SINK**                   |x| | | | |
| **IOT\_BLUETOOTH\_A2DP\_SOURCE**                 |x| | | | |
| **IOT\_BLUETOOTH\_HFP\_AUDIOGATEWAY**            |x| | | | |
| **IOT\_CONTAINERS**                              |x (x64,arm32)|x(x64)|x(x64)| | |
| ~~IOT\_CORTANA~~ (Deprecated)                    |N/A|x|x|x| |
| ~~IOT\_CORTANA\_OBSCURELAUNCH~~ (Deprecated)     |N/A|x|x|x| |
| **IOT\_CP210x\_MAKERDRIVER**                     |x|x|x|x| |
| **IOT\_CRASHCONTROL\_SETTINGS**                  |x|x| | | |
| **IOT\_CRT140**                                  |x|x|x|x|x|
| **IOT\_DIRECTX\_TOOLS**                          |x|x|x|x|x|
| **IOT\_DISABLE\_FLIGHTSIGNING**                  |x|x|x|x|x|
| **IOT\_DISABLE\_TESTSIGNING**                    |x|x|x|x|x|
| ~~IOT\_DISABLE\_UMCI~~ (Deprecated)              |N/A|N/A|N/A|x|x|
| **IOT\_DISABLEBASICDISPLAYFALLBACK**             |x|x|x|x|x|
| **IOT\_DMAP\_DRIVER**                            |x|x|x|x|x|
| **IOT\_EFIESP**                                  |x|x|x|x|x|
| **IOT\_EFIESP\_BCD**                             |x|x|x|x|x|
| **IOT\_EFIESP\_BCD_MBR**                         |x|x|x|x| |
| **IOT\_EFIESP\_TEST**                            |x|x|x|x|x|
| **IOT\_ENABLE\_ADMIN**                           |x|x|x|x|x|
| **IOT\_ENABLE\_FLIGHTSIGNING**                   |x|x|x|x|x|
| **IOT\_ENABLE\_TESTSIGNING**                     |x|x|x|x|x|
| **IOT\_FFU\_FLASHMODE**                          |x(arm)|x(arm)| | | |
| **IOT\_FONTS\_CHINESE\_EXTENDED**                |x|x|x|x| |
| **IOT\_FTSER2K\_MAKERDRIVER**                    |x|x|x|x|x|
| ~~IOT\_GENERIC\_POP~~ (Deprecated)               |N/A|x|x|x|x|
| ~~IOT\_HWN\_CLASS\_EXTENSION~~ (Deprecated)      |N/A|N/A|N/A|x| |
| **IOT\_HEADLESS\_CONFIGURATION**                 |x| | | | |
| **IOT\_KD\_ON**                                  |x|x|x|x|x|
| **IOT\_KDNETUSB\_SETTINGS**                      |x|x|x|x|x|
| **IOT\_KDSERIAL\_SETTINGS**                      |x|x|x|x|x|
| **IOT\_KDUSB\_SETTINGS**                         |x|x|x|x|x|
| **IOT\_MIRACAST\_RX\_APP**                       |x|x| | | |
| **IOT\_MTP**                                     |x|x| | | |
| **IOT\_NANORDPSERVER**                           |x|x|x|x|x|
| ~~IOT\_NETCMD~~ (Deprecated)                     |N/A|N/A|N/A|x|x|
| **IOT\_NARRATOR**                                |x| | | | |
| **IOT\_OCR\_ALL\_LANGS**                         |x| | | | |
| **IOT\_OCR\_EN_US**                              |x| | | | |
| **IOT\_ONBOARDING\_APP**                         |x|x|x| | |
| **IOT\_POWER\_SETTINGS**                         |x|x|x|x|x (x86/x64)|
| **IOT\_POWERSHELL**                              |x|x|x|x|x|
| **IOT\_SHELL\_HOTKEY\_SUPPORT**                  |x|x|x|x|x|
| **IOT\_SHELL\_ONSCREEN\_KEYBOARD**               |x|x|x|x| |
| **IOT\_SHELL\_ONSCREEN\_KEYBOARD\_FOLLOWFOCUS**  |x|x|x|x| |
| **IOT\_SIREP**                                   |x|x|x|x|x|
| **IOT\_SPEECHDATA\_AR\_SA**                      |x| | | | |
| **IOT\_SPEECHDATA\_DE\_DE**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_EL\_GR**                      |x| | | | |
| **IOT\_SPEECHDATA\_EN\_CA**                      |x|x|x|x| |
| **IOT\_SPEECHDATA\_EN\_GB**                      |x|x|x|x|x|
| ~~IOT\_SPEECHDATA\_EN\_US~~ (Deprecated)         |N/A|N/A|N/A|N/A|x|
| **IOT\_SPEECHDATA\_ES\_ES**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_ES\_MX**                      |x|x|x|x| |
| **IOT\_SPEECHDATA\_FR\_CA**                      |x|x|x|x| |
| **IOT\_SPEECHDATA\_FR\_FR**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_IT\_IT**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_JA\_JP**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_KO\_KR**                      |x| | | | |
| **IOT\_SPEECHDATA\_NL\_NL**                      |x| | | | |
| **IOT\_SPEECHDATA\_PL\_PL**                      |x| | | | |
| **IOT\_SPEECHDATA\_PT\_BR**                      |x| | | | |
| **IOT\_SPEECHDATA\_PT\_PT**                      |x| | | | |
| **IOT\_SPEECHDATA\_RO\_RO**                      |x| | | | |
| **IOT\_SPEECHDATA\_RU\_RU**                      |x| | | | |
| **IOT\_SPEECHDATA\_ZH\_CN**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_ZH\_HK**                      |x|x|x|x|x|
| **IOT\_SPEECHDATA\_ZH\_TW**                      |x|x|x|x|x|
| **IOT\_SSH**                                     |x|x|x|x|x|
| **IOT\_TOOLKIT**                                 |x|x|x|x|x|
| **IOT\_UAP\_DEFAULTAPP**                         |x|x|x|x|x|
| **IOT\_UAP\_OOBE**                               |x|x|x|x|x|
| **IOT\_UMDFDBG\_SETTINGS**                       |x|x|x|x|x|
| **IOT\_UNIFIED\_WRITE\_FILTER**                  |x|x|x|x|x|
| **IOT\_USBFN\_CLASS\_EXTENSION**                 |x|x|x|x|x|
| **IOT\_WDTF**                                    |x|x|x|x|x|
| **IOT\_WEBB\_EXTN**                              |x|x|x|x|x|

## Related topics

[What's in the Windows ADK IoT Core Add-ons](iot-core-adk-addons.md)

[IoT Core manufacturing guides](iot-core-manufacturing-guide.md)
