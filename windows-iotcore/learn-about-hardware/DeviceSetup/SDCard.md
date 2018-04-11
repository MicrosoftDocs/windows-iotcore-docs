--- 
title: Setting up your device with a SD Card
author: saraclay 
ms.author: saclayt 
ms.date: 04/10/2018 
ms.topic: article 
description: Learn about how to set up your device with Windows 10 IoT Core using a SD Card.
keywords: Windows 10 IoT Core, SD Card, Windows 10 IoT Core Dashboard
--- 

# Setting up your device with a SD Card

## About

Devices that can be flashed with a SD card include Raspberry Pi boards and MinnowBoard Turbot boards. You'll want to grab the latest firmware update possible.

> [!IMPORTANT]
> The latest 64-bit firmware for Minnowboard Turbot can be found on the [Minnowboard website](https://minnowboard.org/tutorials/updating-the-firmware) (skip step 4 on the Minnowboard site's instructions).

## Using the Dashboard
> [!Video https://www.youtube.com/embed/JPRUbGIyODY]

1. Download the Windows 10 IoT Core Dashboard [here](https://developer.microsoft.com/en-us/windows/iot/Downloads).
2. Once downloaded, open the Dashboard and click on *set up a new device* and insert a SD card into your computer.

> [!TIP]
> We recommend using a high-performance SD card for increased stability.

![Dashboard screenshot](../../media/SDCard/Dashboard-Screenshot.jpg)

3. Fill out all of the fields as indicated
4. Accept the software license terms and click *Download and install*.

> [!TIP]
> We recommend plugging your device into an external display to see the default application booting up.

## Connecting to a network

### Wired connection
If your device comes with an Ethernet port or USB Ethernet adapter support to enable a wired connection, attach an Ethernet cable to connect it to your network.

### Wireless connection
If your device supports Wi-Fi connectivity and you've connected a display to it, you'll need to:

1. Go into your default application and click the settings button next to the clock.
2. On the settings page, select *Network and Wi-Fi*.
3. Your device will begin scanning for wireless networks.
4. Once your network appears in this list, select it and click *Connect*.

If you haven't connected and display and would like to connect via Wi-Fi, you'll need to:

1. Go to the IoT Dashboard and click on *My Devices*.
2. Find your unconfigured board from the list. Its name will begin with "AJ_"... (e.g. AJ_58EA6C68). If you don't see your board appear after a few minutes, try rebooting your board.
3. Click on *Configure Device* and enter your network credentials. This will connect your board to the network.

## Connecting to Windows Device Portal

Use the [Windows Device Portal](../../manage-your-device/DevicePortal.md) to connect your device through a web browser. The device portal makes valuable configuration and device management capabilities available. 

