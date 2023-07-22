---

description: 'Creating your own board support package (BSP)'
title: 'Lab 2: Creating your own board support package (BSP)'

ms.date: 10/15/2018
ms.topic: article


---

# Lab 2: Creating your own board support package (BSP)

A BSP includes a set of device drivers that are specific to the components/silicon used in the board. These are provided by the component vendors / silicon vendors, mostly in the form of .inf and associated .sys/.dll files.

Create a new Board Support Package (BSP) when:

- Creating a new hardware design

- Replacing a driver or component on an existing hardware design

Whether you're creating a new BSP or modifying an existing BSP, you become the owner. This lets you decide whether to allow updates to install on your boards.

In our lab, we'll create a new BSP based on the Raspberry Pi 2, removing the existing GPIO driver and replacing it with the sample GPIO driver: [GPIO KMDF demo](https://github.com/ms-iot/samples/tree/master/DriverSamples/gpiokmdfdemo).

## <span id="Create_a_new_BSP_working_folder"></span><span id="create_a_new_bsp_working_folder"></span><span id="CREATE_A_NEW_BSP_FILE"></span>Create a new BSP working folder

1. From the IoT Core Shell, create a BSP working folder that you'd like to modify using [Add-IoTBSP](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTBSP.md).

    ``` powershell
    Add-IoTBSP MyRPi2
    (or) newbsp MyRPi2
    ```

## <span id="Add_packages_into_the_feature_manifest"></span>Add packages into the feature manifest

1. Open the feature manifest file for your new BSP, `C:\MyWorkspace\Source-arm\BSP\MyRpi2\MyRpi2FM.xml`.

    In another window, open the Raspberry Pi 2 feature manifest to use as a template.

2. Add your base packages (BasePackages).

   - UEFI drivers for the boot partition (RASPBERRYPI.RPi2.BootFirmware.cab)

   - Drivers required for UpdateOS (SV.PlatExtensions.UpdateOS.cab)

   - Mandatory device drivers (bcm2836sdhc.cab, dwcUsbOtg.cab, rpiq.cab)

     When creating your own BSP, it's typical to require a display driver and a storage driver, and sometimes a network driver.

   - Device-specific customizations

3. Copy in the device layout and platform packages (DeviceLayoutPackages, OEMDevicePlatformPackages).

    Note that both the OEMDevicePlatform.xml and devicelayout.xml can be packaged into one package, for example, DeviceLayout.MBR4GB. The same package can then be specified as input in both the sections (for example, under `<OEMDevicePlatformPackages>` and `<DeviceLayoutPackages>`).  To learn more, see [Device layout](device-layout.md).

4. Copy in features (Features).

    Copy in features you want. Exclude any that don't apply to your project.

    For example, copy in each of the drivers **except** the existing GPIO driver:

    ``` xml
    <PackageFile Path="$(mspackageroot)\Retail\$(cputype)\$(buildtype)" Name="RASPBERRYPI.RPi2.GPIO.cab">
        <FeatureIDs>
          <FeatureID>RPI2_DRIVERS</FeatureID>
        </FeatureIDs>
    </PackageFile>
    ```

    Note: To make grouping packages easier, you can combine them into one or more Feature IDs. For example, all of the Raspberry Pi 2 optional drivers use the Feature ID: RPI2_DRIVERS.

5. Add the HelloBlinky driver

    ``` xml
        <PackageFile Path="%PKGBLD_DIR%" Name="%OEM_NAME%.Drivers.HelloBlinky.cab">
          <FeatureIDs>
            <FeatureID>BLINKY_DRIVER</FeatureID>
          </FeatureIDs>
        </PackageFile>
    ```

## <span id="Create_a_new_product_folder"></span><span id="create_a_new_product_and_folder"></span><span id="CREATE_A_NEW_PRODUCT_FOLDER"></span>Create a new product folder

1. Create a new working product folder, adding your BSP name to the end.

    ``` powershell
    newproduct ProductC MyRpi2
    ```

    This creates the folder: `C:\MyWorkspace\Source-<arch>\Products\ProductC`, which is linked to the new BSP.

## <span id="Update_the_project_s_configuration_files"></span><span id="update_the_project_s_configuration_files"></span><span id="UPDATE_THE_PROJECT_S_CONFIGURATION_FILES"></span>Update the project's configuration files

1.  Update the product test configuration file using [Add-IoTProductFeature](https://github.com/ms-iot/iot-adk-addonkit/blob/master/Tools/IoTCoreImaging/Docs/Add-IoTProductFeature.md)

    ``` powershell
    Add-IoTProductFeature ProductC Test BLINKY_DRIVER -OEM
    (or) addfid ProductC Test BLINKY_DRIVER -OEM
    ```

## <span id="Build_and_test_the_image"></span><span id="build_and_test_the_image"></span><span id="BUILD_AND_TEST_THE_IMAGE"></span>Build and test the image

### Build the image

1. From the IoT Core Shell, create the image:

    ``` powershell
    buildimage ProductC Test
    ```

    This creates the product binaries at `C:\MyWorkspace\Build\<arch>\ProductC\Flash.ffu`.

2. Start **Windows IoT Core Dashboard** &gt; **Setup a new device** &gt; **Custom**, and browse to your image.

    Put the Micro SD card in the device, select it, accept the license terms, and click **Install**. This replaces the previous image with our new image.

3. Put the card into the IoT device and start it up.

    After a short while, the device should start automatically, and you should see your app.

### Check to see if your driver works

1. Use the [testing procedures in the Hello, Blinky! lab](https://github.com/microsoft/Windows-iotcore-samples/tree/master/Samples/HelloBlinky) to test your driver.

## <span id="Related_topics"></span>Related topics

[Device layout](device-layout.md)

## <span id="Next_steps"></span><span id="next_steps"></span><span id="NEXT_STEPS"></span>Next steps

[Lab 3: Update apps](/windows-hardware/service/iot/updating-iot-core-apps)