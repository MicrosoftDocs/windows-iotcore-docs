---
title: CSPs supported by Windows 10 IoT Core
ms.date: 04/03/2023
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn configuration service provider (CSP) supported by Windows 10 IoT Core.
keywords: windows iot, csp, mdm
---

# CSPs supported in Windows 10 IoT Core

## Configuration Service Providers (CSPs)

| Service Provider | Description |
|------------------|-------------|
| [AllJoynManagement CSP](/windows/client-management/mdm/alljoynmanagement-csp)                 | The AllJoynManagement configuration service provider (CSP) allows an IT administrator to enumerate the AllJoyn devices that are connected to the AllJoyn bus. |
| [Application CSP](/windows/client-management/mdm/application-csp.md)                          | The APPLICATION configuration service provider is used to configure an application transport using Open Mobile Alliance (OMA) Client Provisioning.|
| [CertificateStore CSP](/windows/client-management/mdm/certificatestore-csp.md)                | The CertificateStore configuration service provider is used to add secure socket layers (SSL), intermediate, and self-signed certificates. |
| [ClientCertificateInstall CSP](/windows/client-management/mdm/clientcertificateinstall-csp.md)| The ClientCertificateInstall configuration service provider enables the enterprise to install client certificates. |
| [CustomDeviceUI CSP](/windows/client-management/mdm/customdeviceui-csp.md)                    | The CustomDeviceUI configuration service provider allows OEMs to implement their custom foreground application, and the background tasks to run on an IoT device running IoT Core. |
| [DevDetail CSP](/windows/client-management/mdm/devdetail-csp.md)                              | The DevDetail configuration service provider handles the management object that provides device-specific parameters to the OMA DM server. |
| [DevInfo CSP](/windows/client-management/mdm/devinfo-csp.md)                                  | The DevInfo configuration service provider handles the managed object, which provides device information to the OMA DM server.|
| [DiagnosticLog CSP](/windows/client-management/mdm/diagnosticlog-csp.md)                      | The DiagnosticLog CSP is used for generating and collecting diagnostic information from the device. DiagnosticLog CSP can also trigger devices to upload existing event logs, log files, and registry values to cloud storage.|
| [DMAcc CSP](/windows/client-management/mdm/dmacc-csp.md)                                      | The DMAcc configuration service provider allows an OMA Device Management (DM) version 1.2 server to handle OMA DM account objects. |
| [DMClient CSP](/windows/client-management/mdm/dmclient-csp.md)                                | The DMClient configuration service provider (CSP) has more enterprise-specific mobile device management (MDM) configuration settings. |
| [HealthAttestation CSP](/windows/client-management/mdm/healthattestation-csp.md)              | The Device HealthAttestation configuration service provider (DHA-CSP) enables enterprise IT administrators to assess if a device is booted to a trusted and compliant state, and perform enterprise policy actions. |
| [NetworkProxy CSP](/windows/client-management/mdm/networkproxy-csp.md)                        | The NetworkProxy configuration service provider (CSP) is used to configure a proxy server for ethernet and Wi-Fi connections. These settings don't apply to VPN connections. |
| [Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider.md)         | The Policy configuration service provider enables the enterprise to configure policies on Windows 10 and Windows 11. Use this configuration service provider to configure any company policies.|
| [Provisioning CSP (Provisioning only)](/windows/client-management/mdm/provisioning-csp.md)    | The Provisioning configuration service provider is used for bulk user enrollment to an MDM service.|
| [Reboot CSP](/windows/client-management/mdm/reboot-csp.md)                                    | The Reboot configuration service provider is used to configure reboot settings. |
| [RemoteWipe CSP](/windows/client-management/mdm/remotewipe-csp.md)                            | The RemoteWipe configuration service provider is used by mobile operators DM server or enterprise management server to remotely reset a device. |
| [RootCATrustedCertificates CSP](/windows/client-management/mdm/rootcacertificates-csp.md)     | The RootCATrustedCertificates configuration service provider enables the enterprise to set the Root Certificate Authority (CA) certificates. |
| [UnifiedWriteFilter CSP](/windows/client-management/mdm/unifiedwritefilter-csp.md)            | The UnifiedWriteFilter (UWF) configuration service provider enables the IT administrator to remotely manage the UWF to help protect physical storage media including any writable storage type.|
| [Update CSP](/windows/client-management/mdm/update-csp.md)                                    | The Update configuration service provider enables the IT administrators to manage and control the rollout of new updates.|
| [VPNv2 CSP](/windows/client-management/mdm/vpnv2-csp.md)                                      | The VPNv2 configuration service provider allows the Mobile Device Management (MDM) server to configure the VPN profile of the device. |
| [WiFi CSP](/windows/client-management/mdm/wifi-csp.md)                                        | The WiFi configuration service provider provides the functionality to add or delete Wi-Fi networks on a Windows device. |

## Policies in Policy CSP supported by Windows 10 IoT Core

- [Camera/AllowCamera](/windows/client-management/mdm/policy-csp-camera.md#allowcamera)
- [Cellular/ShowAppCellularAccessUI](/windows/client-management/mdm/policy-csp-cellular.md#showappcellularaccessui)
- [CredentialProviders/AllowPINLogon](/windows/client-management/mdm/policy-csp-credentialproviders.md#allowpinlogon)
- [CredentialProviders/BlockPicturePassword](/windows/client-management/mdm/policy-csp-credentialproviders.md#blockpicturepassword)
- [DataProtection/AllowDirectMemoryAccess](/windows/client-management/mdm/policy-csp-dataprotection.md#allowdirectmemoryaccess)
- [InternetExplorer/DisableActiveXVersionListAutoDownload](/windows/client-management/mdm/policy-csp-internetexplorer.md#disableactivexversionlistautodownload)
- [InternetExplorer/DisableCompatView](/windows/client-management/mdm/policy-csp-internetexplorer.md#disablecompatview)
- [InternetExplorer/DisableGeolocation](/windows/client-management/mdm/policy-csp-internetexplorer.md#disablegeolocation)
- [DeliveryOptimization/DOAbsoluteMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#doabsolutemaxcachesize)
- [DeliveryOptimization/DOAllowVPNPeerCaching](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#doallowvpnpeercaching)
- [DeliveryOptimization/DOCacheHost](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#docachehost)
- [DeliveryOptimization/DOCacheHostSource](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#docachehostsource)
- [DeliveryOptimization/DODelayBackgroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dodelaybackgrounddownloadfromhttp)
- [DeliveryOptimization/DODelayForegroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dodelayforegrounddownloadfromhttp)
- [DeliveryOptimization/DODelayCacheServerFallbackBackground](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dodelaycacheserverfallbackbackground)
- [DeliveryOptimization/DODelayCacheServerFallbackForeground](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dodelaycacheserverfallbackforeground)
- [DeliveryOptimization/DODownloadMode](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dodownloadmode)
- [DeliveryOptimization/DOGroupId](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dogroupid)
- [DeliveryOptimization/DOGroupIdSource](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dogroupidsource)
- [DeliveryOptimization/DOMaxBackgroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domaxbackgrounddownloadbandwidth)
- [DeliveryOptimization/DOMaxCacheAge](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domaxcacheage)
- [DeliveryOptimization/DOMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domaxcachesize)
- [DeliveryOptimization/DOMaxDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md) (Deprecated)
- [DeliveryOptimization/DOMaxForegroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domaxforegrounddownloadbandwidth)
- [DeliveryOptimization/DOMaxUploadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md) (Deprecated)
- [DeliveryOptimization/DOMinBackgroundQos](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dominbackgroundqos)
- [DeliveryOptimization/DOMinBatteryPercentageAllowedToUpload](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dominbatterypercentageallowedtoupload)
- [DeliveryOptimization/DOMinDiskSizeAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domindisksizeallowedtopeer)
- [DeliveryOptimization/DOMinFileSizeToCache](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dominfilesizetocache)
- [DeliveryOptimization/DOMinRAMAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dominramallowedtopeer)
- [DeliveryOptimization/DOModifyCacheDrive](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domodifycachedrive)
- [DeliveryOptimization/DOMonthlyUploadDataCap](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#domonthlyuploaddatacap)
- [DeliveryOptimization/DOPercentageMaxBackgroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dopercentagemaxbackgroundbandwidth)
- [DeliveryOptimization/DOPercentageMaxDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md) (Deprecated)
- [DeliveryOptimization/DOPercentageMaxForegroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dopercentagemaxforegroundbandwidth)
- [DeliveryOptimization/DORestrictPeerSelectionBy](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dorestrictpeerselectionby)
- [DeliveryOptimization/DOSetHoursToLimitBackgroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dosethourstolimitbackgrounddownloadbandwidth)
- [DeliveryOptimization/DOSetHoursToLimitForegroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization.md#dosethourstolimitforegrounddownloadbandwidth)
- [DeviceHealthMonitoring/AllowDeviceHealthMonitoring](/windows/client-management/mdm/policy-csp-devicehealthmonitoring.md#allowdevicehealthmonitoring)
- [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringScope](/windows/client-management/mdm/policy-csp-devicehealthmonitoring.md#configdevicehealthmonitoringscope)
- [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringUploadDestination](/windows/client-management/mdm/policy-csp-devicehealthmonitoring.md#configdevicehealthmonitoringuploaddestination)
- [Privacy/LetAppsActivateWithVoice](/windows/client-management/mdm/policy-csp-privacy.md#letappsactivatewithvoice)
- [Privacy/LetAppsActivateWithVoiceAboveLock](/windows/client-management/mdm/policy-csp-privacy.md#letappsactivatewithvoiceabovelock)
- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update.md#configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update.md#configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update.md#configuredeadlinegraceperiod)
- [Update/ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update.md#configuredeadlinenoautoreboot)
- [Wifi/AllowAutoConnectToWiFiSenseHotspots](/windows/client-management/mdm/policy-csp-wifi.md#allowautoconnecttowifisensehotspots)
- [Wifi/AllowInternetSharing](/windows/client-management/mdm/policy-csp-wifi.md#allowinternetsharing)
- [Wifi/AllowWiFi](/windows/client-management/mdm/policy-csp-wifi.md#allowwifi)
- [Wifi/WLANScanMode](/windows/client-management/mdm/policy-csp-wifi.md#wlanscanmode)

## Related articles

[Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider.md)
