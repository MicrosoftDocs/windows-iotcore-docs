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
- [ ] Download / Build BSPs for board
- [ ] Select the correct Image Type (arm / x86 / x64)
- [ ] Create basic image
- [ ] Boot basic image 
### Drivers
- [ ] Add drivers for the Image (if required)
- [ ] Boot test image with drivers
### Custom Apps
- [ ] Add custom UWP app to image
- [ ] Test Image with custom app
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image
- [ ] Test Image with custom provisioning
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image
- [ ] Test Image with custom provisioning
### Test Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image
---
## Retail Image
### Retail Image
- [ ] Aquire retail code-signing EV certificate
- [ ] Aquire cross-signing certificate that match your CA of code-signing certificate
- [ ] Code Sign your custom UWP app
- [ ] Create and include Certificates package (if needed - adding more then one UWP app, drivers, etc)
- [ ] Turn on retailsign
- [ ] Create retail image
- [ ] Test retail Image
### Security
- [ ] Enable secure boot
- [ ] Enable TPM
- [ ] Enable BitLocker
- [ ] Enable UEFI Security
- [ ] Test secure retail image
### Retail Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image
---

## Testing Retail Image
