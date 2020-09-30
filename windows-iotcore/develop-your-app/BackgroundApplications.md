---
title: Background Applications
ms.date: 08/28/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to develop background applications for your IoT device. See how background applications start and are used, what languages are available, and more.
keywords: windows iot, background applications
---

# Developing Background Applications

> [!NOTE]
> Visual Studio will generate a cryptic error when deploying to a RS5 (or RS4 with OpenSSH enabled) IoT image unless a SDK from RS4 or greater is installed that Visual Studio can access.

Background applications are applications that have no direct UI. Once deployed and configured, these applications launch at machine startup and run continuously without any process lifetime management resource use limitations. If they crash or exit the system will automatically restart them.
These Background Applications have a very simple execution model. The templates create a class that implements the "IBackgroundTask" interface and generates the empty "Run" method. This "Run" method is the entry point to your application.

![Background Task](../media/BackgroundApplications/backgroundTaskScreenshot.png)

There is one critical point to note: by default, the application will shut down when the run method completes. This means that apps that follow the common IoT pattern of running a server waiting for input or on a timer will find the app exit prematurely. To prevent this from happening you must call the "GetDeferral" method to prevent the application from exiting. You can find more information on the deferral pattern [here](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskDeferral).

## Where can Background Applications be installed from? 

You can download and install IoT templates to enable Background Applications from the Visual Studio Gallery [here](https://go.microsoft.com/fwlink/?linkid=847472).  Alternatively, the templates can be found by searching for `Windows IoT Core Project Templates` in the [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) or directly from Visual Studio in the Extension and Updates dialog (Tools > Extensions and Updates > Online).

## What languages are available?

**Background Application (IoT)** templates can be found for:

* **C++** `File > New > Project > Installed > Visual C++ > Windows > Windows IoT Core`
* **C#** `File > New > Project > Installed > Visual C# > Windows > Windows IoT Core`
* **Visual Basic** `File > New > Project > Installed > Visual Basic > Windows > Windows IoT Core`
* **JavaScript** `File > New > Project > Installed > JavaScript > Windows > Windows IoT Core`

## How are background applications used? 

Creating a background application is very similar to creating a Background Task.  When the Background Application starts, the Run method is called:

```csharp
public void Run(IBackgroundTaskInstance taskInstance)
{
}
```

When the Run method ends, unless a deferral object is created, the background application ends. The common practice, for asynchronous programming is to take a deferral like this:

```csharp
private BackgroundTaskDeferral deferral;
public void Run(IBackgroundTaskInstance taskInstance)
{
    deferral = taskInstance.GetDeferral();
    
    //
    // TODO: Insert code to start one or more asynchronous methods
    //
}
```

Once a deferral is taken, the background application will continue until the deferral object's Complete method is called.

```csharp
deferral.Complete();
```

## How do background applications start?

This question can be broken into deployment and invocation.  

To deploy a background application, you can either:

* Use Visual Studio's F5 (which will build, deploy, and invoke).  For more details, see our [Hello World sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/HelloWorld) where we describe how to deploy and launch from Visual Studio.

> [!NOTE]
> This will not configure your background application to start when the device boots.

* Create an AppX in Visual Studio by selecting Project > Store > Create App Packages.  Once you have created an AppX, you can use [Windows Device Portal](../manage-your-device/DevicePortal.md) to deploy it to your Windows 10 IoT Core device.

To invoke a background application, you can either:

* As mentioned above, Visual Studio's F5 functionality will deploy and immediately start your Background Application.

> [!NOTE]
> This will not configure your background application to start when the device boots.

* For a background application that has been deployed to an IoT device, you can use the iotstartup.exe utility to configure your background application to start when the device boots.  To specify your background application as a Startup App, follow these instructions (**substitute your app's name** for `BackgroundApplication1` below):

1. Start a PowerShell (PS) session with your Windows IoT Core device as described [here](../connect-your-device/PowerShell.md).

2. From the PS session, type:
            
`[<your IP address>]: PS C:\> iotstartup list BackgroundApplication1`

3. You should see the full name of your background application, i.e. something like:

`Headed   : BackgroundApplication1-uwp_cqewk5knvpvee!App
Headless : BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee`

4. The utility is confirming that your background application is an 'headless' application, and is installed correctly.  You will likely see a Headed entry as well for your Background Applications, but this can be disregarded.

5. Now, it's easy to set this app as a 'Startup App'. Just type the command:

`[<your IP address>]: PS C:\> iotstartup add headless BackgroundApplication1`

6. The utility will confirm that your background application has been added to the list of headless 'Startup Apps':

`Added Headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpveeplication1`

7. Go ahead and restart your Windows IoT Core device. From the PS session, you can issue the shutdown command:

`[<your IP address>]: PS C:\> shutdown /r /t 0`

8. Once the device has restarted, your background application will start automatically and Windows 10 IoT Core will make sure that it gets restarted anytime it stops.  

> [!NOTE]
> Once a background app is registered to run automatically, if the app exits or crashes it will be automatically restarted.  The app isn't informed of the reason that it's being started or restarted so if you want to take special action on a restart you will need to track the app state in your app.

9. You can remove your background application from the list of headless Startup Apps by typing the command:

`[<your IP address>]: PS C:\> iotstartup remove headless BackgroundApplication1`

10. The utility will confirm that your background application has been removed from the list of headless 'Startup Apps':

`Removed headless: BackgroundApplication1-uwp_1.0.0.0_x86__cqewk5knvpvee`

## See Also
To add a background app when building a custom image see [Create an Appx package](../build-your-image/createinstallpackage.md)
