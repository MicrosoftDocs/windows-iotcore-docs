---
title: Use DISM to flash Windows 10 IoT Core
author: bfjelds
ms.author: Brian.Fjeldstad
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use DISM to flash Windows 10 IoT Core onto a micro SD card.
keywords: windows iot, DISM, Deployment Image Servicing Management, SD card, flash, OS
---

# Use DISM to flash Windows 10 IoT Core

## An alternative method to IoT Dashboard

You can use Deployment Image Servicing and Management(Dism.exe) to flash Windows 10 IoT Core on your SD card. You will need a FFU image file corresponding to your device type. 

* Open an administrator command prompt and navigate to the folder containing your local flash.ffu file.

* Plug-in your SD card to your machine. 

* Find the disk number that your SD card is on your computer.  This will be used when the image is applied in the next step.  To do this, you can use the diskpart utility.  Run the following commands:
	
	    c:\FFUFolder>diskpart
	    	
	    DISKPART>list disk
	
    It should list all the storage devices attached to the computer. 
	
	![DISM List Disk](../media/Dism/DiskpartListDisk.png)
	
	Note the disk number and type exit to exit diskpart. 

	    DISKPART>exit
	
* Using the administrator command prompt, apply the image to your SD card by running the following command (be sure to replace PhysicalDriveN with the value you found in the previous step, for example, in this case SD card is disk number 4, so we will use  `/ApplyDrive:\\.\PhysicalDrive4` below)

	    dism.exe /Apply-Image /ImageFile:"[FULLPATH]\flash.ffu" /ApplyDrive:\\.\PhysicalDriveN /SkipPlatformCheck
		
* Click on the "Safely Remove Hardware" icon in your task tray and select your USB SD card reader to safely remove it from the system.  Failing to do this can cause corruption of the image.

> [!NOTE]
> If you want to remove Windows 10 IoT Core from your SD card after you are done using it, see the [FAQ](https://developer.microsoft.com/en-us/windows/iot/faqs) section titled **How do I remove Windows 10 IoT Core from my SD card?**.
