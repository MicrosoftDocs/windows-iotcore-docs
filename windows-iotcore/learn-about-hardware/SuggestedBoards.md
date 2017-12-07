---
title: Suggested Boards and SoCs for Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the hardware features for a variety of suggested boards and community devices.
keywords: windows iot, development devices, boards, SOC, system on chips, Raspberry Pi 2, Raspberry Pi 3, Minnowboard Max, Dragonboard
---

# Suggested Boards and SoCs

## Windows 10 IoT Core Development Devices
While we suggest a few boards to get started on, if you want to work with something else for prototyping or development, we have a number of additional options in the ecosystem.

## Microsoft-enabled SoCs
Microsoft works alongside Broadcom, Intel, and Qualcomm to verify support for Windows 10 IoT Core on several of the silicon vendors' SoC. These IoT Core-powered SoCs are used in hundreds of different devices that you can ues to prorotype and commercialize your idea with.

| Broadcom | Intel | Qualcomm |
|----------|-------|----------|
| BCM2837  | [Intel® Joule™](https://software.intel.com/en-us/iot/hardware/joule) | [Snapdragon 212 (APQ8009)](https://www.qualcomm.com/products/snapdragon/processors/212) |
| BCM2836  | [Intel® Atom™ processor E3900 series (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | [Snapdragon 410 (APQ8016)](https://www.qualcomm.com/products/snapdragon/processors/410) |
| | [Intel® Celeron® processor N3350 (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | [Snapdragon 617 (APQ8052)](https://www.qualcomm.com/products/snapdragon/processors/617) |
| | 	[Intel® Pentium® processor N4200 platform (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded) | |
| | 	[Intel® Pentium® and Celeron® Processor N3000 Series (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded) | |
| | 	[	Intel® Atom® x5-E8000 Processor (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded) | |
| | 	[Intel® Atom® x5-Z8350 Processor (Cherry Trail)](https://ark.intel.com/products/93361/Intel-Atom-x5-Z8350-Processor-2M-Cache-up-to-1_92-GHz) | |
| | 	[Intel® Atom™ Processor E3800 Product Family (Bay Trail-I)](http://ark.intel.com/products/codename/55844/#@Embedded) | |
| | 	[Intel® Pentium® and Celeron® Processor N and J Series (Bay Trail-M/D)](http://ark.intel.com/products/codename/55844/) | |

## Suggested devices
The publicly available boards below are some of the same devices Microsoft uses as part of our operating system engineering efforts. These are also the devices Microsoft requires reported OS issues to reproduce on for engineering support. We provide an easy process for you to get started with these devices right away. Learn more about the features of each device below and check out the [supported hardware peripherals](HardwareCompatList.md) for each board to decide what device is right for you. If you don't see a device below that works to prorotype or commercialize your idea, please check additional devices or community devices.

> [!NOTE]
> Hardware features listed below may not be fully supported in all configurations


|                      |Raspberry Pi 2 v1.1 boards and earlier|Raspberry Pi 3| MinnowBoard Max| DragonBoard 410c |
|----------------------|-------------------|--------------|-------------------|---------------|
|SoC  | Broadcom BCM2836 | Broadcom BCM2837 | [Intel Atom Processor E3825](http://ark.intel.com/products/78474/Intel-Atom-Processor-E3825-1M-Cache-1_33-GHz) | [Qualcomm Snapdragon 410](https://www.qualcomm.com/products/snapdragon/processors/410) |
|BSPs | [Raspberry drivers](https://github.com/ms-iot/bsp) | [Raspberry drivers](https://github.com/ms-iot/bsp) | [Baytrail drivers](https://www.intel.com/content/www/us/en/embedded/products/bay-trail/software-and-drivers.html) | [Dragonboard 410c drivers](https://developer.qualcomm.com/hardware/dragonboard-410c/software) |
|CPU  | 900MHz Quad-Core ARM Cortex A7| 	1.2GHz Quad-Core ARM Cortex A53 | 1.3GHz x86/x64 | 	1.2GHz Quad-Core ARM Cortex A53 |
|Memory| 1GB | 1GB | 2 GB| 1GB |
|GPU | Broadcom Video Core IV @ 250MHz (no DirectX or Hardware Acceleration support) | 	Broadcom Video Core IV @ 400MHz (no DirectX or Hardware Acceleration support) | Intel HD Graphics | Qualcomm Adreno 306 @ 400MHz (only 720p / 1280 x 720 supported) |
| USB | 4x USB 2.0 | 4x USB 2.0 | 1x USB 2.0, 1x USB 3.0 | 2x USB 2.0 |
| Networking | 10/100/1000 MBit/s Ethernet | Wi-Fi 802.11 b/g/n, 10/100/1000 MBit/s Ethernet, Bluetooth 4.1 | 10/100/1000 MBit/s Ethernet | Wi-Fi 802.11 a/b/g/n, Bluetooth 4.1 |
| Video Output | HDMI, DSI | HDMI, DSI | Micro HDMI	| HDMI, DSI |
| Audio Output | Analog via 3.5 mm jack | Analog via 3.5 mm jack | Digital via HDMI	| Digital via HDMI |
| GPS| No | No | No | Yes | 
| Peripherals |   [Raspberry Pi 2 Pin Mappings](PinMappings/PinMappingsRPI.md) | [Raspberry Pi 3 Pin Mappings](PinMappings/PinMappingsRPI.md) | [Minnowboard Max Pin Mappings](PinMappings/PinMappingsMBM.md) | [Dragonboard Pin Mappings](PinMappings/PinMappingsDB.md) |
|         | 24x GPIO pins | 24x GPIO pins | 10x GPIO pins | 11x GPIO pins |
|  | 1x Serial UART | 1x Serial mini UART | 2x Serial UARTs | 2x Serial UARTs |
|  | 2x SPI bus | 2x SPI bus | 1x SPI bus | 1x SPI bus |
|  | 1x I2C bus | 1x I2C bus | 1x I2C bus | 2x I2C bus |

## Additional Devices
In addition to the suggested development devices, IoT Core-supported SoCs power hundreds of different devices that you can use to prototype or commercialize your idea with.

| Broadcomm | Intel | Qualcomm |
|-------------|----------|---------|
| [Element 14 / Raspberry Pi Customization Service](https://www.element14.com/community/docs/DOC-76955/l/raspberry-pi-customization-service)| [Intel commercialization devices](https://solutionsdirectory.intel.com/solutions-directory/processors/278/processors/309/processors/402/processors/782/processors/788/processors/1103/processors/1107/processors/1110/processors/1175/processors/1344/processors/1348/processors/1349) | [Qualcomm-based devices](https://developer.qualcomm.com/hardware/snapdragon-410) |

## Community Devices
While Microsoft has engineered support for IoT Core with specific SoCs that enable hundreds of devices, several companies have independently enabled support for IoT Core on their devices with additional SoCs to address the broad needs of the IoT market.

> [!NOTE] 
> IoT Core on these devices is not validated or supported by Microsoft. If you choose to use any of these solutions, please work with the listed vendor to ensure that they are able to adequately deliver support for the current and future updates of IoT Core.

> [!TIP]
> If you'd like to add your device to the community devices list, please submit a PR for this page.

| Device | SoC | Software image | Contact |
|-------------|----------|---------|---------|
| [Banana Pi M64](http://www.banana-pi.org/m64.html) | [Allwinner A64](http://www.allwinnertech.com/index.php?c=product&a=index&id=9) | [Get started tutorial](http://forum.banana-pi.org/c/BPI-M64/Win-10-IoT) | [Email](mailto:jasonye@banana-pi.com) |
| [Pine 64](https://www.pine64.org/) | [Allwinner A64](http://www.allwinnertech.com/index.php?c=product&a=index&id=9) | [Download image](http://files.pine64.org/os/win10-iot/Windows10IoT_Pine64.ffu) | [Email](mailto:support@pine64.org) |

## Legacy Devices
This is a list of boards that we no longer provide long-term support for. Developers may still use these devices, but will not receive the latest updates for them. For any questions or concerns, please open an issue on GitHub.

* Intel Joule
