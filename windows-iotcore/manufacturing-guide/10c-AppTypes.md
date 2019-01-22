---
title: Developing applications
author: lmaung
ms.author: lmaung
ms.date: 11/30/2018
ms.topic: article
description: Learn about the languages and app types that are supported by IoT Core.
keywords: windows iot, languages, app types, UWP, supported
---
# Developing applications
Learn about the languages that are supported on Windows 10 IoT Core as well as the UWP and non-UWP app types that are supported on IoT Core.

## Application Types

### Traditional UWP Apps
UWP apps just work on IoT Core, just as they do on other Windows 10 editions. A simple, blank Xaml app in Visual Studio will properly deploy to your IoT Core device just as it would on a phone or Windows 10 PC. All of the standard UWP languages and project templates are fully supported on IoT Core.

There are a few additions to the traditional UWP app-model to support IoT scenarios and any UWP app that takes advantage of them will need the corresponding information added to their manifest. In particular the "iot" namespace needs to be added to the manifest of these standard UWP apps. 

Inside the <Package> attribute of the manifest, you need to define the iot xmlns and add it to the IgnorableNamespaces list. The final xml should look like this: 

```
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:iot="http://schemas.microsoft.com/appx/manifest/iot/windows10"
  IgnorableNamespaces="uap mp iot">
```

### Background Apps
In addition to the traditional UI apps, IoT Core has added a new UWP app type called "Background Applications". These applications do not have a UI component, but instead have a class that implements the "IBackgroundTask" interface. They then register that class as a "StartupTask" to run at system boot. Since they are still UWP apps, they have access to the same set of APIs and are supported from the same language. The only difference is that there is no UI entry point.

Each type of IBackgroundTask gets its own resource policy. This is usually restrictive to improve battery life and machine resources on devices where these background apps are secondary components of foreground UI apps. On IoT devices, Background Apps are often the primary function of the device and so these StartupTasks get a resource policy that mirrors foreground UI apps on other devices.

The following sample shows the code necessary to build a C# Background App that blinks an LED:

```C#
namespace BlinkyHeadlessCS
{
    public sealed class StartupTask : IBackgroundTask
    {
        BackgroundTaskDeferral deferral;
        private GpioPinValue value = GpioPinValue.High;
        private const int LED_PIN = 5;
        private GpioPin pin;
        private ThreadPoolTimer timer;

        public void Run(IBackgroundTaskInstance taskInstance)        {
            deferral = taskInstance.GetDeferral();
            InitGPIO();
            timer = ThreadPoolTimer.CreatePeriodicTimer(Timer_Tick, TimeSpan.FromMilliseconds(500));

        }
        private void InitGPIO()
        {
            pin = GpioController.GetDefault().OpenPin(LED_PIN);
            pin.Write(GpioPinValue.High);
            pin.SetDriveMode(GpioPinDriveMode.Output);
        }

        private void Timer_Tick(ThreadPoolTimer timer)
        {
            value = (value == GpioPinValue.High) ? GpioPinValue.Low : GpioPinValue.High;
            pin.Write(value);
        }
    }
}
```

You can find in-depth information on Background apps [here](https://docs.microsoft.com/windows/iot-core/develop-your-app/backgroundapplications).

### Arduino Wiring
 Arduino Wiring requires the download of the "Windows IoT Core Project Templates" from the Visual Studio **Tools->Extensions and Updates** manager.  Arduino Wiring supports only Background Applications. You can also build *Windows Runtime Components* using C#, C++, or Visual Basic and then reference those libraries from any other language.

### C# and Visual Basic (VB)
C# and VB are both supported as UWP apps and have access to the portion of the .Net Framework available to UWP applications. They support UI apps built with Xaml as well as Background Apps. You can also build *Windows Runtime Components* that can be used from other supported languages.

Samples:


* [C# Blinky Headless with Full Documentation](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinkyBackground)
* [C# Blinky Headless Code Only](https://github.com/ms-iot/samples/tree/develop/HelloBlinkyBackground/CS)
* [VB Blinky Headless Code Only](https://github.com/ms-iot/samples/tree/develop/HelloBlinkyBackground/VB)
* [C# Blinky UI App](https://developer.microsoft.com/en-us/windows/iot/samples/helloblinky)


### Javascript
You can use Javascript to build both UI and Background Apps. The UI apps work the same way they do on all UWP editions. The Background Apps are new for IoT Core but are very simple. The following sample code shows the output of a the *JS New Project Template*:

```javascript
// The Background Application template is documented at http://go.microsoft.com/fwlink/?LinkID=533884&clcid=0x409
(function () {
    "use strict";

    // TODO: Insert code here for the startup task

})();
```

### C++
With C++ you can build Xaml or DirectX UI apps, as well as UWP Background projects and *non-UI* Win32 apps.

Samples:

* [Blinky Headless](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinkyBackground/CPP)
* [Blinky Headed](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinky/Cpp)
* [Console App](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/MemoryStatus)

> [!NOTE]
> For those who are planning to write their app in C++, you'll need to check the UWP C++ checkbox upon downloading.

![C++ for Visual Studio](../media/BuildingAppsForIoTCore/VS-CPP.jpg)


### Arduino Wiring
With Arduino Wiring support you can build apps in Arduino Wiring for many popular components and peripherals in the IoT ecosystem.

Our [Arduino Wiring Project Guide](../learn-about-hardware/ArduinoWiringProjectGuide.md) provides full instructions on how to get set up to build these apps. The samples copied and linked below will help you get started building your own.  You can even [build WinRT components in Arduino](https://github.com/ms-iot/samples/tree/develop/ArduinoLibraryBlinky) that can then be used from other languages. 

*Blinky Sample Code*
The full [sample code and docs](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/HelloBlinkyBackground/VB) are available on our samples page and you can find the full code below:

```C++
void setup()
{
    // put your setup code here, to run once:

    pinMode(GPIO5, OUTPUT);
}

void loop()
{
    // put your main code here, to run repeatedly:

    digitalWrite(GPIO5, LOW);
    delay(500);
    digitalWrite(GPIO5, HIGH);
    delay(500);
}
```

  ## Outline
* [10a-Debug and Deploy Apps Via Visual Studio](10a-DebugAndDeployApps.md)
* [10b-Installing Appx Packages](10b-InstallApp.md)
* [10c-Types of Applications for IoT Core](10c-AppTypes.md)
* [10d-Default App Overview](10d-defaultapp.md)
* [10e-Setting Appx as default application](10e-SettingDefaultApps.md)
* [10f-UWP Loopback debugging](10f-uwploopback.md)