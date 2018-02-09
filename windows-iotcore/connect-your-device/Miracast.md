---
title: Miracast on IoT Core 
author: derekameer
ms.author: demeer
ms.date: 11/30/2017
ms.topic: article
description: Learn how to include Miracast capabilities on your device 
keywords: windows iot, miracast, connectivity 
---
# Miracast on IoT Core

This document will show you how to include Miracast functionality on your IoT Core device.

> [!IMPORTANT]
> This feature is only available on Insider Build 17093 and above

## Miracast Overview

A Miracast connection is made up of two components: the Source and the Sink. The **Miracast Source** sends content to the **Miracast Sink**, which displays the content. To create the connection, the Sink advertises itself to the connected Wi-Fi network. The Source uses the **Device Picker** to select the Sink and request a connection. Once the connection is requested, a user at the Sink receives an alert that the source is attempting to make a connection and must verify that the connection should take place. Once this happens, the Source begins casting to the Sink until either the Source cancels the connection or the Sink stops advertising.

## Hardware requirements

Both Source and Sink devices require Miracast-compatible Wi-Fi and Graphics drivers and chipsets to function properly. To find out if your device has Miracast-compatible hardware, run 
```
netsh wlan show driver
```
in the device's command prompt.

If the device supports Miracast, you should see the output below:

![Compatible Device Output](../media/Miracast/CompatibleDevice.png)

The below table shows Miracast compatibility for the IoT Core reference platforms:

| Board | SoC | WiFi Drivers Present | Graphics Drivers Present | Miracast-Compatible |
|-------|-----|----------------------|--------------------------|---------------------|
| Qualcomm Dragonboard 410c | Snapdragon 410 | Yes | Yes | Yes |
| Raspberry Pi 2/3 | Broadcom BCM283x | Yes | No | No |
| Minnowboard Max | Intel Atom E3825 | Yes | No | No |
| UP Squared | Intel Celeron N3350 | Yes | Yes | Yes |


### Wi-Fi

The Wi-Fi driver and chipset for the device must support Wi-Fi Direct, among other capabilities, to support Miracast. If your device does not have these features, you can use a USB Wi-Fi dongle instead. We recommend the [300M Wireless USB Adapter](http://a.co/fdhEhV9).

### Graphics

The Graphics driver and chipset must support h.264 encoding and decoding to support Miracast. If your device does not have a compatible graphics driver and/or chipset, you will have to pick a new device. Please consult the above matrix when choosing a Miracast-compatible device.

## Windows IoT as a Miracast Sink

To enable your device as a Miracast sink, you will need to enable the Connect app on your device, then enable Miracast in the registry.

### Enable the Connect App

To enable the Connect app, you'll need to include the **IOT_MIRACAST_RX_APP** feature to your image. You'll also need to include 
**Microsoft-Connect-Package.cab** and **Microsoft-Connect-Package_Lang_XXXX.cab** in your image (where XXXX is a language, i.e. "enUS"). See [this page](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/deploy-your-app-with-a-standard-board#update-the-feature-manifest) for more details about how to add features and packages to your image. You will also need to add the 

### Enable Miracast

Connect to your device through [PowerShell](https://docs.microsoft.com/en-us/windows/iot-core/connect-your-device/powershell) or the [Windows Device Portal](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/deviceportal) and run the following commands:
```
reg add HKLM\Software\Microsoft\PlayToReceiver /v AutoEnabled /t REG_DWORD /d 1  
reg add HKLM\Software\Microsoft\MiracastReceiver /v  ConsentToast /t REG_DWORD /d 0  
reg add HKLM\Software\Microsoft\MiracastReceiver /v NetworkQualificationEnabled /t REG_DWORD /d 1  
reg add HKLM\Software\Microsoft\MiracastReceiver /v EnabledOnACOnly /t REG_DWORD /d 1  
```
This will enable Miracast without a consent notification, only on secure networks, and only while connected to A/C power. This is the recommended way to run a Miracast receiver on IoT Core.

## Windows IoT as a Miracast Source

> [!IMPORTANT]
> Before trying to use your device as a Miracast Source, please turn off the IoTOnboardingTask app from the [Windows Device Portal](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/deviceportal) as shown below, which you'll only need to do once:
> ![Turn off IoTOnboardingTask app](../media/Miracast/IoTOnboardingOff.gif)
> Afterwards, please restart the device

You can set up Miracast casting on your compatible device through public APIs from the `Windows.Media.Casting` namespace in your app.

To see these APIs in action, download the [BasicMediaCasting UWP sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicMediaCasting) and run it on your device. The APIs in the sample cover the following scenarios, all of which run on Miracast-compatible IoT Core devices:
1. Basic Media Casting, which uses the built-in casting to send content to Miracast, DLNA, and Bluetooth devices
2. Casting Using the Casting Picker, which allows you to further customize the Device Picker
3. Casting Using a Custom Picker, which illustrates how to build custom UX for selecting devices

> [!NOTE]
> Some Miracast sinks (Surface Laptop, Surface Hub, PC with a Wireless Display Adapter) are incompatible with IoT Core casting devices. We recommend using the [Microsoft Wireless Display Adapter](https://www.microsoft.com/accessories/en-us/products/adapters/wireless-display-adapter-2/p3q-00001) with a compatible monitor as your Miracast sink.
