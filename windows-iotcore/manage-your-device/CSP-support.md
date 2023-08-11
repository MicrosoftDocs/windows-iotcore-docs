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
| [Application CSP](/windows/client-management/mdm/application-csp)                          | The APPLICATION configuration service provider is used to configure an application transport using Open Mobile Alliance (OMA) Client Provisioning.|
| [CertificateStore CSP](/windows/client-management/mdm/certificatestore-csp)                | The CertificateStore configuration service provider is used to add secure socket layers (SSL), intermediate, and self-signed certificates. |
| [ClientCertificateInstall CSP](/windows/client-management/mdm/clientcertificateinstall-csp)| The ClientCertificateInstall configuration service provider enables the enterprise to install client certificates. |
| [CustomDeviceUI CSP](/windows/client-management/mdm/customdeviceui-csp)                    | The CustomDeviceUI configuration service provider allows OEMs to implement their custom foreground application, and the background tasks to run on an IoT device running IoT Core. |
| [DevDetail CSP](/windows/client-management/mdm/devdetail-csp)                              | The DevDetail configuration service provider handles the management object that provides device-specific parameters to the OMA DM server. |
| [DevInfo CSP](/windows/client-management/mdm/devinfo-csp)                                  | The DevInfo configuration service provider handles the managed object, which provides device information to the OMA DM server.|
| [DiagnosticLog CSP](/windows/client-management/mdm/diagnosticlog-csp)                      | The DiagnosticLog CSP is used for generating and collecting diagnostic information from the device. DiagnosticLog CSP can also trigger devices to upload existing event logs, log files, and registry values to cloud storage.|
| [DMAcc CSP](/windows/client-management/mdm/dmacc-csp)                                      | The DMAcc configuration service provider allows an OMA Device Management (DM) version 1.2 server to handle OMA DM account objects. |
| [DMClient CSP](/windows/client-management/mdm/dmclient-csp)                                | The DMClient configuration service provider (CSP) has more enterprise-specific mobile device management (MDM) configuration settings. |
| [HealthAttestation CSP](/windows/client-management/mdm/healthattestation-csp)              | The Device HealthAttestation configuration service provider (DHA-CSP) enables enterprise IT administrators to assess if a device is booted to a trusted and compliant state, and perform enterprise policy actions. |
| [NetworkProxy CSP](/windows/client-management/mdm/networkproxy-csp)                        | The NetworkProxy configuration service provider (CSP) is used to configure a proxy server for ethernet and Wi-Fi connections. These settings don't apply to VPN connections. |
| [Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider)         | The Policy configuration service provider enables the enterprise to configure policies on Windows 10 and Windows 11. Use this configuration service provider to configure any company policies.|
| [Provisioning CSP (Provisioning only)](/windows/client-management/mdm/provisioning-csp)    | The Provisioning configuration service provider is used for bulk user enrollment to an MDM service.|
| [Reboot CSP](/windows/client-management/mdm/reboot-csp)                                    | The Reboot configuration service provider is used to configure reboot settings. |
| [RemoteWipe CSP](/windows/client-management/mdm/remotewipe-csp)                            | The RemoteWipe configuration service provider is used by mobile operators DM server or enterprise management server to remotely reset a device. |
| [RootCATrustedCertificates CSP](/windows/client-management/mdm/rootcacertificates-csp)     | The RootCATrustedCertificates configuration service provider enables the enterprise to set the Root Certificate Authority (CA) certificates. |
| [UnifiedWriteFilter CSP](/windows/client-management/mdm/unifiedwritefilter-csp)            | The UnifiedWriteFilter (UWF) configuration service provider enables the IT administrator to remotely manage the UWF to help protect physical storage media including any writable storage type.|
| [Update CSP](/windows/client-management/mdm/update-csp)                                    | The Update configuration service provider enables the IT administrators to manage and control the rollout of new updates.|
| [VPNv2 CSP](/windows/client-management/mdm/vpnv2-csp)                                      | The VPNv2 configuration service provider allows the Mobile Device Management (MDM) server to configure the VPN profile of the device. |
| [WiFi CSP](/windows/client-management/mdm/wifi-csp)                                        | The WiFi configuration service provider provides the functionality to add or delete Wi-Fi networks on a Windows device. |

## Policies in Policy CSP supported by Windows 10 IoT Core

- [Camera/AllowCamera](/windows/client-management/mdm/policy-csp-camera#allowcamera)
- [Cellular/ShowAppCellularAccessUI](/windows/client-management/mdm/policy-csp-cellular#showappcellularaccessui)
- [CredentialProviders/AllowPINLogon](/windows/client-management/mdm/policy-csp-credentialproviders#allowpinlogon)
- [CredentialProviders/BlockPicturePassword](/windows/client-management/mdm/policy-csp-credentialproviders#blockpicturepassword)
- [DataProtection/AllowDirectMemoryAccess](/windows/client-management/mdm/policy-csp-dataprotection#allowdirectmemoryaccess)
- [InternetExplorer/DisableActiveXVersionListAutoDownload](/windows/client-management/mdm/policy-csp-internetexplorer#disableactivexversionlistautodownload)
- [InternetExplorer/DisableCompatView](/windows/client-management/mdm/policy-csp-internetexplorer#disablecompatview)
- [InternetExplorer/DisableGeolocation](/windows/client-management/mdm/policy-csp-internetexplorer#disablegeolocation)
- [DeliveryOptimization/DOAbsoluteMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization#doabsolutemaxcachesize)
- [DeliveryOptimization/DOAllowVPNPeerCaching](/windows/client-management/mdm/policy-csp-deliveryoptimization#doallowvpnpeercaching)
- [DeliveryOptimization/DOCacheHost](/windows/client-management/mdm/policy-csp-deliveryoptimization#docachehost)
- [DeliveryOptimization/DOCacheHostSource](/windows/client-management/mdm/policy-csp-deliveryoptimization#docachehostsource)
- [DeliveryOptimization/DODelayBackgroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodelaybackgrounddownloadfromhttp)
- [DeliveryOptimization/DODelayForegroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodelayforegrounddownloadfromhttp)
- [DeliveryOptimization/DODelayCacheServerFallbackBackground](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodelaycacheserverfallbackbackground)
- [DeliveryOptimization/DODelayCacheServerFallbackForeground](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodelaycacheserverfallbackforeground)
- [DeliveryOptimization/DODownloadMode](/windows/client-management/mdm/policy-csp-deliveryoptimization#dodownloadmode)
- [DeliveryOptimization/DOGroupId](/windows/client-management/mdm/policy-csp-deliveryoptimization#dogroupid)
- [DeliveryOptimization/DOGroupIdSource](/windows/client-management/mdm/policy-csp-deliveryoptimization#dogroupidsource)
- [DeliveryOptimization/DOMaxBackgroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#domaxbackgrounddownloadbandwidth)
- [DeliveryOptimization/DOMaxCacheAge](/windows/client-management/mdm/policy-csp-deliveryoptimization#domaxcacheage)
- [DeliveryOptimization/DOMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization#domaxcachesize)
- [DeliveryOptimization/DOMaxDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization) (Deprecated)
- [DeliveryOptimization/DOMaxForegroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#domaxforegrounddownloadbandwidth)
- [DeliveryOptimization/DOMaxUploadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization) (Deprecated)
- [DeliveryOptimization/DOMinBackgroundQos](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominbackgroundqos)
- [DeliveryOptimization/DOMinBatteryPercentageAllowedToUpload](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominbatterypercentageallowedtoupload)
- [DeliveryOptimization/DOMinDiskSizeAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#domindisksizeallowedtopeer)
- [DeliveryOptimization/DOMinFileSizeToCache](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominfilesizetocache)
- [DeliveryOptimization/DOMinRAMAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#dominramallowedtopeer)
- [DeliveryOptimization/DOModifyCacheDrive](/windows/client-management/mdm/policy-csp-deliveryoptimization#domodifycachedrive)
- [DeliveryOptimization/DOMonthlyUploadDataCap](/windows/client-management/mdm/policy-csp-deliveryoptimization#domonthlyuploaddatacap)
- [DeliveryOptimization/DOPercentageMaxBackgroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#dopercentagemaxbackgroundbandwidth)
- [DeliveryOptimization/DOPercentageMaxDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization) (Deprecated)
- [DeliveryOptimization/DOPercentageMaxForegroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#dopercentagemaxforegroundbandwidth)
- [DeliveryOptimization/DORestrictPeerSelectionBy](/windows/client-management/mdm/policy-csp-deliveryoptimization#dorestrictpeerselectionby)
- [DeliveryOptimization/DOSetHoursToLimitBackgroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#dosethourstolimitbackgrounddownloadbandwidth)
- [DeliveryOptimization/DOSetHoursToLimitForegroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#dosethourstolimitforegrounddownloadbandwidth)
- [DeviceHealthMonitoring/AllowDeviceHealthMonitoring](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#allowdevicehealthmonitoring)
- [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringScope](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#configdevicehealthmonitoringscope)
- [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringUploadDestination](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#configdevicehealthmonitoringuploaddestination)
- [Privacy/LetAppsActivateWithVoice](/windows/client-management/mdm/policy-csp-privacy#letappsactivatewithvoice)
- [Privacy/LetAppsActivateWithVoiceAboveLock](/windows/client-management/mdm/policy-csp-privacy#letappsactivatewithvoiceabovelock)
- [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforfeatureupdates)
- [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforqualityupdates)
- [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiod)
- [Update/ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot)
- [Wifi/AllowAutoConnectToWiFiSenseHotspots](/windows/client-management/mdm/policy-csp-wifi#allowautoconnecttowifisensehotspots)
- [Wifi/AllowInternetSharing](/windows/client-management/mdm/policy-csp-wifi#allowinternetsharing)
- [Wifi/AllowWiFi](/windows/client-management/mdm/policy-csp-wifi#allowwifi)
- [Wifi/WLANScanMode](/windows/client-management/mdm/policy-csp-wifi#wlanscanmode)

## Related articles

[Policy CSP](/windows/client-management/mdm/policy-configuration-service-provider)
