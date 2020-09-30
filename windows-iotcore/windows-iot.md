---
title: Overview of Windows 10 IoT 
ms.date: 01/30/2018
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: See an overview of Windows 10 IoT and what you can do with it. Review differences between Windows 10 IoT Core, Windows 10 IoT Enterprise, and Windows 10 Desktop.
keywords: Windows 10 IoT Enterprise, Windows 10 IoT Core, headless, speech, features, binary edition, editions 
---

# An overview of Windows 10 IoT 

> [!NOTE]
> Windows Containers are supported for commercial deployments on Windows Server, Windows IoT Server, Windows IoT Enterprise and Windows IoT Core.  As of Windows October Update 2018 (Build 17763), Windows Containers can only be used with Windows Enterprise and Professional for dev/test purposes.

## What is Windows 10 IoT?
Windows 10 IoT is a member of the Windows 10 family that brings enterprise-class power, security, and manageability to the Internet of Things.  It leverages Windows' embedded experience, ecosystem and cloud connectivity, allowing organizations to create their Internet of Things with secure devices that can be quickly provisioned, easily managed, and seamlessly connected to an overall cloud strategy.  

## Windows 10 IoT Editions
Windows 10 IoT comes in two editions.  Windows 10 IoT Core is the smallest member of the Windows 10 operating system family.  While only running a single app, it still has the manageability and security expected from Windows 10.  By contrast, Windows 10 IoT Enterprise is a full version of Windows 10 with specialized features to create dedicated devices locked down to a specific set of applications and peripherals. 

## Differences between Windows 10 IoT Core and Windows 10 IoT Enterprise

While Windows 10 IoT Core and Windows 10 IoT Enterprise are similar in name, there are differences in what they offer as well as what they support. Below is a feature list that highlights edition differences.

> | Feature&nbsp;/&nbsp;Edition | Windows 10 IoT Core  |  Windows 10 IoT Enterprise  |
> |-------------|----------|---------|
> | User experience | One UWP app in the foreground at a time (see [IoT Shell documentation](https://docs.microsoft.com/windows/iot-core/develop-your-app/iotcoreshell) for app backstack handling) with supporting background apps and services. | Traditional Windows Shell with Advanced Lockdown Features |
> | Headless supported | Yes | Yes |
> | App architecture supported | UWP UI only | Full Windows UI support (e.g. UWP, WinForms, etc) |
> | Cortana | [*Cortana SDK*](https://developer.microsoft.com/cortana/devices) | Yes |
> | Domain join | AAD only | AAD and Traditional Domain |
> | Management | MDM | MDM |
> | Device Security Technologies | [TPM](https://docs.microsoft.com/windows/iot-core/secure-your-device/tpm), [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/windows/iot-core/secure-your-device/securebootandbitlocker), and Device Health Attestation | [TPM](https://docs.microsoft.com/windows/iot-core/secure-your-device/tpm), [Secure Boot, BitLocker, Device Guard](https://docs.microsoft.com/windows/iot-core/secure-your-device/securebootandbitlocker) and Device Health Attestation |
> | CPU Architecture support | x86, x64, and ARM | x86 and x64 |
> | Licensing | Online Licensing Agreement and Embedded OEM Agreements, Royalty-free | Direct and Indirect Embedded OEM Agreements |
> | Usage scenarios | [Digital Signage](https://www.microsoft.com/windowsforbusiness/digital-signage), Smart Building, IoT Gateway, HMI, Smart Home, Wearables | Industry Tablets, Retail Point of Service, Kiosk, [Digital Signage](https://www.microsoft.com/windowsforbusiness/digital-signage), ATM, Medical Devices, Manufacturing Devices, Thin Client |

For minimum requirement details, please visit [the Windows Hardware site](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview).

If you're interested in learning more about Point of Service, please visit the [UWP docs on this topic](https://aka.ms/pointofservice).

## Differences between Windows 10 Desktop and Windows 10 IoT Core

### Different features available on Desktop and IoT Core

* Inbox Cortana is no longer available on Windows 10 IoT Core since version 1809 (17763). If you are looking to bring a voice-enabled device to market quickly, you can integrate Cortana support into the device using the [preview of the Cortana Devices SDK](https://developer.microsoft.com/cortana/devices).
* The [FileOpenPicker API](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker) is not supported in Windows 10 IoT Core. To access local drives or removable storage, you can implement this in your own application.
* The Windows 10 IoT Core device will boot to the [default app](https://docs.microsoft.com/windows/iot-core/develop-your-app/iotcoredefaultapp) instead of a desktop-like PC. The purpose of this application is not only to provide you with a friendly shell to interact with upon first boot, but to also allow you to use the [open-sourced code](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/IoTCoreDefaultApp) for this application so that you can use these features to plug and play your own custom application(s).

### Differences in driver-supported areas

* Windows 10 Desktop has more supported drivers than Windows 10 IoT Core. To make the same device(s) work on Windows 10 IoT Core as on Desktop, you may need to build a driver from source for a Windows 10 IoT Core device or find another workaround, especially for ARM architecture.
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

* The registry key must be set from the Default Account. If the ScrollViewer's XAML setting is "Visible", the registry setting of 0 will force the scroll bar to appear regardless of whether there is sufficient content to have the scroll appear in the UI. A registry setting of 1 will keep the scroll bar hidden until there is sufficient content.

```
<TextBox Height="200" Width="100" IsEnabled="True" FontSize="50" TextWrapping="Wrap" ScrollViewer.VerticalScrollBarVisibility="Visible" Text="..."/>
```

* Lastly, if the ScrollViewer XAML's setting is "Auto" then the registry setting of 0 will only show the full scroll bar when there is enough content to display the scroll bar. When the registry setting is 1, the scroll bar will appear then when there is enough content or hidden if there is no content.

```
<TextBox Height="200" Width="100" IsEnabled="True" FontSize="50" TextWrapping="Wrap" ScrollViewer.VerticalScrollBarVisibility="Auto" Text="..."/>
```

### Different commands supported

* The PowerShell Remove-AppxPackage command works on Desktop but not on Windows 10 IoT Core.
* Not all folders on your device are accessible by Universal Windows Apps. On Windows 10 IoT Core, you can use the FolderPermissions tool to make a folder accessible to a UWP app. For example, run FolderPermissions c:\test -e to give UWP apps access to c:\test folder. However, this is not available on Desktop.

Commands shown in this post may change as time goes on since Windows 10 IoT Core keeps updating.

## IoT Edge Support for Windows 10 IoT
To learn more about IoT Edge support for Windows 10 IoT, please read more about "Operating Systems" in the Azure IoT Edge article [here](https://docs.microsoft.com/azure/iot-edge/support#operating-systems).


## Helpful resources
* [Windows 10 IoT Enterprise](windows-iot-enterprise.md)
* [Windows 10 IoT Core](windows-iot-core.md)
