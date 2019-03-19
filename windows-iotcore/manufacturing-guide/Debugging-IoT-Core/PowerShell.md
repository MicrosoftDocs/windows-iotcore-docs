---
title: Using PowerShell for Windows IoT
author: lmaung
ms.author: lmaung
ms.date: 01/22/19
ms.topic: article
description: Learn how to use PowerShell to connect to your device as well as manage your device.
keywords: windows iot, PowerShell, Windows PowerShell, command line, command-line shell
---

# Using PowerShell for Windows IoT

Remotely configure and manage any Windows 10 IoT Core device by using Windows PowerShell.
PowerShell is a task-based command-line shell and scripting language, designed especially for system administration.

Make sure to follow these steps to correctly configure your device running Windows 10 IoT Core to work well with Visual Studio 2017.

## Initiating a PowerShell session
1. To start a PowerShell session with your Windows 10 IoT Core device, you'll first need to create a trust relationship between your host PC and your device. After starting your Windows IoT Core device, an IP address will be shown on the screen attached to the device.

    ![DefaultApp on Windows 10 IoT Core](../../media/PowerShell/DefaultApp.png)

   You can find the same information on the Windows 10 IoT Core Dashboard.

2. Open an administrator PowerShell console on your local PC. Type **powershell** in the **Search the web and Windows** box near the Windows Start menu. Windows will find PowerShell on your PC.

    ![Find PowerShell](../../media/PowerShell/start-ps.png)

3. To start PowerShell as an administrator, right-click **Windows PowerShell**, and then select **Run as administrator**.

    ![Run PowerShell as administrator](../../media/PowerShell/start-ps2.png)

   Now you should see the PowerShell console.

    ![PowerShell console](../../media/PowerShell/ps.PNG)

4. You may need to start the WinRM service on your desktop to enable remote connections. To do so, from the PowerShell console, type the following command:

        net start WinRM

5. From the PowerShell console, type the following, substituting `<machine-name or IP address>` with the appropriate value (using your **machine-name** is the easiest, but if your device is not uniquely named on your network, try the IP address):

        Set-Item WSMan:\localhost\Client\TrustedHosts -Value <machine-name or IP Address>

6. Enter `Y` to confirm the change.

> [!NOTE]
> If you want to connect multiple devices, you can use commas and quotation marks to separate each device.
        
        Set-Item WSMan:\localhost\Client\TrustedHosts -Value "<machine1-name or IP Address>,<machine2-name or IP Address>"
	
7. Now you can start a session with your Windows IoT Core device. From you administrator PowerShell console, type:

        Enter-PSSession -ComputerName <machine-name or IP Address> -Credential <machine-name or IP Address or localhost>\Administrator

8. In the credential dialog, enter the following default password: `p@ssw0rd`
    
    <div class="alert alert-note">
      <h5><span class="win-icon win-icon-Page"></span>
        NOTE
      </h5>
      <p>The connection process is not immediate and can take up to 30 seconds.</p>
    </div>    
    
    If you successfully connected to the device, you should see the IP address of your device before the prompt.

    ![PowerShell console](../../media/PowerShell/ps_device.png)

9. Update your account password. We *highly recommend* that you update the default password for the Administrator account. To do this, issue the following commands in your PowerShell connection:

	a. Replace `[new password]` with a strong password:
	
	        net user Administrator [new password]
	        
	b. Next, establish a new PowerShell session using `Exit-PSSession` and `Enter-PSSession` with the new credentials.
	
	        Exit-PSSession
	        
	        Enter-PSSession -ComputerName <machine-name or IP Address> -Credential <machine-name or IP Address or localhost>\Administrator

## Commonly used PowerShell commands

### Configure your Windows IoT Core device

If you want, you can rename your device. 

1. To change the computer name, use the `setcomputername` utility:

        setcomputername <new-name>

2. Restart the device for the change to take effect. You can use the `shutdown` command as follows:

        shutdown /r /t 0

3. Because the computer name was changed, after you restart you will need to rerun this command to connect to your device using the new name:

        Set-Item WSMan:\localhost\Client\TrustedHosts -Value <new-name>
        
Your Windows IoT Core device should now be properly configured and ready to use!

### Commonly used utilities

* `IotStartup list` lists installed applications
* `IotStartup list headed` lists installed headed applications
* `IotStartup list headless` lists installed headless applications
*  `DeployAppx install MyApp.appx` installs the .APPX and the certificate of the same name if found.
* `DeployAppx install force MyApp.appx` forces uninstalling the currently installed .APPX with the same package name if found before installing the new .APPX.  This is useful for installing an .APPX with the same or lower version number as the currently installed .APPX.
* `DeployAppx uninstall App_1.0.1.0_x86__publisherid123` uninstall the .appx with the matching package full name.
*  `DeployAppx uninstall MyApp.appx` uninstall any installed .APPX with a matching package family name.

For a list of commands and utilities that you can use with PowerShell, see the [Command Line Utils](../../manage-your-device/CommandLineUtils.md) page.
