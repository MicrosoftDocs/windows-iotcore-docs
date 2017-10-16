---
title: Install your app on an IoT Core device
author: parameshbabu
ms.author: pabab
ms.date: 08/28/2017
ms.topic: article
description: Learn how to install your app using the Windows Device Portal or as part of the IoT core image.
keywords: windows iot, app installation, Windows Device Portal, devices
---

# Install your app on an IoT Core device
You can install your app by various methods and they are listed below.

## Using Windows Device Portal
To install your application on the device please do the following:

1. Open the [Windows Device Portal](https://docs.microsoft.com/windows/iot-core/manage-your-device/deviceportal) for your IoT device.

2. In the *Apps* menu add your UWP App Package, certificate and dependency App Packages(s).
 ![Install App](../media/AppInstaller/InstallApp.png)

3. Deploy the app.

4. The application will now be visible on the list of applications on your device.
 ![App List](../media/AppInstaller/AppList.png)

## Using provisioning package from WCD
You can create a provisioning package with the app and install the provisioning package on the device.

> [!NOTE]
> The Package Family Name (PFN) can be found in the Windows Dev Center under **App Management > App Identity**

1. Open [Windows Configuration Designer (WICD)](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-install-icd)

2. Select **Advanced Provisioning**, Enter the project name and a description

3. Choose Windows 10 IoT Core for the project settings and skip the provisioning package import

4. On the left hand side expand **Runtime Settings** and click on **Universal App Install > User Context App**

5. Enter the Package Family Name of your app and click **Add**

6. Under the newly added PFN
    - add the Appx and its dependencies
    - set the DeploymentOptions to "Force target application shutdown"

7. For Store signed apps, you will need to specify the license. Under UserContextAppLicense,
    - add LicenseProductID (available as LicenseID in the license XML file)
    - change the license xml extension to *.ms-windows-store-license*.
    - select your License Product ID on the left hand side and browse your license file to assign LicenseInstall field

8. For non-store signed apps, you will need to add the app.cer file under **Certificates > RootCertificates** 

9. Export the package

10. Copy the exported .ppkg file to _C:\Windows\Provisioning\Packages_ on the IoT device using [SSH](../connect-your-device/SSH.md) or [Powershell](../connect-your-device/powershell.md)) and reboot. When the device reboots, the provisioning package is processed and the app is installed.


## Add to the IoT core image(.ffu)   
You can add the app to be part of the IoT Core image itself. This is the widely used mechanism for OEMs. 

See how to [add an app to your image](https://docs.microsoft.com/windows-hardware/manufacture/iot/deploy-your-app-with-a-standard-board) and a [sample app package](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Source-arm/Packages/Appx.IoTCoreDefaultApp).
