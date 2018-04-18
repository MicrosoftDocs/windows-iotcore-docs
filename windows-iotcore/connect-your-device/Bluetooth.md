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

## About Bluetooth
There are two different bluetooth technologies that you can choose to implement in your app:

* Classic Bluetooth (RFCOMM)
Before Bluetooth LE, devices commonly used this protocol to communicate using Bluetooth. This protocol is simple and useful for device-to-device communication without the need of energy savings. Connectivity requires pairing.

* Bluetooth Low-Energy (BLE/LE)
Bluetooth Low Energy (LE) is a specification that defines protocols for discovery and communication between devices that have an efficient energy usage requirement. For more information including code samples, As per recent builds, a device can connect to to a BLE device without pairing.

## Supported Bluetooth Profiles
Windows 10 IoT Core supports the following Bluetooth profiles:

1.  **Human Interface Device Profiles Concepts (HID)**
An HID device takes input from a human and presents output for human consumpation. Examples are keyboard, mouse, game controller, barcode reader, LED, and alphanumeric display. A Windows 10 IoT Core device can connect to an HID device over Bluetooth. See the general topic about HID in the Windows context: [Introduction to HID Concepts](https://docs.microsoft.com/en-us/windows-hardware/drivers/hid/introduction-to-hid-concepts). 

2.  **Radio Frequency Communication (RFCOMM)**
RFCOMMM is the underlying serial communications for Classic Bluetooth. With UWP apps, the following RFCOMM services are supported:

* serialPort
* obexObjectPush
* obexFileTransfer
* phoneBookAccessPce
* phoneBookAccessPse
* genericFileTransfer

> [!NOTE]
> You will need to manually specify these in the AppManifest.  See the [UWP-Bluetooth RFCOMM](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/send-or-receive-files-with-rfcomm) topic. Also see the [UWP-Bluetooth Rfcomm Chat Sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BluetoothRfcommChat) topic.

3. **Generic Attribute Profile (GATT)**
See the [UWP-Bluetooth Low Energy](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/bluetooth-low-energy-overview) topic. 

## Connecting Bluetooth devices using the device portal
When using one of the [Windows 10 IoT Core Release Image](https://developer.microsoft.com/en-us/windows/iot/downloads) Bluetooth devices can be paired with the Windows IoT Core device using the device portal. When navigating to the Bluetooth tab the device will look for Bluetooth devices and will also be discoverable to other Bluetooth devices. The picture below shows an incoming pairing request. 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_2.png)

After the device is successfully paired it will be listed under the paired device section 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_3.png)

## Bluetooth Onboarding

Currently, we offer three different ways of allowing users to go about wifi onboarding. We've documented the benefits and drawbacks for each method of onboarding. 

> | Samples | Description | Benefits  |  Drawbacks  |
> |-------------|----------|---------|
> | [Companion App](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/CompanionApp) | Create a simple app that can configure your device's Wi-Fi. | * Simple * Headed or headless for IoT Core Server * Doesn't require AllJoyn # Clients work across device types | * User is creating his or her own protocol * Insecure, needs customer to implement security |
> | [IoT Onboarding with Bluetooth RFCOMM](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTOnboarding_RFCOMM) | Create solution to configure your headless IoT device to connect with your Wi-Fi using Bluetooth RFCOMM.  | * Designed for headless devices * Familiar technologies and concepts used * Does not require IoT device to start a SoftAP first * Does not need to adjust firewall settings | * Requires Bluetooth support for client and server devices * Sample only proivdes client app for Windows 10 * Server app pre-defines/hard-codes the names of the client device. |
> | [IoT Onboarding with AllJoyn](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTOnboarding) | Remotely join your headless IoT device with your home Wi-Fi network. | * Works with AllJoyn | * Some support for AllJoyn is deprecated |

