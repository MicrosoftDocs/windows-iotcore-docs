---
title: Lightning Performance Testing
author: msalehmsft
ms.author: msaleh
ms.date: 04/03/2023
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn about Windows IoT Lightning functionality and toggle frequency for different platforms and languages.
keywords: windows iot, lightning performance, lightning functionality, GPIO
---

# Windows IoT Lightning Performance Testing

> [!IMPORTANT]
> The Windows 10 IoT team is no longer actively supporting Arduino.

The GPIO performance was tested for Windows IoT Lightning functionality using a simple GPIO toggle app, [available here](https://github.com/ms-iot/lightning/tree/develop/PerformanceTestSuite). The tests were performed by toggling GPIO 5 between 0 and 1 at the fastest possible speed. The toggle frequency for each case was measured using a Tektronix TPS 2024 Oscilloscope.

The following results were obtained from the analysis:

> | Platform Tested                     | Language        | Frequency     |
> | ----------------------------------- | --------------- | ------------- |
> | Arduino Uno                         | Arduino Sketch  | 75.06 kHz     |
> | Windows 10 IoT Core Native Stack    | C#              | 239 KHz       |
> | Windows 10 IoT Core Native Stack    | C++/CX          | 278 kHz       |
> | Windows 10 IoT Core Native Stack    | WinJS           | 34 kHz        |
> | Windows 10 IoT Core Arduino Wiring  | Arduino Wiring  | **7.36 MHz**  |
> | Windows 10 IoT Core DMAP Stack      | C#              | **1.76 MHz**  |
> | Windows 10 IoT Core DMAP Stack      | C++/CX          | **3.78 MHz**  |
> | Windows 10 IoT Core DMAP Stack      | WinJS           | 42 kHz        |

Windows 10 IoT Core tests were run on a Raspberry Pi 3 using Windows 10 IoT Core Insider Preview Build 15026 (codename Redstone 2) and built using Microsoft IoT Lightning SDK 1.1.0.
