---
title: Overview of Windows CE App Container
ms.date: 08/12/2020
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Windows CE App Container Migration Technology
keywords: Windows 10 IoT Core, Windows CE, application migration, cepal
---

# An Overview of the Windows CE App Container

Microsoft has provided platforms and operating systems for embedded devices for decades. As new offerings such as Windows 10 IoT have become available, our customers and partners are increasingly interested in the advanced security, platform, and cloud connectivity features that these OS provide. Customers moving from most earlier editions of Windows, like Windows XP and Windows 7, can do so with little effort because of binary compatible applications. Other operating systems, like Windows CE, require device builders to modify source code. Porting applications like this can be challenging.

To help these customers move to Windows 10 IoT and harness the full power of the intelligent edge including artificial intelligence and machine learning, Microsoft has developed technology that will allow most customers to run their existing, unmodified Windows CE applications on Windows 10 IoT while they continue to invest in updating their applications. You can learn more about how this technology works in the IoT Show episode [Modernizing Windows CE Devices](https://channel9.msdn.com/Shows/Internet-of-Things-Show/Modernizing-Windows-CE-Devices)

## What are the platform requirements

The Windows CE App Migration technology works by running a Windows CE 2013 instance on top of Windows 10 IoT Core.

The solution works with 32-bit application code and requires an ARM32 or x64 base platform that is [compatible](https://docs.microsoft.com/windows/iot-core/learn-about-hardware/socsandcustomboards) with Windows 10 IoT Core.
You should be comfortable building a Windows CE 2013 system image using platform builder as well as building an image for Windows 10 IoT Core.

A more detailed list of the requirements can be found under [Prerequisites](https://docs.microsoft.com/windows/iot-core/windows-ce-app-container-getting-started#prerequisites) in the article, [Getting Started with CE App Container](https://docs.microsoft.com/windows/iot-core/windows-ce-app-container-getting-started).

## Is Windows CE App Container the right choice for me

For designs that need to leverage ARM32 or have complex CE applications that will require multiple development cycles to migrate, the CE App Container with [Windows 10 IoT Core Services](https://docs.microsoft.com/windows-hardware/manufacture/iot/iotcoreservicesoverview) offers a great solution for gradual migration.

Developers place a special ARM32 or x86 Windows CE2013 platform image within their IoT Core system image, which they deploy on Windows 10 IoT Core compatible hardware. Developers have access to begin adding functionality, like Azure cloud connectivity or modern peripherals, though the Windows 10 layer and can move portions of the CE application over as well aiming for complete migration before 2029.

With IoT Core Services, your Windows 10 IoT Core OS will continue to receive security updates until 2029. And, with capabilities like Device Update Center, OEMs can manage the timing of the OS updates as well as distribute application updates easily.

Check out [Getting Started with CE App Container](https://docs.microsoft.com/windows/iot-core/windows-ce-app-container-getting-started) for a step-by-step guide that will walk you through your migration journey.

However, if you have existing designs that just need a few more years of manufacturing, the best course is to remain on Windows CE 2013. The path forward is explained more deeply in [Moving forward with Windows CE using the Windows CE App Container on Windows 10 IoT Core](https://techcommunity.microsoft.com/t5/internet-of-things/moving-forward-with-windows-ce-using-the-windows-ce-app/ba-p/1582360).
