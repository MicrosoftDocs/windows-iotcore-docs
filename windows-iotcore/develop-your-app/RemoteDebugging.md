---
title: Debug your app using Remote Console App Debugging
author: bfjelds
ms.author: brian.fjeldstad
ms.date: 09/12/17
ms.topic: article
description: Learn how to remotely debug your IoT Core console application remotely in Visual Studio.
keywords: windows iot, visual studio, app deployment, remote debugging
---

# Debug your app using Remote Console App Debugging

## Overview

Here's how to debug your IoT Core console application remotely in Visual Studio:

* You will first need to setup the Remote Debugger on your Windows IoT Core device. First follow the steps [here](AppDeployment.md) to deploy any other Universal Windows Application on your device (try the HelloWorld project). This will copy all the required binaries to your device. 

* To start the remote debugger on your device, open a Web Browser on your PC and point it to `http://<device name/IP address>:8080` to launch [Windows Device Portal](../manage-your-device/DevicePortal.md). In the credentials dialog, use the default username and password: `Administrator`, `p@ssw0rd`. Windows Device Management should launch and display the web management home screen.

* Now navigate to the Debug settings section of Windows Device Portal and click the Start button under Start Visual Studio Remote Debugger. 

    ![WindowsDevicePortalDebugSettings Start remote debugger](../media/Console/device_portal_start_debugger.png)

* This will show pop-up a message box and give you the connection information. 

*  In Visual Studio, you can configure your target by editing your project's properties (be sure to make all of the highlighted changes as appropriate to your board's name or IP address):

    ![ConsoleApplication Remote Machine Project Settings](../media/Console/console_project_settings.png)

> [!TIP]
> You can use the IP address instead of the Windows IoT Core device name.

* The project configuration needs to be modified to enable deployment.  To do this, open the Configuration Manager by selecting the Configuration manger from the Solution Configuration drop-down menu on the toolbar.

    ![ConsoleApplication SolutionConfiguration](../media/Console/configuration_management.png)

    From the Configuration Manager, ensure that the Deploy checkbox is selected for your project configuration (if this options is disabled, it is likely that the deployment options have not been fully entered into the Debugging tab of the project properties)

    ![ConsoleApplication Remote Machine Project Settings](../media/Console/deploy_checkbox.png)

* Now we're ready to deploy to the remote Windows IoT Core device. Simply press F5 (or select Debug \| Start Debugging) to start debugging our app. You can also use Build \| Deploy Solution to simply deploy your application without starting a debug session.

> [!NOTE]
> When run from Visual Studio, the output will not display anywhere, but you will be able to set breakpoints, see variable values, etc.

* To stop the app, press on the 'Stop Debugging' button (or select Debug \| Stop Debugging).

* You can now run the application.  Simply open a PowerShell/SSH connection (instructions can be found [here for PowerShell](../connect-your-device/PowerShell.md) and [here for SSH](../connect-your-device/SSH.md)) and enter the Remote Command you specified above.

    ![ConsoleApplication Output](../media/Console/console_output.png)

* Once you are done debugging your application, remember to stop the remote debugger on the Windows IoT Core device. You can do this by navigating to Debug settings section of Windows Device Portal and clicking on the Stop Remote Debugger button.

    ![WindowsDevicePortalDebugSettings Stop remote debugger](../media/Console/device_portal_stop_debugger.PNG)

## Troubleshooting Visual Studio Remote Debugger
___
To be able to deploy applications from Visual Studio 2017, you will need to make sure that the Visual Studio Remote Debugger is running on your Windows IoT Core device. The remote debugger should open automatically when you start your computer. To double check, use the `tlist` command to list all the running processes from PowerShell. There should be two instances of msvsmon.exe running on the device.

It is possible for the Visual Studio Remote Debugger to time out after long periods of inactivity. If Visual Studio cannot connect to your Windows IoT Core device, try restarting the device.

### Configure your Windows IoT Core device

If you want, you can rename your device. 

1. To change the computer name, use the `setcomputername` utility:

        setcomputername <new-name>

2. Restart the device for the change to take effect. You can use the `shutdown` command as follows:

        shutdown /r /t 0

3. Because the computer name was changed, after you restart you will need to rerun this command to connect to your device using the new name:

        Set-Item WSMan:\localhost\Client\TrustedHosts -Value <new-name>
        
Your Windows IoT Core device should now be properly configured and ready to use!