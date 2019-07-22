---
title: Windows IoT and NXP i.MX
author: chsha 
ms.author: chsha 
ms.date: 02/22/2019 
ms.topic: article 
description: Learn about Windows 10 IoT Core and NXP i.MX SoCs
keywords: Windows 10 IoT Core, Get Started, i.MX, NXP
---

# Window 10 IoT Core and NXP i.MX SoCs

In 2018, Microsoft and NXP announced a private preview of Windows 10 IoT Core on NXP i.MX 6 and i.MX 7 silicon and began work on the i.MX 8M SoCs. Hundreds of commercial developers, researchers, and Makers expressed their interest in the combination of 10 years of Windows security updates and the flexibility and reliability of NXP silicon. 
 
During the preview, Microsoft and NXP engineers spent thousands of hours tuning and improving the BSP based on input from those evaluating the solution. We worked with customers interested in modernizing legacy industrial controllers, developing new cloud connected building automation solutions, and gateways with class leading security such as [trusted I/O](https://blogs.windows.com/windowsexperience/2018/04/24/trusted-cyber-physical-systems-looks-to-protect-your-critical-infrastructure-from-modern-threats-in-the-world-of-iot/#A0WkfgLBpgbLaFe3.97).
 
Based on the overwhelming interest in the solution, Microsoft and NXP are now making BSPs for the i.MX 6, i.MX 7, and i.MX 8M family of SoCs available as a non-commercial public preview. Because of the long history Microsoft and NXP have in the embedded and IoT markets, we understand the need for design flexibility. Therefore, in addition to the multiple single board computers and system on module solutions Microsoft, NXP, and our hardware partners have enabled, the i.MX 6, i.MX 7, and i.MX 8M BSPs are provided under open source licensing. Now, everyone will be able to access the complete BSP contents for the i.MX 6, i.MX 7, and i.MX 8M product families for evaluation use on their hardware along with the October 2018 release of Windows 10 IoT Core.


## BSP Access

If you are interested to enable support for your own i.MX hardware, please access the BSP source and documentation on [Github]( https://github.com/ms-iot/imx-iotcore). Unless noted, the majority of the source is provided under MIT license. The code is released for commercial use with support provided by NXP and can be found [here](https://www.nxp.com/support/developer-resources/evaluation-and-development-boards/i.mx-evaluation-and-development-boards/i.mx-software-and-development-tool:IMX-SW).

If you have NXP hardware/BSP releated questions or feedback on how the BSP can better support your targeted solution, please post to the [NXP Community](https://community.nxp.com/community/imx/content?filterID=contentstatus%5Bpublished%5D%7Ecategory%5Bwindows%5D). For any Windows related questions, please use the [Microsoft Community](https://social.msdn.microsoft.com/forums/en-US/home?forum=WindowsIoT).


## Ecosystem Resources

Several Microsoft and NXP partners have enabled commercial i.MX 6, i.MX 7, and i.MX 8M devices with support for Windows 10 IoT Core. Please contact the partner directly for hardware and a platform image.


> | Device | Contact |
> |-------|------|
> | [Aaeon PICO-IMX6](https://www.aaeon.com/en/p/pico-itx-boards-pico-imx6/) | [David Hung](mailto:davidhung@aaeon.com.tw) |
> | [Advantech RSB-4411](http://www.advantech.com/products/single_board_computer/rsb-4411/mod_d3901250-b0a0-4a5f-9762-b26fa0c36858) | [buy@advantech.com](mailto:buy@advantech.com) |
> | [Compulab IoT-Gate](https://www.compulab.com/products/iot-gateways/iot-gate-imx7-nxp-i-mx-7-internet-of-things-gateway/) | [Igor Vaisbein](mailto:igor@compulab.co.il) | 
> | [FS Eletronik Systme armStone A9](https://www.fs-net.de/en/products/armstone/armstonea9/) | [support@fs-net.de](mailto:support@fs-net.de) |

> | [Geniatech SoM-iMX6Q-Q7](https://www.geniatech.com/product/som-imx6q-q7/) | [Mike Decker](mailto:mike.decker@geniatech.com) or [Fang Jijun](mailto:Fjj@geniatech.com) |
> | [Geniatech SoM-iMX7D](https://www.geniatech.com/product/som-imx7d/) | [Mike Decker](mailto:mike.decker@geniatech.com) or [Fang Jijun](mailto:Fjj@geniatech.com) |
> | [Ka-Ro Electronics TX6UL, TX6S, TX6DL, and TX6Q](https://www.karo-electronics.de/tx-standard.html?&L=1) | [Uwe Steinkohl](mailto:us@karo-electronics.de) |
> | [Keith & Koep pConXS](https://keith-koep.com/de/produkte/produkte-baseboards/pconxs-baseboard-vollausstattung-technische-daten/) with [Trizeps VII](https://keith-koep.com/de/produkte/produkte-trizeps/trizeps-vii-technische-daten-imx6/) | [contact@keith-koep.com](mailto:contact@keith-koep.com) |
> | [Kontron SMARC-sAMX6i](https://www.kontron.com/products/boards-and-standard-form-factors/smarc/smarc-samx6i.html) | [Martin Unverdorben](mailto:martin.unverdorben@kontron.com) |
> | [Novtech Meerkat](http://novtech.com/products/meerkat96.html) | [sales@novtech.com](mailto:sales@novtech.com) |
> | [phyBOARD-i.MX 7 Development Kit](https://phytec.com/product/phyboard-imx7-development-kit/) | [Fernando Benitez](mailto:sales@phytec.com) |
> | [Solid Run Hummingboard Edge](https://www.solid-run.com/imx6-win-10-iot-core/) | [Ilya Viten](mailto:ilya@solid-run.com) |
> | [VIA VAB-820](https://www.viaembeddedstore.com/shop/boards/vab-820/) | [Michael Fox](mailto:MichaelFox@via.com.tw) or [Dream Ku](mailto:dreamku@via.com.tw) |
> | [WeAreDev WAD-MX6W](http://www.wearedev.net/?mod=wadmx6w) | [help@wearedev.net](mailto:help@wearedev.net) |
> | [MCIMX6ULL-EVK](https://www.nxp.com/products/processors-and-microcontrollers/arm-based-processors-and-mcus/i.mx-applications-processors/i.mx-6-processors/evaluation-kit-for-the-i.mx-6ull-and-6ulz-applications-processor:MCIMX6ULL-EVK) | [Wei Wang](mailto:Wei.A.Wang@nxp.com) |
> | [MCIMX8M-EVK](https://www.nxp.com/support/developer-resources/software-development-tools/i.mx-developer-resources/evaluation-kit-for-the-i.mx-8m-applications-processor:MCIMX8M-EVK) |  |
> | [MCIMX8MMINI-EVK](http://www.nxp.com/imx8mminievk) | []() |
