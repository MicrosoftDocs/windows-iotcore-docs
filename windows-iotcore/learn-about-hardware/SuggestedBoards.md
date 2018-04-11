---
title: Suggested Boards, SoCs, and SoMs for Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the hardware features for a variety of suggested boards and community devices.
keywords: windows iot, development devices, boards, SOC, SOM, system on chips, Raspberry Pi 2, Raspberry Pi 3, Minnowboard Max, Dragonboard
---

# Suggested Boards, SoCs, and SoMs

## Windows 10 IoT Core Development Devices
Below you'll find a few boards we suggest to help you get started with Windows 10 IoT Core. Some of these boards offer a Full Flash Update (FFU) image, making prototyping faster with a ready-made image and making the process of flashing Windows 1 IoT Core a breeze.

> [!IMPORTANT]
> Our licensing terms do not allow commercializing using FFU images downloaded from Microsoft.

| Boards | Information | Where To Buy | FFU Link | How To Set Up | Starter Kit (if available) |
| Raspberry Pi 2 | https://www.raspberrypi.org/products/raspberry-pi-2-model-b/ | https://www.raspberrypi.org/products/raspberry-pi-2-model-b/ | http://go.microsoft.com/fwlink/?LinkId=733603 | [SD-Card](DeviceSetup/SDCard.md) | https://developer.microsoft.com/en-us/windows/iot/Docs/AdafruitMakerKit.htm |
| Raspberry Pi 3 | https://www.raspberrypi.org/products/raspberry-pi-3-model-b/ | https://www.raspberrypi.org/products/raspberry-pi-3-model-b/ | http://go.microsoft.com/fwlink/?LinkId=733603 | [SD-Card](DeviceSetup/SDCard.md) | https://developer.microsoft.com/en-us/windows/iot/Docs/AdafruitMakerKit.htm |
| DragonBoard 410c | https://developer.qualcomm.com/hardware/dragonboard-410c | https://www.arrow.com/en/products/dragonboard410c/arrow-development-tools | http://go.microsoft.com/fwlink/?LinkId=733603 | [SD-Card](DeviceSetup/SDCard.md) | N/A | 
| AAEON Up Squared | http://www.up-board.org/upsquared/specifications-up2/ | https://up-shop.org/4-up-boards | https://downloads.up-community.org/?post_type=wpdmpro&p=204&preview=true | [eMMC](DeviceSetup/eMMC.md) | N/A |
| MinnowBoard Turbot | https://minnowboard.org | https://minnowboard.org/get-a-board | http://go.microsoft.com/fwlink/?LinkId=733603 | [SD-Card](DeviceSetup/SDCard.md) | N/A |


If you want to work with something else for prototyping or development, we have hundreds of different other devices that you can use to get started as well, as shown below.

| Broadcomm/Raspberry Pi | Intel | Qualcomm |
|-------------|----------|---------|
| [Element 14 / Raspberry Pi Customization Service](https://www.element14.com/community/docs/DOC-76955/l/raspberry-pi-customization-service)| [Intel commercialization devices](https://solutionsdirectory.intel.com/solutions-directory/processors/278/processors/309/processors/402/processors/782/processors/788/processors/1103/processors/1107/processors/1110/processors/1175/processors/1344/processors/1348/processors/1349) | [Qualcomm-based devices](https://developer.qualcomm.com/hardware/snapdragon-410) |

## Microsoft-enabled SoCs
Microsoft works alongside Broadcom, Intel, and Qualcomm to verify support for Windows 10 IoT Core on several of the silicon vendors' SoC. These IoT Core-powered SoCs are used in hundreds of different devices that you can use to prototype and commercialize your idea with. 

| Broadcom | Intel | Qualcomm | NXP (coming soon) |
|----------|-------|----------|-----|
| BCM2837  | [Intel® Joule™](https://software.intel.com/en-us/iot/hardware/joule) | [Snapdragon 212 (APQ8009)](https://www.qualcomm.com/products/snapdragon/processors/212) | [i.MX 6QuadPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| BCM2836  | [Intel® Atom™ processor E3900 series (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | [Snapdragon 410 (APQ8016)](https://www.qualcomm.com/products/snapdragon/processors/410) | [i.MX 6Quad](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | [Intel® Celeron® processor N3350 (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | [Snapdragon 617 (APQ8052)](https://www.qualcomm.com/products/snapdragon/processors/617) | [i.MX 6DualPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[Intel® Pentium® processor N4200 platform (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | | [i.MX 6Dual](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[Intel® Pentium® and Celeron® Processor N3000 Series (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded) | | [i.MX 6DualLite] (https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[	Intel® Atom® x5-E8000 Processor (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded) | | [i.MX 6SoloX](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[Intel® Atom® x5-Z8350 Processor (Cherry Trail)](https://ark.intel.com/products/93361/Intel-Atom-x5-Z8350-Processor-2M-Cache-up-to-1_92-GHz) | | [i.MX 6SoloLite](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[Intel® Atom™ Processor E3800 Product Family (Bay Trail-I)](http://ark.intel.com/products/codename/55844/#@Embedded) | | [i.MX 6SLL](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| | 	[Intel® Pentium® and Celeron® Processor N and J Series (Bay Trail-M/D)](http://ark.intel.com/products/codename/55844/) | |

## Manufacture a board
If you're still looking at different options for your board, you also have the option of having your board built. The following companies specialize in building custom boards:

* [All PCB](http://www.allpcb.com/)
* [JLC PCB](https://jlcpcb.com/)
* [Myro PCB](http://www.myropcb.com/)
* [OSH PARK](https://oshpark.com/)
* [seeed studio](https://www.seeedstudio.com/)

