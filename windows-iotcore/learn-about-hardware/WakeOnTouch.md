---
title: Wake on Touch
author: jordanrh1
: jordanrh
ms.date: 09/17/2018
ms.topic: article
description: Configure your device to wake on touch
keywords: windows iot, screen, sleep, wake, touch, standby, power
ms.custom: RS5
---

# Configure your device to wake on touch

In some scenarios, you want your device's screen to turn off while not in use and to turn on quickly when a user touches the touchscreen. This document describes how to configure your device to achieve this scenario.

## Setting a video idle timeout

You can configure the screen to turn off after a period of inactivity by setting a video idle timeout. When the user has not interacted with the device for a specified length of time, the screen will turn off. This will enable the device to enter a low power state by powering down components related to the display.

```
	powercfg.exe /setacvalueindex SCHEME_CURRENT SUB_VIDEO VIDEOIDLE 10
	powercfg.exe /setdcvalueindex SCHEME_CURRENT SUB_VIDEO VIDEOIDLE 10
	powercfg.exe /setactive SCHEME_CURRENT
```

For more information, see [Display Idle Timeout](/windows-hardware/customize/power-settings/display-settings-display-idle-timeout) and [Display, sleep, and hibernate idle timers](/windows-hardware/design/device-experiences/display--sleep--and-hibernate-idle-timers).

## Disabling modern standby

On AoAC systems (which includes all ARM systems), the system will automatically enter [modern standby](/windows-hardware/design/device-experiences/modern-standby) when the display goes off. When a system is in modern standby, it can only be woken by certain inputs. This is not an exhaustive list, but these inputs include pressing the power button, opening the lid on a laptop, or clicking the mouse. Touching the screen will not wake up the device from modern standby. If you want your device to wake up by touch, you have to configure the device not to enter modern standby. To disable modern standby, set the following registry key and reboot.

```
	reg add HKLM\System\CurrentControlSet\Control\Power /v PlatformAoAcOverride /t REG_DWORD /d 0
```
	
Disabling modern standby can impact power consumption when the system is idle. You should measure your system's power consumption with modern standby enabled and disabled before making the decision to disable modern standby.

Modern standby is a software mechanism that attempts to quiet system activity as much as possible, thereby allowing hardware to enter a low power state. In theory, a sufficiently quiet device with modern standby disabled can achieve the same low power consumption as a device in modern standby. It is important to minimize background activity including software timers and periodic tasks if modern standby is disabled.
