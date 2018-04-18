---
title: Glossary for Windows IoT
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
ms.prod: Windows
ms.technology: IoT
description: Learn about the various Windows IoT Core-related terms through our documentation.
keywords: windows iot, glossary, terms, terminology, definitions
---

# Glossary for Windows IoT

**Advanced Configuration & Power Interface (ACPI)**
ACPI (Advanced Configuration and Power Interface) is an open industry specification co-developed by Hewlett-Packard, Intel, Microsoft, Phoenix, and Toshiba.  ACPI establishes industry-standard interfaces enabling OS-directed configuration, power management, and thermal management of mobile, desktop, and server platforms.

**Basic Input/Output System (BIOS)**
The set of essential software routines that test hardware at startup, start the operating system, and support the transfer of data among hardware devices.

**Commercialize**
Developing and manufacturing a device with the intention of putting it out to the public commercially.

**General-Purpose Input/Output (GPIO)**
GPIO is a generic pin on an integrated circuit whose behavior, including whether it is an input or output pin, can be controlled by the user at run time.  You can use the Windows.Devices.Gpio namespace in your app to manipulate the GPIO pins on your board.

**Headed**
Windows IoT Core can either be in headed or headless mode. The difference between these two modes is the presence or absence of any form of UI. By default, Windows 10 IoT Core is in headed mode and displays system information like the computer name and IP address.

**Headless**
In headless mode, there is no UI stack available and apps are not interactive. Headless mode apps can be thought of as services.

**Inter-Integrated Circuits (I2C)**
Simple bidirectional two-wire serial data (SDA) and serial clock (SCL) buses for inter-integrated circuit control.  You can use the Windows.Devices.I2c namespace in your app to communicate with a device over I2C.

**Light-Emitting Diode (LED)**
A LED is a two-lead semiconductor light source. It is a pn-junction diode, which emits light when activated.

**Microsoft Windows Kernel Mode Driver Framework (KMDF)**
Microsoft development framework which allows driver developers to expose driver functionality in kernel mode, giving the driver access to system memory and hardware.

**Prototype**
Developing a more raw version of a final version of a device that you're hoping to create. Prototyping is highly recommended, if not an obligatory step in the manufacturing process. This stage should be used for testing any and all features you're hoping to use for the final version of your device.

**Serial Peripheral Interface Bus (SPI)**
The SPI bus is a synchronous serial communication interface specification used for short distance communication, primarily in embedded systems.  You can use the Windows.Devices.Spi namespace in your app to communicate with a device over SPI.

**Universal Asynchronous Receiver/Transmitter (UART)**
UART is a piece of computer hardware that takes bytes of data and transmits the individual bits serially.

**Universal Windows Platform (UWP)**
The Universal Windows Platform provides a guaranteed core API layer across devices.  You can create a single app package that can be installed onto a wide range of devices.

**Virtual Machine (VM)**<br/>
Software that acts as an interface between compiler binary code and the microprocessor that actually performs the program's instructions.  In Windows, you can use Hyper-V Manager to manage virtual machines.

**Windows Device Console (Devcon.exe)**
DevCon (Devcon.exe), the Device Console, is a command-line tool that displays detailed information about devices on computers running Windows. You can use DevCon to enable, disable, install, configure, and remove devices.  This tool is mostly used for manually installing and removing drivers.
