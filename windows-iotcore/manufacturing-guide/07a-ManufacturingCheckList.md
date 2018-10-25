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
A user can easily test the basic test image of IoT core just by turning on a device with the image flashed on the device. Once the device is running, you can run thru various checks to verify that the device is truly functional in all aspects. The ease of tests depends on levels of security factors baked into the image. On a basic test image, since there is no security protocols build in, you can use all development tools to test an IoT device. The task of testing becomes harder as all security protocols are baked into the device. Due to the nature of security protocols baked into the retail image, you may want to write a test application that can run on the IoT device that can  tests various areas and functions of the device. 

The testing can be done in a few ways. 
### Clean retail image test
If you truly want to have a clean image, you will need to create two (2) retail images. The two images will be indentical except for one feature. The testing retail image will have the test app that will be configured as a Fore-Ground-App and you can use that to test the various features. Once features are tested, you can use the second image (without test app) for distribution.
*Pros*: Final image will be totally clean and only the items that are deemed neccessary are baked into the image.
*Cons*: There are potential user error while adding a test app to the retail image. There are potential modifications made to provisioning package(s) that could be totally different from final retail image.

### One time only pass thru test
