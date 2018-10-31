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
- [ ] Download / Build BSPs for board [[link]](04a-BoardSupportPackages.md)
- [ ] Select the correct Image Architecture [[link]](04-CreateBasicImage.md)
- [ ] Create basic image [[link]](04-CreateBasicImage.md)
- [ ] Flash basic image [[link]](05-FlashingImage.md)
### Drivers
- [ ] Add drivers for the Image (if required) [[link]](06d-AddingDrivers.md)
- [ ] Flash test image with drivers [[link]](05-FlashingImage.md)
### Custom Apps
- [ ] Add custom UWP app to image [[link]](06a-AddingApps.md)
- [ ] Test Image with custom app [[link]](05-FlashingImage.md)
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image [[link]](06b-CreateProvisioningPackage.md)
- [ ] Test Image with custom provisioning [[link]](05-FlashingImage.md)
### Test Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image 
---
## Retail Image
### Retail Image
- [ ] Aquire retail code-signing EV certificate [[link]](https://docs.microsoft.com/en-us/windows-hardware/drivers/dashboard/get-a-code-signing-certificate) 
- [ ] Aquire cross-signing certificate that match your CA of code-signing certificate [[link]](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)
- [ ] Code Sign your custom UWP app [[link]](07-CreateRetailImage.md)
- [ ] Create and include Certificates package (if needed - adding more then one UWP app, drivers, etc) [[link]](07-CreateRetailImage.md)
- [ ] Turn on security features (see section below)
- [ ] Turn on retailsign [[link]](07-CreateRetailImage.md)
- [ ] Create retail image [[link]](07-CreateRetailImage.md)
- [ ] Test retail Image (see below)
### Security
- [ ] Enable TPM
- [ ] Enable Secure Boot
- [ ] Enable UEFI Security
- [ ] Enable Device Guard
- [ ] Enable BitLocker
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

**Pros**: Final image will be totally clean and only the items that are deemed necessary are baked into the image.

**Cons**: There are potential user error while adding a test app to the retail image. There are potential modifications made to provisioning package(s) that could be totally different from final retail image.

### One time only pass thru test
In the case of a one time only pass thru image, test app is written and included in final retail image. Once OOBE app is launched, test app is launched as FGA app. A conditional statement within the test app can be triggered so that the app is aware of the fact that it has ran before.

```CSharp
// Declare variable
Windows.Storage.ApplicationDataContainer localSettings = 
    Windows.Storage.ApplicationData.Current.LocalSettings;
    
// Set variable as boolean, numbers, or string values as needed at approperiate location within the test app
localSettings.Values["appRanOnce"] = false;    

// Read variable and verify value to check and apply logic
Object value = localSettings.Values["appRanOnce"];

```
> [!NOTE]
> For best result, only use `localSettings` to store the variables to store the settings values.
> There is a possible chance of undesirable results from using `roamingSettings` features.
> `localSettings` can only hold 64k of data at the time of this writing [[More on Application Settings]](https://docs.microsoft.com/en-us/windows/uwp/design/app-settings/store-and-retrieve-app-data)

Using the code block above, you can apply the logic on launch of the application so that on the subsequent launches, the application takes approperiate actions.

So what types of actions can I take?

- Launch another FGA app
- Edit the Registry to modify the boot sequence

#### Launching another FGA app from test app

If you are launching a Microsoft store app, you can use the following code snippit to launch apps installed and updated thru the store.
Additional information URI schemes can be found [here](https://docs.microsoft.com/en-us/windows/uwp/launch-resume/launch-store-app).

````CSharp
// Following will launch the Microsoft store app and navigate to the Games section
bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri
    ("ms-windows-store://navigatetopage/?Id=Games"));

// Following will launch the One Note app using the package family name (PFN)
bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri
    ("ms-windows-store://pdp/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe"));
`````

If you are launching a custom (non Microsoft store) app, you can use `AppServiceConnection` to launch an app using package family name (PFN). 


First, you must register the final app (com.concurrency.lwinsapp) with app services within the system. You will need to modify the `Package.appxmanifest` file to include the following code block in the `<Applications>` section of the manifest.
```Xaml
<Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="AppServiceProvider.App">
      <Extensions>
        <uap:Extension Category="windows.appService" EntryPoint="MyAppService.AppLaunchService">
          <uap3:AppService Name="com.concurrency.lwinsapp" uap4:SupportsMultipleInstances="true" />
        </uap:Extension>
      </Extensions>
      ...
</Application>
```

Following code segment will launch a custom application:

````CSharp
private AppServiceConnection appLaunchService;
...
this.appLaunchService = new AppServiceConnection();
this.appLaunchService.AppServiceName = "com.concurrency.lwinsapp";
this.appLaunchService.PackageFamilyName = "f3a114f7-e099-4773-8c93-77abcba14f62_004hcn5rxyy0y";
var status = await this.appLaunchService.OpenAsync();
````

By combining logic between `localSettings` and `AppServiceConnection`, you can by pass the test app on every boot of the device. In essance, the test app runs every boot but pass thru to the final app on boot. If needed, you can set your logic in such a way that device will not continue to final app if tests fails on the test app on every boot. This might be helpful if you need to verify that device is fully tested and functional on every boot.

**Pros**: You can test the device automatically on every boot to ensure that certain conditions are set correctly on every boot and the device is fully tested (and secure).

**Cons**: Your test app is included with the retail image. If you may have security holes in your app. Please make sure that your test app is locked down as needed. Due to the nature of the app, you app may be able to modify features of the device.

**What other options can I take?** If you do not want to launch the test app every time, you can create a console app and include it within the app in addition to the test app and run console app to take control of the registry and modify the registry to change the launch order of the app after the tests are successful. Please see [this](https://github.com/ms-iot/iot-utilities/tree/master/TakeRegistryOwnership) project to create a console app to modify the registry keys. You will need to modify these registry keys:
````
 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
 HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce
 HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
````
