---
title: Deploying an App with Visual Studio
author: bfjelds
ms.author: bfjelds
ms.date: 08/28/2017
ms.topic: article
description: Learn how to deploy an app using the Visual Studio remote debugging feature.
keywords: windows iot, visual studio, app deployment, remote debugging
---

# Deploying an App with Visual Studio

Deploying and debugging your application is straightforward with Visual Studio. We'll use the **Remote Debugging** feature to deploy the app to your locally connected Windows 10 IoT Core device. 

> [!NOTE]
> Visual Studio will generate a cryptic error when deploying to a RS5 (or RS4 with OpenSSH enabled) IoT image unless a SDK from RS4 or greater is installed that Visual Studio can access.

> [!NOTE]
> In order to use remote debugging, your IoT Core device must first be connected to the same local network as your development PC and UDP/TCP communications should be allowed on the network. If in doubt, check with your IT on allowed network traffic. See [Connecting to a device](../connect-your-device/SetupWiFi.md) for instructions.

## Deploy apps to your Windows 10 IoT Core device

1. With the application open in Visual Studio, set the architecture in the toolbar dropdown. If you're building for a Minnowboard Max, select `x86`. If you're building for Raspberry Pi 2, Raspberry Pi 3 or the Dragonboard, select `ARM`.

2. Next, in the Visual Studio toolbar, click on the `Local Machine` dropdown and select `Remote Machine`.

![Remote machine in Visual Studio](../media/AppDeployment/remote-vs.png)

3. At this point, Visual Studio will present the **Remote Connections** dialog. If you previously used [PowerShell](../connect-your-device/PowerShell.md) to set a unique name for your device, you can enter it here (in this example, we're using **my device**). Otherwise, use the IP address of your Windows IoT Core device.

4. After entering the device name/IP select `Universal (Unencrypted Protocol)` Authentication Mode, then click **Select**. 

![Universal authentication mode](../media/AppDeployment/remote-connections.png)

You can verify or modify these values by navigating to the project properties (select **Properties** in the Solution Explorer) and choosing the `Debug` tab on the left:

![Debug tab](../media/AppDeployment/debug-tab.png)

5. Now we're ready to deploy. Simply press F5 (or select Debug | Start Debugging) to start debugging our app. You should see the app come up on your device's screen.

6. Once deployed, you can set breakpoints, see variable values, etc. To stop the app press on the 'Stop Debugging' button (or select Debug | Stop Debugging).

7. After successfully deploying and debugging your UWP application, create a Release version - change the Visual Studio toolbar configuration dropdown from `Debug` to `Release`.  You can now build and deploy your app to your device by selecting Build | Rebuild Solution and Build | Deploy Solution.
