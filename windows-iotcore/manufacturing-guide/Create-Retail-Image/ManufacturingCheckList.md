---
title: Device Manufacturing Check List
author: lmaung
ms.author: lmaung
ms.date: 10/08/2018 
ms.topic: article 
description: Concepts check list for manufacturing guide.
keywords: Windows 10 IoT Core, 
---

# Device Manufacturing Check List

One of the ultimate goals for creating an IoT image for a device is so that you can have a eventually have a mass produced IoT device. The follwing is a list of check boxes and guides that you may want to complete before you send the device for mass production. Although it is a guide, you do not have to follow every single step in the guide for a device to be "manufacturing" ready. The manufacturing readiness is ultimately set by you and your needs alone.

---
We will split the tasks into multiple sections.

## Test Image
### Basic Image
- [ ] Download / Build BSPs for board [[link]](../Concepts-Terms-Basics/BoardSupportPackages.md)
- [ ] Select the correct Image Architecture [[link]](../Create-IoT-Image/CreateBasicImage.md)
- [ ] Create basic image [[link]](../Create-IoT-Image/CreateBasicImage.md)
- [ ] Flash basic image [[link]](../Create-IoT-Image/FlashingImage.md)
### Drivers
- [ ] Add drivers for the Image (if required) [[link]](../Customize-Image/AddingDrivers.md)
- [ ] Flash test image with drivers [[link]](../Create-IoT-Image/FlashingImage.md)
### Custom Apps
- [ ] Add custom UWP app to image [[link]](../Customize-Image/AddingApps.md)
- [ ] Test Image with custom app [[link]](../Create-IoT-Image/FlashingImage.md)
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image [[link]](../Customize-Image/CreateProvisioningPackage.md)
- [ ] Test Image with custom provisioning [[link]](../Create-IoT-Image/FlashingImage.md)
### Test Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image 
---
## Retail Image
### Retail Image
- [ ] Aquire retail code-signing EV certificate [[link]](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate) 
- [ ] Aquire cross-signing certificate that match your CA of code-signing certificate [[link]](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)
- [ ] Code Sign your custom UWP app [[link]](../Create-Retail-Image/CreateRetailImage.md)
- [ ] Create and include Certificates package (if needed - adding more then one UWP app, drivers, etc) [[link]](07-CreateRetailImage.md)
- [ ] Turn on security features (see section below)
- [ ] Turn on retailsign [[link]](../Create-Retail-Image/CreateRetailImage.md)
- [ ] Create retail image [[link]](../Create-Retail-Image/CreateRetailImage.md)
- [ ] Test retail Image (see below)
### Security
- [ ] Enable TPM
- [ ] Enable Secure Boot
- [ ] Enable UEFI Security
- [ ] Enable Device Guard
- [ ] Enable BitLocker
- [ ] Test secure retail image
### Retail Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image
