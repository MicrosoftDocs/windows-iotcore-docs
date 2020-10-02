---
title: Frequently Asked Questions - CE Migration
ms.date: 09/25/2020
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: FAQ for Windows CE App Container Migration Technology
keywords: Windows 10 IoT Core, Windows CE, application migration, cepal, Windows CE Migration FAQ
---
# CE migration - Frequently Asked Questions
In this section, we will cover frequently asked questions (FAQ) about CE Migration. We will cover the product roadmap, your migration options as well as how to start the migration process.

## What is Windows CE?  
Windows CE, also known as Windows Embedded Compact or Windows Embedded CE is an operating system developed for Windows Embedded devices. The Windows CE operating system has powered industrial, medical, and a variety of other devices for more than 20 years.  Microsoft licenses Windows CE to original equipment manufacturers (OEMs), who can modify and create their own user interfaces and experiences, with Windows CE providing the technical foundation to do so. The current version of Windows Embedded Compact supports x86 and ARM processors with board support package (BSP) directly.  

## When is the end of life for Windows CE?  
While Windows CE 2013 will reach end of extended support in late 2023, Microsoft will allow license sales to continue for Windows Embedded Compact 2013 until 2028. And of course, Windows CE devices can continue to be used indefinitely.  

## What does that mean for existing solutions?  
It may mean that depending on your hardware configuration, company goals and processes, right now may be the best time for you to modernize your platform software.  

Microsoft has offered its customers multiple solutions on how to navigate this process – move to [Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise), utilize the [Windows CE App Container](https://docs.microsoft.com/windows/iot-core/windows-ce-app-container) with Windows 10 IoT Core, or continue licensing Windows CE 2013.  

## What are my migration options?  
The OS choice for your designs will depend on your timeline for migration and hardware requirements.   

### Windows 10 IoT Enterprise  
For devices needing access to the full range of x64 hardware, ARM64 hardware like NXP i.MX8, advanced UX, or have CE applications that can be migrated in one product design iteration, the best option is to move to [Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) directly. You will be able to begin taking advantage of the features quickly and have the maximum product support lifetime.  

### Windows 10 IoT Core  
For designs that need to leverage ARM32 or have complex CE applications that will require multiple development cycles to migrate, the [CE App Container](https://docs.microsoft.com/windows/iot-core/windows-ce-app-container) with [Windows 10 IoT Core Services](https://docs.microsoft.com/windows-hardware/manufacture/iot/iotcoreservicesoverview) offers a solution for gradual migration to Windows 10 IoT Core. With Windows 10 IoT Core Services, you receive licenses for both Windows Embedded Compact 2013 and Windows 10 IoT Core. The IoT Core OS will continue to receive security updates until 2029.  

### Windows CE 2013
As you work towards a Windows 10 based design, or if you need to continue providing CE 2013 devices for your customers, Microsoft will allow license sales to continue for Windows Embedded Compact 2013 until 2028.   


## Will Microsoft offer the option to pay for additional support on Windows CE 2013 after 2023?
Microsoft does not currently have plans to provide extended support beyond 2023.  

## What’s are the associated costs with migrating?  
Please contact your distributor for specific pricing on the various migration options available as well to gain access to the latest Windows updates for your technical evaluation.  

## What is CE App Container?
Windows CE App Container works by running a Windows CE 2013 instance on top of Windows 10 IoT Core. The goal of the technology is to allow most customers to run their existing, unmodified Windows CE applications on Windows 10 IoT while they continue to invest in updating their applications. To see if CE App Container is the right solution for your organization, check out the following article(https://docs.microsoft.com/windows/iot-core/windows-ce-app-container).
