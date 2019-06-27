---
title: Azure IoT Device Agent
author: rcheeran
ms.author: rcheeran
ms.date: 06/25/2019
ms.topic: article
description: Learn about how to manage your devices using Azure IoT Device Agent on Windows IoT.
keywords: windows iot, Azure IoT, Azure Device Agent, device management, remote management
---

# Azure IoT Device Agent

When it comes to connected devices, remote device management is one of the key features used by system operators. It enables operators to reconfigure and update software and parameters of the device remotely without the need to have local, physical access to the device. With Windows 10 IoT Core, OEMs can build devices that offer these capabilities out-of-the box. Windows 10 IoT Core, as well as other Windows 10 versions, already offers Mobile Device Management (MDM) based on [OMA DM](https://en.wikipedia.org/wiki/OMA_Device_Management). This is mainly utilized in enterprise solutions with management tools such as SCCM or Intune. While those solutions are well suited for devices placed in an enterprise setting, it has challenges in the more diverse settings that we see in IoT solutions. Those challenges are also seen in IoT devices requiring light weight device management. For those devices, Microsoft offers [device management through Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-overview).

## Scalable device management with Windows IoT

With Windows IoT Core running in devices such as home appliances, HVAC systems and others, there is a need for a customizable, light weight device management solution. OEMs can use the [Azure IoT Device Agent](https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/device-agent.md) to add device management capabilities to their Azure IoT Hub connected devices. This ready-to-build open-source package that enable remote device management capabilities by accessing the standard Windows device management components ([Configuration Service Providers](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference), CSP).  OEMs can now build devices that support SCCM, Intune and Azure IoT Hub for device management and leave it up to their customers to select the device management solution that fits them best. 

![Azure IoT Hub Device Management](../media/AzureIoTDM/azureDM.png)


## How does it work?

![Azure IoT Device Agent](https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/high-level-e2e.png)
The [Azure IoT Device Agent](https://aka.ms/iot-core-azure-dm-client) consists of 2 core components. 
The Device Provisioning Client(DPS) automates device provisioning. It connects to the Azure Device Provisioning Service with the device's Enrollment Key and DPS ScopeID. The Azure DPS service identifies the device and provisions it in the configured IoT Hub and returns a connection string back to the device. The DPS client then uses this connection string to connect the device to the right IoT Hub.  

The Device Management Client enables remote management capabilities by leveraging the capabilities made available via the ([Configuration Service Providers](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference), CSP) The Azure Device Agent's remote management capabilities are built on a plug-in architecture allowing you to selectively choose capabilities that you want to include in your device. In addition to that, the plug-in architecture is extendable. You can write your own plug-in for a device management capability that you need and add it to the Azure Device Agent. All the device management capabilities are remotely accessible using the Device Twin or Module Twin properties and commands, thereby enabling a single-pane-of-glass management approach for all your Windows IoT devices deployed. For a complete list of device management capabilities available refer to [this](https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/reference.md)

In addition to this, the Azure Device Agent also creates and manages SAS tokens for other UWP applications running on the device. The Azure Device Agent can provision other UWP apps as either a Device Twin or as a Module Twin and add their connection strings to the respective TPM slots. The UWP app leverages the [UWP Bridge] (https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/uwp-bridge.md) to read their connection string from the TPM slot and can use that to connect to the IoT Hub. 

## How to get started?

The Azure IoT Device Agent is available on GitHub. The project it also includes samples to get started quickly. For more information see the links below.

### Project GitHub page

[Azure IoT Device Agent](https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/device-agent.md) is available on GitHub.

## Migrating from Azure Device Agent V1 to V2
If you are currently using the v1 version of the Device Agent, one significant change between V1 and V2 is that in the V2 version, the Azure Device Agent no longer shares the connection with an UWP app. With enhancements to the IoT Hub you can now have both the UWP app and the Azure Device Agent have independent connection strings and still be associated with the same device in IoT Hub. Refer [here](https://github.com/ms-iot/azure-client-tools/blob/master/docs/device-agent/migration-from-old-client.md) for more details.
For more information on the Azure Device Agent V1, refer [here](https://docs.microsoft.com/en-us/windows/iot-core/manage-your-device/azureiotdm)

## Other Useful Tools 
### DM Dashboard
[DM Dashboard](https://aka.ms/iot-core-azure-dm-client-dashboard) is an application to test the DM function on a device. The app connects to the device via Azure IoT Hub. The app can be used to validate the DM capabilities of the device. It can be extended to test any third-party DM functions that were added to the Azure Device Agent.

### TPM Tool - Limpet.exe
The Azure Device Provisioning Service allows customers to automatically associate and configure a device with an IoT Hub post-production. For this process Device Provisioning Service will need a unique and challengeable device ID to help configure the device securely when the device is put in operation. Device Provisioning Service uses the TPM’s public Endorsement Key (EKeyPub) for this purpose. To register the device with DPS, the EKeyPub needs to be harvested from the device. The preferred time for this step is during production (during end-of-line testing of the device). However, the process can also be done post-production if needed.  

Microsoft provides the Limpet tool to streamline the Device Provisioning Service registration process. Depending on your manufacturing setup, if there is an online connection available, the device can be registered using Limpet directly with Device Provisioning Service, or Limpet can harvest the EKeyPub for a later, offline registration of the device with Device Provisioning Service.

For more details on the Device Provisioning Service registration process with Limpet, see the [Enroll the device in Device Provisioning Service](https://github.com/ms-iot/azure-dm-client/blob/master/docs/limpet.md#setup-azure-cloud-resources)  section in the [Limpet documentation](https://github.com/ms-iot/azure-dm-client/blob/master/docs/limpet.md). 

Project repository: [Limpet project repository] (https://github.com/ms-iot/azure-dm-client/) 

License: Limpet is licensed under the MIT open source license 

## Device Health Attestation
For a secure operation of IoT devices it is essential to assess if a device is booted to a trusted and compliant state. With [Windows IoT Device Health Attestation (DHA)](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/device-health-attestation.md) operators can verify the secure state of a device, and take appropriate remedial actions if necessary through [Azure IoT Hub Device Management](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/README.md). DHA is part of the Windows IoT Core Azure Device Management Client. To use the DHA capability in your solution it requires access to the Microsoft DHA service. A subscription to the service is available through the [Windows 10 IoT Core Services](https://docs.microsoft.com/windows-hardware/manufacture/iot/iotcoreservicesoverview).

### Reference
[Device Health Attestation for Azure IoT DM](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/device-health-attestation.md)

[Deploy Azure Resources for Device Health Attestation](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/dha-deploy.md#deploy-azure-resources-for-device-health-attestation)








### More about the Azure Device Provision Service (DPS) 


  
  

