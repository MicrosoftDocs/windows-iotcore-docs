---
title: Arduino Wiring for Windows IoT Core Devices
author: msalehmsft
ms.author: msaleh
ms.date: 09/06/17      
ms.topic: article
description: Learn how to create, deploy, and debug Arduino Wiring sketches on supported Windows IoT Core devices.
keywords: windows iot, Arduino, Arduino Wiring, template, IoT Core, UWP
---

# Arduino Wiring for Windows IoT Core Devices

To enable the development and reuse of the familiar [Arduino Wiring](https://www.arduino.cc/en/Reference/HomePage) sketches on IoT Core devices, a Visual Studio project template for Arduino Wiring is provided as part of the [Windows IoT Core Project Templates extension](https://go.microsoft.com/fwlink/?linkid=847472).

The Arduino Wiring project template enables developers and makers to create, deploy and debug Arduino Wiring sketches on supported IoT Core devices using the same Arduino Wiring language semantics and constructs available on Arduino platforms. Not only this can help port existing Arduino sketches to IoT Core with very little cost, but Arduino Wiring sketches running on IoT Core are full Windows 10 apps that can make use of the Univeral Windows Platform (UWP) API. So, Arduino Wiring sketches have full access to APIs such as communication, data access, networking, graphics, among many others, which can be used to create end to end scenarios running on Windows 10 IoT Core devices. For more information on developing Universal Windows Platform (UWP) Apps, please refer to [Building Applications for Windows 10 IoT Core](../develop-your-app/BuildingAppsForIoTCore.md) as well as the [FAQ](https://developer.microsoft.com/en-us/windows/iot/support/faqs) page.

Additionally, Arduino Wiring sketches make use of a direct memory mapped driver that offers high performance on supported devices. For more details on performance details, please refer to the [Windows IoT Lightning Performance Testing](../develop-your-app/LightningPerformance.md) report.

To start building Arduino Wiring projects for Raspberry Pi2, Pi3 or Minnowboard Max, please refer to the [Arduino Wiring project guide](ArduinoWiringProjectGuide.md).

> [!NOTE]
> Arduino Wiring is *not* currently supported on DragonBoard 410c.
