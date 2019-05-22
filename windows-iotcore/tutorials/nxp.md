---
title: Setting up a NXP device
ms.author: saclayt 
ms.date: 05/22/2019 
ms.topic: article 
description: Learn about how to set up your NXP device with Windows 10 IoT Core.
keywords: Windows 10 IoT Core, NXP
ms.custom: RS5
---

# Setting up a NXP device

> [!IMPORTANT]
> When the "format this disk" pop up comes up, do _not_ format the disk. We are working on a fix for this issue.

When setting up a NXP device for prototyping, we recommend using the Windows 10 IoT Core Dashboard. However, if you're looking to manufacture with a NXP device, please refer to the [IoT Core Manufacturing Guide](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-manufacturing-guide). You cannot use maker images for manufacturing.

## Using the Dashboard

To flash, or download, IoT Core onto your NXP device, you'll need:
* A computer running Windows 10 
* [Windows 10 IoT Core Dashboard](https://docs.microsoft.com/windows/iot-core/downloads)
* A high-performance SD card, such as a SanDisk SD card
* An external display
* Any other peripherals (e.g. mouse, keyboard, etc.)

1. Run the Windows 10 IOT Core Dashboard and click on *Set up a new device* and insert a SD card into your computer.
2. Hook up your NXP device to an external display.
3. Fill out the fields. Make sure to give your device a new name and password. Otherwise the default credentials will remain as:

```
Device: minwinpc
Password: p@ssw0rd
```

4. Accept the software license terms and click *Download and Install*. If all goes well, you'll see that Windows 10 IoT Core is now flashing your SD card.

![Dashboard screenshot](../media/DeviceSetup/Dashboard-Screenshot.jpg)

> [!Video https://www.youtube.com/embed/JPRUbGIyODY]

## Connect to a network
### Wired connection
If your device comes with an Ethernet port or USB Ethernet adapter support to enable a wired connection, attach an Ethernet cable to connect it to your network.

### Wireless connection
If your device supports Wi-Fi connectivity and you've connected a display to it, you'll need to:

1. Go into your default application and click the settings button next to the clock.
2. On the settings page, select _Network and Wi-Fi_.
3. Your device will begin scanning for wireless networks.
4. Once your network appears in this list, select it and click _Connect_.

If you haven't connected a display and would like to connect via Wi-Fi, you'll need to:

1. Go to the IoT Dashboard and click on _My Devices_.
2. Find your unconfigured board from the list. Its name will begin with "AJ_"... (e.g. AJ_58EA6C68). If you don't see your board appear after a few minutes, try rebooting your board.
3. Click on _Configure Device_ and enter your network credentials. This will connect your board to the network.

> [!NOTE]
> Wifi on your computer will need to be turned on in order to find other networks.

## Connect to Windows Device Portal

Use the [Windows Device Portal](../manage-your-device/DevicePortal.md) to connect your device through a web browser. The device portal makes valuable configuration and device management capabilities available. 

