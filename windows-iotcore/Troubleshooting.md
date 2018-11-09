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

### ASUS Tinkerboard and Rockchip support

While the ASUS Tinkerboard and Rockchip are not officially supported by us, there are cases where Rockchip has worked with other third parties to get SoC working on Windows 10 IoT Core.

### Issue when connecting a MBM device when roaming

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

### Raspberry Pi 3B+

If you're looking to work with the Raspberry Pi 3B+, one of our outstanding MVPs, Jiong Shi, came up with this tutorial that you can find on Hackster.io [here](https://www.hackster.io/JiongShi/windows-10-iot-core-for-raspberry-pi-3-model-b-92b1a3).

Please keep in mind that for any device flashing, you will need to have Windows 10. Your SD card will need to be 8GB even though the Windows 10 IoT Core image is under 1 GB (so there's space to install additional content). 

If you're looking to remove the image from your SD card and restore the card back for general use, you'll need to run a series of commands in an elevate command prompt (simply reformatting the card alone won't work):

```
diskpart
list disk (this command lists the drives you have connected to your computer. Take note of the disk number of your SD card)
select disk <number> (Replace <number> with the disk number of your SD card from the previous step)
clean
create partition primary
format fs=ntfs quick
exit
```


### Yubikey support

Windows 10 IoT Core does not have smart card support. However, smart cards are usually devices used for user identity and not device identity because they are secured with PINs and, in the case of the Yubikey, a button to press. This does not harmonize with an IoT device. If you're looking for an alternative, a TPM 2.0 on the device may serve better than a Yubikey or smart card. We have full certificate support for TPMs and they are meant to store devices as well as user certificates and Azure IoT access credentials (Limpets).
