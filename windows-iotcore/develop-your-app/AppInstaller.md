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
You can install your app using one of the two methods that are listed below.

> [!NOTE]
> Installing apps using the Windows Device Portal is only for developer scenarios.
> Please create a provisioning package or add the app to your Windows IoT Core image for production scenarios.

## Using Windows Device Portal

> [!NOTE]
> An .appx or .appxbundle is required for Windows Device Portal. Beginning with version 17763 of the SDK and tools if the minimum target version of the app project> is 17763 or greater the tools will create an [.msix or .msixbundle](https://developercommunity.visualstudio.com/content/problem/391934/makeappx-now-creates-msix-files-instead-of-appx.html).
> To create an .appx or .appxbundle set the minimum version to a version less than 17763 or
> [run makeappx.exe directly](https://docs.microsoft.com/windows/desktop/appxpkg/make-appx-package--makeappx-exe-#command-line-syntax). It may also be possible to rename the .msix to .appx, or .msixbundle to .appxbundle.

For this method, you will need to ensure that you are connected to the internet. If you do not have access to the internet, you can also have a peer-to-peer ethernet connection between the device and a client machine that doesn't include a path to access the open internet. However, going about the latter way will install the app but will fail to launch if the app is store-signed.

To install your application on the device please do the following:

1. Open the [Windows Device Portal](https://docs.microsoft.com/windows/iot-core/manage-your-device/deviceportal) for your IoT device.

2. In the **Apps** menu, install your app by selecting your app files and clicking **Install**.

3. Click **Select File**

4. Select your .appx file and click **Open**

5. Check **Allow me to select framework packages**

6. Click **Next**

7. For each item in the **Dependencies** folder for your .appx repeat step 7.1 and 7.2

    7.1 Click **Choose File**

    7.2 Select the depenency .appx and click **Open**

8. When all of the dependencies are added click **Install**

9. Wait for the install is completed and click **Done**

 ![Install App](../media/AppInstaller/install-app.gif)

10. The application will now be visible on the list of applications on your device.
 ![Install App](../media/AppInstaller/install-app.gif)


## Using provisioning package from WCD
You can create a provisioning package with the app and install the provisioning package on the device. This method works even on devices that do not have internet connection, and is the preferred method for installing the store license file. For example, this enables factory scenarios where the device is not connected to the internet but the primary app is a store-signed UWP app.

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


## Add the app to the Windows IoT Core image(.ffu)
You can add the app to be part of the Windows IoT Core image itself.
This is the preferred method for OEMs to install apps on their devices.

See how to [add an app to your image](https://docs.microsoft.com/windows-hardware/manufacture/iot/deploy-your-app-with-a-standard-board) and a [sample app package](https://github.com/ms-iot/iot-adk-addonkit/tree/master/Workspace/Source-arm/Packages/Appx.IoTCoreDefaultApp).
