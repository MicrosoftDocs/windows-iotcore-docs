---
title: OS Customizations
author: parameshbabu
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
description: Learn how to customize the Windows 10 IoT Core OS.
keywords: windows iot, image creation, image customizations, OEM customizations
---

# OS Customizations for OEM
OEM can customize various aspects of the OS using the below specified methods.

## OOBE App
IoTCore has an inbox OOBE App that runs when the device boots up for the first time. This is shown until all the provisioning packages are processed in the background and an OEM App is available to be launched as a startup app.

This OOBE app can be customised with a `settings.json` with the following attributes:

- backgroundColor : Screen background color 
- background : Background image (jpg file)
- progressRingVisible : Spinning dots can be shown or hidden
- welcomeText : Text displayed in large font at the center of the screen
- pleaseWaitText : Text displayed below the spinning dots
- animation : Animation gif can be specified here
- animationMargin : Positioning of the animation gif
    - left , top , right, bottom

All files referenced in the settings.json should be in the same folder as the settings.json file.
A sample snippet is given below

```
{
"backgroundColor":  "#FF0000FF",
"progressRingVisible": true,
"welcomeText": "Welcome to OOBE customization",
"pleaseWaitText": "please wait ..."
}
```

Note that the settings.json file needs to be encoded in Unicode (UCS-2) encoding. UTF-8 will not work.

### Validate settings manually 

1. Author the `settings.json` file with your required settings
2. Connect to the IoT device ([using SSH](../connect-your-device/SSH.md) or [using Powershell](../connect-your-device/powershell.md)) and place the `settings.json` file along with all graphical assets in a directory, say `C:\Data\oobe`
3. Configure the device to allow access to this directory from all appx files, using

    ```
    folderpermissions C:\Data\oobe -e
    ```

4. Launch the OOBE application using

    ```
    iotstartup add headed IoTUAPOOBE
    ```

5. Verify the user interface

### Add settings to IoT Core image

1. Use [Custom.OOBEApp](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Custom.OOBEApp) package and modify the package xml file to add your graphical assets

2. Copy your settings.json and graphical assets to that package folder.

3. In the oemcustomizations.cmd file, add  `folderpermissions 
    C:\Data\oobe -e` , to ensure that this is called at the system boot.

4. In the OEMInput.xml, include the feature id **CUSTOM_OOBEAPP**, note that this is defined in the OEMCOMMONFM.xml.


## Crash Settings

For IoT Core products, it is recommended that you configure your devices to reboot on crash and also hide the crash dump screen (BSOD). 
This is achieved with setting the following registry keys:

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\CrashControl
        AutoReboot set to 1
        DisplayDisabled set to 1
    ```

### Validate settings manually

1. Connect to your IoT device ([using SSH](../connect-your-device/SSH.md) or [using Powershell](../connect-your-device/powershell.md)) and set the following registry keys

    ```
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl" /v AutoReboot /t REG_DWORD /d 1 /f
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl" /v DisplayDisabled /t REG_DWORD /d 1 /f
    ```

2. See [Forcing a System Crash from the keyboard](https://docs.microsoft.com/windows-hardware/drivers/debugger/forcing-a-system-crash-from-the-keyboard) and configure a key to force the system crash.
3. Force a system crash using the configured key and verify that the device reboots automatically and does not show the crashdump screen.

### Add settings to IoT Core image

1. Use [Custom.Settings](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Custom.Settings) package
2. In the OEMInput.xml, include the feature id **CUSTOM_SETTINGS**, note that this is defined in the OEMCOMMONFM.xml.

## BCD Settings
Boot Configuration Database settings can be used to configure various features. See [BCDEdit Command-LineOptions](https://docs.microsoft.com/windows-hardware/manufacture/desktop/bcdedit-command-line-options) for the various settings and options available.

A few key features are listed below

### Disable Boot UX animation 

1. Manual setting can be done with the below command

    ```
    bcdedit -set {bootmgr} nobootuxprogress true
    ```

2. Specify this setting in a `Custom.BCD.xml` file 

    ```xml
    <?xml version='1.0' encoding='utf-8' standalone='yes'?>
    <BootConfigurationDatabase 
           xmlns="http://schemas.microsoft.com/phone/2011/10/BootConfiguration"
           xmlns:xsd="http://www.w3.org/2001/XMLSchema"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           IncludeDescriptions="true" IncludeRegistryHeader="true">
           <Objects>
                <!-- Windows Boot Manager -->
              <Object SaveKeyToRegistry="false">
                <FriendlyName>Windows Boot Manager</FriendlyName>
                <Elements>
                    <Element>
                    <DataType>
                      <WellKnownType>Boot UX Progress Animation Disable</WellKnownType>
                    </DataType>
                    <ValueType>
                      <BooleanValue>true</BooleanValue>
                    </ValueType>
                    </Element>
                </Elements>
              </Object>
            </Objects>
        </BootConfigurationDatabase>
        ```
3. Include this setting in the image using [Custom.BCD](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Custom.BCD) package and add feature id **CUSTOM_BCD** to OEMInput.xml file

### Replacing the Boot Logo
There are multiple ways to replace the boot logo that is displayed by the BIOS or UEFI.
One way is to license the UEFI, or pay a board manufacturer vendor to do so, and make changes directly to the UEFI source code.
Alternatively, on devices whose UEFI implementation supports signed loadable UEFI drivers there is a sample here:
https://github.com/Microsoft/MS_UEFI/tree/share/MsIoTSamples
that shows how to build a driver that replaces the boot logo and supply a BGRT table to bootmgr so that the Windows boot process leaves your logo in place during boot instead of replacing it with the Windows logo.

### Enable Flight Signing

1. Manual setting can be done with the below commands:

    ```
    bcdedit /set {bootmgr} flightsigning on
    bcdedit /set flightsigning on
    ```

2. To include this setting in the image, you can add the below fragment to the `Custom.BCD.xml`

    ```xml
        <!--  Allow Flight Signing Certificate -->
        <Object SaveKeyToRegistry="false">
         <FriendlyName>Global Settings Group</FriendlyName>
         <Elements>
          <Element>
            <DataType>
              <WellKnownType>Allow Flight Signatures</WellKnownType>
            </DataType>
            <ValueType>
              <BooleanValue>true</BooleanValue>
            </ValueType>
          </Element>
         </Elements>
        </Object>
    ```

## Runtime customisations
In addition to the static customisations discussed above, you can also customize during the runtime.

1. `OEMCustomizations.cmd`
    - This command file is invoked by IoTCore Shell on every boot with system privileges, placed in `c:\windows\system32`
    - You can specify any customization actions here in this cmd file, though it is recommended to keep this as a last resort option for customizations
    - In the iot-adk-addonkit, this file is created for each product under the product directory. Add feature id **CUSTOM_CMD** in the OEMInput xml file to include this in the image.
    - See [Custom.Cmd](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Custom.Cmd) package and [sample oemcustomizations.cmd](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/Products/SampleA/oemcustomization.cmd) 
2. `Customizations.xml`
    - This is the settings file used to create the provisioning package
    - To automatically process this provisioning package at boot time, this package is placed in `c:\windows\provisioning\packages`
    - In the iot-adk-addonkit, this file is created for each product under the product directory. Add feature id **PROV_AUTO** in the OEMInput xml file to include this in the image.
    - See [Provisioning.Auto](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Common/Packages/Provisioning.Auto) package and [sample Customizations.xml](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Source-arm/Products/SampleA/prov/customizations.xml)
    - For more details, refer to:
        - [Add a provisioning package](https://docs.microsoft.com/windows-hardware/manufacture/iot/add-a-provisioning-package-to-an-image)
        - [Provisioning](https://aka.ms/iotcsplist) for supported Configuration Service Providers (CSPs) in IoT Core

