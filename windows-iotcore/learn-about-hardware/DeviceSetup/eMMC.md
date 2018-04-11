--- 
title: Setting up your device with eMMC
author: saraclay 
ms.author: saclayt 
ms.date: 04/11/2018 
ms.topic: article 
description: Learn about how to set up your device with Windows 10 IoT Core using eMMC.
keywords: Windows 10 IoT Core, eMMC, flashing
--- 

# Setting up your device with eMMC

## About

Devices that can be flashed with a SD card include the AAEON Up Squared Board.

## Flashing with eMMC

1. Download and install the [Windows Assessment and Deployment kit](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install) with the correlating version of Windows 10 you're running.
2. Insert a USB drive into your machine.
3. Create a US-tootable WinPE image:
* Start the Deployment and Imaging Tools Environment `(C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools)` as an administrator.
* Create a working copy of the Windows PE files. Specify either x86, amd64 or ARM: `Copype amd64 C:\WINPE_amd64`
* Install Windows PE to the USB flash drive, specifying the WinPE drive letter below. More information can be found [here](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-create-usb-bootable-drive). `MakeWinPEMedia\UFD C:\WinPE+amd64 P:`
4. Download the [Windows 10 IoT Core image](https://downloads.up-community.org/?post_type=wpdmpro&p=204&preview=true) by double-clicking on the downloaded ISO file and locating the mounted Virtual CD-drive.
5. This drive will contain an install file (.msi); double click it. This will create a new directory on your PC under C:\Program Files (x86)\Microsoft IoT\FFU\ in which you shoul d see an image file, "flash.ffu".
6. Download, unzip and copy the [eMMC Installer script](https://github.com/ms-iot/content/blob/develop/Resources/eMMCInstaller.zip) to the USB device's root directory, along with the device's FFU.
7. Connect the USB drive, mouse, and keyboard to the USB hub. Attach the HDMI display to your device, the device to the USB hub, and the power cord to the device.
8. Go to the BIOS setup of the device. Select *Windows* as the Operating system and set the device to boot from your uSB drive. When the system reboots, you will see the WinPE command prompt. Switch the WinPE prompt to the USB Drive. This is usually C: or D: but you may need to try other driver letters.
9. Run the eMMC Installer script, which will install the Windows 10 IoT Core image to the device's eMMC memory. When it completes, press any key and run `wpeutil reboot`. The system should boot into Windows 10 IoT Core, start the configuration process, and load the default application.

> [!NOTE]
> Make sure the device is now booting from the eMMC memory by entering the BIOS setup again and switching the Boot Drive order to load from the Hard Drive instead of from the USB Drive.


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

