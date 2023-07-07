---

description: 'We''ll show you one of two ways to add a driver to the image.'
title: 'Lab 1e: Add a driver to an image'

ms.date: 10/15/2018
ms.topic: article


---

# Lab 1e: Add a driver to an image


In this lab, we'll add the sample driver - [Toaster](https://github.com/Microsoft/Windows-driver-samples/tree/6c1981b8504329521343ad00f32daa847fa6083a/general/toaster/toastDrv) - package it up, and deploy it to our device.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites/Requirements

Make sure you've created a basic image from  [Create a basic image](create-a-basic-image.md). 

You will need the following tools installed to complete this section:

* Windows Assessment and Deployment Kit (Windows ADK)
* IoT Core PowerShell Environment
* Windows 10 IoT Core Packages
* IoT Core ADK Add-Ons
* A text editor like Notepad or VS Code

## <span id="Check_for_similar_drivers"></span>Check for similar drivers

Before adding drivers, you may want to review your pre-built Board Support Package (BSP) to make sure there's not already a similar driver. 

For example, review the list of drivers in the file: `\\IoT-ADK-AddonKit\\Source-arm\\BSP\\Rpi2\\Packages\\RPi2FM.xml`

- If there's not an existing driver, you can usually just add one.

- If there is a driver, but it doesn't meet your needs, you'll need to replace the driver by creating a new BSP. We'll cover that in [Lab 2](create-a-new-bsp.md).

## <span id="Create_your_test_files"></span><span id="create_your_test_files"></span><span id="CREATE_YOUR_TEST_FILES"></span>Create your driver files

-  Complete the steps listed under the [Toaster Driver sample](https://github.com/Microsoft/Windows-driver-samples/tree/6c1981b8504329521343ad00f32daa847fa6083a/general/toaster/toastDrv) to build this sample. You'll create a file, wdfsimple.sys, which you'll use to install the driver.

You can also use your own IoT Core driver, as long as it doesn't conflict with the existing Board Support Package (BSP).

-  Copy the files, wdfsimple.sys and wdfsimple.inf, into a test folder, for example: `C:\wdfsimple\`

## <span id="Build_a_package_for_your_driver"></span><span id="build_a_package_for_your_driver"></span><span id="BUILD_A_PACKAGE_FOR_YOUR_DRIVER"></span>Build a package for your driver

Once the driver files are created, we need to create a package that includes them, and then add that package to our Windows IoT Core image.

1.  Run **IoT Core PowerShell Environment** as an administrator. Select your appropriate architecture.

2. Create a **driver package** using [New-IoTDriverPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTDriverPackage.md).

``` powershell
Add-IoTDriverPackage C:\wdfsimple\wdfsimple.inf Drivers.Toaster
(or) newdrvpkg C:\wdfsimple\wdfsimple.inf Drivers.Toaster
```

This creates a new folder at `C:\MyWorkspace\Source-<arch>\Packages\Drivers.Toaster`.

This also adds a FeatureID **DRIVERS_TOASTER** to the `C:\MyWorkspace\Source-<arch>\Packages\OEMFM.xml` file.

3.  Build the package using [New-IoTCabPackage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTCabPackage.md).

``` powershell
New-IoTCabPackage Drivers.Toaster
(or) buildpkg Drivers.Toaster
```

## <span id="Update_the_project_s_configuration_files"></span><span id="update_the_project_s_configuration_files"></span><span id="UPDATE_THE_PROJECT_S_CONFIGURATION_FILES"></span>Update the project's configuration files

Update the product test configuration file using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md).

``` powershell
Add-IoTProductFeature ProductB Test DRIVERS_TOASTER -OEM
(or) addfid ProductB Test DRIVERS_TOASTER -OEM
```

## <span id="Build_and_test_the_image"></span><span id="build_and_test_the_image"></span><span id="BUILD_AND_TEST_THE_IMAGE"></span>Build and test the image

Build the FFU image again, as specified in [Create a basic image](create-a-basic-image.md). You should only have to run the [New-IoTFFUImage](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/New-IoTFFUImage.md) command: 

``` powershell
New-IoTFFUImage ProductX Test
(or)buildimage ProductX Test 
```
## Verify driver is installed properly

You can verify that the test driver was installed properly by following the steps in the [Toaster Driver sample](https://github.com/Microsoft/Windows-driver-samples/tree/6c1981b8504329521343ad00f32daa847fa6083a/general/toaster/toastDrv) to test your driver.

Otherwise, if you used another test driver, you can follow these steps:

1. Boot up your Windows 10 IoT Core device and make note of its IP address.
2. On your technician PC, open **File Explorer** and in the address bar type in `\\<TARGET_DEVICE_IP>\c$` and press **Enter**. **TARGET_DEVICE_IP** will correspond to the IP address of you rdevice.

If you are prompted for credentials, please enter these and click OK. If you have not changed the default credentials use the following:

```
User ID: Administrator
Password: p@ssw0rd
```

3. Once your credentials are accepted and **File Explorer** displays the c$ directory of your device, navigate to `c:\Windows\System32\Drivers` and look for the **gpiokmdfdemo.sys** file. If present, this validates that your driver has been properly installed on your device.

## <span id="Next_steps"></span><span id="next_steps"></span><span id="NEXT_STEPS"></span>Next steps

[Lab 1f: Add Win32 services to an image](add-win32-services.md)
