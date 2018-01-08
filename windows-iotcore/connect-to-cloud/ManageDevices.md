---
title: Manage your Windows devices with the Azure IoT Hub
author: saraclay
ms.author: saclayt
ms.date: 01/08/2018
ms.topic: article
description: Learn how to manage your Windows devices with the Azure IoT Hub.
keywords: windows iot, Azure, DM, device management, Azure IoT Hub, IoT Hub, device health
---

# Manage your Windows devices with the Azure IoT Hub

## Overview
Device Management (DM) allows operators to remotely configure and monitor very high volumes of IoT devices simultaneously.

Configuration for the devices can be pushed to devices, whether the target devices are online or offline. If the device is offline it will pick up the new configuration when it reconnects. Device operators can also retrieve the status of each device, including whether device configuration updates have been successfully applied or not.

Enabling these features for IoT devices requires a central, robust, and reliable mechanism to store and to deploy the configuration data to the target devices, and monitor device status - at scale.

A complete solution requires the following:

* A Robust/Scalable Cloud Service to store the desired and reported states of the various devices.
  * Azure IoT Hub and Azure Device Management offer a highly scalable and efficient cloud service for managing millions of devices.

* A Client that runs on the device and can apply the desired configuration and report the state of the device.
  * The Windows IoT Azure DM Client (an open source SDK + runtime), in conjunction with Azure IoT Hub, can apply and report on a large set of common, sometimes critical, Windows configurations.

* A Portal or an Application that will be used by the operator to configure and query the devices remotely.
  * This must be customized for devices by the device OEM or operator. As part of this solution, we also provide an open source data model and implementation for easier interaction with the IoT Hub storage and the Windows IoT client.

The links provided below will point to resources in the main [Device Management Client repo])https://github.com/ms-iot/iot-core-azure-dm-client/tree/develop) that will help you in managing your Windows devices.

1. [Overview of the Device Management Client for Windows IoT Core](https://github.com/ms-iot/iot-core-azure-dm-client/tree/develop)
2. [Overview of Device Health Attestation](https://github.com/ms-iot/iot-core-azure-dm-client/blob/develop/docs/device-health-attestation.md)
3. [Device Health Attestation Architecture](https://github.com/ms-iot/iot-core-azure-dm-client/blob/develop/docs/dha-architecture.md)
