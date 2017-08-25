# Hardware compatibility list

Windows 10 IoT Core supports a variety of peripheral interfaces and protocols, including support for common busses like I2C, UART, USB, and more. This page lists known supported peripherals and is current as of the latest RTM release. Specific entries may only work on Insider releases and will be noted as such.

Browse, search, and filter, peripherals that are known to be supported on Windows 10 IoT Core devices. You can also contribute to this list on GitHub by clicking the “Contribute” links.

This list is not exhaustive. There are many other peripherals not listed on this page that are compatible with Windows 10 IoT Core. We encourage you to contribute to this list to improve this resource!

Looking for information about supported hardware platforms? Click [here](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/windows-compatible-hardware-development-boards) for a list of development boards compatible with Windows.

## USB Devices

### WiFi Dongles
> | Part Name / No. | Compatible Boards | Description | Projects, Samples, Libraries | Notes |Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|------------------------------------|
> | Official Raspberry Pi WiFi dongle | RPi2/RPi3 | The official Raspberry Pi WiFi dongle offers the best possible WiFi performance for its diminutive size." |  |  | 
> | Airlink Wireless N 150 Mini USB Adapter Adapter | MBM | Airlink 101 AWL5077 Golden 150Mbps Wireless Mini USB Adapter with WPA2, WPA, and WEP enhanced wireless security | | | |
> | Panda PAU06 | MBM |  Panda 300Mbps Wireless N USB Adapter with High Gain Antenna | | | |
> | TP-LINK TL_WN725N |  RPi2/RPi3, MBM | TP-LINK TL-WN725N Wireless N Nano USB Adapter 150 Mbps `(USB/VID_0BDA&PID_8179)` | | | |
> | NET-DYN USB WiFi Adapter | MBM | WiFi USB Adapter NET-DYN | | | |
> | Realtek 8191 USB Wireless WiFi | RPi2/RPi3, MBM | Realtek 8191 300Mbps 802.11n/g/b/ USB Wireless WiFi LAN Network Card Adapter | | | |
> | Realtek 8192 USB Wireless WiFi | RPi2/RPi3, MBM | Realtek Single-Chip IEEE 802.11b/g/n 2T2R WLAN Controller with USB 2.0 Interface | | | |
> | CanaKit USB Wireless WiFi | MBM | Chipset Ralink 5370 | Not supported on RPi2/RPi3; WiFi Direct supported on MBM | | |

### Bluetooth Dongles
> | Part Name / No. | Compatible Boards | Description | Projects, Samples, Libraries | Notes |Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|------------------------------------|
> | CSR Mini USB Blueooth V 4.0 Adapter | RPi2/RPi3, MBM | Class 2 Bluetooth 4.0 Smart Ready Adapter, low energy, dual power | | | |
> | ORICO BTA-403 Mini Bluetooth 4.0 USB Dongle | RPi2/RPi3, MBM | Low-energy Bluetooth 4.0 adapter USB Micro Adapter Dongle | | | |
> | CSR Mini USB Bluetooth V 4.0 Adapter | MBM | Class 2 Bluetooth 4.0 Smart Ready Adapter, low energy, dual power | | | |

### Cameras
> | Microsoft Lifecam 3000 USB Camera | RPi2/RPi3, MBM | USB Webcam | Limited to less than five frames per second, no known performance workarounds | [Home Security Camera Project](https://developer.microsoft.com/en-us/windows/iot/samples/webcamapp) | | 
> | Microsoft Lifecam HD-5000 | RPi2/RPi3, MBM | Microsoft LifeCam HD-5000 720p HD Webcam | USB 2.0 | | |
> | Microsoft® LifeCam Studio™ | RPi2/RPi3 | Microsoft® LifeCam Studio™ (model: 1425) 1080p HD Webcam | USB 2.0 (max. 30 frames per second) | | |
> | Logitech Webcam C210 | RPi2/RPi3, MBM | USB Webcam, 1.3mp photo | | | |

### Audio
> | Part Name / No. | Compatible Boards | Description | Projects, Samples, Libraries | Notes |Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|------------------------------------|
> | Sabrent USB External Stereo Sound Adapter, Model AU-EMAC1 | RPi2/RPi3, MBM | Converts USB to 3.5mm audio and microphone signals | Attaching an external USB sound card to RPi2/RPi3 will add an extra audio endpoint (playback device) to the already existing onboard PWM headphone jack. Since the default order of the audio devices cannot be guaranteed at reboot, it is recommended that applications enumerate the audio endpoints and ensure the correct one is used. | | |

### Miscellaneous
> | Part Name / No. | Compatible Boards | Description | Projects, Samples, Libraries | Notes |Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|------------------------------------|
> | Aeon Labs Z-Wave Z-Stick Series 2 USB Dongle DSA02203-ZWUS | RPi2/RPi3 | Series 2 Z-Wave USB Z-Stick Controller | Easy network creation with push button pairing | [ZWave Sample](https://developer.microsoft.com/en-us/windows/iot/samples/zwaveadapter) | |
> | Chalkboard Electronics 7” LCD Capacitive Touchscreen Display | RPi2/RPi3 | [Product Information](https://www.chalk-elec.com/?page_id=1280#!/7-black-frame-universal-HDMI-LCD-with-capacitive-multi-touch/p/21750201/category=3094861) | To get this working with Windows 10 IoT Core, do the following: 
1. Follow the Firmware Update instructions on chalk-elec.com 
2. Flash firmware version 7-bf-mt-v2-2.hex onto the touchscreen 
3. Hookup the HDMI and USB cables to the RPi2 or RPi3 
4. Power on the touchscreen first, then power on your RPi2 or RPi3 | [Updating firmware](https://www.chalk-elec.com/?p=1826) | | 
> | Vodafone (Huawei) K5150 | RPi2/RPi3, MBM | Vodafone (Huawei) K5150 150Mbps 4G LTE FDD USB Mobile Broadband Modem | | | | 
> | Sierra Wireless Beam (AirCard 340U) | MBM | 	Sierra Wireless Beam (AirCard 340U) 4G LTE USB Mobile Broadband Modem | | | |
> | Microsoft Xbox 360 Controller | RPi2/RPi3 | An HID-compliant USB gamepad for Microsoft's Xbox 360 | Access using [HidDevice](https://docs.microsoft.com/en-us/uwp/api/Windows.Devices.HumanInterfaceDevice.HidDevice) (not [Gamepad](https://docs.microsoft.com/en-us/uwp/api/Windows.Gaming.Input.Gamepad)) | Robot Kit | | 
> | [MyTeletouch](http://myteletouch.com/) | RPi2/RPi3 | An HID-compliant USB wireless mouse, keyboard and gamepad | Access using your phone (Iphone, Android, Windows) | |

## Other Hardware Peripherals

### Storage Media
> | Part Name / No. | Compatible Boards | Description | Projects, Samples, Libraries | Notes |Microsoft Verified |
> |----------------|-------------------|-------------|--------|------------------------------|------------------------------------|
