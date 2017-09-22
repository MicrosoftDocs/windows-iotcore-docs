---
title: Windows File Sharing
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about how to use Windows file sharing to transfer files to and from your device.
keywords: windows iot, file transfer, file share, windows file sharing
---

# Windows file sharing

You can use Windows file sharing to transfer files to and from your device.

## Accessing your files using Windows file sharing
* The file sharing server on your Windows IoT Core device starts automatically on boot.  In order to connect to it, you need the IP address of your device.  You can find the IP address on the default app that boots when your device starts.

    ![DefaultApp on Windows IoT Core](../media/WindowsFileSharing/DefaultApp.png)
    
* Once you have the IP, open up **File Explorer** on your computer and type `\\<TARGET_DEVICE>\c$`, where `<TARGET_DEVICE>` is either the name or the IP Address of your Windows IoT Core device, then hit Enter.  

Enter your administrator username and password if prompted. The username should be prefixed with the IP Address of your Windows IoT Core device. Example: **Username:** `192.168.1.118\Administrator`  **Password:** `{your_password}`.

![File explorer](../media/WindowsFileSharing/smb_file_explorer.png)

* Now you can access the files on your device using Windows file sharing.

## Starting and stopping the file sharing server
* Connect to your device through [PowerShell](../connect-your-device/powershell.md) or [SSH](../connect-your-device/ssh.md).
* By default the file sharing  server is started when the device is booted.
* To stop the file sharing  server, type `net stop Server /y`
* To start the file sharing  server, type `net start Server`

    ![Server start and stop](../media/WindowsFileSharing/smb_start_stop.png)
    
## Disabling and enabling the file sharing server on startup
* Connect to your device through [PowerShell](../connect-your-device/powershell.md) or [SSH](../connect-your-device/ssh.md).
* By default the file sharing  server is started when the device is booted.
* To disable the file sharing  server so that it does not start when the device starts, type `reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\lanmanserver /v Start /t REG_DWORD /d 0x3 /f`
* To enable the file sharing  server so that starts when the device starts, type `reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\lanmanserver /v Start /t REG_DWORD /d 0x2 /f`

    ![Server enable disable](../media/WindowsFileSharing/smb_enable_disable.png)
