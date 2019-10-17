---
title: Get started with the mDNS Responder Sample Source
ms.date: 02/26/2019
ms.topic: article
description: Learn how to get started with the mDNS Responder Sample Source.
keywords: Windows 10 IoT Core, mDNS Responder Sample Source
---

# Getting Started with mDNS Responder Sample Source

## Getting started

1.	Compile the project *mDNSResponder* to get mDNSResponder.exe, which is a service. Copy the .exe to the target machine then register the service and run.
2. Run “mDNSResponder.exe /?” to print the usage
3.	Compile the project *dnssd*, it would generate dnssd.dll
4.	Compile the project *mDNSUWP*. It’s a UWP broker that talks to dnssd.dll and will generate its own dll and winmd
5.	Compile the project *mDNSTest*, which is a sample UWP app to consume mDNSUWP and eventually talks into mDNSResponder service.
6.	This UWP app depends on both dnssd.dll and the UWP broker (there is script configured to copy everything into the UWP appx folder)
7.	Deploy/launch mDNSTest, set an ID and click Register, the respond code should be 0 (SUCCESS)
8.	If you run any Bonjour Browser at the same time, the new (fake) device should be listed.

![Registration for mDNS](media/mDNS/mDNS1.png)

## Resources

* Download the Bonjour-compatible mDNS Responder for Windows IoT (sample source) [here](https://go.microsoft.com/fwlink/?linkid=2077676).

