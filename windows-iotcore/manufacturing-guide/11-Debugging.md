---
title: IoT Core Introduction
author: lmaung
ms.author: lmaung

ms.date: 10/1/2018 
ms.topic: article 
description: Debugging on Windows IoT Core
keywords: Windows 10 IoT Core, 
---

# Debugging on Windows IoT Core
Once you have your IoT Core image setup with running application, it is important that you can debug the application or the system as needed. The best time to debug and test the system is while the test image state. Once IoT Core based systems is out in the wild, debugging can become challanging. That is not to say it can not be done but with additional layers of difficulties added to debug compare to a testing phases. You can use the following to debug your application or image while in test mode:

## Device Portal
Windows Device Portal (WDP) allows for you to configure and manage your IoT Device remoately over local network. WDP can be reachable via local ip of the IoT Device. Additional information on WDP on IoT can be found [here](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/DevicePortal)
### Collecting ETW / WPP Logs 

-----
### File Sharing
The App File Explorer can allow access to the directories that your apps can access
*vCameraRoll is shared among all apps
* Documents is shared among all apps
* LocalAppData contains folders specific to each app. This folder will be the same name as your app and other apps cannot access it.
See above link for additional information.

### Kernel Debug
You can download live Kernel dumps via WDP as well. Any system crashes will be automatically be logged and available for download. See above link for additional information.

### Enable Crash Dump
You can download crash dumps of applications on IoT Device via WDP. See above link for additional information.

## SSH/PowerShell/TShell
PowerShell is a task-based command-line shell and scripting language, designed especially for system administration. Details on debugging and setting up powershell can be found [here](10k-powershell.md)


## Debug through Visual Studio Deployment
Deploying and debugging your application is straightforward with Visual Studio. Remote Debugging feature can be used to deploy and debug the app to your locally connected Windows 10 IoT Core device. Detailed on deployment and debugging can be found [here](10a-DebugAndDeployApps.md)

-----
## Live App Debug
In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from Azure Application Insights. The feature is later extended to include desktop and UWP applications in Visual Studio 2017 and via Azure Portal. Additional information on debugging your project can be found [here](https://docs.microsoft.com/en-us/azure/azure-monitor/app/visual-studio) and monitoring usage, and performance in desktop or UWP appplications can be found [here](https://docs.microsoft.com/en-us/azure/azure-monitor/app/windows-desktop  
