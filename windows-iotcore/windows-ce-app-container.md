---
title: Overview of Windows CE App Container
ms.date: 05/22/2020
ms.topic: article
description: Get access to the private preview of the Windows CE App Container
keywords: Windows 10 IoT Core, Windows CE, application migration, cepal 
---

# An Overview of the Windows CE App Container
Microsoft has provided platforms and operating systems for embedded devices for decades. As new offerings such as Windows 10 IoT have become available, our customers and partners are increasingly interested in the advanced security, platform, and cloud connectivity features that these OS provide. Customers moving from most earlier editions of Windows, like Windows XP and Windows 7, can do so with little effort because of binary compatible applications. Other operating systems, like Windows CE, require device builders to modify source code. Porting applications like this can be challenging.

To help these customers move to Windows 10 IoT and harness the full power of the intelligent edge including artificial intelligence and machine learning, Microsoft is developing technology that will allow most customers to run their existing, unmodified Windows CE applications on Windows 10 IoT while they continue to invest in updating their applications. You can learn more about how this technology works in the IoT Show episode <a href="https://channel9.msdn.com/Shows/Internet-of-Things-Show/Modernizing-Windows-CE-Devices">Modernizing Windows CE Devices</a>.

## How to get started with the private preview

We anticipate having the Windows CE App Container technology generally available later this year as part of <a href="https://docs.microsoft.com/en-us/windows-hardware/manufacture/iot/iotcoreservicesoverview">Windows 10 IoT Core Services</a>. However, if you are a commercial developer with a Windows CE solution and would like to begin evaluating the technology, please contact <a href="mailto:cemigrat@microsoft.com">cemigrat@microsoft.com</a> from your company email account to access the private preview.

## What are the platform requirements? 
The Windows CE App Migration technology works by running a Windows CE 2013 instance on top of Windows 10 IoT Core. 

The solution works with 32-bit application code and requires an ARM32 or x64 base platform that is <a href="https://docs.microsoft.com/en-us/windows/iot-core/learn-about-hardware/socsandcustomboards">compatible</a> with Windows 10 IoT Core.
You should be comfortable building a Windows CE 2013 system image using platform builder as well as building an image for Windows 10 IoT Core.
