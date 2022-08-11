---
title: Embedded mode
author: lilyhou
ms.author: lihou
ms.date: 11/10/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to configure Windows to allow embedded mode, enabling background applications and other capabilities.
keywords: windows iot, embedded mode, background applications
---

# Embedded mode

Embedded Mode is supported on Windows IoT Core and Windows IoT Enterprise. Embedded Mode enables:

* [Background Applications (read more)](./backgroundapplications.md)
* Use of the lowLevelDevice capability
* Use of systemManagement capability

Embedded mode is always enabled on Window IoT Core.
Embedded mode must be enabled by following the steps below on Windows IoT Enterprise.

## Background Applications

Background Applications are created using the Background Application (IoT) template in Visual Studio.
Read more about creating [Background Applications](./backgroundapplications.md).

Background applications run without stopping and without resource limits. Also, if the background application stops for some reason and embedded mode is enabled the background application will be restarted by the system.

While the system will automatically restart background applications, system lockdown features must be enabled to prevent users from stopping or interfering with the operation of Background Applications.

## lowLevel device Capability and lowLevelDevice capability

The **lowLevel** device Capability gives access to low-level hardware interfaces like GPIO, SPI, and I2C.

* [Blinky Sample(GPIO)](/samples/microsoft/windows-iotcore-samples/hello-blinky)
* [Accelerometer Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/Accelerometer)

The **lowLevelDevices** Capability allows apps to access custom devices when a number of additional requirements are met. This
capability should not be confused with the lowLevel device capability, which allows access to GPIO, I2C, SPI, and PWM devices.

Refer to [App capability declarations](/windows/uwp/packaging/app-capability-declarations) for details.

## systemManagment Capability

When you enable the systemManagment capabilities for your application, this is the set of APIs that gets unlocked:  

* [Windows.System.ProcessLauncher](/uwp/api/Windows.System.ProcessLauncher)
* [Windows.System.TimeZoneSettings](/uwp/api/Windows.System.TimeZoneSettings)
* [Windows.System.ShutdownManager](/uwp/api/Windows.System.ShutdownManager)
* [Windows.Globalization.Language.TrySetInputMethodLanguageTag](/uwp/api/Windows.Globalization.Language#Windows_Globalization_Language_TrySetInputMethodLanguageTag_System_String_)

## Debugging Background Applications

If you are debugging on a device that is not running Windows IoT Core and you see either of the following error messages you need to ensure AllowEmbeddedMode is enabled on the device and that the Embedded Mode service is running:

* There are no more endpoints available from the endpoint mapper.
* This program is blocked by group policy. For more information, contact your system administrator.

## Changing the mode
To enable embedded mode, you will need to create a provisioning package in Imaging and Configuration Designer (ICD) that sets AllowEmbeddedMode=1.  To install ICD, you need to download and install the Windows ADK for Windows 10.

* [Download the Windows ADK for Windows 10](https://go.microsoft.com/fwlink/p/?LinkId=526740)
* [Learn about what's new in the Windows ADK for Windows 10](/windows-hardware/get-started/what-s-new-in-kits-and-tools)

1. When installing the ADK select **Imaging and Configuration Designer (ICD)**
2. After installation is complete, run Windows Imaging and Configuration Designer (WICD).

    ![WICD Icon](../media/EmbeddedMode/WICD_Icon.png)

3. Click **Advanced provisioning**.  Name the project **AllowEmbeddedMode** and click **Next**.
    ![Step #3](../media/EmbeddedMode/Step3.png)

4. Choose **Common to all Windows editions** then **Next**.
    ![Step #4](../media/EmbeddedMode/Step4.png)

5. Click **Finish**.

    ![Step #5](../media/EmbeddedMode/Step5.png)

6. In the search box type **EmbeddedMode** and then click on **AllowEmbeddedMode**.

    ![Step #6](../media/EmbeddedMode/Step6.png)

7. In the center pane set the value of **AllowEmbeddedMode** to **Yes**
    ![Step #7](../media/EmbeddedMode/Step7.png)

8. Click Export > Provisioning Package

    ![Step #8](../media/EmbeddedMode/Step8.png)

9. Click Next.

    ![Step #9](../media/EmbeddedMode/Step9.png)

10. Click Next.

    ![Step #10](../media/EmbeddedMode/Step10.png)

11. Click Next.

    ![Step #11](../media/EmbeddedMode/Step11.png)

12. Click Build.

    ![Step #12](../media/EmbeddedMode/Step12.png)

13. To install the embedded mode .PPKG on Windows IoT Enterprise double-click on the .PPKG.

14. Click **Yes, add it**.
    Click yes on the LUA dialog if it appears, and the click **Yes, add it** on the dialog shown below.
    ![Step #14 Standard](../media/EmbeddedMode/Step14Standard.png)


## Configuring a Background Application to Run automatically
1. To configure a Background Application to automatically run, you will need to follow the directions to [create an MinnowBoardMax SD Card](https://developer.microsoft.com/windows/iot/getstarted) and copy `D:\windows\system32\iotstartup.exe` (where D: is your SD Card).

2. To get a list of installed Background Applications type:
```
        C:\> iotstartup list BackgroundApplication1
```
3. The output should include the full name of each installed Background Application, which will look like this:
```
        Headless : BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee
```
5. To configure this app to run at boot type:
```
        C:\> iotstartup add headless BackgroundApplication1
```
6. If the Background Application has been successfully added to the startup list, you should see this:
```
        Added Headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpveeplication1
```
7. Restart the embedded mode device:

8. Once the device has restarted, your Background Application will start automatically.  The Embedded Mode service that manages Background Applications can take a few minutes to start.  The embedded mode service will monitor Background Applications on the startup list and make sure they get restarted if they stop.  If a Background Application stops several times in a short period of time, it will no longer be restarted.

9. To remove your Background Application from the startup list type:
```
        C:\> iotstartup remove headless BackgroundApplication1
```
10. If the Background Application is removed from the startup list the output will look like this:
```
        Removed headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee
```