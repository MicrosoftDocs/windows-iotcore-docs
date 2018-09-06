# Get the tools needed to customize Windows IoT Core

Here's the software you'll need to create OEM images using the Windows 10 IoT Core (IoT Core) ADK Add-Ons:

## PCs and devices
Here's how we'll refer to them:

* <b>Technician PC</b>: Your work PC. This PC should have at least 15GB of free space for installing the software and for modifying IoT Core images. 

We recommend either Windows 10 or Windows 8.1 with the latest updates. The minimum requirement is Windows 7 SP1, though this may require additional tools or workarounds for tasks such as mounting .ISO images.

* <b>IoT device:</b> A test device or board that represents all of the devices in a single model line.

For our examples, you'll need a Raspberry Pi 3. For more options, see [SoCs and Custom Boards](../learn-about-hardware/SoCsAndCUstomBoards.md).

* An <b>HDMI cable</b>, and a <b>monitor or TV</b> with a dedicated HDMI input. We'll use this to verify that the image is loaded and that our sample apps are running.

## Storage
* A <b>Micro SD card</b>. (Note, we just use this for our guide. You can build devices with other drives. Learn more about existing [supported storage](../learn-about-hardware/HardwareCompatList.md#other-hardware-peripherals) options.)

If your technician PC doesn't include a Micro SD slot, you may also need an adapter.

## Software
<b>Install the following tools on your technician PC</b>

1. [Windows Assessment and Deployment Kit (Windows ADK)](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install#winADK) including at least the features shown below. You'll use these tools to create images and provisioning packages.

![Dashboard screenshot](../media/ManufacturingGuide/WindowsADKSetup.jpg)

2. [Windows Driver Kit (WDK) 10](https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk) (optional, required only if you are building drivers)

3. [Windows 10 IoT Core Packages](https://www.microsoft.com/en-us/software-download/windows10iotcore). The .iso package adds the IoT Core packages and feature manifests used to create IoT Core images. By default, these packages are installed to <b>C:\Program Files (x86)\Windows Kits\10\MSPackages\Retail</b>. Install one or more of the IoT Core packages, depending on the architecture you are building an image for (ARM, x86, x64).

![Dashboard screenshot](../media/ManufacturingGuide/IoTCorePackagesInstall.jpg)

4. IoT Core ADK Add-Ons. Click <b>Clone or Download > Download ZIP</b>, and extract it to a folder, for example, <b>C:\IoT-ADK-AddonKit</b>. This kit includes the sample scripts and base structures you'll use to create your image. To learn about the contents, see [What's in the Windows ADK IoT Core Add-ons](https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iot-core-adk-addons).

5. [Windows 10 IoT Core Dashboard](http://go.microsoft.com/fwlink/p/?LinkId=708576).

6. [The Raspberry Pi BSP](https://github.com/ms-iot/iot-adk-addonkit/releases/download/v4.4/rpibsp-wm.zip). Since this lab uses a Raspberry Pi, you'll need to download the Raspberry Pi BSP. If you're working with a device other than Raspberry Pi, visit the [Windows 10 IoT Core BSP](https://docs.microsoft.com/en-us/windows/iot-core/build-your-image/createbsps) page to download other BSPs.

7. Get a [code-signing certificate](https://docs.microsoft.com/en-us/windows-hardware/drivers/dashboard/get-a-code-signing-certificate). For the kernel driver signing, Standard Code signing certificate is sufficient. You will require an EV cert to access the [Device Update Center](https://docs.microsoft.com/en-us/windows-hardware/service/iot/using-device-update-center) in Hardware Dev Center portal. This will be required when you build a retail image.

Other helpful software:

* <b>A text editor such as Notepad++</b>. You can also use the Notepad tool, though for some files, you won't see the line breaks unless you open each file as a UTF-8 file.

* <b>A compression program such as 7-Zip</b>, which can uncompress Windows app packages.

* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/), used to create an app in [Lab 1b: Add an app to your image](AddApps.md).

## Other software
* <b>An app built for IoT Core</b>. Our samples use the [IoT Core Default](https://github.com/ms-iot/samples/tree/develop/IoTCoreDefaultApp) app, though you can use your own.

* <b>A driver built for IoT Core</b>. Our samples use the [Hello, Blinky](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinky) driver, though you can use your own.

## Next steps
[Lab 1a: Create a basic image](CreateBasicImage.md)