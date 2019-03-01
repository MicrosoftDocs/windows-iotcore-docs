---
title: Embedded mode
author: lmaung
ms.author: lmaung
ms.date: 01/22/19
ms.topic: article
description: Learn how to configure Windows to allow embedded mode, enabling background applications and other capabilities.
keywords: windows iot, embedded mode, background applications
---

# Embedded mode

Embedded Mode is supported on Windows IoT Core and Windows IoT Enterprise. Embedded Mode enables:

* [Background Applications (read more)](https://docs.microsoft.com/windows/iot-core/develop-your-app/backgroundapplications)
* Use of the lowLevelDevice capability
* Use of systemManagement capability

Embedded mode is always enabled on Window IoT Core.

## Background Applications

Background Applications are created using the Background Application (IoT) template in Visual Studio.
Read more about creating [Background Applications](https://docs.microsoft.com/windows/iot-core/develop-your-app/backgroundapplications).

Background applications run without stopping and without resource limits. Also, if the background application stops for some reason and embedded mode is enabled the background application will be restarted by the system.

While the system will automatically restart background applications, system lockdown features must be enabled to prevent users from stopping or interfering with the operation of Background Applications.

## lowLevelDevice Capability

The lowLevelDevice Capability gives access to low-level hardware interfaces like GPIO, SPI, and I2C.

* [Blinky Sample(GPIO)](https://developer.microsoft.com/en-us/windows/iot/samples/helloblinky)
* [Accelerometer Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/Accelerometer)

## systemManagment Capability

When you enable the systemManagment capabilities for your application this is the set of APIs that gets unlocked:  

* [Windows.System.ProcessLauncher](https://msdn.microsoft.com/library/windows/apps/windows.system.processlauncher.aspx)
* [Windows.System.TimeZoneSettings](https://msdn.microsoft.com/library/windows/apps/windows.system.timezonesettings.aspx)
* [Windows.System.ShutdownManager](https://msdn.microsoft.com/library/windows/apps/windows.system.shutdownmanager.aspx)
* [Windows.Globalization.Language.TrySetInputMethodLanguageTag](https://msdn.microsoft.com/library/windows/apps/windows.globalization.language.trysetinputmethodlanguagetag.aspx)

## Changing the mode
To enable embedded mode you will need to create a provisioning package in Imaging and Configuration Designer (ICD) that sets AllowEmbeddedMode=1.  To install ICD you need to download and install the Windows ADK for Windows 10.

## Configuring a Background Application to Run automatically
1. To configure a Background Application to automatically run you will need to follow the directions to [create an MinnowBoardMax SD Card](https://developer.microsoft.com/en-us/windows/iot/getstarted) and copy `D:\windows\system32\iotstartup.exe` (where D: is your SD Card).

2. To get a list of installed Background Applications type:

        C:\> iotstartup list BackgroundApplication1

3. The output should include the full name of each installed Background Application, which will look like this:

        Headless : BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee

5. To configure this app to run at boot type:

        C:\> iotstartup add headless BackgroundApplication1

6. If the Background Application has been successfully added to the startup list you should see this:

        Added Headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpveeplication1

7. Restart the embedded mode device:

8. Once the device has restarted, your Background Application will start automatically.  The Embedded Mode service which manages Background Applications can take a few minutes to start.  The embedded mode service will monitor Background Applications on the startup list and make sure they get restarted if they stops.  If a Background Application stops several times in a short period of time it will no longer be restarted.

9. To remove your Background Application from the startup list type:

        C:\> iotstartup remove headless BackgroundApplication1

10. If the Background Application is removed from the startup list the output will look like this:

        Removed headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee
        
        
Indepth information about embedded mode can be found [here](https://github.com/MicrosoftDocs/windows-iotcore-docs/blob/master/windows-iotcore/develop-your-app/EmbeddedMode.md)
