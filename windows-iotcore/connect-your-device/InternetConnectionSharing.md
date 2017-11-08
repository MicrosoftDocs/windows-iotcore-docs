---
title: Internet Connection Sharing
author: derekameer
ms.author: demeer
ms.date: 08/28/2017
ms.topic: article
description: Learn how to enable and configure internet connection sharing on Windows IoT Core.
keywords: windows iot, Internet Connection Sharing, ICS, Device Portal
---

# Internet connection sharing

This document describes how internet connection sharing (ICS) can be enabled on Windows IoT Core. Developers can use the NetworkTetheringManager API to configure ICS programmatically. The API is described in the [NetworkOperatorTetheringManager](https://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.networkoperators.networkoperatortetheringmanager.aspx) class.
When using one of the [Windows 10 IoT Core Release Image](https://developer.microsoft.com/en-us/windows/iot/downloads) ICS can also be configured using the device portal.

For the Sharing Tutorial, please view the [Windows IoT Core November 2015 Release](InternetConnectionSharingNov2015.md) document.

## Configuring ICS using the device portal
See documentation on [Windows Device Portal](../manage-your-device/deviceportal.md) (WDP).

## ICS code sample
The code sample below demonstrates how the [NetworkOperatorTetheringManager](https://msdn.microsoft.com/en-us/library/windows/apps/windows.networking.networkoperators.networkoperatortetheringmanager.aspx) API is used to start sharing an Ethernet connection over Wi-Fi. The CreateFromConnectionProfile method accepts arguments that specifies the public and private interface. In any cases of misconfiguration, such as the Wi-Fi radio is turned off, or Ethernet has limited connectivity, then the attempt to start internet sharing conveys an appropriate error code pertaining to this scenario.

```
using Windows.Networking.NetworkOperators;
using Windows.Networking.Connectivity; 
 
// Find the Ethernet profile (IANA Type 6)
var connectionProfiles = NetworkInformation.GetConnectionProfiles(); 
var ethernetConnectionProfile = connectionProfiles.FirstOrDefault(x => x.NetworkAdapter.IanaInterfaceType == 6); 

// Find an 802.11 wireless network interface (IANA Type 71)
var wirelessConnectionProfile = connectionProfiles.FirstOrDefault(x => x.NetworkAdapter.IanaInterfaceType == 71);
var targetNetworkAdapter = wirelessConnectionProfile.NetworkAdapter;

if (ethernetConnectionProfile != null && targetNetworkAdapter != null)
{
    var tetheringManager = NetworkOperatorTetheringManager.CreateFromConnectionProfile(ethernetConnectionProfile, targetNetworkAdapter); 

    var result = await tetheringManager.StartTetheringAsync(); 
    if (result.Status == TetheringOperationStatus.Success)
    {
        UpdateUI();
    }
    else
    {
        ProcessTetheringError(result);
    }
}
```
