---
title: Getting Started Building Drivers for Windows CE App Container
ms.date: 10/1/2020
ms.topic: article
description: Windows CE App Container Migration Getting Started with Drivers Guide
keywords: Windows 10 IoT Core, Windows CE, application migration, CE App Container
---

# Getting Started Building Drivers for Windows CE App Container

The Windows CE App Container is a technology that allows most CE applications to run on top of Windows 10 IoT Core. More information on how to get started can be found in the article, [Getting Started with CE App Container](windows-ce-app-container-getting-started.md)

> [!NOTE]
> PRERELEASE - This technology is currently in prerelease. If you would like to explore creating a CE App Container Plug-in Driver
> please contact your Microsoft account representative or your Microsoft OEM distributor.

The architecture for the CE App Container provides a way for existing Windows CE developers to provide custom stream drivers that can be access by your CE application.

![CE App Container Architecture](.//media/WindowsCEAppContainer/image1.png)

As you migrate your CE application you can provide matched drivers that make use of the driver plug-in capability of the CE App Container. This capability enables you as a developer to create a custom driver for your CE application that communicates to `CEPALDRV.DLL`. This dll communicates across the Pico Process boundary to `PALCORE.SYS` and eventually to the second part of your custom driver pair under `DKMON.EXE`. This driver makes use of the driver plug-in capability in `DKMON.EXE` to communicate not only with your custom Windows IoT Core device but also back to the CE Application running in the CE App Container. The following diagram shows this typical architecture.

![CE App Container Driver Plug-in Architecture](.//media/WindowsCEAppContainer/image3.png)

The recommended way to deploy this driver pair is to include the CE App Container driver as part of the CE App Container OS Design and to include the plug-in and Windows IoT Core drivers in the Board Support Package (BSP) for the specific Windows IoT Core device. By including the drivers this way you will have the required components included as part of the device install image. Additionally you may include the drivers in `.CAB` files that can be deployed to an existing device. More information about this ability is covered in [Deploying the Windows CE App Container to a device when using an existing FFU](windows-ce-app-container-getting-started.md#deploying-the-windows-ce-app-container-to-a-device-when-using-an-existing-ffu).

## The CE App Container Driver Interface

The CE App Container driver interface provides the capability to support driver initialization, de-initialization, open, close, io control, read and write for your custom CE stream driver. A minimal linker definition file for the `CEPAL_MYDEVICE.DLL` file in the architecture diagram above would look like:

```cpp
LIBRARY CEPAL_MyDevice

EXPORTS
CEPAL_MyDevice_Init         = cepaldrv.CEPAL_DRV_Init
CEPAL_MyDevice_Deinit       = cepaldrv.CEPAL_DRV_Deinit
CEPAL_MyDevice_Open         = cepaldrv.CEPAL_DRV_Open
CEPAL_MyDevice_Close        = cepaldrv.CEPAL_DRV_Close
CEPAL_MyDevice_IOControl    = cepaldrv.CEPAL_DRV_IOControl
CEPAL_MyDevice_Read         = cepaldrv.CEPAL_DRV_Read
CEPAL_MyDevice_Write        = cepaldrv.CEPAL_DRV_Write
```

Calls to these interfaces are handled by `CEPALDRV.DLL` and eventually passed through to your plug-in driver. The calls to a driver resource can be via a common name. This name is defined in the drivers registry section. The code below shows what an example of a serial device stream CE App Container driver:

```cpp
[HKEY_LOCAL_MACHINE\Drivers\BuiltIn\Serial1]
"Flags"=dword:0010            ; User Mode: DEVFLAGS_LOAD_AS_USERPROC
"Dll"="cepal_serial.dll"
"Prefix"="COM"
"Index"=dword:1
"Order"=dword:0
"DeviceArrayIndex"=dword:1
"IClass"="{CC5195AC-BA49-48a0-BE17-DF6D1B0173DD}"
"UserProcGroup"=dword:$(PROCGROUP_DRIVER_MSFT_DEFAULT)
```

In this example, the CE App Container common stream driver will convert map a device name of "COM1" to a stream named "COM:1".  The values "COM" and "1" are both derived from the registry values set in Prefix and Index above. The ":1" is then passed along as an argument into the corresponding example serial driver plugin hosted in `DKMON.EXE` to figure out which serial port should be opened, in this case port 1. Your actual driver could refer to any stream device and this information would then be passed to your plug-in driver that would determine how to communicate with the Windows IoT Core driver to open the appropriate resource.

## The CE App Container Plug-in Driver

This driver is responsible for handling the various callbacks from `DKMON.EXE` for initialization, open, close etc. It is also responsible for taking the appropriate actions by communication with the appropriate Windows IoT Core driver. This driver is executed in the context of Windows IoT Core. OEMs and developers can load these plug-in drivers by specifying them in the custom `C:\WindowsCE\Monitor\<arch>\DrawBridgeOEM.ini` file.  In this INI file, the `[Providers]` section identifies the custom plug-in stream provider:

```cpp
[Providers]
MyDeviceStreamProvider=MyDevicePlugin.dll,PlugInInitialize
```

Your plug-in driver needs to export the `PlugInInitialize` entry point where you define the `CEPAL_DRIVER_PLUGIN` structure. This structure enables `DKMON.EXE` to find the relevant plug-in. For the serial plug-in example above `PlugInInitialize` could look like:

```cpp
    HRESULT
    CEPAL_CALL
    PlugInInitialize (
        _In_        PVOID OpaqueInput,
        _Outptr_    PVOID *OpaqueOutput
        )
    {
        // ... misc stuff ...

        CEPAL_DRIVER_PLUGIN PlugIn = {0};

        PlugIn.ApiVersion   = 1;
        PlugIn.DeviceType   = L"com"; // <- This is how the stream name is defined

        // ... other callback registrations ...
```

The CE App Container can support multiple plug-in drivers that each define their own stream and communicate via the public device driver API:
![CE App Container Multiple Drivers](.//media/WindowsCEAppContainer/image4.png)

## References

- [Getting Started with CE App Container](windows-ce-app-container-getting-started.md)
- [Get the tools needed to customize Windows 10 IoT Core](/windows-hardware/manufacture/iot/set-up-your-pc-to-customize-iot-core)
- [IoT Core Board Supported Packages (BSP)](/windows-hardware/manufacture/iot/bsphardware)
- [IoT Core Manufacturing Guide](/windows-hardware/manufacture/iot/iot-core-manufacturing-guide)
- [Windows 10 IoT Core Dashboard](/windows/iot-core/connect-your-device/iotdashboard)
- [Create and Install Packages](/windows-hardware/manufacture/iot/create-install-package)
