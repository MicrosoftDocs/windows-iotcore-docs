---
title: Communicating with Localhost 
author: paulmon
ms.author: paul.monson
ms.date: 08/28/2017
ms.topic: article
description: Learn how to create a TCP/IP connection with two processes by enabling localhost loopback.
keywords: windows iot, localhost, loopback, UWP, visual studio
---

# Communicating with localhost (loopback)

On Windows IoT Core, if you want to create a TCP/IP connection between 2 processes running on the same device and one of them is a UWP app you must enable localhost loopback.

## Loopback and the debugger 
By default, running under the Visual Studio debugger enables outbound loopback automatically for that debug session only.  You shouldn’t have to do anything as long as the loopback checkbox is checked in the debugger settings for your startup project.  If you want to implement a socket listener the you must enable localhost loopback for inbound connections (see below).
 
## Enabling the inbound loopback policy
The localhost inbound loopback policy for **Windows IoT Core** must be enabled for UWP apps that implement servers.  This policy is controlled by the following registry key:

        [HKEY_LOCAL_MACHINE\system\currentcontrolset\services\mpssvc\parameters]
            "IoTInboundLoopbackPolicy"=dword:00000001

This IoTInboundLoopbackPolicy registry key value must be set to dword:00000001 to enable. If you change the IoTInboundLoopbackPolicy registry value you must reboot for the change to take effect.  The localhost loopback policy should be enabled by default on **Windows IoT Core**

To verify that the value is set execute the following command on the **Windows IoT Core** device:

        reg query hklm\system\currentcontrolset\services\mpssvc\parameters /v IoTInboundLoopbackPolicy

To enable the policy execute the following command on the **Windows IoT Core** device:

        reg add hklm\system\currentcontrolset\services\mpssvc\parameters /v IoTInboundLoopbackPolicy /t REG_DWORD /d 1
 

## Enabling loopback for a UWP application
Before you can enable loopback for an application you will need the package family name.  You can find the package family name for an installed application by running **iotstartup list**.  If the **iotstartup list** entry for the application is IoTCoreDefaultApp\_1w720vyc4ccym!App then the package family name is IoTCoreDefaultApp\_1w720vyc4ccym

To enable loopback for client connections use `CheckNetIsolation.exe -a -n=<AppContainer or Package Family>`.  CheckNetIsolation.exe will configure loopback for the application and exit. This will enable the application to make outbound connections to a server.

Example: `CheckNetIsolation.exe LoopbackExempt -a -n=IoTCoreDefaultApp_1w720vyc4ccym`

To enable a server application to receive inbound connections use `CheckNetIsolation.exe -is -n=<AppContainer or Package Family>`. Unlike outbound connection configuration, inbound connections require CheckNetIsolation.exe to run continuously while the server application is receiving connections.  This requires an OS build newer than 10.0.14393.

Example: `CheckNetIsolation.exe LoopbackExempt -is -n=IoTCoreDefaultApp_1w720vyc4ccym`

The best way to run CheckNetIsolation.exe automatically on startup is to use schtasks.exe: `schtasks /create /tn MyTask /f /sc onstart /ru system /tr "checknetisolation LoopbackExempt -is -n=IoTCoreDefaultApp_1w720vyc4ccym"`

Upon rebooting you should be able to verify that checknetisolation.exe is running by using tlist.exe or [Windows Device Portal](https://developer.microsoft.com/en-us/windows/iot/docs/deviceportal)
