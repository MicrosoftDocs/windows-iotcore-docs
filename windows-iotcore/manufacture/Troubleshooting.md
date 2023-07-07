---
author: EliotSeattle
description: Troubleshooting different commercialization-related issues.
title: 'Troubleshooting'
ms.author: eliotgra
ms.date: 08/28/2018
ms.topic: article
ms.custom: RS5
---

# Troubleshooting
Having worked with a number of people, teams, and companies interested in commercializing, the Windows 10 IoT team decided to publish learnings from troubleshooting different issues. To find something specific, use Ctrl+F to find a word or phrase. Have any insight you want to add? Create a PR for this documentation or provident content feedback below.

> [!TIP]
> For troubleshooting issues related to development, please read the [Troubleshooting doc]() in our developer documentation.


## Identifying SKU
```GetProductInfo API``` identifies the IoT Core SKU/Edition information.
Edition/Product ID will be baked into the image.

PRODUCT_IOTUAP:
```0x0000007B``` = Windows 10 IoT Core

You can find more information about edition IDs [here](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getproductinfo). 

## Mapping hardware vkeys on Windows 10 IoT Core

Switch to reporting as a HID keyboard and sending VKs instead of consumer controls. 

## Minimizing memory allocation
If you want to minimize OS controlled memory and processing for display, make sure that the OS is clear and that no display is attached. Make sure the Intel INF settings are not faking a display when none is attached and configure any outputs to be external DisplayPort. This should result in DWM running but acting as if the monitor is idle. 

## Retrieving lots and getting crash dumps

For UWP apps specifically:
1. Get your app store-signed and you'll receive telemetry through the app portal on Dev Center. You will receive cal stacks, but not full dumps.
2. You can use [_WerRegisterAppLocalDump_](/windows/desktop/api/werapi/nf-werapi-werregisterapplocaldump) to get your app to dump logs and then you can have the app upload them to wherever you like.
3. Additionally, you can instrument even further with VSAppCenter or [HockeyApp](https://hockeyapp.net/#s).

For system issues (NTServices, OS stability or driver):
1. We are working on a Partner Telemetry Insights portal to enable customers to receive call stacks and info on crashing services, OS components, and drivers.
2. You can have a custom script or exe to harvest dmp files from the device.
3. You can use Azure IoT DM to configure ETW tracing on the device as required and [capture logs](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/diagnostic-logs-management.md).
4. You can build a custom exe to call into wevtapi.dll and record the last shutdown reason.

## Running SLEEPSTUDY

If you run into the error 0x080004005 while trying to run SLEEPSTUDY in Windows 10 IoT Core, you will need to do the following to generate a SLEEPSTUDY report:
1. From SSH/PowerShell, run this command on IoT COre; ```powercfg / sleepstudy / xml```
2. This will generate a "sleepstudy-report.xml".
3. Copy the generated sleepstudy-report.xml report to a desktop machine and run "powercfg/sleepstudy/transformxml sleepstudy-report.xml"
4. The final sleepstudy-report.html will be generated.

## Servicing apps and dealing with NTServices

Fast app iterations can be done with the App Store or using Azure Blob. With the app store, you do not have to pay for the CDN and egrees. There is also worldwide CDN coverage for free with the store. It is a good rule of thumb to get a Store ID and Store Update ready when shipping for a fast app update.

## Setting Bluetooth Class of Device to "not a PC"

For good interop and Bluetooth compatibility, it’s important that the Bluetooth stack indicates a proper class of device (COD). The various values are defined by the standard are [here](https://www.bluetooth.com/specifications/assigned-numbers/baseband).
  
By default, Windows reads the form factor data from the SmBios enclosure type value (See table 17 on page 38) and derives the Major Device Class and Minor Device Class fields of the CoD from that. If a platform wants to override the default COD assigned via the enclosure type, it can do so by setting the “COD Major” and “COD Type” values documented [here](/previous-versions//ff536602(v=vs.85)). 


## Setting the computer name

IoT has a built-in Win32 tool called “SetComputerName”.  This can be called to change the computername.  A reboot is required to change the name.  Unfortunately, this utility must be called from the administrator context and UWP apps run in the DefaultAccount user context. 
  
One way to workaround this is to run a batch file from a manually triggered scheduled task that calls SetComputerName.  The batch file, will need to read the desired computername from a text file that your main UWP app will save the name into.  For example, the UWP app could could save a file to the public documents folder and the batch file would read it from there.  The UWP app would then need to use the process launcher (to trigger the scheduled task to run (e.g. schtasks /run /TN “SetMyComputerNameTask”) 
  
Read processlauncher docs [here](/uwp/api/windows.system.processlauncher)
Read schTasks docs [here](/windows/win32/taskschd/schtasks)