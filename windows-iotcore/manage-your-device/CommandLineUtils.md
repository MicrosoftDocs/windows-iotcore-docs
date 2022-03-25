---
title: Windows 10 IoT Core Command Line Utilities
author: bfjelds
ms.author: bfjelds
ms.date: 08/28/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn the command line utilities to use with PowerShell after connecting to your device.
keywords: windows iot, command line, command line utilities, PowerShell
---

# Windows 10 IoT Core Command Line Utils

Looking to configure some of the settings on your device? The below tools are available at your disposal. Use PowerShell to run these commands after [connecting to your device](../connect-your-device/PowerShell.md).

> [!NOTE]
> These tools are not pre-loaded - you will need to include appropriate feature IDs to get these tools in the image.

## IoT Core-specific Command Line Utils

### **Setting startup app:**
Use the startup editor to configure startup apps on your Windows IoT Core device. Run `IotStartup` with any of the following options:

* `IotStartup list` lists installed applications
* `IotStartup list headed` lists installed headed applications
* `IotStartup list headless` lists installed headless applications
* `IotStartup list [MyApp]` list installed applications that match pattern `MyApp`
* `IotStartup add` adds headed and headless applications
* `IotStartup add headed [MyApp]` adds headed applications that match pattern `MyApp`.  Pattern must match only one application.
* `IotStartup add headless [Task1]` adds headless applications that match pattern `Task1`
* `IotStartup remove` removes headed and headless applications
* `IotStartup remove headed [MyApp]` removes headed applications that match pattern `MyApp`
* `IotStartup remove headless [Task1]` removes headless applications that match pattern `Task1`
* `IotStartup startup` lists headed and headless applications registered for startup
* `IotStartup startup [MyApp]` lists headed and headless applications registered for startup that match pattern `MyApp`
* `IotStartup startup headed [MyApp]` lists headed applications registered for startup that match `MyApp`
* `IotStartup startup headless [Task1]` lists headless applications registered for startup that match `Task1`
* `IotStartup run [MyApp]` start app identified by `MyApp`
* `IotStartup stop [MyApp]` stop app identified by `MyApp`
* For further help, try `IotStartup help`

### **Change settings for region and user or speech language:**

The `IoTSettings` tool changes region, user language, or speech language. This is a command line tool that can be invoked from an application using the ProcessLauncher API. These commands must be run as default account, not administrator.

* `IotSettings del account {all | username}` deletes all MSA or Azure AD accounts on the system or a specific account.  Specific accounts take the form username@provider.com
* `IotSettings del diagnostics` deletes diagnostic information in the cloud for the current device.  Note that this removes the history up to the time of invocation.  New diagnostics information will continue to be logged.
* `IotSettings list account` lists all MSA or Azure AD accounts that have been signed into the device.
* `IotSettings list uilanguage` lists all UI languages
* `IotSettings list speechlanguage` lists all speech languages
* `IotSettings get uilanguage` displays current UI language
* `IotSettings get speechlanguage` displays current speech language
* `IotSettings get region` displays current region
* `IotSettings set uilanguage language\_tag - (e.g. fr-CA)` sets default UI language French Canadian)
* `IotSettings set speechlanguage language\_tag - (e.g. fr-CA)` sets speech language French Canadian)
* `IotSettings set region region\_code - (e.g. CA)` sets default region to Canada)
* `IotSettings set bluetoothpref {sink | source}` Specifies the Bluetooth role preference to select when devices built with both IOT_BLUETOOTH_A2DP_SOURCE and IOT_BLUETOOTH_A2DP_SINK features connect to another device that also supports both roles.
* `IotSettings get bluetoothpref` returns the current Bluetooth role preference for devices built with both IOT_BLUETOOTH_A2DP_SOURCE and IOT_BLUETOOTH_A2DP_SINK.  The default is source.

> [!TIP]
> `IoTSettings -list uiLanguage` will give back the list of supported UI language (in the version of Windows IoT core image it has been executed against)

### **Change default audio device and volume:**

The `IoTCoreAudioControlTool` tool controls audio related options, such as setting default capture and playback devices and changing the volume. For a full list of parameters, run `IoTCoreAudioControlTool h`.

### **Manually installing .APPX files:**
DeployAppx enables installing, and removing in .APPX packages in development scenarios.  The correct method for installing .APPX packages in production images is to use a provisioning package as documented in the [Install your app](../develop-your-app/appinstaller.md#using-provisioning-package-from-wcd) subject.  DeployAppx also supports querying .APPX package information.

*  `DeployAppx install MyApp.appx` installs the .APPX and the certificate of the same name if found.
* `DeployAppx install force MyApp.appx` forces uninstalling the currently installed .APPX with the same package name if found before installing the new .APPX.  This is useful for installing an .APPX with the same or lower version number as the currently installed .APPX.
* `DeployAppx install retry MyApp.appx` retry installing the .APPX 10 times on failure with 2-second delay between attempts.
* `DeployAppx uninstall App_1.0.1.0_x86__publisherid123` uninstall the .appx with the matching package full name.
*  `DeployAppx uninstall MyApp.appx` uninstall any installed .APPX with a matching package family name.
* `DeployAppx getpackages` lists installed package full names.
* `DeployAppx getpackageid IotCoreDefaultApp.appx` prints out the package name, the package family name, and the package full name for the .APPX.
```cmd
DeployAppx getpackageid IotCoreDefaultApp.appx
         Package Name: 16454Windows10IOTCore.IOTCoreDefaultApplication
  Package Family Name: 16454Windows10IOTCore.IOTCoreDefaultApplication_rz84sjny4rf58
    Package Full Name: 16454Windows10IOTCore.IOTCoreDefaultApplication_2.0.8.0_arm__rz84sjny4rf58
```
* `DeployAppx register appxmanifest.xml` unsupported


## General Command Line Utils

### **Update account password:**

It is highly recommended that you update the default password for the Administrator account. To do this, you can issue the following command: `net user Administrator [new password]` where `[new password]` represents a strong password of your choice.

### **Create local user accounts:**

If you wish to give others access to your Windows IoT Core device, you can create additional local user accounts using PS by typing in `net user [username] [password] /add`. If you wish to add this user to other groups, such as the Administrator group, use `net localgroup Administrators [username] /add`.

### **Set password:**

To change the password on an account on your device, run `net user [account-username] [new-password]` to change the account password.

### **Query and set device name:**

To identify your current device name, simply type `hostname`. To change the name of your Windows IoT Core device, type `SetComputerName [new machinename]`. You may need to restart your device for the name change to take effect.

### **Basic network configuration:**

Many of the basic network configuration utilities you may already be familiar with are available in Windows IoT Core, including commands such as `ping.exe`, `netstat.exe`, `netsh.exe`, `ipconfig.exe`, `tracert.exe`, and `arp.exe`.

### **Copy utilities:**

Microsoft is providing familiar tools, including `sfpcopy.exe` as well as `xcopy.exe`.

### **Process Management:**

To view currently running processes, you can try either `get-process` or alternatively `tlist.exe`. To stop a running process, type `kill.exe [pid or process name]`.


### **Set Boot Option (Headless vs. headed boot):**

Windows IoT Core devices can be set to headed (when display capabilities are required) or headless (when a display is not required or available) device mode. To change this setting, use `setbootoption.exe [headed | headless]`.

> [!NOTE]
> Changing this setting will require a reboot in order for the change to take effect.

### **Task scheduler:**

To view the current list of scheduled tasks, use the `schtasks.exe` command. You can create new tasks with the `/create` switch or run on-demand tasks with the `/run` switch. For a full list of supported parameters, use `schtasks.exe /?`

### **Device drivers:**

The device console utility is useful in identifying and managing installed devices and drivers. For a full list of parameters, use `devcon.exe /?`

### **Registry Access:**

If you need to access the registry to view or modify settings, use the `reg.exe /?` Command for the full list of supported parameters.

### **Services:**

Managing Windows services can be accomplished via the `net.exe` command. To see a list of running services, type `net start`. To start or stop a specific service, type `net [start | stop] [service name]`. Alternatively, you can also use the service control manager via `sc.exe` command.

### **Boot configuration:**

You can make changes to the boot configuration of your Windows IoT Core device by using `bcdedit.exe`. For instance, you can enable testsigning with `bcdedit –set testsigning on` command.

### **Shutdown/restart device:**

To shut down your device, type `shutdown /s /t 0`. To restart the device, use the `/r` switch instead with the command `shutdown /r /t 0`.

### **Viewing and changing display settings**
The SetDisplayResolution tool may be used for listing the current display settings and to show the list of supported values.  It can further be used for adjusting the display's resolution, refresh rate and/or orientation to values supported by your platform.  The utility accepts the following command line arguments:

* `SetDisplayResolution` Lists the current display resolution.
* `SetDisplayResolution -list` Lists supported display resolutions.
* `SetDisplayResolution -orientation:[n]` Change the display orientation, where n=0,90,180 or 270.
* `SetDisplayResolution [width] [height]` Change the width and height in pixels
* `SetDisplayResolution [width] [height] [refreshrate]` Change width, height, and refresh rate where width and height are in pixels and refreshrate in Hz
* `SetDisplayResolution [width] [height] [refreshrate] [orientation]` Change width, height, refreshrate and screen orientation where width and height are in pixels, refreshrate in Hz and orientation is one of 0, 90, 180 or 270.

### **Take screenshot:**

You can take the screenshot of your Windows IoTCore device by using `ScreenCapture.exe`. For example, run `ScreenCapture c:\folder\screencap.jpg` will take the screenshot and save it in screencap.jpg file.

### **Get information about Network Adapters:**

To view the list of all the available network adapters, run `GetAdapterInfo` tool.

### **Set folder permissions for UWP apps:**

Not all folders on your device are accessible by Universal Windows Apps. To make a folder accessible to a UWP app, you can use `FolderPermissions` tool. For example, run `FolderPermissions c:\test -e` to give UWP apps access to `c:\test` folder. Note this will work only with native Win32 apis for eg. CreateFile2 and not with WinRT apis like StorageFolder, StorageFile etc.

### **Work with Serial Ports:**
[MinComm](https://github.com/ms-iot/samples/tree/develop/MinComm) allows you to work with serial ports from the command line. It is provided as a sample project in the ms-iot samples repo.

```
Usage: MinComm.exe [-list] device_path [baud=<B>] [parity=<P>] [data=<D>] [stop=<S>] [xon={on|off}] [odsr={on|off}] [octs={on|off}] [dtr={on|off|hs}] [rts={on|off|hs|tg}] [idsr={on|off}]

  -list                List all available serial ports on the system and exit.
  device_path          Device path or COM port to open (e.g. COM1)
  baud=<B>             Specifies the transmission rate in bits per second.
  parity={n|e|o|m|s}   Specifies how the system uses the parity bit to check
                       for transmission errors. The abbreviations stand for
                       none, even, odd, mark, and space.
  data={5|6|7|8}       Specifies the number of data bits in a character.
  stop={1|1.5|2}       Specifies the number of stop bits that define the end of
                       a character.
  xon={on|off}         Specifies whether the xon or xoff protocol for data-flow
                       control is on or off.
  odsr={on|off}        Specifies whether output handshaking that uses the
                       Data Set Ready (DSR) circuit is on or off.
  octs={on|off}        Specifies whether output handshaking that uses the
                       Clear To Send (CTS) circuit is on or off.
  dtr={on|off|hs}      Specifies whether the Data Terminal Ready (DTR) circuit
                       is on or off or set to handshake.
  rts={on|off|hs|tg}   Specifies whether the Request To Send (RTS) circuit is
                       set to on, off, handshake, or toggle.
  idsr={on|off}        Specifies whether the DSR circuit sensitivity is on
                       or off.

Parameters that are not specified will default to the port's current
configuration. For more information on the connection parameters, see the
Technet documentation for the Mode command:
  https://technet.microsoft.com/library/cc732236.aspx

Examples:
  Connect to the first serial port found in the port's current configuration:
    MinComm.exe

  List all serial ports on the system:
    MinComm.exe -list

  Open COM1 in 115200 8N1 configuration:
    MinComm.exe COM1 baud=115200 parity=n data=8 stop=1

  Open COM1 in 115200 8N1 configuration:
    MinComm.exe \\.\COM1 baud=115200 parity=n data=8 stop=1

  Open device interface in 115200 8N1 configuration:
    MinComm.exe \\?\USB#VID_FFFF&PID_0005#{86e0d1e0-8089-11d0-9ce4-08003e301f73} baud=115200 parity=n data=8 stop=1
```