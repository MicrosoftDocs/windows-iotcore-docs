---
title: Develop an app for your device
ms.date: 04/03/2023
ms.topic: article 
ms.prod: windows-iot
ms.technology: iot
description: Learn about how to add and develop apps for your device. See links to suggested starter samples and app development resources.
keywords: Windows 10 IoT Core, Get Started, develop apps, apps
---

# Develop an app for your device

> [!NOTE]
> Visual Studio will generate a cryptic error when deploying to a RS5 (or RS4 with OpenSSH enabled) IoT image unless a SDK from RS4 or greater is installed that Visual Studio can access.

Now that you have a working device with the default app running, you'll want to take your device to the next level by developing and deploying an app on your device. Before diving into samples, you'll need to download [Visual Studio 2017](https://www.visualstudio.com/downloads/) for application development.

If you're planning to use C++ for your projects, when downloading Visual Studio 2017, make sure to check the boxes the same way as they are in the example below:

![Essentials for C++ and Windows 10 IoT](../../media/DevelopApp/VS-CPP.jpg)

If you're interested in developing background, Arduino Wiring or console applications in the future, you'll also want to download project templates from the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=MicrosoftIoT.WindowsIoTCoreProjectTemplatesforVS15).


To get up and running with an app, we recommend starting with a suggested starter sample below. But if you're ready to deploy your own app, we've also provided helpful links in the section after.

## Suggested starter samples

* [Hello Blinky](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinky)
* [Hello World](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloWorld)
* [IoT Startup App sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTStartApp)
* [RPi Cognitive Service sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/RPiCognitiveService) 



Once you've deployed your app - congratulations, you've finished this quickstarter! Continue to play around or, if you have a few ideas bouncing around in your head, check out our documentation on commercializing with Windows 10 IoT. 

## App development resources

| Topic | Description |
| ----- | ----------- |
| [Developing foreground applications](../../develop-your-app/buildingappsforiotcore.md) | Learn about the different languages that are supported on Windows 10 IoT Core as well as the UWP and non-UWP app types that are supported. |
| [Developing background applications](../../develop-your-app/backgroundapplications.md) | Learn about the different languages that are supported on Windows 10 IoT Core as well as the UWP and non-UWP app types that are supported. |
| [Deploy an App with Visual Studio](../../develop-your-app/appdeployment.md) | Learn how to deploy your different apps with Visual Studio to your Windows 10 IoT Core device. |
| [Debug your app using Remote Console App Debugging](../../develop-your-app/remotedebugging.md) | Learn how to debug your apps using Remote Console App Debugging in Visual Studio. |
| [Install your app on your Windows 10 IoT Core device](../../develop-your-app/appinstaller.md) | Learn how to install your app to your Windows 10 IoT Core device. |
