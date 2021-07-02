---
title: Setting up Qualcomm devices
ms.date: 05/22/2019 
ms.topic: article 
ms.prod: windows-iot
ms.technology: iot
description: Learn about how to set up your Qualcomm device with Windows 10 IoT Core.
keywords: Windows 10 IoT Core, Qualcomm
ms.custom: RS5
---

# Setting up a Qualcomm device

If you're looking to manufacture with a Qualcomm device, please refer to the [IoT Core Manufacturing Guide](/windows-hardware/manufacture/iot/iot-core-manufacturing-guide). You cannot use maker images for manufacturing.

> [!NOTE]
> Make sure the device is now booting from the eMMC memory by entering the BIOS setup again and switching the Boot Drive order to load from the Hard Drive instead of from the USB Drive.

## Using eMMC

1. Download and install the DragonBoard Update Tool for your [x86](https://developer.qualcomm.com/download/db410c/windows-10-iot-update-tool-dragonboard-410c-x86.zip) or [x64](https://developer.qualcomm.com/download/db410c/windows-10-iot-update-tool-dragonboard-410c-x64.zip) machine.
2. Download the [Windows 10 IoT Core DragonBoard FFU](/windows/iot-core/downloads).
3. Double-click on the downloaded ISO file and locate the mounted Virtual CD-drive. This drive will contain an installer file (.msi); double-click on it. This creates a new directory on your PC under `C:\Program Files (x86)\Microsoft IoT\FFU\` in which you should see an image file, "flash.ffu".
4. Ensure your DragonBoard is in download mode by setting the first boot switch on the board to USB Boot, as shown below. Then, connect the DragonBoard to the host PC via a microUSB cable, then plug in the DragonBoard to a 12V (> 1A) power supply.
5. Start the DragonBoard Update Tool, which should detect that the DragonBoard is connected to your PC with a green circle. "Browse" to the DragonBoard's FFU that you downloaded, then click the _Program_ button.
6. Click "Browse" again and select "rawprogram0.xml" that was generated in step 5. Then click the "Program" button.
7. Once the download is complete, disconnect the power supply and microUSB cable from the board and toggle the USB Boot switch back to _OFF_. Connect an HDMI display, a mouse, and a keyboard to the DragonBoard and reconnect the power supply. After a few minutes, you should see the Windows 10 IoT Core default application. 

![DragonBoard in download mode](../media/DeviceSetup/db1.png)

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



