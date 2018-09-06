---
title: Windows 10 IoT Core Services
author: saraclay
ms.author: saclayt
ms.date: 06/05/2018
ms.topic: article
description: Learn about Windows 10 IoT Core Services
keywords: Windows 10 IoT Core Services, subscription, overview
---

# Windows 10 IoT Core Services

Windows 10 IoT Core Services is a new cloud services subscription that provides the essential services needed to commercialize a device on Windows 10 IoT Core. Through this subscription, OEMs have access to 10 years of support on Windows 10 IoT Core Long Term Servicing Channel (LTSC) releases along with services to manage device updates and assess device health.

Earlier in the year, [we announced](https://blogs.windows.com/business/2018/02/27/microsoft-doubles-down-on-windows-10-iot-with-added-support/) that with the next release of Windows 10 IoT, we will provide 10 years of support for both Windows 10 IoT Core and Windows 10 IoT Enterprise. We also announced a partnership with NXP to support Windows 10 IoT Core on their i.MX 6 and i.MX 7 processors. The Windows 10 IoT Core Services offering builds on these announcements, as we continue to evolve the Windows IoT platform and make investments to support commercialization of devices running Windows 10 IoT.


## What's included with Windows 10 IoT Core Services?

A subscription to Windows 10 IoT Core Services comes with three main benefits:

> | _Benefit_  |  _Description_  |
> |----------|---------|
> | [10 years of support](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel) | Access to Windows 10 IoT Core LTSC releases with security and quality updates only (no new features). |
> | [Update control with Device Update Center](http://aka.ms/deviceupdatecenter) | Create and manage device updates at scale using cloud-side controls. |
> | [Device Health Attestation (DHA)](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/dha-architecture.md) | Rights to commercialize a device with DHA to affirm device health remotely. |

## 10 Years of Support
OEMs get 10 years of support on Windows 10 IoT Core via access to monthly updates from the [Windows Long-Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel) releases. This includes security and quality updates for the operating system to keep device security up to date. Devices using LTSC releases won’t receive feature updates, enabling OEMs to focus updates on stability by minimizing changes to the base operating system. Microsoft typically offers new LTSC releases every 2-3 years, with each release supported over a 10-year lifecycle.
## Update Control with Device Update Center

Update control with the newly announced [Device Update Center](http://aka.ms/deviceupdatecenter/) (DUC) provides the ability to create, customize, and control device updates. These updates are distributed by the same content distribution network (CDN) as Windows Update which is used daily by millions of Windows customers around the world. Updates can be applied to the operating system and device drivers as well as OEM-specific applications and files. Updates can be flighted to test devices prior to broader distribution.

Here's a diagram of the update flow in Device Update Center:

![Diagram of Device Update Center](../media/IoTCoreServices/IoTCoreServicesOverview-DUC.png)


## Commercialize with Device Health Attestation

[Device Health Attestation (DHA)](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/dha-architecture.md) enables enterprises and OEMs to raise the security bar of their organization's assets with hardware-attested security. Evaluating the trustworthiness of a device at boot time is essential for a trusted IoT system. However, a device cannot attest to its own trustworthiness - this must be done by an external entity such as the [DHA cloud service](https://docs.microsoft.com/windows-server/security/device-health-attestation). This service evaluates device health and can be combined with a device management system, such as Azure IoT Device Management. Based on DHA report data, the device management system can take corrective actions such as re-imaging the device, denying network access, or creating a service ticket.

## Is this for me?

If you work with IoT devices, you might be wondering if Windows 10 IoT Core Services is right for you or your organization. The answer depends on how you use and obtain Windows 10 IoT devices. The following information will help you decide whether this subscription service is right for you.
  1. If you are creating a device and you control the update and maintenance of the full software image on the device, this service is for you. If you only install apps on the device and someone else updates the full software image, such as the operating system and drivers, this service isn't for you. If you're not sure, contact your supplier and ask if they maintain the operating system, drivers, and other parts of the system image on the device or whether you are expected to maintain the system image. This service is designed for the party that maintains the system image for the device which is typically the ODM or OEM of the device, not the end customer purchasing or using the device.
  2. Your devices should be running Windows 10 IoT Core. If they are running Windows 10 IoT Enterprise, another version of Windows, or another operating system, this service isn't for you. Services such as [Azure IoT Device Management](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-device-management-overview) and [Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune) offer cross-platform support which may be useful ingredients in configuring alternate solutions for those operating systems.
  3. If you want to build a device with the [Long Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels) releases of Windows 10 IoT Core, this service is for you. You must subscribe to Windows 10 IoT Core Services to commercialize a device with an LTSC release of Windows 10 IoT Core. If you only want to run Semi-Annual Channel releases of Windows 10 IoT Core, you aren't required to subscribe to this service.
  4. If you want to use any one of the three services included in Windows 10 IoT Core Services on your devices, this service is for you. Even if you only need one of the three services included in the subscription, you need to purchase the subscription for your devices. The services are only sold together as a single product - they are not available for purchase separately.

## Getting started

Windows 10 IoT Core Services is currently available in preview through Azure at a discounted rate. If you already meet the prerequisites below and are familiar with creating resources in  Azure, you can skip straight to the [Windows 10 IoT Core Services](http://aka.ms/iotservice) page on Azure.com and the [Create blade in the Azure Portal](https://aka.ms/iotservicesubscribe) to get started. For more details on these steps, keep reading below.

### Prerequisites

  1. Create or use an existing [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/get-started-azure-ad) domain for registering with Windows Hardware Dev Center. You will need to sign in with an account with administrator rights to your AAD tenant domain to sign legal agreements during the registration process.
  2. You must have an [Extended Validation (EV) code signing certificate](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate). Please check whether your company already has an EV code signing certificate. If your company already has an EV code signing certificate, have the certificate available during the registration process. If your company doesn't have a certificate, you will need to purchase a certificate from an [authorized partner](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate#code-signing-faq) as part of the registration process.
  3. Register for a [Windows Hardware Dev Center account](http://aka.ms/ducregister) to get access to Device Update Center. Make sure you sign in as an administrator with the Azure Active Directory domain you will use for Device Update Center and have your Extended Validation (EV) code signing certificate available.

### Creating a new resource

After you've completed the prerequisites above, follow these steps when you are ready to create a resource for Windows 10 IoT Core Services with your Azure subscription.
1. Log into the [Azure Portal](https://portal.azure.com) with the AAD account you will use for purchasing the resource.
2. In the navigation pane on the left, click on Create a resource.
![Create a resource](../media/IoTCoreServices/IoTCoreServicesOverview-CreateAResource.png)
3. In the Search box, search for "IoT" and select "Windows 10 IoT Core Services" from the list.
4. Review in the information on the overview blade for Windows 10 IoT Core Services, including the Prerequisites information. When you're ready, click the Create button at the bottom of the overview blade.
5. On the Create blade, fill out the fields in the form. These fields can also be edited later in the resource properties.
   - **Name**: This is a friendly name for this instance of the Windows 10 IoT Core Services resource. This name is only used in the Azure Portal. Pick something that will help you distinguish this resource instance from others you might add to your Azure subscription. For example, consider a name that describes this group of devices such as "Industrial Extraction Monitor Device - Preproduction".
   - **Quantity**: Specify the number of devices to use with this resource. If you need to add more devices later, you can increase the quantity of devices using this resource or you can create a separate resource to track the additional devices. The minimum quantity is 10. If you have more than 500,000 devices, create separate resource instances with at most 500,000 devices per instance.
   - **Billing AAD domain name**: This corresponds to the Azure Active Directory domain name associated with the organization that is purchasing this resource. This field is automatically populated with the AAD domain of the user currently logged into the Azure Portal.
   - **Admin AAD domain name**: This corresponds to the Azure Active Directory domain name associated with the organization that logs into Device Update Center to manage the system image for the device. By default (or if left blank), this field is populated with the AAD domain of the user currently logged into the Azure Portal. However, it can be changed to a different AAD domain, if needed.
   - **Notes**: This is a free-form text field to attach your own custom notes to this resource instance. This optional field is only used in the Azure Portal to help you organize your resources.
   - **Subscription**: Specify the Azure subscription to use for purchasing this resource. For more details on which subscriptions are available in your account, see the Subscriptions section of the Azure Portal in the navigation pane on the left.
   - **Resource group**: Specify the Resource Group to use for organizing this resource. All resources in Azure are organized into [Resource Groups](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ResourceGroup). You can use an existing group or create a new resource group when creating this resource.
6. After filling out the fields above, click the Create button at the bottom of the form. This will start the deployment process to add a new instance of the Windows 10 IoT Core Services resource to your Azure subscription.
7. After the resource is successfully deployed, you can find it on the Dashboard or All Resources section of the Azure Portal. If the deployment fails, check the error message for details. Also verify that you've completed the Prerequisites above and specified the correct Admin AAD domain name for logging into Windows Hardware Dev Center.

### Updating a resource

After you've created a resource for Windows 10 IoT Core Services, you can update the resource by editing its properties in the Azure Portal.
1. Log into the [Azure Portal](https://portal.azure.com) with the AAD account you used when creating the resource.
2. Find the instance of the resource you want to change by selecting it in the Dashboard or All Resources section of the navigation pane in the Azure Portal.
3. On the Overview page of the resource properties, click the Edit button.
![Update a resource](../media/IoTCoreServices/IoTCoreServicesOverview-UpdateAResource.png)
4. Change the fields as needed and then click Save.

### Deleting a resource

When you no longer need the resource for Windows 10 IoT Core Services, you can delete the resource from your Azure subscription in the Azure Portal.
1. Log into the [Azure Portal](https://portal.azure.com) with the AAD account you used when creating the resource.
2. Find the instance of the resource you want to delete by selecting it in the Dashboard or All Resources section of the navigation pane in the Azure Portal.
3. On the Overview page of the resource properties, click the Delete button.
![Delete a resource](../media/IoTCoreServices/IoTCoreServicesOverview-DeleteAResource.png)

### Using Device Update Center

As a device manufacturer, you can maintain the security and reliability of your device by regularly updating the device image. This is accomplished by using Device Update Center to create and publish updates specific to your device model which will be offered by Windows Update when the device scans for applicable updates.
1. Before creating updates, start by creating a baseline image which is applied to the device during manufacturing as described in the [Build Your Image](https://docs.microsoft.com/windows/iot-core/build-your-image/createinstallpackage) section of the Windows IoT Core docs.
2. It's critical that you correctly [populate the SMBIOS fields](https://docs.microsoft.com/windows/iot-core/commercialize-your-device/oemlicenserequirements#smbios-support) of your device and that your build environment is set up with the [same corresponding values](https://docs.microsoft.com/en-us/windows-hardware/service/iot/using-device-update-center#step-2-create-a-new-product).
3. Ensure that you've registered for a [Windows Hardware Dev Center account](http://aka.ms/ducregister) to get access to Device Update Center. Make sure you sign in as an administrator with the Azure Active Directory domain you will use for Device Update Center and have your Extended Validation (EV) code signing certificate available.
4. Log into [Device Update Center](https://developer.microsoft.com/dashboard/hardware/iot) using the same AAD account you used when registering with Windows Hardware Dev Center. The AAD domain name on this account should also match the Admin AAD domain name specified when creating the resource in the Azure Portal.
5. Follow the instructions in the [Device Update Center User Guide](http://aka.ms/deviceupdatecenter) to create and publish updates for your device.

### Frequently Asked Questions (FAQs)

For a list of frequently-asked questions, see the [Pricing page](https://azure.microsoft.com/pricing/details/windows-10-iot-core/) for Windows 10 IoT Core Services on Azure.com.



