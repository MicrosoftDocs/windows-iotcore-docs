---
title: SoCs and Custom Boards for Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the hardware features for a variety of suggested boards and community devices.
keywords: windows iot, development devices, boards, SOC, SOM, system on chips, Raspberry Pi 2, Raspberry Pi 3, Minnowboard Max, Dragonboard
---

# SoCs and Custom Boards

## Microsoft-enabled SoCs
Microsoft works alongside Broadcom, Intel, Qualcomm to verify support for Windows 10 IoT Core on several of the silicon vendors' SoC. These IoT Core-powered SoCs are used in hundreds of different devices that you can use to prototype and commercialize your idea with. 

| Broadcom | Intel | Qualcomm | NXP (coming soon) |
|----------|-------|----------|-----|
| BCM2837 | [Intel® Atom™ processor E3900 series (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                                | [Snapdragon 410 (APQ8016)](https://www.qualcomm.com/products/snapdragon/processors/410) | [i.MX 6QuadPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| BCM2836 | [Intel® Celeron® processor N3350 (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                                    | [Snapdragon 212 (APQ8009)](https://www.qualcomm.com/products/snapdragon/processors/212) | [i.MX 6Quad](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)     |
|         | [Intel® Pentium® processor N4200 platform (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                           |                                                                                         | [i.MX 6DualPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Pentium® and Celeron® Processor N3000 Series (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded)                    |                                                                                         | [i.MX 6Dual](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)     |
|         | [Intel® Atom® x5-E8000 Processor (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded)                                        |                                                                                         | [i.MX 6DualLite](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Atom® x5-Z8350 Processor (Cherry Trail)](https://ark.intel.com/products/93361/Intel-Atom-x5-Z8350-Processor-2M-Cache-up-to-1_92-GHz) |                                                                                         | [i.MX 6SoloX](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)    |
|         | [Intel® Atom™ Processor E3800 Product Family (Bay Trail-I)](http://ark.intel.com/products/codename/55844/#@Embedded)	                     |                                                                                         | [i.MX 6SoloLite](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Pentium® and Celeron® Processor N and J Series (Bay Trail-M/D)](http://ark.intel.com/products/codename/55844/)	                     |                                                                                         | [i.MX 6SLL](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)      |

Choosing which one to adopt will depend on considerations such as performance requirements, power profile, cost, physical connectivity options, long term support, operating conditions etc.

You will also need to decide whether to use off-the-shelf board or device, or build a custom device using System-On-Module (SOM) modules + custom carrier board or a complete custom board.

## Customized Boards
If an off-the-shelf device is in a form factor with connectivity options that works for your scenarios, that will often be the most cost and time effective choice.  

For most people, developing a complete custom board would make sense when the product is expected to be sold in volumes greater than tens or even hundreds of thousands of units. For smaller volumes, using a SOM and design a custom carrier board, rather than a completely new board design, can significantly reduce your cost and time to market, and ease software development and integration.

Each of the platforms have unique quirks that need attention during implementation.  Below are some suggestions on where to get started, and while there are many companies building on Windows 10 IoT Core that we don't have direct contact with, we have listed a few we have contact with and know having experience working with Windows IoT Core.

* __[Rasberry Pi](#Rasberry_Pi_derived_custom_design)__
* __[Intel](#Intel_based_custom_design)__
* __[Qualcomm](#Qualcomm_Dragonboard_410c_(APQ8016)_based_custom_design)__
* __[NXP](#Custom_NXP_boards)__

*If you are a SOM provider or an ODM and would like to be added to the list below, please send email to [winiotsomhelp@microsoft.com](mailto:winiotsomhelp@microsoft.com) or directly edit this page and submit a pull request.*

*Many companies below are large and complex.  If you have attempted to contact one of the partners and was unable to reach the right person, please email [winiotsomhelp@microsoft.com](mailto:winiotsomhelp@microsoft.com) and we'll connect you to the right people.*

## **Rasberry Pi derived custom design** 
[Element 14] (https://www.element14.com/community/docs/DOC-76955/l/raspberry-pi-customization-service) offers board customization service for Rasberry Pi to allow you to add or remove connectivity options.  If you also need to make customizations to the BSP, you can leverage the [open source BSP code on Github](https://github.com/ms-iot/bsp).

## **Intel based custom design**
There is a vibrant ecosystem of [experienced Intel device builders](https://solutionsdirectory.intel.com/solutions-directory/processors/278/processors/309/processors/402/processors/782/processors/788/processors/1103/processors/1107/processors/1110/processors/1175/processors/1344/processors/1348/processors/1349) for Windows you can work with.  Compared to the more common Windows 10 PCs, an Intel device designed to run Windows 10 IoT Core have couple of differences: 

1.  If you need to provide user mode UWP API access to simple buses like I2C, GPIO and SPI, you need make sure that ACPI table in your UEFI firmware contains  appropriate entries for RHProxy. Please refer to [user mode access](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/enable-usermode-access) for more information.
2.  You must ensure that the SMBIOS in the firmware contains information as listed in [OEM License Requirement](https://docs.microsoft.com/en-us/windows/iot-core/commercialize-your-device/oemlicenserequirements)

If you are building your own board, please contact your BIOS vendor if you need guidance on ACPI or SMBIOS changes or work with one of the experienced partner below.

### *Experienced Partners*
*  [Aaeon](http://www.aaeon.com/en/)
*  [Advantech](http://www.advantech.com/)
*  [Kontron](http://www.advantech.com/)
*  [Nexcom](http://www.nexcom.com/)

## **Qualcomm Dragonboard 410c (APQ8016) based custom design**
Binary BSP for Dragonboard 410c (based on Qualcomm AQP8016 SoC) can be downloaded from [Qualcomm Developer Network](https://developer.qualcomm.com/hardware/dragonboard-410c/software).  

The BSP package include the source code for ACPI to allow for simple hardware customizations that only requires ACPI changes.  

If you need additional hardware customizations, eg. using a specific MIPI-DSI display panel, enabling Platform Secure Boot, RF calibration etc.,you will need access access to BSP source code or work with a provider with such access.

We suggest that:
1.   If you're using SOM, work with an experienced SOM provider to enable customized component.
2.   If you are building a custom board, we recommend that you work with a SOM vendors or an experienced Qualcomm BSP customization service provider such as [Intrynsic](https://www.intrinsyc.com/) or [Thundersoft] (www.thundersoft.com/) for BSP customization.
3.   If you expect to have very high volume (millions) [contact Qualcomm] (https://assets.qualcomm.com/contact-sales-iot.html).

### *Experienced Partners*
*  [eInfochips](https://eragon.einfochips.com/products/system-on-modules/qualcomm-snapdragon-410-apq8016-eragon-eic-q410-200-som.html)
*  [Intrinsyc](https://www.intrinsyc.com/computing-platforms/410-som/)
*  [Keith & Koep](https://keith-koep.com/en/products/products-som/myon-1-features-snapdragon-410/)
*  [Unitech](http://ute.com/products_info.php?pc1=4&pc2=461&rbu=0&pid=2395)

## **NXP preview**
NXP support for Windows 10 IoT Core is in private preview. Please sign up to express interest [here](http://aka.ms/iotnxp).

You can also reach out to partners we're working with during preview.
*  Aaeon [PICO-IMX6](http://www.aaeon.com/en/p/pico-itx-boards-pico-imx6/)
*  Advantech [RSB-4411](http://www.advantech.com/products/single_board_computer/rsb-4411/mod_d3901250-b0a0-4a5f-9762-b26fa0c36858)
*  Keith & Koep [pConXS](http://wce.keith-koep.com/en/products/pconxs-ff/) with [Trizeps VII](http://wce.keith-koep.com/en/products/trizeps7-i.MX6/)
* Solid Run [Hummingboard Edge](https://www.solid-run.com/product/hummingboard-edge-imx6s-wa-e/)
* Kontron [SMARC-sAMX6i](https://www.kontron.com/products/boards-and-standard-form-factors/smarc/smarc-samx6i.html)