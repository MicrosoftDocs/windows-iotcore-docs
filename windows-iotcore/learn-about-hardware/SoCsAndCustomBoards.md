---
title: SoCs and Custom Boards for Windows 10 IoT Core
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the hardware features for a variety of suggested boards and community devices.
keywords: windows iot, development devices, boards, SOC, SOM, system on chips, Raspberry Pi 2, Raspberry Pi 3, Minnowboard Max, DragonBoard
---

# SoCs and custom boards

## Microsoft-enabled SoCs
Microsoft works alongside Broadcom, Intel, NXP, and Qualcomm to verify support for Windows 10 IoT Core on several vendors' system on a chip (SoCs). These IoT Core-powered SoCs are used in hundreds of different devices that you can use to prototype and commercialize your idea. 

| Broadcom | Intel | Qualcomm | NXP (coming soon) |
|----------|-------|----------|-----|
| BCM2837 | [Intel® Atom® processor E3900 series (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                                | [Snapdragon 410 (APQ8016)](https://www.qualcomm.com/products/snapdragon/processors/410) | [i.MX 6QuadPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
| BCM2836 | [Intel® Celeron® processor N3350 (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                                    | [Snapdragon 212 (APQ8009)](https://www.qualcomm.com/products/snapdragon/processors/212) | [i.MX 6Quad](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)     |
|         | [Intel® Pentium® processor N4200 platform (Apollo Lake)](https://ark.intel.com/products/codename/80644/#@embedded)                           |                                                                                         | [i.MX 6DualPlus](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Pentium® and Celeron® Processor N3000 Series (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded)                    |                                                                                         | [i.MX 6Dual](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)     |
|         | [Intel® Atom® x5-E8000 Processor (Braswell)](http://ark.intel.com/products/codename/66094/#@embedded)                                        |                                                                                         | [i.MX 6DualLite](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Atom® x5-Z8350 Processor (Cherry Trail)](https://ark.intel.com/products/93361/Intel-Atom-x5-Z8350-Processor-2M-Cache-up-to-1_92-GHz) |                                                                                         | [i.MX 6SoloX](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)    |
|         | [Intel® Atom® Processor E3800 Product Family (Bay Trail-I)](http://ark.intel.com/products/codename/55844/#@Embedded)	                 |                                                                                         | [i.MX 6SoloLite](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u) |
|         | [Intel® Pentium® and Celeron® Processor N and J Series (Bay Trail-M/D)](http://ark.intel.com/products/codename/55844/)	                 |                                                                                         | [i.MX 6SLL](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9XpjGK4S5xLp4jJORm7749UQVg4STc5UlcyR0ozWkkzUDYzMjI2RjhHVC4u)      |

The SoC you choose to adopt will depend on considerations such as performance requirements, power profile, cost, physical connectivity options, long term support, and operating conditions.

You'll also need to decide whether you want to use an off-the-shelf board or device, build a custom device using a system on a module (SoM) plus a custom carrier board, or build a complete custom board. Cost and the degree of customization are the key factors in this decision, with both generally increasing as you customize further.

## Windows 10 IoT Core Features by Processor Family

> [!NOTE] 
> This list takes into consideration processors that will be available in Fall 2018. 

To help you select the right platform for your device, the table below shows the features that are supported by processor family with Windows 10 IoT Core. All features listed below are supported in Windows 10 IoT Core, however some SoCs may not have the specific IP included in their design, and are such indicated with "N/A". In such cases, a 3rd party solution can be incorporate into the design to provide the required functionality.  In a limited number of cases where a Windows 10 IoT Core feature is not implemented on a processor, the entry is left blank.


> |    | Intel  |  Qualcomm  | NXP i.MX6 | NXP i.MX7 | Broadcom |
> |----|--------|------------|-----------|-----------|-----------------|
> | Audio | x | x | x | x | x |
> | GPIO | x | x | x | x | x | 
> | I2C | x | x | x | x | x |
> | Ethernet | x | N/A | x | x | x |
> | SPI | x | x | x | x | x |
> | Display | x | x | x | x | x |
> | UART | x | x | x | x | x |
> | USB | x | x | x | x | x |
> | PCIe | x | N/A | x | Under development | N/A |
> |MIPI-CSI | N/A | x | N/A | N/A | N/A |
> | Graphics/Video | x | x | Software-rendered | Software-rendered | Software-rendered |
> | GPS | N/A | x | N/A | N/A | N/A |
> | Wi-Fi/BT | N/A | x | N/A | N/A | N/A |
> | Trusted I/O | N/A | N/A | x | x | N/A |
> | Processor power management |  | x | x | x | | 
> | TPM | x | x | x | x | N/A | 
> | Secure Boot | x | x | Under development | Under development | |
> | PWM | x | N/A | x | x | |
> | JTAG | x | N/A | x | x | | 
> | eMMC | x | x | x | x | |
> | SDHC | x | x | x | x | x |

## Customized boards
If an off-the-shelf device is in a form factor that includes the connectivity options that work for your scenarios, that will often be the most cost- and time-effective choice.  

For most people, developing a complete custom board would make sense when the product is expected to be sold in volumes greater than tens, or even hundreds, of thousands of units. For smaller volumes, using a SoM and designing a custom carrier board, instead of designing a completely new board, can significantly reduce your cost and time-to-market, as well as streamlining software development and integration.

Each of the platforms has unique quirks that need attention during implementation.  Below are some suggestions on how to get started. And while there are many companies building on Windows 10 IoT Core, here is a list of some that have proven experience working with Windows 10 IoT Core:

* __[Raspberry Pi](#raspberry-pi-derived-custom-design)__
* __[Intel](#intel-based-custom-design)__
* __[Qualcomm](#qualcomm-dragonboard-410c-apq8016-based-custom-design)__
* __[NXP](#nxp-preview)__

*If you are a SoM provider or an ODM and would like to be added to the list below, please send email to [winiotsomhelp@microsoft.com](mailto:winiotsomhelp@microsoft.com) or directly edit this page and submit a pull request.*

*Many companies listed here are large and complex.  If you have trouble reaching the right person, please email [winiotsomhelp@microsoft.com](mailto:winiotsomhelp@microsoft.com) and we'll do our best to connect you to the right people.*

### **Raspberry Pi-derived custom design** 
[Element 14](https://www.element14.com/community/docs/DOC-76955/l/raspberry-pi-customization-service) offers board customization service for Raspberry Pi to allow you to add or remove connectivity options. If you also need to make customizations to the BSP, you can leverage the [open source BSP code on Github](https://github.com/ms-iot/bsp).

### **Intel-based custom design**
There is a vibrant ecosystem of [experienced Intel device builders](https://solutionsdirectory.intel.com/solutions-directory/processors/278/processors/309/processors/402/processors/782/processors/788/processors/1103/processors/1107/processors/1110/processors/1175/processors/1344/processors/1348/processors/1349) for Windows you can work with. An Intel device designed to run Windows 10 IoT Core has a couple of differences from the more common PCs: 

1.  If you need to provide user mode Universal Windows Platform (UWP) API access to simple buses like I2C, GPIO and SPI, you need make sure that ACPI table in your UEFI firmware contains  appropriate entries for RHProxy. Please refer to [user mode access](https://docs.microsoft.com/en-us/windows/uwp/devices-sensors/enable-usermode-access) for more information.
2.  You must ensure that the SMBIOS in the firmware contains information as listed in [OEM License Requirement](https://docs.microsoft.com/en-us/windows/iot-core/commercialize-your-device/oemlicenserequirements).

If you are building your own board, please contact your BIOS vendor if you need guidance on ACPI or SMBIOS changes.

#### *Experienced partners*
*  [Aaeon](http://www.aaeon.com/en/)
*  [Advantech](http://www.advantech.com/) - buy@advantech.tw
*  [Kontron](http://www.kontron.com/) - martin.unverdorben@kontron.com
*  [Nexcom](http://www.nexcom.com/)

### **Qualcomm DragonBoard 410c (APQ8016)-based custom design**
Binary BSP for DragonBoard 410c (based on Qualcomm AQP8016 SoC) can be downloaded from [Qualcomm Developer Network](https://developer.qualcomm.com/hardware/dragonboard-410c/software).  

The BSP package includes the source code for ACPI to allow for simple hardware customizations that only require ACPI changes.  

**IMPORTANT** If you need additional hardware customizations, such as using a specific 
MIPI-DSI display panel, enabling Platform Secure Boot, RF calibration and certification 
(eg. FCC, CE), you'll need become a Qualcomm BSP source code licensee, or to work with a 
provider that has access (see Experienced partners below).

Recommendations:
1.   If possible, work with an experienced SoM vendor to enable customized design.
2.   If you're building a custom board, work with a SoM vendor or an experienced Qualcomm BSP customization service provider, such as [Intrinsyc](https://www.intrinsyc.com/) or [Thundersoft](http://www.thundersoft.com/) for BSP customization and design assistance.
3.   If you expect to have very high volume (millions), [contact Qualcomm](https://assets.qualcomm.com/contact-sales-iot.html).


#### *Experienced partners*
*  [Intrinsyc](https://www.intrinsyc.com/computing-platforms/410-som/) - Mark Waldenberg (mwaldenberg@intrinsyc.com)
*  [Keith & Koep](https://keith-koep.com/en/products/products-som/myon-1-features-snapdragon-410/) - contact@keith-koep.com
*  [Reycom](http://www.reycom.swiss/en/home-swiss.html) - welcome@reycom.swiss
*  [Unitech](http://ute.com/products_info.php?pc1=4&pc2=461&rbu=0&pid=2395) - Sam (saml@tw.ute.com); Perry (perryt@te.ute.com)


### **NXP preview**
NXP support for Windows 10 IoT Core is in private preview. Please sign up to express interest [here](http://aka.ms/iotnxp).

You can also reach out to partners we're working with during preview:
*  Advantech [RSB-4411](http://www.advantech.com/products/single_board_computer/rsb-4411/mod_d3901250-b0a0-4a5f-9762-b26fa0c36858) - buy@advantech.tw
*  Keith & Koep [pConXS](http://wce.keith-koep.com/en/products/pconxs-ff/) with [Trizeps VII](http://wce.keith-koep.com/en/products/trizeps7-i.MX6/) - contact@keith-koep.com
*  Kontron [SMARC-sAMX6i](https://www.kontron.com/products/boards-and-standard-form-factors/smarc/smarc-samx6i.html) - Martin Unverdorben (martin.unverdorben@kontron.com)
*  Solid Run [Hummingboard Edge](https://www.solid-run.com/imx6-win-10-iot-core/ )- Ilya Viten (ilya@solid-run.com)
*  Geniatech [SoM-iMX6Q-Q7](https://www.geniatech.com/product/som-imx6q-q7/) & [SoM-iMX7D](https://www.geniatech.com/product/som-imx7d/) - Mike Decker (mike.decker@geniatech.com) or Fang Jijun (Fjj@geniatech.com)
*  VIA [VAB-820](https://www.viaembeddedstore.com/shop/boards/vab-820/) - Michael Fox (MichaelFox@via.com.tw) or Dream Ku (dreamku@via.com.tw)
*  Phytec [phyBOARD-i.MX7](https://phytec.com/products/single-board-computers/phyboard-i.mx7/) - Brad Dodson (sales@phytec.com)

## Other options
If you find that you'd still like to create a custom board, we have provided a few suggestions of manufacturers below that can help with schematics and layout for a board.

* [All PCB](http://www.allpcb.com/)
* [Geppetto/Gumstix](https://www.gumstix.com/geppetto/)
* [JLC PCB](https://jlcpcb.com/)
* [Myro PCB](http://www.myropcb.com/)
* [OSH PARK](https://oshpark.com/)
* [seeed studio](https://www.seeedstudio.com/)
