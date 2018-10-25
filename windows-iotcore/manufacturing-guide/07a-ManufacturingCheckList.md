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
- [ ] Download / Build BSPs for board
- [ ] Select the correct Image Type (arm / x86 / x64)
- [ ] Create basic image
- [ ] Boot basic image 
### Drivers
- [ ] Add drivers for the Image (if required)
- [ ] Boot test image with drivers
### Custom Apps
- [ ] Add custom UWP app to image
- [ ] Test Image with custom app
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image
- [ ] Test Image with custom provisioning
### Boot Sequence / Registry / Custom Provisioning
- [ ] Create / Modify provisioning package for the image
- [ ] Test Image with custom provisioning
### Test Image Recovery
- [ ] Create recovery image
- [ ] Flash recovery image
- [ ] Test recovery image
---
## Retail Image
### Retail Image
- [ ] Aquire retail code-signing EV certificate
- [ ] Aquire cross-signing certificate that match your CA of code-signing certificate
- [ ] Code Sign your custom UWP app
- [ ] Create and include Certificates package (if needed - adding more then one UWP app, drivers, etc)
- [ ] Turn on retailsign
- [ ] Create retail image
- [ ] Test retail Image
### Security
- [ ] Enable secure boot
- [ ] Enable TPM
- [ ] Enable BitLocker
- [ ] Enable UEFI Security
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

**Pros**: Final image will be totally clean and only the items that are deemed neccessary are baked into the image.

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

Using the code block above, you can apply the logic on launch of the application so that on the subsequent launches, the application takes approperiate actions.

So what types of actions can I take?

- Launch another FGA app
- Edit the Registry to modify the boot sequence

*** Launching another FGA app from test app

If you are launching a Microsoft store app, you can use the following code snippit to launch apps installed and updated thru the store.
Additional information URI schemes can be found here[https://docs.microsoft.com/en-us/windows/uwp/launch-resume/launch-store-app].

````CSharp
// Following will launch the Microsoft store app and navigate to the Games section
bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-windows-store://navigatetopage/?Id=Games"));

// Following will launch the One Note app using the package family name (PFN)
bool result = await Windows.System.Launcher.LaunchUriAsync(new Uri("ms-windows-store://pdp/?PFN= Microsoft.Office.OneNote_8wekyb3d8bbwe"));
`````

If you are launching a custom (non Microsoft store) app, you can use `AppServiceConnection` to launch an app using package family name (PFN). 


First, you must register the final app (com.concurrency.lwinsapp) with app services within the system. You will need to modify the `Package.appxmanifest` file to include the following code block in the `<Applications>` section of the manifest.
```Xaml
<Application Id="App" Executable="$targetnametoken$.exe" EntryPoint="AppServiceProvider.App">
      <Extensions>
        <uap:Extension Category="windows.appService" EntryPoint="MyAppService.UpdateService">
          <uap3:AppService Name="com.concurrency.lwinsapp" uap4:SupportsMultipleInstances="true" />
        </uap:Extension>
      </Extensions>
      ...
</Application>
```

Following code segment will launch a custom application:

````CSharp
private AppServiceConnection updaterService;
...
this.updaterService = new AppServiceConnection();
this.updaterService.AppServiceName = "com.concurrency.lwinsapp";
this.updaterService.PackageFamilyName = "f3a114f7-e099-4773-8c93-77abcba14f62_004hcn5rxyy0y";
var status = await this.updaterService.OpenAsync();
````

By combining logic between `localSettings` and `AppServiceConnection`, you can by pass the test app on every boot of the device. In essance, the test app runs every boot but pass thru to the final app on boot. If needed, you can set your logic in such a way that device will not continue to final app if tests fails on the test app on every boot. This might be helpful if you need to verify that device is fully tested and functional on every boot.
