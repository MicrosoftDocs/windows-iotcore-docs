---
title: Arduino Wiring Project Guide
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the creation, setup, and deployment of an Arduino Wiring project using Windows IoT Core.
keywords: windows iot, Arduino, Arduino wiring, Lightning Performance, Visual Studio
---

# Arduino Wiring Project Guide

This guide will walk through the creation, setup, and deployment of an Arduino Wiring project using Windows IoT Core.

Arduino Wiring projects utilize the familiar, easy to use Arduino Wiring API with Windows IoT Lightning DMAP driver: a driver using direct memory mapping to provide significant [performance speeds](../develop-your-app/LightningPerformance.md). You can copy & paste Arduino sketches and libraries into your IoT Core Arduino Wiring projects and run them on supported IoT Core devices, including Raspberry Pi2, 3 and Minnowboard Max! See the develop section of this page for more information.

## Install the Microsoft IoT Templates

We've provided a Visual Studio extension which will automatically install a VS template for the Arduino Wiring projects as well as other Microsoft IoT project types. 

- Head over to [Windows IoT Core Project Templates extension page](https://go.microsoft.com/fwlink/?linkid=847472) to download the extension from the Visual Studio Gallery!
- Install the extension and restart Visual Studio if it was already open

## Change the Default Controller Driver

You will need to be running the Direct Memory Mapped Driver to write Arduino Wiring solutions! Refer to the [Lightning Setup Guide](../develop-your-app/LightningSetup.md) for instructions!

## Develop
Complete one of the "Wiring" samples on the [Samples Page](https://developer.microsoft.com/en-us/windows/iot/samples), or build your own project! Any of the samples we've created that are written using Arduino Wiring will be listed like so: [Blinky (Wiring)](https://developer.microsoft.com/en-us/windows/iot/samples/helloblinkybackgroundwiring). Blinky, the cononical "Hello World" project for IoT projects, is a great place to start for your first project!

### Create a new Project
1. Open Visual Studio.

2. Select File -> New -> Project...

3. From the dialogue that appears, choose:  
Visual C++ -> Windows -> Windows IoT Core -> Arduino Wiring Application for Windows IoT Core  
(might appear instead as)  
Visual C++ -> Windows IoT Core -> Arduino Wiring Application for Windows IoT Core 


![App Create](../media/ArduinoWiring/appcreate.png)

### Porting

The Arduino Wiring API has been carefully implemented to make it possible to copy/paste your libraries and sketches into an Arduino Wiring project. Nevertheless there are, in some circumstances, slight modifications you may have to make to your sketches or libraries. We've created an easy to follow [Arduino Wiring Porting Guide](ArduinoWiringPortingGuide.md) to cover these potential issues.

## Build and Deploy

- In Visual Studio, make sure "Remote Machine" is selected as your deployment target.
- Also, make sure the  architecture is set to match the board you're running your project on. For Raspberry Pi 2 or 3 choose "ARM" and for Minnowboard Max, choose "x86".

![Remote Machine](../media/ArduinoWiring/wiringapp_remotemachine.png)

- Open the solution properties found on the Debug context menu in Visual Studio.

![Solution Properties](../media/ArduinoWiring/wiringapp_properties.png)

- locate the IP address or machine name of your device. Either use the Windows 10 IoT Core Dashboard application or hook up your device to a monitor.
- Type the machine name (minwinpc by default) or the IP address of the remote machine into the 'machine name' field. If you have renamed your device to something besides 'minwinpc' use that name in the login box instead.
- Ensure the Authentican Type is: Universal (Unencrypted Protocol)

![Solution Properties](../media/ArduinoWiring/wiringapp_properties2.png)

- Press F5 to build and deploy your project on your device.
