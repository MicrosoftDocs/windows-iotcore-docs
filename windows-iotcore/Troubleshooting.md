---
author: saraclay
Description: 'Troubleshooting different commercialization-related issues.'
title: 'Troubleshooting'
ms.author: saclayt
ms.date: 08/28/18
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-oem
---

# Troubleshooting
This is an article that contains common troubleshooting issues that people have come across. To find something specific, use Ctrl+F to find a word or phrase. Have any insight you want to add? Create a PR for this documentation or provident content feedback below.

> [!NOTE]
> This documentation is a work in progress. 

## ASUS Tinkerboard and Rockchip support

While the ASUS Tinkerboard and Rockchip are not officially supported by us, there are cases where Rockchip has worked with other third parties to get SoC working on Windows 10 IoT Core.

## Issue when connecting a MBM device when roaming

There are two things to consider when enabling roaming:

1. The profile.xml configures roaming and sets the behavior to automatically establish a connection to the cellular network.
To set a profile for roaming please refer to [this article](https://docs.microsoft.com/windows/desktop/mbn/schema-root).

```
  <!-- applicability to any combination of home carrier, partner MOs and non-partner MOs, except for HomeAndNonPartner -->
  <xs:simpleType name="roamApplicabilityType">
    <xs:restriction base="xs:token">
       <xs:enumeration value="NonPartnerOnly"/>
       <xs:enumeration value="PartnerOnly"/>
       <xs:enumeration value="HomeOnly"/>
       <xs:enumeration value="HomeAndPartner"/>
       <xs:enumeration value="PartnerAndNonpartner"/>
       <xs:enumeration value="AllRoaming"/>
    </xs:restriction>
  </xs:simpleType>
  
  <xs:simpleType name="roamControlType">
    <xs:restriction base="xs:token">
       <xs:enumeration value="AllRoamAllowed"/>
       <xs:enumeration value="PartnerRoamAllowed"/>
       <xs:enumeration value="NoRoamAllowed"/>
    </xs:restriction>
  </xs:simpleType>
``` 

To set a profile for automatic connection, select "auto":

```  
<!-- Connection Mode, default is "manual" -->
    <xs:element name="ConnectionMode" minOccurs="0">
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <!-- manual connect always -->
          <xs:enumeration value="manual" />
          <!-- auto connect always -->
          <xs:enumeration value="auto" />
          <!-- auto connect when not roaming -->
          <xs:enumeration value="auto-home"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:element>
```

2. Another factor is that the per-interface roaming policy must be satisfied. By default, that policy is set to FALSE ("home carrier only"). This can be queried and changed in command line via `netsh mbn get/set dataroamcontrol.`

Example:

```
    netsh mbn show dataroamcontrol int=*
    netsh mbn set dataroamcontrol interface=Cellular profileset=all state=all
    netsh mbn set dataroamcontrol help
```

You may get error **0x139f (ERROR_INVALID_STATE)** in the case when the device is roaming but the roaming policy disallows data roaming - error on a connect request sent to wwansvc.

## Raspberry Pi 3B+ booting issues

The Raspberry Pi 3 Model B+ is the latest product in the Raspberry Pi 3 range, boasting a 64-bit quad core processor running at 1.4GHz, dual-band 2.4GHz and 5GHz wireless LAN, Bluetooth 4.2/BLE, faster Ethernet, and PoE capability via a separate PoE HA.

Recently, many customers who are interested in Windows 10 IoT Core encountered a problem where the device could not boot normally after flushing Windows 10 IoT Core, but the Raspbian works fine on it. The following are some suggestions on how to troubleshoot the boot problem.

1.The RPi 3B+ was announced in March this year (2018), but Microsoft had not announced that Windows 10 IoT Core fully supports RPi 3B+. The Insider preview image can be downloaded from [this link](https://www.microsoft.com/en-us/software-download/windowsiot). Currently there is no timeline for the 3B+ release version.

2. There are some known issues in this Insider Preview image. Please note that:
* This image is only meant for the Raspberry Pi 3B+ and will not boot on the Raspbierry Pi 2.
* F5 driver deployment from Visual Studio does not work on Windows 10 IoT Core.
* Onboard Wi-Fi and Bluetooth do not work on the Raspberry Pi 3B+.
* Ft5406 touch screen driver is disabled on the Raspberry Pi 3B+.
* SD card activity LED is disabled.

3. There are only two requirements when choosing which SD cards to use with Windows 10 IoT Core. You need to use a class 10 SD card and make sure the card has enough space - at least 8 GB of space. There are a couple of SD cards that have been verified by Microsoft to be compatible with Windows 10 IoT Core:
* Samsung EVO 32 GB class 10 Micros SDHC card
* SanDisk Ultra Micro SDHC, 16 GB card

Generally, you need to check if the SD card is fake or if it is damaged or corrupt. The SD card is equally prone to corruption due to a variety of factors such as power shortage or improper removal. It is important to safeguard your memroy card from damage.

4. To flash your image to a SD card, you can use the [Windows 10 IoT Core Dashboard](https://docs.microsoft.com/en-us/windows/iot-core/connect-your-device/iotdashboard). You will need to choose "Custom" in the OS Build field, then select the FFU file to flash. 

5. Check to see if there are any hardware failure in the device. There are two LEDs on the Raspberry Pi 3B+ board, same as the 3B. One is for PWR while another is for ACT. The number of blinks the ACT light makes will determine whether or not your board is booting. The SD card activity LED will not flash during some portions of booting on the Raspberry Pi 3B+.

6. When the device is booting and the device shows the waiting page, please wait patiently. Generally, this will last up to a minute. But sometimes, due to the SD card read-write speed, it may take longer.

7. If the device can't boot normally with Windows 10 IoT Core, you can try to flash a Linux OS (such as Raspbian) to the SD card to narrow down whether the issue is caused by hardware. 


## Yubikey support

Windows 10 IoT Core does not have smart card support. However, smart cards are usually devices used for user identity and not device identity because they are secured with PINs and, in the case of the Yubikey, a button to press. This does not harmonize with an IoT device. If you're looking for an alternative, a TPM 2.0 on the device may serve better than a Yubikey or smart card. We have full certificate support for TPMs and they are meant to store devices as well as user certificates and Azure IoT access credentials (Limpets).
