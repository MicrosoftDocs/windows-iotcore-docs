---
title: Managing Windows IoT Core Devices
author: parameshbabu
ms.author: pabab
ms.date: 04/03/2023
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn about the different ways to manage Windows 10 IoT Core devices, such as using a traditional OMA DM MDM server that supports certificate-based enrollment.
keywords: windows iot, device management, windows iot, Azure DM, Azure Hub, Azure IoT
---

# Managing Windows IoT Core Devices

Windows 10 IoT Core devices can be managed using a traditional OMA DM MDM server that supports certificate-based enrollment or using Azure IoT Hub's Device Management.  

 *Learn more about MDM and Windows 10 [here](/windows/client-management/mdm/).*

For devices that are managed using an OMA DM server the MDM policies for Windows 10 IoT Core align with the policies supported in other editions of Windows 10. To learn more about policies as well as what can be managed on IoT Core devices, see Configuration service provider reference for Windows 10 [here](/windows/client-management/mdm/configuration-service-provider-reference). The MDM support in Windows 10 is based on Open Mobile Alliance (OMA) Device Management (DM) protocol 1.2.1 specification.

## How do I enroll an IoT Core device into a MDM?

MDM enrollment of an IoT Core device is accomplished using a Provisioning package. Provisioning packages can be created using Windows Image Configuration and Designer (WICD). Let's try enrolling a device into a MDM.

### Creating a Provisioning package

#### Microsoft System Center Configuration Manager (Standalone or SCCM+Intune Hybrid)

1. Open the Configuration Manager Management Console (ConfigMgr Console)

1. Navigate to *Assets and Compliance > Compliance Settings > Company Resource Access > Certificate Profiles*
   ![Certificate Profiles](../media/ManagingDevices/ConfigMgr-Certificate-Profiles.PNG)

1. Click **Create Certificate Profile**

1. Provide a name and description for the profile
   - Name: ConfigMgr Example Trusted Root Certificate
     - Type of certificate profile: Trusted CA certificate  
     ![Trusted certification](../media/ManagingDevices/ConfigMgr-Certificate-Profiles-Wizard.png)

1. Click **Next**.

1. Import the certificate file.

1. Select **Computer certificate store - Root** for the **Destination Store**.

1. Click **Next**.

1. Choose **Select all** for Supported Platforms
   ![Supported platforms](../media/ManagingDevices/ConfigMgr-Certificate-Profiles-Wizard-Supported-Platforms.png)

1. Click **Summary, Next, and Close** to exit the wizard.

1. Right-click on the profile just created and click **Export**.

1. Click **Browse**, find a location where the .ppkg file should be exported, and then click **Save**.

1. Click **Export** and click **OK** to exit the wizard.

#### Other MDM Servers

1. Download and install the [Windows Assessment and Deployment Kit (Windows ADK)](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit).

1. Open Windows Imaging and Configuration Designer (WICD).
   ![Windows Imaging and Configuration Designer](../media/ManagingDevices/WICD-Start-Page.png)

1. Choose **Advanced Provisioning**

1. Set a name for your package.

1. Choose settings common to Windows 10 IoT Core.

1. Skip the Import Package step.
   ![WICD-New-Project-Details](../media/ManagingDevices/WICD-Advanced-Provisioning-New-Project-Details.PNG)
   ![WICD-New-Project-Editions](../media/ManagingDevices/WICD-Advanced-Provisioning-New-Project-Editions.PNG)
   ![WICD-New-Project-Import](../media/ManagingDevices/WICD-Advanced-Provisioning-New-Project-Import.PNG)

1. Navigate to Workplace -> Enrollments.

1. In the UPN field, enter the account you wish to enroll your device under (i.e. trmck@contoso.co) and click **Add**.

   ![Workplace enrollments filled](../media/ManagingDevices/WICD-Workplace-Enrollments-UPN-Filled.png)

1. For AuthPolicy choose between Username Password based authentication (OnPremises) or Certificate-based authentication.

1. Enter the Discovery Service URL for your MDM server.

    > [!NOTE]
    > Enrollment Service URL and Policy Service URL are optional.

1. For the Secret enter  
    - OnPremises: The password for the account you're enrolling with  
    - Certificate: The thumbprint of the certificate

    ![Filled OnPremise](../media/ManagingDevices/WICD-Workplace-Enrollments-UPN-Details-Filled-Premise.png)  

1. At the top of WICD window click **Export > Provisioning package**.

1. Provide a name and version for your package and click **Next**.

    > [!NOTE]
    > Be sure to increment the version number to ensure an updated package is executed.

1. Click **Next** on the **security details page**.

1. Choose the location where the package is to be exported on the local machine and click **Next**.

1. Click **Build** and then **Finish** to exit the wizard.

### Installing the Provisioning package

There are a few ways in which a Provisioning package can be deployed to an IoT device. It is possible to deploy a package by copying the package to the device or adding the package to the image during the imaging process.

#### Copying package to device

Take the Provisioning package that was exported from SCCM or WICD and copy the .ppkg file to `C:\Windows\Provisioning\Packages` directory on the IoT device. Upon reboot of the device, the package will be executed and the device will start the enrollment process.

#### Adding package to image

See [Add a provisioning package to an image](/windows-hardware/manufacture/iot/add-a-provisioning-package-to-an-image). Upon first boot, the device will execute the package and start the enrollment process.
