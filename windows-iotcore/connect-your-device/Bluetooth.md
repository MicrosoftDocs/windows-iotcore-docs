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

## Supported Bluetooth Profiles
IoT Core supports the following Bluetooth profiles:

1.  Human Interface Device Profile **HID**  [HID Concepts](https://docs.microsoft.com/en-us/windows-hardware/drivers/hid/introduction-to-hid-concepts)

2.  Radio Frequency Communication **RFCOMM**

3.  Generic Attribute Profile **GATT**  [GATT Specification on Bluetooth.org](https://www.bluetooth.com/specifications/gatt/generic-attributes-overview)

## Connecting Bluetooth devices using the device portal
When using one of the [Windows 10 IoT Core Release Image](https://developer.microsoft.com/en-us/windows/iot/downloads) Bluetooth devices can be paired with the Windows IoT Core device using the device portal. When navigating to the Bluetooth tab the device will look for Bluetooth devices and will also be discoverable to other Bluetooth devices. The picture below shows an incoming pairing request. 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_2.png)

After the device is successfully paired it will be listed under the paired device section 

![Bluetooth Incoming Pairing](../media/Bluetooth/Portal_BT_3.png)
