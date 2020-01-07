---
title: Bus Providers
author: msalehmsft
ms.author: msaleh
ms.date: 08/28/2017
ms.topic: article
description: Learn about the different providers available through Windows 10 IoT Core.
keywords: windows iot, providers, bus providers, UWP, Gpio, Spi
---

# Usermode access to GPIO, I2C and SPI

Windows 10 contains new APIs for accessing GPIO, I2C, SPI, and UART directly from usermode. Development boards like Raspberry Pi 2 expose a subset of these connections which enable users to extend a base compute module with custom circuitry to address a particular application. These low level buses are usually shared with other critical onboard functions, with only a subset of GPIO pins and buses exposed on headers. To preserve system stability, it is necessary to specify which pins and buses are safe for modification by usermode applications.

Usermode access to low level buses on Windows is plumbed through the existing `GpioClx` and `SpbCx` frameworks. A new driver called RhProxy, available on Windows IoT Core and Windows Enterprise, exposes `GpioClx` and `SpbCx` resources to usermode. To enable the APIs, a device node for rhproxy must be declared in your ACPI tables with each of the GPIO and SPB resources that should be exposed to usermode.

Additional in-depth documentation on UserMode access via RhProxy can be found [here](https://docs.microsoft.com/windows/uwp/devices-sensors/enable-usermode-access).

## Bus Providers

Starting with Windows 10, Windows has had in-box UWP APIs that provide direct access to Gpio, Spi, or I2c busses located on-soc. This gives very easy access to this hardware from a high level API. However, there are many times when a device maker wants to use an off-soc controller to access a bus. It can be as simple as a cheap chip that adds 16 GPIO pins, or as rich as a full MCU (like an Arduino) that not only adds Gpio, SPI, and I2C pins, but also supports PWM and ADC. With the "Bus Provider" model, we give developers the ability to access these off-soc busses using the in-box APIs, using a user-mode provider that bridges the gap.

Someone building a provider implements a set of interfaces into a UWP class library and then any developer who wants to talk to that hardware simply includes the component and tells the in-box APIs about it. If you look at the sample code from the [Remote Arduino provider](https://github.com/ms-iot/BusProviders/tree/develop/Arduino) you can see how easy it is to configure the provider and, once set as the default provider for that app, the rest of the code in the client app is identical to the code required to access an on-soc bus.


```
ArduinoProviders.ArduinoProvider.Configuration = 
    new ArduinoProviders.ArduinoConnectionConfiguration("VID_2341", "PID_0043", 57600);
Windows.Devices.LowLevelDevicesController.DefaultProvider =  new ArduinoProviders.ArduinoProvider();

gpioController = await GpioController.GetDefaultAsync();
i2cController = await I2cController.GetDefaultAsync();
adcController = await AdcController.GetDefaultAsync();
pwmController = await PwmController.GetDefaultAsync();

GpioPin pin = gpioController.OpenPin(LED_PIN, GpioSharingMode.Exclusive);`
```

## Available Providers

We currently have a number of providers available on the [Bus Providers](https://github.com/ms-iot/BusProviders) github repo. In addition to the code for the provider, each provider has a sample VS solution that demonstrates how a client would use that provider. 

- **ADC**
  - Ads1x15
  - Mcp3008
  - Remote Arduino

- **PWM**
  - PCA9685
  - Simulated with Gpio
  - Remote Arduino
  
- **Gpio, SPI, I2C**
  - Remote Arduino

In addition to the providers that give you access to real hardware, we have built a [Simulated Provider](https://github.com/ms-iot/BusProviders/tree/develop/SimulatedProvider) that will act as if it was an inifitely capable provider and is designed to let you write and debug your applications without having to first deploy them to a working device. For a richer experience, you can customize it to simulate your actual hardware. For example: updating the I2c provider to return back the result "75" when you send it the command for a temperature reading on a device with the designated slave address.

## Additional Resources

Additional bus tools, sample codes, and building and testing on I2C, SPI, GPIO, MinComm/UART can be found [here](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/BusTools).

