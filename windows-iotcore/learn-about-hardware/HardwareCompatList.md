---
title: Hardware Compatbility List
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn about the peripheral interfaces and protocols that Windows 10 IoT Core best supports. 
keywords: windows iot, peripherals, protocols, compatibility, busses, hardware
---

# Hardware compatibility list

Windows 10 IoT Core supports a variety of peripheral interfaces and protocols, including support for common busses like I2C, UART, USB, and more. This page lists known supported peripherals and is current as of the latest RTM release. Specific entries may only work on Insider releases and will be noted as such. We encourage you to contribute to this list on GitHub!

> [!IMPORTANT]
> This list is not exhaustive. There are many other peripherals not listed on this page that are compatible with Windows 10 IoT Core. If a device you don't see listed but is class-compliant with what's already supported in Windows 10 IoT Core, then it will work. 


Looking for information about supported hardware platforms? Click [here](https://developer.microsoft.com/en-us/windows/iot/getstarted/prototype/selectdevice) for a list of development boards compatible with Windows.

## USB Devices

### WiFi Adapters
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|---------------|------------------------------|
> | Official Raspberry Pi WiFi dongle | ARM32, x64, x86 | The official Raspberry Pi WiFi dongle offers the best possible WiFi performance for its diminutive size. | | &#10004;  |
> | Airlink Wireless N 150 Mini USB Adapter Adapter | x64, x86 | Airlink 101 AWL5077 Golden 150Mbps Wireless Mini USB Adapter with WPA2, WPA, and WEP enhanced wireless security | | &#10004;  
> | Panda PAU06 | x64, x86 |  Panda 300Mbps Wireless N USB Adapter with High Gain Antenna | |  &#10004;  
> | TP-LINK TL_WN725N |  ARM, x32, x64, x86 | TP-LINK TL-WN725N Wireless N Nano USB Adapter 150 Mbps `(USB/VID_0BDA&PID_8179)` |  | &#10004;  
> | NET-DYN USB WiFi Adapter | MBM | WiFi USB Adapter NET-DYN | |  &#10004;  
> | Realtek 8191 USB Wireless WiFi | ARM32, x64, x86 | Realtek 8191 300Mbps 802.11n/g/b/ USB Wireless WiFi LAN Network Card Adapter | | &#10004;  
> | Realtek 8192 USB Wireless WiFi | ARM32, x64, x86 | Realtek Single-Chip IEEE 802.11b/g/n 2T2R WLAN Controller with USB 2.0 Interface | | &#10004; |
> | Realtek 8188EU USB Wireless WiFi | ARM32, Mx64, x86BM | Realtek RTL8188EU Wireless LAN 802.11n/g/b USB 2.0 Network Adapter | | &#10004; |
> | Realtek 8192EU USB Wireless WiFi | ARM32, x64, x86 | Realtek RTL8192EU Wireless LAN 802.11n/g/b USB 2.0 Network Adapter | | &#10004; |
> | CanaKit USB Wireless WiFi | x64, x86 | Chipset Ralink 5370 | | &#10004;
> | D-Link DWA-172 | ARM32 | Wireless AC600 Dual-Band High-Gain USB Adapter | [Datasheet](ftp://ftp.dlink.de/dwa/dwa-172/documentation/DWA-172_ds_en_Datasheet.pdf) |

### Bluetooth Dongles
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | CSR Mini USB Bluetooth V 4.0 Adapter | ARM32, x64, x86 | Class 2 Bluetooth 4.0 Smart Ready Adapter, low energy, dual power |  | &#10004; 
> | ORICO BTA-403 Mini Bluetooth 4.0 USB Dongle | ARM32, x64, x86 | Low-energy Bluetooth 4.0 adapter USB Micro Adapter Dongle |  | &#10004; 
> | CSR Mini USB Bluetooth V 4.0 Adapter | x64, x86 | Class 2 Bluetooth 4.0 Smart Ready Adapter, low energy, dual power |  | &#10004;|

### Cameras
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | Microsoft Lifecam 3000 USB Camera | ARM32, x64, x86 | USB Webcam | [Home Security Camera Project](https://developer.microsoft.com/en-us/windows/iot/samples/webcamapp)|&#10004;|
> | Microsoft Lifecam HD-5000 | ARM32, x64, x86 | Microsoft LifeCam HD-5000 720p HD Webcam | | &#10004; |
> | Microsoft® LifeCam Studio™ | ARM32 | Microsoft® LifeCam Studio™ (model: 1425) 1080p HD Webcam | | |
> | Logitech Webcam C210 | ARM32, x64, x86 | USB Webcam, 1.3mp photo |  |&#10004; |

### Audio
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|
> | Sabrent USB External Stereo Sound Adapter, Model AU-EMAC1 | ARM32, x64, x86 | Converts USB to 3.5mm audio and microphone signals | | &#10004; 

### Miscellaneous
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | Aeon Labs Z-Wave Z-Stick Series 2 USB Dongle DSA02203-ZWUS | ARM32 | Series 2 Z-Wave USB Z-Stick Controller |  | &#10004; |
> | [Chalkboard Electronics 7” LCD Capacitive Touchscreen Display](https://www.chalk-elec.com/?page_id=1280#!/7-black-frame-universal-HDMI-LCD-with-capacitive-multi-touch/p/21750201/category=3094861) | ARM32 | | [Updating firmware](https://www.chalk-elec.com/?p=1826) | &#10004; |
> | Vodafone (Huawei) K5150 | ARM32, x64, x86 | Vodafone (Huawei) K5150 150Mbps 4G LTE FDD USB Mobile Broadband Modem |  | &#10004;  |
> | Vodafone (Huawei) K5160 | ARM32, x64, x86 | Vodafone (Huawei) K5160 150Mbps GSM/EDGE/3G/HSPA+/LTE-CAT4 USB Mobile Broadband Modem |  | |
> | Sierra Wireless Beam (AirCard 340U) | x64, x86 | 	Sierra Wireless Beam (AirCard 340U) 4G LTE USB Mobile Broadband Modem |  |&#10004; |
> | Microsoft Xbox 360 Controller | ARM32 | An HID-compliant USB gamepad for Microsoft's Xbox 360 | [Robot Kit](https://microsoft.hackster.io/en-US/windowsiot/robot-kit-6dd474) |  &#10004; |
> | [MyTeletouch](http://www.myteletouch.com/) | ARM, x32 | An HID-compliant USB wireless mouse, keyboard and gamepad |  | &#10004; |

## Other Hardware Peripherals

### Storage Media
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | [Samsung 32GB EVO Class 10 Micro SDHC](https://www.amazon.com/gp/product/B00IVPU786) | AARM32, x64, x86 | A recommended SD card for devices that can have Windows 10 IoT Core flashed. | | &#10004;|
> | [SanDisk Ultra Micro SDHC 16GB](https://www.amazon.com/SanDisk-Ultra-Micro-SDHC-16GB/dp/9966573445) | ARM32, x64, x86 | A recommended SD card for devices that can have Windows 10 IoT Core flashed. | | &#10004; |

### Pi Hats
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | [Adafruit 16-Channel PWM](https://www.adafruit.com/product/2327#description-anchor) | ARM32 | Adds the capability to control up to 16 servos with no additional Raspberry Pi processing overhead. Capable of doing PWM up to 1.6KHz with 12 bit precision. | [Adafruit Tutorial C# IoT Sample](https://github.com/golaat/Adafruit.Pwm) | |
> | [Dexter Industries GrovePi](https://www.dexterindustries.com/shop/grovepi-board/) | ARM32 | You can connect hundreds of different sensors without soldering, so you can program them to monitor, control, and automate devices in your life. | [GrovePi Samples](https://github.com/DexterInd/GrovePi/) | |
> | Dexter Industries GoPiGo | ARM, x32 | The GoPiGo is a delightful and complete robot for the Raspberry Pi that turns your Pi into a fully operating robot. GoPiGo is a mobile robotic platform for the Raspberry Pi developed by Dexter Industries. | [GoPiGo Samples](https://github.com/DexterInd/GoPiGo/tree/master/Software/CSharp) | |

### Sensors
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | DHT11 basic temperature-humidity sensor | ARM32, x64, x86 | A basic, ultra low-cost digital temperature and humidity sensor. It uses a capacities humidity sensor and a thermistor to measure the surrounding air, and spits out a digital signal on the data pin (no analog input pins needed).  | [GpioOneWireSample (DHT11)](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/GpioOneWire)| &#10004; |
> | DHT22 temperature-humidity sensor | ARM32, x64, x86 | A basic, ultra low-cost digital temperature and humidity sensor. It uses a capacities humidity sensor and a thermistor to measure the surrounding air, and spits out a digital signal on the data pin (no analog input pins needed).  | [GpioOneWireSample (DHT11)](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/GpioOneWire) | &#10004; |
> | SparkFun Triple Axis Accelerometer Breakout - ADXL345 | ARM32, x64, x86 | Small, thin, low power, 3-axis MEMS accelerometer with high resolution (13-bit) measurement at up to ±16 g. Digital output data is formatted as 16-bit twos complement and is accessible through either a SPI (3- or 4-wire) or I2C digital interface. |[Accelerometer Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/Accelerometer) | &#10004; |
> | Adafruit BMP280 Temperature and Barometric Sensor | ARM32 | Bosch environmental sensor with temperature, barometric pressure | |   &#10004; |
> | [Adafruit TCS34725 Color Sensor](http://www.adafruit.com/products/1334) | ARM, x32 | RGB Color Sensor with IR filter and white LED - TCS34725 | | &#10004; |
> | Rohm BH1750FVI ambient light sensor | ARM32 | Small I2C sensor for ambient light measurement | [I2C Samples](https://github.com/mickut/Win10-IoT-Sensors) | |
> | Bosch BMP180 temperature and barometric sensor | ARM, x32 | Bosch environmental sensor with tempreature, barometric pressure | [I2C Samples](https://github.com/mickut/Win10-IoT-Sensors) | |
> | Dorji DSTH01 relative humidity sensor | ARM32 | I2C relative humidity sensor | [I2C Samples](https://github.com/mickut/Win10-IoT-Sensors)| |
> | Honeywell HMC5883L digital 3-axis compass/magnetometer | ARM32 | A small 3-axis magnetometer for digital compass use and magnetic field measurements | [I2C Samples](https://github.com/mickut/Win10-IoT-Sensors) | |


### Port Expanders
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified  | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | MCP23008 8-bit I/O Port Expander | ARM32, x64, x86 | I2C Interface Chip, GPIO Port Expander. 8 ports, 18-PDIP package | [I2C Port Explander Sample](https://www.hackster.io/4803/i2c-port-expander-sample-0a6d4f) | &#10004; |
> | MCP23S17 16-bit I/O Port Expander | ARM32, x64, x86 | I2C Interface Chip, GPIO Port Expander. 16 ports, 28-SPDIP package | [Interactive Piano sample](https://www.hackster.io/windowsiot/build-2014-piano-3b449c) | &#10004; |

### NFC/RFID/Proximity
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|
> | NXP OM5577 demo board | ARM32 | Demo board for the NXP PN7120 NFC chip. | [ProximityDevice documentation](https://docs.microsoft.com/en-us/uwp/api/Windows.Networking.Proximity.ProximityDevice) | &#10004; |
> | NXP PN547/PN548/PN7120 | ARM32, x64, x86 | Supported NXP NFC chips. | | &#10004; |

### Miscellaneous
> | Part Name / No. | Compatible Architecture | Description | Relevant Links | Microsoft Verified | 
> |----------------|-------------------|-------------|--------|------------------------------|
> | Official Pi display | ARM32 | 7" 800x480 touch display. | [Raspberry Pi 7" Touch Screen](https://www.raspberrypi.org/products/raspberry-pi-touch-display/) | &#10004; |
> | Monochrome 1.3” 128x64 OLED graphic display |ARM, x32, x64, x86 | 1.3” diagonal, high contrast B/W OLED display. 128x64 individual white OLED pixels, each one is turned on or off by the controller chip. | [SPI Display Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/SPIDisplay) | &#10004; |
> | SN74HC595N Shift Register IC | ARM32, x64, x86 | IC 8-BIT SHIFT REGISTER 16-DIP | [Shift Register Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/ShiftRegister) | &#10004; |
> | Microchip Technology ADC MCP3002-I/P | AARM32, x64, x86 | MCP3002 10bit Analog to Digital converter. |  [Potentiometer Sensor Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/PotentiometerSensor) | &#10004; |
> | Microchip Technology ADC MCP3208-CI/P | ARM32, x64, x86 | MCP3208 12bit Analog to Digital converter. | [Potentiometer Sensor Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/PotentiometerSensor) | &#10004; |
> | ADS1115 | ARM, x32, x64, x86 | Ultra-small, low-power, 16-bit ADC | [ADC Bus Providers](https://github.com/ms-iot/BusProviders/tree/develop/ADC) | &#10004; |
> | CP2102 USB 2.0 to TTL Module Serial Converter | ARM32, x64, x86 | CP2102 USB 2.0 to TTL Module Serial Converter | [Serial Port Sample](https://github.com/Microsoft/Windows-iotcore-samples/tree/master/Samples/SerialUART) | &#10004; |
> | PCA9685 | ARM32, x64, x86 | 16-channel, 12-bit PWM Fm+ I2C-bus LED controller. | [PWM Bus Providers](https://github.com/ms-iot/BusProviders/tree/develop/PWM) | &#10004; |


