---
title: Overview of Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 01/18/2018
ms.topic: article
description: Learn about what Windows 10 IoT Core is and what you can do with it.
keywords: Windows 10 IoT Core, small footprint, headless 
---

# An overview of Windows 10 IoT Core

> [!NOTE]
> Windows Containers are supported for commercial deployments on Windows Server, Windows IoT Server, Windows IoT Enterprise and Windows IoT Core.  As of Windows October Update 2018 (Build 17763), Windows Containers can only be used with Windows Enterprise and Professional for dev/test purposes.

## What is Windows 10 IoT Core?
Windows 10 IoT Core is a version of Windows 10 that is optimized for smaller devices with or without a display that run on both ARM and x86/x64 devices. The Windows IoT Core documentation provides information on connecting, managing, updating, securing your devices, and more. 

If you're ready to go to the next level and start commercializing your solution, you can learn how to manufacture with Windows 10 IoT Core with our [Windows 10 IoT Core Manufacturing Guide](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-manufacturing-guide). 

## Getting started

Before attempting to manufacture a device, it's best to first try and prototype a device with Windows 10 IoT Core. That way, you can understand what features you'll need and what configurations you'll want when it's time to manufacture.

<table>  
<colgroup>  
<col width="50%" />  
<col width="50%" />  
</colgroup>  
<thead>  
<tr class="header">  
<th align="left">Topic</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>

<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/en-us/windows/iot-core/tutorials/quickstarter/PrototypeBoards"
>1. Pick a prototype board</a></p></td>
<td align="left"><p>Take a look at common prototype boards and choose one to start prototyping with.</p></td>
</tr>

<tr class="odd">
<td align="left"><p>2. Flash a prototype image</p></td>
<td align="left"><p>Go to our tutorial sections to learn how to flash prototype images onto your selected device(s). </p></td>
</tr>

<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/appinstaller">2. 3. Install your app</a></p></td>
<td align="left"><p>Learn how to install your app using different tools.</p></td>
</tr>

<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/appdeployment">4. Deploy your app</a></p></td>
<td align="left"><p>Learn how to deploy an app using Visual Studio.</p></td>
</tr>

</tbody>
</table>

## Differences between Windows 10 Desktop and Windows 10 IoT Core

### Different features available on Desktop and IoT Core

* Inbox Cortana is no longer available on Windows 10 IoT Core since version 1809 (17763). If you are looking to bring a voice-enabled device to market quickly, you can integrate Cortana support into the device using the [preview of the Cortana Devices SDK](https://developer.microsoft.com/en-us/cortana/devices).
* The [FileOpenPicker API](https://docs.microsoft.com/en-us/uwp/api/windows.storage.pickers.fileopenpicker) is not supported in Windows 10 IoT Core. To access local drives or removable storage, you can implement this in your own application.
* Out of the box, The Windows 10 IoT Core device will boot to the [default app](https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/iotcoredefaultapp) instead of a desktop-like PC. However, for commercialization, this default app **must** be replaced by either a custom app or a default app that can be modified. The purpose of this application is not only to provide you with a friendly shell to interact with upon first boot, but to also allow you to use the [open-sourced code](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/IoTCoreDefaultApp) for this application so that you can use these features to plug and play your own custom application(s).

### Differences in driver-supported areas

* Windows 10 Desktop has more supported drivers than Windows 10 IoT Core. To make the same device(s) work on Windows 10 IoT Core as on Desktop, you may need to build a driver from soruce for a Windows 10 IoT Core device or find another workaround, especially for ARM architecture.
* There is no out-of-the-box driver for libusb for Windows 10 IoT Core (ARM) - you will need to build from source to target the ARM architecture.

### Differences in available registry set

* On desktop, there is an option to "Automatically hide scroll bars in Windows" that can be set to off. It is controlled by the following registry entry: 

```
HKEY_CURRENTUSER\Control Panel\Accessibility
```

* There is no such registry on Windows 10 IoT Core devices by default. You will need to add a "Dynamic Scrollbars" register if you want.
* To enable hide scroll bars automatically in a UWP application, you can add the "DynamicScrollbars" register and set the value to "1" like this:

```
REG ADD "HKCU\Control Panel\Accessibility" /v DynamicScrollbars /t REG_DWORD \d "1"
```

* The registry key must be set from the Default Account. If the ScrollViewer's XAML setting is "Visible", the nthe registry setting of 0 will force the scroll bar to appear regardlss of whether there is sufficient content to have the scroll appear in the UI. A registry setting of 1 will keep the scroll bar hidden until there is sufficient content.

```
<TextBox Height="200" Width="100" IsEnabled="True" FontSize="50" TextWrapping="Wrap" ScrollViewer.VerticalScrollBarVisibility="Visible" Text="..."/>
```

* Lastly, if the ScrollViewer XAML's setting is "Auto" then the registry setting of 0 will only show the full scroll bar when there is enough content to display the scroll bar. When the registry setting is 1, the scroll bar will appear then when there is enough content or hidden if there is no content.

```
<TextBox Height="200" Width="100" IsEnabled="True" FontSize="50" TextWrapping="Wrap" ScrollViewer.VerticalScrollBarVisibility="Auto" Text="..."/>
```

### Different commands supported

* The PowerShell Remove-AppxPackage command works on Desktop but not on Windows 10 IoT Core.
* Not all folders on your device are accessible by Universal Windows Apps. On Windows 10 IoT Core you can use the FolderPermissions tool to make a folder accessible to a UWP app. For example, run FolderPermissions c:\test -e to give UWP apps access to c:\test folder. However, this is not available on Desktop.

All differences described in this post may not be valid in the future because Windows 10 IoT Core is constantly being updated.

## Helpful resources
[Read our documentation](https://docs.microsoft.com/windows/iot-core/) to learn more about Windows 10 IoT Core.
