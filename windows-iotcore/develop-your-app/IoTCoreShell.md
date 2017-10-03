---
title: IoT Shell Overview
author: derekameer
ms.author: demeer
ms.date: 08/28/2017
ms.topic: article
description: Learn about how to leverage the IoT Shell to navigate between navigations on your device.
keywords: windows iot, IoT core shell, applications, foreground applications, background applications
---

# IoT Shell Overview

This document covers the IoT Shell, foreground and background applications, and how to navigate between these applications on your device.

## IoT Shell, Foreground, and Background Apps

Your IoT Core device runs the IoT Shell. It has many responsibilities, but its primary job is to make sure registered startup apps are launched. It has two modes: Headed and Headless. 
In Headed mode, the IoT Shell will launch a single registered startup app that will show its UI in full screen (also known as a Headed app). Headed mode assumes you have a screen connected and shows UI. In Headless mode (explained in detail [here](../learn-about-hardware/HeadlessMode.md)), there is no UI; the IoT Shell launches background applications only.

Here are the main differences between foreground and background applications:

- **Foreground applications** have a UI. One of these is launched at startup when the device is in headed mode. All foreground apps are registered on the device and the user can switch between foreground apps during device operation.

- **Background applications** have no UI and thus save device resources by turning off the UI stack. Background applications often run continuously from startup and are often used to monitor the device.

## Switching between apps with a Home App

There are two approaches to create a home app for IoT Core which allows you to switch between different foreground applications. Each has an associated sample on GitHub.

The **IoT Home App** ([sample](https://developer.microsoft.com/en-us/windows/iot/samples/iothomeapp) shows you how to create a simple "Home" app that can navigate back and forth between your other apps and the "Home" app.

The **IoT Startup App** ([sample](https://developer.microsoft.com/en-us/windows/iot/samples/iotstartapp) represents a simple startup app that lists the installed apps on your device, then launches one using the PackageManager APIs.

Use either one of these apps as a starting point for your multi-app experience as you see fit.

## Switching between apps with HID Injection Keys

The below instructions show you how to turn on Hotkey support through entries to the registry. If you are building your own image and want to support the below hotkeys (Home, previous app, and next app) without needing to access the registry, you can include an optional feature package that handles these steps for you.

The feature package to look for is called: **Microsoft-OneCore-IoTUAP-Shell-HotKeys-Feature-Package.cab** and the feature is called **IOT_SHELL_HOTKEY_SUPPORT**. See the [Settings.HotKey sample package](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Common/Packages/Settings.HotKey/Settings.HotKey.pkg.xml) for an example.

The rest of this document covers how to implement this feature manually.

### Return Home

With the Windows 10 IoT Anniversary Update (1607), the IoT Shell supports bringing the default application window to the foreground when another application is running by pressing the "GO HOME" key, which is set to the release of the Windows Button on a keyboard. If you don't have a keyboard on your IoT Device and need to inject low-level keyboard events through [HID Injection](https://developer.microsoft.com/en-us/windows/iot/samples/hidinjection), or if you just want to re-map the "GO HOME" functionality to a different key in your app, you can adjust the key value in the registry. For example, to enable pressing the ESCAPE key (0x1B) to "GO HOME", enter the following command in the registry:

``
“HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\HotKeys” “HOME” QWORD    0x0000000 0000001B  
``

As a REG file, this looks as follows:

``
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\HotKeys]
"Home"=hex(b):1B,00,00,00,00,00,00,00
``

### Switch Between Apps

Alternatively, if you want to switch between your foreground apps, you can set up Alt-Tab (next app) and Shift-Alt-Tab (previous app) functionality in your image by entering the following command in the registry:

``
“HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\HotKeys”
“PREV” QWORD 0x00010000 00010009 
“NEXT” QWORD 0x00020000 00050009 
``

As a REG file, this looks as follows:
``
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\HotKeys]
"Prev"=hex(b):09,00,01,00,00,00,01,00
"Next"=hex(b):09,00,05,00,00,00,02,00
``

### Bit Translation

The above REG file entries decode left to right as follows:

- Bits 0-15: Virtual Key Code (i.e. 1B,00 for ESCAPE). See [Virtual Key Code](https://msdn.microsoft.com/library/windows/desktop/dd375731(v=vs.85).aspx) for the complete list of key code values
- Bits 16-19: Modifier Key. 0x0 = No Modifier, 0x1 = ALT, 0x2 = CTRL, and 0x4 = SHIFT. Combining keys adds the values together (i.e. ALT+SHIFT is 0x5)
- Bits 20-47: Reserved for future use; must be 0
- Bits 48-62:  Action
    - 0 = Home
    - 1 = Previous View (may not work in future releases)
    - 2 = Next View (may not work in future releases)
- Bit 63: Reserved; must be 0

