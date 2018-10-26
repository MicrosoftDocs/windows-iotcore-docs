---
title: Using WiFi on your Windows 10 IoT Core device
author: derekameer
ms.author: demeer
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use, setup, and configure wifi on your Windows 10 IoT Core device.
keywords: windows iot, wifi, setup, devices
---

# Using WiFi on your Windows 10 IoT Core device

WiFi is supported on Windows 10 IoT Core devices through the use of a USB WiFi adapter. Using WiFi provides all the functionality of a wired connection,
including [SSH](../connect-your-device/SSH.md), [Powershell](../connect-your-device/PowerShell.md), [Windows Device Portal](../manage-your-device/DevicePortal.md), and application debugging and deployment.

> [!NOTE]
> Plugging in a wired Ethernet cable will override WiFi as the default network interface.

### Supported Adapters
A list of WiFi adapters that have been tested on Windows 10 IoT Core can be found on our [Supported Hardware](../learn-about-hardware/HardwareCompatList.md) page.

### Configuring WiFi
To use WiFi, you'll need to provide Windows 10 IoT core with the WiFi network credentials. In addition to documentation on how to build companion app and WPS custom solutions, there are a few different options for doing so listed below.

## Custom Companion App & WPS Wi-Fi Onboarding Samples

Currently, we offer a number of ways for developers to build a custom wifi onboarding solution for thier device. 

> | Samples | Description | Benefits  |  Drawbacks  |
> |-------------|----------|---------|---------|
> | [Companion App](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/CompanionApp) | Create a simple Xamarin app that can configure your device's Wi-Fi. |  Simple to use; Headed or headless for IoT Core; Clients work cross-platform | Developer is creating his or her own protocol; requires developer to implement security |
> | [IoT Onboarding with Bluetooth RFCOMM](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTOnboarding_RFCOMM) | Create solution to configure your headless IoT device to connect with your Wi-Fi using Bluetooth RFCOMM.  | Relevant in headed or headless devices; Uses familiar technologies and concepts; Does not require IoT device to start a SoftAP; Does not need to adjust firewall settings | Requires Bluetooth support for client and server devices; Sample only provides client app for Windows 10; Server app pre-defines/hard-codes the names of the client device. |
> | [IoT Onboarding with AllJoyn](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTOnboarding) | Remotely join your headless IoT device with your home Wi-Fi network. | Works with AllJoyn | Some support for AllJoyn is deprecated |
> | Wi-Fi Protected Setup (WPS) APIs for devices | Perform WPS discovery to query the WPS methods supported by the network. | Simply leverage the [WiFiAdapter.GetWpsConfigurationAsync(WiFiAvailableNetwork](https://docs.microsoft.com/en-us/uwp/api/windows.devices.wifi.wifiadapter.getwpsconfigurationasync) and [WiFiAdapter.ConnectAsync](https://docs.microsoft.com/en-us/uwp/api/windows.devices.wifi.wifiadapter.connectasync) methods to connect wi-fi devices to specific networks. | You will need to become familiar with these APIs to leverage them.; only compatible with WPS-enabled routers|

## Headed Options:

### Option 1: Startup Configuration
**Prerequisite:** The Windows 10 IoT core device needs a mouse, keyboard, display, and USB WiFi Adapter plugged in

The first time you boot Windows 10 IoT Core with a supported USB WiFi adapter, you will be presented with a configuration screen.
On the configuration screen, select the WiFi network you would like to connect to and supply the password. Click **connect** to initiate the connection.

![Startup WiFi Configuration Screen](../media/SetupWiFi/WiFiStartupConfig.png)

### Option 2: Default App Configuration
**Prerequisite:** The Windows 10 IoT core device needs a mouse, keyboard, display, and USB WiFi Adapter plugged in

An alternative way to configure WiFi is to use the default app. You can use this to configure or modify WiFi settings after the device has booted.

1. Click on the gear-shaped settings icon on the homepage
2. Select **Network & Wi-Fi** in the left pane
3. Click on the WiFi network you want to connect to. Supply the password if prompted, and click **Connect**

![Default App WiFi Configuration](../media/SetupWiFi/DefaultAppWiFiConfig.png)

## Headless Options:




### Option 1: Web-Based Configuration
**Prerequisite:** Your device will already need to be connected to your local network through Ethernet and should have a USB WiFi Adapter plugged in

If you have device a with no UI, display, or input devices, you can still configure it through the [Windows Device Portal](../manage-your-device/DevicePortal.md).
In **Windows 10 IoT Core Dashboard**, *Click* on the **Open in Device Portal** icon for your device.

<!-- This content is replicated at en-US/Docs/KitSetupRPI.md -->

1. Enter **Administrator** for the username, and supply your password (p@ssw0rd by default)
2. Click on **Network** in the left-hand pane
3. Under **Available networks**, select network you would like to connect to and supply the connection credentials. Click **Connect** to initiate the connection

![Web Based WiFi Configuration](../media/SetupWiFi/WebBWiFiConfig.png)

<!-- End of Replicated Content -->


### Option 2: Connect using WiFi Profiles

**Prerequisite:** Your device will already need to be connected to your local network through Ethernet and should have a USB WiFi Adapter plugged in. You also need a Windows PC with WiFi capability.

Setting up WiFi using wireless profiles is supported in Windows 10 IoT Core. See [MSDN](https://msdn.microsoft.com/en-us/library/windows/desktop/aa369853) for details and examples.

1. Connect your Windows PC to the desired wireless network and create WiFi profile XML file with these commands:

    * `netsh wlan show profiles` -> find the name of the profile you just added

    * `netsh wlan export profile name=<your profilename>`. This will export the profile to an XML file

2. Open up a **File Explorer** window, and in the address bar type `\\<TARGET_DEVICE>\C$\` and then hit enter.  In this particular case, `<TARGET_DEVICE>` is either the name or the IP address of your Windows 10 IoT Core device:

    ![SMB with File Explorer](../media/SetupWifi/smb1.png)

    If you are prompted for a user name and password, use the following credentials:

        User Name: <TARGET_DEVICE>\Administrator
        Password:  p@ssw0rd

    ![SMB with File Explorer](../media/SetupWifi/cred1.png)

> [!NOTE]
> It is **highly recommended** that you update the default password for the Administrator account.  Please follow the instructions found [here](../connect-your-device/PowerShell.md).

3. Copy the exported WiFi profile XML file from the Windows PC to your Windows 10 IoT Core device

4. Connect to your device using [PowerShell](../connect-your-device/PowerShell.md) and add the new WiFi profile to your device by executing the following commands

    * `netsh wlan add profile filename=<copied XML path>`

    * `netsh wlan show profiles`

5. Connect the Windows 10 IoT Core device to wireless network via netsh

    * `netsh wlan connect name=<profile name>`

6. Verify that your device is connected to the wireless network and can reach the internet

    * `netsh wlan show interfaces`

    * `ipconfig /all`

    * `ping /S <your WiFi adapter ip address> bing.com`


#### Connecting to WPA2-PSK Personal networks

If you need to connect to a WPA2-PSK Personal WiFi network, follow the instructions above first, but make the following changes to the XML file. The only difference is that when your Windows PC exports the XML it encrypts the password.

> [!WARNING] 
> This will make your connection insecure.

Profile XML exported from Windows PC:

    <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>true</protected>
        <keyMaterial><Your Encrypted password></keyMaterial>
    </sharedKey>


Changes needed to work on Windows 10 IoT Core:

    <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>false</protected>
        <keyMaterial><Your Unencrypted password></keyMaterial>
    </sharedKey>
