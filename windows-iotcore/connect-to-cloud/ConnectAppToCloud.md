---
title: Connect your app to the cloud
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to connect your app to the cloud.
keywords: windows iot, cloud, Azure, Azure IoT Hub
---

# Connect your app to the cloud

This step-by-step guide will allow you to familiarize yourself with Windows 10
IoT Core, set up your device and create your first application that
connects to Azure IoT Hub.

## Step 1: Prepare your device

You can find instructions on how to prepare your device on the [Get Started Page](https://developer.microsoft.com/en-us/windows/iot/getstarted) 
Make sure you [provision the TPM of your device](../connect-to-cloud/ConnectDeviceToCloud.md)

## Step 2: Install Visual Studio 2017 and tools

Install [Visual Studio
2017](https://go.microsoft.com/fwlink/?linkid=845271). You
can install any edition of Visual Studio, including the free Community edition.

Make sure to select the **Universal Windows App Development Tools**, the
component required for writing apps Windows 10:

![Universal Windows App Development Tools](../media/ConnectAppToCloud/install_tools_for_windows10.png)

## Step 3: Install the Connected Services for Azure IoT Hub

The Connected Services for Azure IoT Hub Visual Studio extension allows you to
connect and start interacting with Azure IoT Hub in less than a minute.

You can install the extension from the [VS Gallery](https://aka.ms/azure-iot-hub-vs-cs-vs-gallery).

## Step 4: Create a Visual Studio UWP solution

To create a UWP solution in Visual Studio, on the **File** menu, click **New** then **Project**:

![New Project Creation](../media/ConnectAppToCloud/new_project_menu.png)

In the New Project dialog that comes up, select **Blank App (Universal Windows) Visual C#**. Give your project a name (e.x. **MyFirstIoTCoreApp**):

![New Solution Dialog](../media/ConnectAppToCloud/new_solution.png)

## Use the Connected Services for Azure IoT Hub to connect to Azure IoT Hub

Follow the instructions from the [Connected Services tool](https://aka.ms/azure-iot-hub-vs-cs-vs-gallery) to connect your project to Azure IoT Hub. The tool will generate two functions, `SendDeviceToCloudMessageAsync` and `ReceiveCloudToDeviceMessageAsync` that you can invoke anywhere in your app. You can modify these functions as you see fit.  

