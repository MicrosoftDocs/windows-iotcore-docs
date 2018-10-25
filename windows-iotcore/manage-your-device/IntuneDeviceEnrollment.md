---
title: Enroll Windows IoT Core Devices in Intune
author: msmimart
ms.author: mimart
ms.date: 05/08/2018
ms.topic: article
description: Learn about how to manage your devices using Microsoft Intune Device Management and Windows IoT.
keywords: windows iot, Azure IoT, Intune Device Management, device management
---
# Enrolling Windows IoT Core devices in Microsoft Intune

Your company can manage IoT Core devices alongside all of your other managed devices. This gives you a consistent way to manage IoT Core, IoT Enterprise, and other Windows devices using Intune.

## How do I enroll an IoT Core device into Intune?

Intune enrollment of an IoT Core device is accomplished by using the Windows IoT Core Dashboard to prepare the device, and then using Windows Configuration Designer to create a provisioning package.

### Change the Intune MDM user scope in Azure AD

1. Sign in to the [Azure portal](https://portal.azure.com), and then select **Azure Active Directory**.
2. Select **Mobility (MDM and MAM)**.


~~~
 ![Selecting Mobility and Microsoft Intune](../media/IntuneDeviceEnrollment/iot-ap-mobility-intune.png)
~~~
1. Select **Microsoft Intune**. On the **Configure Microsoft Intune** page, next to **MDM user scope**, select **All**. This will allow your IoT Core device user to be enrolled in Intune after joining Azure AD.

### Create a setup SD card for the IoT Core device
1. Insert a microSD card into the card reader on your PC. 
     > [!NOTE]
     > The microSD card will be formatted during this process, so any data on the card will be deleted.
2. Go to [Windows IoT Core Dashboard](https://docs.microsoft.com/en-us/windows/iot-core/connect-your-device/iotdashboard) to download and install the dashboard.
3. After the dashboard installs, open it and select **Set up a new device**.

     ![Windows IoT Core Dashboard](../media/IntuneDeviceEnrollment/IoT-dashboard-my-devices.png)

4. Type a **Device name**.
5. Enter a new administrator password. 
6. If you want to enable Wi-Fi for the device, select the **Wi-Fi Network Connection** checkbox. Skip this if the device will use an ethernet network connection only.

     ![Wi-Fi checkbox on the IoT dashboard](../media/IntuneDeviceEnrollment/IoT-dashboard-wifi-connection.png)

7. Select the **I accept the software license terms** checkbox, and then select **Download and Install**.
8. When the confirmation message appears, select the option to **Format** the SD Card. 
     > [!NOTE]
     > Watch for the **Format** confirmation message during setup. The message could be hidden by another open application, but it’s important to select the Format option. If the drive isn't properly formatted, boot will fail.
9. The message **Your SD card is ready** appears.

     ![SD card ready message](../media/IntuneDeviceEnrollment/IoT-dashboard-sd-card-ready.png)

10. Minimize this page.  You'll come back to it later.

### Create a provisioning package for Intune enrollment
1. Install the Windows Configuration Design app by following the steps in [Install Windows Configuration Designer](https://docs.microsoft.com/en-us/windows/configuration/provisioning-packages/provisioning-install-icd).

2. Open the **Windows Imaging and Configuration Designer**.
3. Choose **Provision desktop devices** to create a project 

     ![Choosing Provision desktop services](../media/IntuneDeviceEnrollment/iot-wcd-provision-desktop-devices.png)

4. Enter the **Project Details** as desired. Then select **Finish**.
5. Go to the **Account Management** page and select **Enroll in Azure AD**.
      > [!NOTE]
     > Installing the app from either the Microsoft Store or the Windows Assessment and Deployment Kit (ADK) is fine.

     ![Choosing Enroll in Azure AD](../media/IntuneDeviceEnrollment/iot-wcd-enroll-in-azure-ad.png)

6. Next to **Bulk Token Expiry**, enter a a bulk token expiry date.
7. Select **Get Bulk Token**. A sign-in message appears for connecting to Azure AD.

     ![Azure AD sign-in page](../media/IntuneDeviceEnrollment/iot-wcd-sign-in.png)

8. Enter your tenant username (for example, john@mycompany.onmicrosoft.com) and your password.   
9. Agree to allow the Windows Configuration Design app to access your Azure AD information. 
10. A message on the page shows that the Bulk AAD token was fetched successfully.

     ![Bulk token successful message](../media/IntuneDeviceEnrollment/iot-wcd-bulk-token-successful.png)

11. Select **Switch to advanced editor**, and then select *Yes*.

     ![Switch to advanced editor confirmation page](../media/IntuneDeviceEnrollment/iot-wcd-switch-to-advanced-editor.png)

12. Under **Selected customizations**, Leave the **Account** settings, but remove all other settings:
13. Select **OOBE**, and then select **Remove**.
14. If **SharedPC** is listed, select it, and then select **Remove**.

     ![Removing customizations](../media/IntuneDeviceEnrollment/iot-wcd-select-customizations.png)

15. Select **Export**, and then choose **Provisioning package**.

     ![Choosing Provisioning package](../media/IntuneDeviceEnrollment/iot-wcd-export-provisioning-package.png)

16. On the next page, accept the default settings and select **Next**.
17. Again, on the next page, accept the default settings and select Next.
18. Change the **Provisioning Package** destination or leave the default path, and then select **Next**.
19. Select **Build**.
20. Select the **Output Location** link so that you can locate the .ppkg file when it's ready.

     ![Output location links](../media/IntuneDeviceEnrollment/iot-wcd-all-done.png)

21. Select **Finish**.
22. Go to File Explorer and copy the provisioning package to your IoT Core device. Save it to the microSD card under the **MainOS** drive in the **c:\windows\provisioning\packages** folder.  You'll have to grant permissions to save the file in this folder.

### Provision and enroll the IoT Core device in Intune
1. Insert the microSD card into your IoT Core device.
2. Turn on your IoT Core device and allow time for it to start up and display the standard screen. 
3. Return to the Microsoft Intune console in the Azure portal. Your device should appear in the list of devices.
     > [!NOTE]
     > Enrollment could take 15 minutes or more to complete.

     ![Intune devices list](../media/IntuneDeviceEnrollment/iot-ap-devices-after-enrollment.png)

## Next steps
- [See device details in Intune](https://docs.microsoft.com/en-us/intune/device-inventory).
- [Sync the device to get the latest policies and actions with Intune](https://docs.microsoft.com/en-us/intune/device-sync).
- [Remotely restart the device with Intune](https://docs.microsoft.com/en-us/intune/device-restart).
