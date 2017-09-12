---
title: AllJoyn Device System Bridge overview
author: saraclay
ms.author: saclayt
ms.date: 09/06/17
ms.topic: article
ms.prod: Windows
ms.technology: IoT
description: Learn about the AllJoyn Device System Bridge, which adapts non-AllJoyn devices to the AllJoyn ecosystem for broader interoperability.
keywords: windows iot, AllJoyn
---

> [!NOTE]
> You are viewing archived documentation. AllJoyn is no longer supported by Windows 10 IoT. For questions, please open an issue on GitHub or leave us feedback in the comments below.

# AllJoyn Device System Bridge

AllJoyn provides developers with the flexibility to use a wide range of platforms and connection technologies to build  devices for the AllJoyn ecosystem.  However, many device makers have existing device solutions in their portfolios. For these situations, Microsoft created the Device System Bridge (DSB). The DSB adapts non-AllJoyn devices to the AllJoyn ecosystem so that the adapted devices can interoperate with AllJoyn as their common language. Microsoft DSB’s support home automation systems such as Zigbee, and Z-Wave, and can even support industrial building automation systems such as BACnet.  Additionally, the source code is available for customization to support other technologies

## How DSB works

The key capability of a DSB is to create a virtual representation of devices on the AllJoyn bus. So these devices, whatever their native connectivity or device ecosystem is, will appear and be accessible as AllJoyn devices. In the picture below two DSBs , one for Z-Wave and one for ZigBee create virtual representation of the two Z-Wave and the one ZigBee devices on the AllJoyn bus. With this all devices on the AllJoyn site can communicate with each other. Because the Z-Wave and ZigBee devices all on the AllJoyn bus they now can communicate with each other as well.

![AJ_Docu_DSB_Overview](../media/AllJoyn/AJ_Docu_DSB_Overview.png)

Another key element of the DSB design is that it will not require any changes to the AllJoyn or non-AllJoyn device system. All necessary adoptions are done in the DSB.

As the picture also shows, there is no mapping from AllJoyn devices to the non-AllJoyn side. The objective of the DSB is to bring devices into the AllJoyn ecosystem. Enabling only one way simplifies the development. It also reduces the risk that AllJoyn security capabilities become weakened by the potentially less secure non-AllJoyn device system.

## DSB Architecture

The Microsoft proposed DSB architecture consists of three main components, Network Access Stack, Adapter and Bridge. The picture below shows the high level overview of this architecture.

![AJ_Docu_DSB_Architecture](../media/AllJoyn/AJ_Docu_DSB_Architecture.png)

### Bridge
* Represents each internal device object as AllJoyn device, separate bus attachment for each device
* Devices are dynamically added to or removed from the AllJoyn bus
* Configuration manages device visibility and security
* Creates bus attachment for bridge and adapter configuration interface
* Bridge code is agnostic to internal device types and reusable for any type

### Adapter
* Instantiates and manages virtual devices on behalf of each device from the non-AllJoyn network
* Translates device schemas into internal device objects
* Manages network resources, e.g. access keys, credentials

### Network Access Stack
* Access to non-AllJoyn Network specific , e.g. Z-Wave stack

## Adapter Classes

The diagram below show the classes developers will use in the Microsoft DSB template to create an abstraction of the native devices that need to be bridged into AllJoyn. The Bridge will use the instance of the adapter class to create the bus attachments for each device in the Adapter.devices list.
![AJ_Docu_DSB_Class_Diagram](../media/AllJoyn/AJ_Docu_DSB_Class_Diagram.png)

## Special Handlers

AllJoyn specifies several base services and standard interfaces frameworks such as LSF, HAE or Control Panel. The DSB can exposes those with special handlers. The current release of the DSB template contains implementations of the LSF and Control Panel interfaces. Developers will connect their code to the callback functions for LSF and Control Panel interfaces in the bridge.

![AJ_Docu_DSB_Special_Handlers](../media/AllJoyn/AJ_Docu_DSB_Special_Handlers.png)

## DSB Resources

### Visual Studio DSB Template

Visual Studio DSB Template is an extension to Visual Studio that lets you easily create new DSB projects. The project will create all the necessary components such as the Bridge, a shell project for the adapter and all solution files to build the DSB as headed or headless device. This Visual Studio extension contains both the Native and Managed AllJoyn Device System Bridge templates.

Download DSB Template from these locations:

* [DSB Template for Visual Studio 2015](https://visualstudiogallery.msdn.microsoft.com/aea0b437-ef07-42e3-bd88-8c7f906d5da8)
* [DSB Template for Visual Studio 2017](https://marketplace.visualstudio.com/vsgallery/c5f52768-8df7-42ff-b84e-d66d3d22fb50)
_DSB Template can also be installed through Visual Studio Tools -> Extensions and Updates … -> Online -> In the "Search" field type "DSB"._

The [Mapping DSB Objects to AllJoyn](AlljoynDsbApiGuide.md) document describes the key interfaces and methods used to build the Alljoyn System Bridge.

### Sample DSBs

* [AllJoyn DSB Mock Adapter Tutorial and Sample](https://developer.microsoft.com/en-us/windows/iot/samples/alljoynmockadapter)
  * This tutorial shows how to use the Device System Bridge app to connect your  IoT Core devices to mock BACnet devices.
* [AllJoyn DSB Z-Wave Adapter Tutorial and Sample](https://developer.microsoft.com/en-us/windows/iot/samples/zwaveadapter)
  * This tutorial shows how to use the Device System Bridge app to connect your  IoT Core devices to Z-Wave devices.
* [AllJoyn DSB GPIO Adapter Tutorial C++](https://developer.microsoft.com/en-us/windows/iot/samples/alljoyndsb)
  * This tutorial demonstrates how to use the AllJoyn Device System Bridge template to create a sample C++ app that exercises the device GPIO.
* [AllJoyn DSB GPIO Adapter Tutorial C#](https://developer.microsoft.com/en-us/windows/iot/samples/alljoyndsbcs)
  * This tutorial demonstrates how to use the AllJoyn Device System Bridge template to create a sample managed app that exercises the device GPIO.
* [AllJoyn DSB ZigBee Adapter Tutorial and Sample](https://developer.microsoft.com/en-us/windows/iot/samples/ZigBeeAdapter)
  * This tutorial shows how to use the Device System Bridge app to connect your IoT Core devices to ZigBee devices.
* [AllJoyn DSB BACnet Adapter Tutorial and Sample](https://developer.microsoft.com/en-us/windows/iot/samples/BACnetAdapter)
  * This tutorial shows how to use the Device System Bridge app to connect your IoT Core devices to BACnet devices.
* [AllJoyn.JS Tutorial](https://developer.microsoft.com/en-us/windows/iot/samples/AllJoynJS)
  * This tutorial shows how to run AllJoyn.JS application developed by Allseen Alliance as a Windows 10 application. AllJoyn.JS allows you to write JavaScript to create, monitor and control AllJoyn devices.
* [AllJoyn DSB OIC Adapter Tutorial and Sample](https://developer.microsoft.com/en-us/windows/iot/samples/OICAdapter)
  * This tutorial shows how to use the Device System Bridge app to connect your  IoT Core devices to IoTivity/OIC devices.
