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
The File Transfer Protol (FTP) allows you to transfer files to and from your Windows 10 IoT Core device

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
    
* Now when you connect to your device through FTP, you will see the contents of the root directory you set.

    ![FTP explorer with new root directory](../media/ftp/ftp_explorer_parameter.png)

* In order to make this change permanent, you need to edit a script and start the FTP server when the device turns on.  If you are using a prebuilt device image, open up **File Explorer** and type `\\<TARGET_DEVICE>\c$\Windows\System32`, where `<TARGET_DEVICE>` is either the name or the IP address of your device.

    ![FTP explorer edit script](../media/ftp/ftp_edit_script.png)
    
* Find `IoTStartupOnBoot.cmd`, right-click it, and click **Edit**.

    ![FTP explorer right-click](../media/ftp/ftp_right_click.png)
    
* If a "Access is denied." dialog pops up right click it, and click **Properties**.

  - Select the Security tab
  - click Advanced *"Advanced Security Settings for IoTStartupOnBoot.cmd" dialog pops up*
  - note the Owner **TrustedInstaller**
  - click Change near Owner *"Select User or Group" dialog pops up*
  - enter **Administrators**
  - click Check Names
  - click OK
  - note the Owner **Administrators (yourdevicename\Administrators)**
  - click Apply
  - close both dialogs with OK

  now the file can be edited

* If a security dialog pops up, just click **Run**.

    ![FTP security dialog](../media/ftp/ftp_security_warning.png)
    
* Your default text editor should now open. After the block text that begins with `REM start W32time` add a block of text to call `start ftpd.exe <PATH_TO_DIRECTORY>` where `<PATH_TO_DIRECTORY>` is the absolute path to the directory you want to set as the root directory, such as `C:\Data\Users\DefaultAccount`.  Similar to the snippet below:

``` 
REM start W32Time
if /i EXIST %SystemDrive%\Windows\System32\w32time.dll (
  net start w32time >nul 2>&1
)

if /i EXIST %SystemDrive%\Windows\System32\ftpd.exe (
  start ftpd.exe C:\Data\Users\DefaultAccount >nul 2>&1
)
```

Then save the file and close the window.

* Now when you reboot your device, the FTP server will start with your new root directory.
