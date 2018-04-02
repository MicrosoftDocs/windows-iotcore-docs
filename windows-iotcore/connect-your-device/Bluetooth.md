---
title: Bluetooth Support
author: zhuridartem
ms.author: artemz
ms.date: 08/28/2017
ms.topic: article
description: Learn how to leverage Bluetooth for devices running Windows 10 IoT Core.
keywords: windows iot, bluetooth, bluetooth support, devices, device portal
---

# Bluetooth Support
Windows 10 IoT Core supports Bluetooth 4.0. A list of supported Bluetooth dongles can be found in the [Hardware Compatibility List](../learn-about-hardware/HardwareCompatList.md).

# About Bluetooth
TThere are two different bluetooth technologies that you can choose to implement in your app:

## Classic Bluetooth (RFCOMM)
Before Bluetooth LE, devices commonly used this protocol to communicate using Bluetooth. This protocol is simple and useful for device-to-device communication without the need of energy savings. . Connectivity requires pairing.

## Bluetooth Low-Energy (BLE/LE)
Bluetooth Low Energy (LE) is a specification that defines protocols for discovery and communication between devices that have an efficient energy usage requirement. For more information including code samples, As per recent builds, a device can connect to to a BLE device without pairing.

## Supported Bluetooth Profiles
Windows 10 IoT Core supports the following Bluetooth profiles:

1.  [Human Interface Device Profiles Concepts (HID)]
An HID device takes input from a human and presents output for human consumpation. Examples are keyboard, mouse, game controller, barcode reader,  LED, alphanumeric display. An IoT Core device can connect to an HID device over Bluetooth. See the general topic about HID in the Windows context: [Introduction to HID Concepts](https://docs.microsoft.com/en-us/windows-hardware/drivers/hid/introduction-to-hid-concepts).

2.  Radio Frequency Communication (RFCOMM)
RFCOMMM is the underlying serial communications for Classic Bluetooth. With UWP apps, the following RFCOMM services are supported via the name value:
- serialPort
- obexObjectPush
- obexFileTransfer
- phoneBookAccessPce
- phoneBookAccessPse
- genericFileTransfer
Note that you need to manually specify these in the AppManifest.   
See the [UWP-Bluetooth RFCOMM](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/send-or-receive-files-with-rfcomm.md) topic. Also see the [UWP-Bluetooth Rfcomm Chat Sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BluetoothRfcommChat.md)

3. Generic Attribute Profile (GATT)
See the [UWP-Bluetooth Low Energy](lhttps://docs.microsoft.com/en-us/windows/uwp/devices-sensors/bluetooth-low-energy-overview) topic. 

## Connecting Bluetooth devices using the device portal
When using one of the [Windows 10 IoT Core Release Image](https://developer.microsoft.com/en-us/windows/iot/downloads) Bluetooth devices can be paired with the Windows IoT Core device using the device portal. When navigating to the Bluetooth tab the device will look for Bluetooth devices and will also be discoverable to other Bluetooth devices. The picture below shows an incoming pairing request. 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_2.png)

After the device is successfully paired it will be listed under the paired device section 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_3.png)
