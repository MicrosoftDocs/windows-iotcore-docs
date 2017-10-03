---
title: File Transfer Protocol
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use File Transfer Protocol (FTP) to transfer files to and from your devices.
keywords: windows iot, FTP, file transfer protocol, file transfer, devices
---

# File Transfer Protocol
The File Transfer Protocol (FTP) allows you to transfer files to and from your Windows 10 IoT Core device

> [!IMPORTANT]
> FTP is recommended generally for developers to ease the initial development process. We do not recommend using FTP in retail devices.

## Starting the FTP server on your device
* By default, the FTP server is disabled on your IoT Core device.  In order to start the FTP server on your device, first you need to connect to your device through [PowerShell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md).
* Type `start C:\Windows\System32\ftpd.exe`
* You can check that the server is running by typing `tlist`, which will list all the running processes.  If the FTP server is running, you should see `ftpd.exe` in the list.

![FTP Start](../media/ftp/ftp_start.png)

## Stopping the FTP server on your device<a name="stopftp"/>
* In order to stop the FTP server on your IoT Core device, first you need to connect to your device through [PowerShell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md).
* If you connected using PowerShell, type `kill -processname ftpd*` to stop the FTP process.

![FTP PowerShell Stop](../media/ftp/ftp_kill_powershell.png)

* If you connected using SSH, type `kill ftpd*` to stop the FTP process.

![FTP SSH Stop](../media/ftp/ftp_kill_ssh.png)

## Accessing your files over FTP
* The FTP server on your IoT Core device starts automatically on boot.  In order to connect to it, you need the IP address of your device.  You can find the IP address on the default app that boots when your device starts.

![DefaultApp on Windows IoT Core](../media/ftp/DefaultApp.png)

* Once you have the IP, open up **File Explorer** on your PC and type `ftp://<TARGET_DEVICE>`, where `<TARGET_DEVICE>` is either the name or the IP address of your device, then hit Enter.  Enter your administrator username and password if prompted.

![FTP explorer](../media/ftp/ftp_explorer.png)

* Now you can access the files on your device through FTP.

## Changing the root FTP directory
* By default the FTP server displays all the folders in the device's root directory C:\\.  In order to change the root directory, follow the same steps to start the FTP server, except you need to pass in the root directory as a parameter.
* In order to change it, first connect to your device through [PowerShell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md).
* [Stop](#stopftp) the FTP process if it's already running.
* Type `start C:\Windows\System32\ftpd.exe <PATH_TO_DIRECTORY>`, where `<PATH_TO_DIRECTORY>` is the absolute path to the directory you want to set as the root directory, such as `C:\Users\DefaultAccount`.

![FTP Start with Parameter](../media/ftp/ftp_start_parameter.png)

Now when you connect to your device through FTP, you will see the contents of the root directory you set.

![FTP explorer with new root directory](../media/ftp/ftp_explorer_parameter.png)

In order to make this change permanent, you need to add
a call to `start ftpd.exe <PATH_TO_DIRECTORY>` where `<PATH_TO_DIRECTORY>` is the absolute path to the directory you want to set as the root directory, such as `C:\Data\Users\DefaultAccount` to OEMCustomization.cmd and place it in `C:\Windows\System32`
