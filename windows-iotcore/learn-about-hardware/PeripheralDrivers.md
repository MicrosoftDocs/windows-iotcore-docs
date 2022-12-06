---
title: Install USB Peripheral Drivers
ms.date: 03/20/2020
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to create a driver package and install third-party drivers on your devices.
keywords: windows iot, USB drivers, peripheral devices, USB
---

# Install USB peripheral drivers
Follow the steps below to add third-party drivers (USB) for peripheral devices such as USB Mobile broadband modems, printers, scanners etc.

## Step 1: Get Drivers from PC
___
The Step is to get the x86 version of the drivers from PC. For ARM, please contact the supplier of the peripheral to get the sys/inf files.


1. Connect the device to the windows PC

2. Install the driver for the device on the PC

3. Go to Device Manager, select this device (listed under Universal Serial Bus controllers) and right click and select Properties.

4. Go to Driver tab in the Properties window, and click on Driver Details. Note the sys files listed there.

5. Copy the sys files from `C:\Windows\system32` and also the related inf file from `C:\Windows\Inf`. You can find the inf file by searching for the sys file reference in the `.inf` files. You may need to copy additional files listed in the Inf and these will be listed in the inf_filelist.txt file created when using  `inf2pkg.cmd` in the next step.


## Step 2: Create a driver package
___

The Driver package contains the references(InfSource)to the Inf file for the driver and also lists all the files referenced in the Inf file. You can author the driver .wm.xml using [Add-IoTDriverPackage](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/Add-IoTDriverPackage.md).

[New-IoTInf2Cab](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Tools/IoTCoreImaging/Docs/New-IoTInf2Cab.md) creates the package xml file and also builds the cab file directly.

> [!NOTE]
> Windows IoT Core only supports [Universal INF and Universal Drivers](/windows-hardware/drivers/develop/getting-started-with-universal-drivers).


See also: [Sample Driver Package](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/BSP/CustomRpi2/Packages/CustomRPi2.GPIO)

## Step 3: Install on device
___

* Connect to the device ([using SSH](/windows/iot-core/connect-your-device/ssh) or [using PowerShell](/windows/iot-core/connect-your-device/powershell))
* Copy the <filename>.cab file to the device to a directory say C:\OemInstall
* Initiate staging of the package using `applyupdate -stage C:\OemInstall\<filename>.cab`. Note that this step is be repeated for each package, when you have multiple packages to install.
* Commit the packages using `applyupdate -commit`.

The device will reboot into the update OS (showing gears) to install the packages and will reboot again to main OS. This process can take a few minutes.

## Step 4: Check status of driver
___

* Launch the [PowerShell](../connect-your-device/PowerShell.md)
* You can get the status of the installed drivers using the following PowerShell commandlets

	* [Get-PnpDevice](/powershell/module/pnpdevice/get-pnpdevice?preserve-view=true&view=win10-ps)
	* [Get-PnpDeviceProperty](/powershell/module/pnpdevice/get-pnpdeviceproperty?preserve-view=true&view=win10-ps)
