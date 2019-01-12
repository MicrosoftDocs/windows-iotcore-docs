---
title: Developing foreground applications
author: lmaung
ms.author: lmaung
ms.date: 11/30/2018
ms.topic: article
description: Learn about the languages and app types that are supported by IoT Core.
keywords: windows iot, languages, app types, UWP, supported
---

# Developing foreground applications
Learn about the languages that are supported on Windows 10 IoT Core as well as the UWP and non-UWP app types that are supported on IoT Core.


> [!NOTE]
> Visual Studio will generate a cryptic error when deploying to a RS5 (or RS4 with OpenSSH enabled) IoT image unless a SDK from RS4 or greater is installed that Visual Studio can access.

## Application Types
___
### Universal Windows Platform (UWP) Apps
IoT Core is a UWP centric OS and UWP apps are its primary app type.

Universal Windows Platform (UWP) is a common app platform across all version of Windows 10, including Windows 10 IoT Core.  UWP is an evolution of Windows Runtime (WinRT). You can find more information and an overview to UWP [here](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide).

Visual Studio is the primary tool for writing UWP apps for IoT Core and in general. You can find a detailed listing of the compatibility requirements for Visual Studio [here](https://docs.microsoft.com/visualstudio/productinfo/vs2017-compatibility-vs).

### Non-UWP Apps
IoT Core supports certain traditional Win32 app types such as Win32 Console Apps and NT Services. These apps are built and run the same way as on Windows 10 Desktop. Additionally, there is an IoT Core C++ Console project template to make it easy to build such apps using Visual Studio.

There are two main limitations on these non-UWP applications:
1. *No legacy Win32 UI support:* IoT Core does not contain APIs to create classic (HWND) Windows. Legacy methods such as CreateWindow() and CreateWindowEx() or any other methods that deal with Windows handles (HWNDs) are not available. Subsequently, frameworks that depend on such APIs including MFC, Windows Forms and WPF, are not supported on IoT Core
2. *C++ Apps Only:* Currently, only C++ is supported for developing Win32 apps on IoT Core.

## Programming Languages
___

IoT Core supports a wide range of programming languages.

### In-Box languages
Traditional UWP languages ship with support in Visual Studio by default. All of the In-Box languages support both UI and Background Applications
 
* Languages
  * C#
  * C++
  * Javascript
  * Visual Basic
  
  
