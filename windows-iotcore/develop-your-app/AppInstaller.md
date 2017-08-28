---
title: Install your app using Windows Device Portal
author: bfjelds
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
ms.prod: Windows
ms.technology: IoT
description: Learn how to install your app using the Windows Device Portal.
keywords: windows iot, app installation, Windows Device Portal, devices
---

# Install your app using Windows Device Portal
___

To install your application on the device please do the following:

1. Open the [Windows Device Portal](https://developer.microsoft.com/en-us/windows/iot/docs/deviceportal) for your IoT device.

2. In the *Apps* menu add your UWP App Package, certificate and dependency App Packages(s).
 ![Install App](../media/AppInstaller/InstallApp.png)

3. Deploy the app.

4. The application will now be visible on the list of applications on your device.
 ![App List](../media/AppInstaller/AppList.png)


## Install the app as a part of the IoT core image   
___

To add the application as a part of your device image follow the instructions outlined in the [manufacturing guide](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/iot/deploy-your-app-with-a-standard-board).

A sample provisioning package with UWP application can be found in our [GitHub repo](https://github.com/ms-iot/iot-adk-addonkit/tree/develop/Source-arm/Packages/Appx.Main).
