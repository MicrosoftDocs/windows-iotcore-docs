---
title: Release Notes for Raspberry Pi 3B+
author: zeeshanfurqan
ms.author: zeeshan.furqan
ms.date: 05/16/2018
ms.topic: article
description: Read and learn about what's in the build for Raspberry Pi 3B+.
keywords: windows iot, Windows Insider, release notes, Raspberry Pi 3B+
---

# Release Notes for Raspberry Pi 3B+

&copy; 2018 Microsoft Corporation. All rights reserved.

> [!NOTE]
> This release for the Raspberry Pi 3B+ is a technical preview and there is currently no timeline for a release version. Limited validation and enablement has been completed. For a better evaluation experience and for any commercial products, please use the Raspberry Pi 3B or other devices with supported Intel, Qualcomm, or NXP SoCs. If there are any reasons as to why you cannot use the 3B over the 3B+ for a production solution, please file an issue on our GitHub, [here](https://github.com/MicrosoftDocs/windows-iotcore-docs/issues). 

## What's new in this build: 
* General bug fixes

## Known issues in this build:
* This image is only meant for RPi3B+ and will not boot on RPi2. 
* F5 driver deployment from Visual Studio does not work on IoT Core. 
* Onboard WIFI and Bluetooth do not work on RPI3B+. 
* Ft5406 touch screen driver is disabled on RPi3B+. 
* SD card activity LED is disabled. 


### Display resolution is monitor is disconnected
The Raspberry Pi 3B+ may not maintain Display Resolution if monitor is disconnected. The EDID of the monitor is used to set the resolution of the system when one is connected. When disconnected, the firmware defaults to what is in the config.txt in the root of the SD card. 


### Video performance
Video playback performance on the platform is not optimized.  Animated user elements including XAML-based dropdown menus may exhibit less than optimal performance.  

### Camera support
Support for camera peripheral devices is limited. The PiCam device directly connected to the onboard camera bus is not supported due to limitations in the platform to support D3D Modern USB webcams produce data streams that are very demanding on the USB Host controller.  Even when used with low resolution settings webcams will require additional USB fine tuning and specialized control logic.  


### Mouse pointer disappears while debugging
In some cases, the mouse pointer is not visible after deploying or debugging apps with Visual Studio, the mouse pointer should reappear if you change focus using the keyboard (Tab) (8038595).

### Server applications with SoftAP
When using the SoftAP clients will not be able to access content exposed by UAP apps. To expose UAP applications via SoftAP the following changes must be made from the console on the device (8111807):  

```
reg add hklm\system\currentcontrolset\services\mpssvc\parameters /v IoTInboundLoopbackPolicy /t REG_DWORD /d 1 
checknetisolation loopbackexempt -a -n=<AppID for SoftAP App> 
checknetisolation loopbackexempt -a -n=<AppID for Additional App>  
For example:  checknetisolation loopbackexempt -a -n=IoTOnboardingTask-uwp_1w720vyc4ccym 
```

Reboot.

### Sensor Driver conflict in pre-built FFUs 
There is a Sensor Driver Conflict in the provided FFUs. The Remote Sensor Framework installs drivers for Compass, Magnetometer, Accelerometer and Gyro. The UWP APIs for accessing these from an application assume just one is installed. If you are developing a driver for a physically attached device, the remote driver on the Microsoft provided FFUs will conflict.  

To solve for this, the conflicting driver can be removed by connecting to the device via SSH or Powershell and using the tool devcon.exe to remove the remote sensor driver by typing: 

```
"devcon.exe remove @"ROOT\REMOTESENSORDRIVER*"
```

The remote sensor driver does not affect OEM created FFUs. 


### Default administrator user name and password
The default administrator user name and password are hard coded in the Windows 10 IoT Core image. This is a security risk for the device, and it should not be exposed to an open internet connection until the password has been changed. 

### Volume controls
Hardware volume controls for USB microphones and speakers which depend on Windows system to change system volume are currently not supported on Windows 10 IoT Core. 

### USB keyboards
Some USB keyboards and mice may not work on IoT Core. Use a different keyboard or mouse. A list of validated peripheral devices can be found in the documentation [here](http://go.microsoft.com/fwlink/?LinkId=619428).
 
### Screen orientation
Setting the orientation to “Portrait” may not be honored in a Universal App.

### Referencing adapters with AllJoyn templates
Attempting to add references to AllJoyn adapter projects may result in errors when using specific SDK versions.  To resolve these errors, change Visual Studio’s target platform to match the current SDK version, then reload the project.  

### WiFi Direct limitations on Windows 10 IoT Core
1. The Windows 10 IoT Core device has to be the connecting device – it will not work as the advertising device with another device initiating the connection.   
2. Advanced pairing must be used.  The sample app demonstrates how to use the advanced pairing API’s to pair the devices prior to connecting. 
3. Not all wireless adapters support WiFi direct. We have tested and validated that the "Realtek RTL8188EU Wireless Lan 802.11n USB 2.0 Network adapter" works, but other adapters may not be supported. 

### Non-default drive mode (3890679) 
On Raspberry Pi and Dragonboard, switching from a non-default drive mode to a different non-default drive mode may produce a glitch on the GPIO pin. To workaround this issue, set drive mode once at the beginning of the application. 

### Application already running (1244550) 
The Default startup app may conflict with itself when it is also deployed from Visual Studio. WORKAROUND: Change the default startup app to an application other than that you wish to deploy. 

### BackgroundMediaPlayer.MessageReceivedFromForeground may crash (2199869) 
The following line of code may crash: 
```
BackgroundMediaPlayer.MessageReceivedFromForeground += OnMessageReceivedFromForeground
```

To prevent the crash, add this code so that it is executed first:
```
var player = BackgroundMediaPlayer.Current;
```

### Azure Active Directory Authentication Support (4266261) 
The Azure Active Directory Authentication Library does not work on Windows 10 IoT Core.  

### Shell Management of Application Crashes
IoT Core’s shell infrastructure monitors APPX-type applications running on the device for crashes, and restarts those applications when crashes occur.  If the restarted applications continue to crash, the shell will employ a failfast – a system critical process that causes a bugcheck and reboot in an attempt to recover.  Comparable logic and handling is used to background tasks and foreground applications in a headed configuration.   Crash handling and retry logic is captured below:

```
Software\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\CBTConfig  (or ForegroundAppConfig for headed) 
  Qword:"FailureResetIntervalMs" – length of time app has to run successfully to reset failures seen to 0. – default is 0x00000000000493E0 == 5 minutes 
  Qword:"BaseRetryDelayMs"  -- wait time coefficient.  Default is 0xa. 
  Dword:"MaxFailureCount". Default is 10 
  DWord:"FallbackExponentNumerator", default is 31. 
  Dword:"FallbackExponentDenominator", default is 20 
  
  
Fallback_exponent = FallbackExponentNumerator / FallbackExponentDenominator; // default is 1.55 
When app crash is detected: 
    if time_since_last_crash > failureresetinterval then crashes_seen = 1 
    else ++crashes_seen; 
  
if crashes_seen > MaxFailureCount then __failfast; 
  
else  
  
delay = (dword) ((float)BaseRetryDelayMs * (crashes_seen ** Fallback_exponent)) 
```

Wait for the delay and relaunch the app.

#### Dragonboard SPI runs at 4.8Mhz
The SPI on the Dragonboard will ignore the requested speed and always run at 4.8 Mhz.  

#### Dragonboard Connected Standby 
Connected Standby is not enabled on the Qualcomm Dragonboard by default.  To enable Connected Standby on DragonBoard the following registry key needs to be set to “1”.


### Time synchronization
If time sync is failing or timing out this may be due to unreachable or a distant time server, the following can be done to add additional or local time servers. 
 
1. From a command line on the device (eg. SSH, Powershell).
   ```
   w32tm /config /syncfromflags:manual /manualpeerlist:"0.windows.time.com 1.pool.ntp.org 2.something else, ..."
   ```
2. You may also make these additions to the registry via a boot script or a custom runtime configuration package included as part of the image creation process if needed. 

### Starting the FTP Server 
* To run once -
Login with SSH\PS and run this command to start FTP:  

```
start ftpd.exe 
```

* To run on every boot, users should create a scheduler task -
Login with SSH\PS and create a scheduler task:

```
schtasks /create /tn "IoTFTPD" /tr ftpd.exe /ru system /sc onstart 
Schtasks /run /tn “IoTFTPD” 
```

### Partition size requirements for Update 
Ensure data partition maintains sufficient space for update functionality.  We recommend 1GB free for full update functionality.  If Data partition does not have enough space, updates will fail in the installation phase. 

### PowerShell log generation on IoT Core 
PowerShell on Iot Core may generate log files by default taking up space on the filesystem. Although the log file sizes are limited they can take up space potentially resulting in a low disk space situation which, among other things, can result in updates failing. The .evtx event log files have a predefined maximum size of 20 MB each. You  can individually limit files to have a different max size via registry. 
For example, To keep security.evtx at 10 MB max size: 
```
regd add HKLM\SYSTEM\CurrentControlSet\Services\EventLog\Security /v MaxSize /t REG_DWORD /d 0xa00000 /f 
```

### Schtasks limitation  
Schtasks does not support using /xml switch. 
For example: 
```
schtasks /create /xml <xmlfile> /TN <taskname>
```
This will fail on IoT Core. 
Running the command will generate the error: ERROR: The specified procedure could not be found. 
