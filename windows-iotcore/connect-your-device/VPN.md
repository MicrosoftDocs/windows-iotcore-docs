---
title: VPN on Windows 10 IoT Core
ms.date: 11/19/2018
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to use, setup, and configure VPN capabilities for your Windows 10 IoT Core device.
keywords: windows iot, VPN, setup, device
---

# Leveraging VPN capabilities for your Windows 10 IoT Core device

In order to leverage the VPN capabilities of Windows 10 IoT Core, follow the instructions below.

> [!NOTE]
> Most of the instructions below must be adapted. They are specific to the VPN host that the user is connecting to. The certs used are examples.

## Establishing a VPN connection

1. Obtain the necessary certs and copy to your IoT device (e.g. to a \vpntest folder).

* RASTest.pfx
* IssuingCA.crl
* RootCA.crl

2. Apply local machine certs
a. PowerShell into device as administrator

```powershell
certmgr -add .\IssuingCA.crl -r localmachine -s root
certmgr -add .\RootCA.crl -r localmachine -s root
```

3. Apply user certs
a. Login to the IoT Device using SSH as "DefaultAccount".
b. From the command prompt, type "PowerShell".
c. Issue the following commands from PowerShell (while logged in as "Default Account"):

```powershell
$mypwd = ConvertTo-SecureString -String "<password>" -Force -AsPlainText
import-pfxcertificate -FilePath RasTest.pfx -CertStoreLocation cert:currentUser\my -Password $mypwd

Cert -add .\IssuingCA.crl -r currentuser -s my
certmgr -add .\RootCA.crl -r currentuser -s my
```

4. Fix hosts file
Add an entry into c:\windows\system32\driverS\etc\hosts file (example shown below);

> | IP Address | Domain Name | Note |
> |----|----| ---|
> | 10.10.10.10 | MyVPN.DomainName.org | Replace with IP address and domain name as needed |

5. Build the VPN test app
Replace the "MyVPN.DomainName.org" in the source code. Augment further as needed.

6. Deploy the code below in the "Starting and stopping a VPN Connection" section to the Windows 10 IoT device.
Enter an arbitrary "Profile name" and press the "Connect to VPN" button.


## Starting and stopping a VPN connection

Use the code below to start and stop a VPN connection.

```csharp

  private async Task ConnectVPNProfile()
        {
            string vpnProfileName = "MyVPNProfileName";

            string[] epdg = { "MyVPN.DomainName.org" };
            VpnManagementErrorStatus status = VpnManagementErrorStatus.Ok;
            IAsyncOperation<VpnManagementErrorStatus> op;

            var vpnMa = new VpnManagementAgent();
            var vpnProfile = new VpnNativeProfile();
            vpnProfile.AlwaysOn = true;
            vpnProfile.ProfileName = vpnProfileName;
            vpnProfile.RequireVpnClientAppUI = true;
            vpnProfile.RememberCredentials = true;
            vpnProfile.RoutingPolicyType = VpnRoutingPolicyType.SplitRouting;
            vpnProfile.TunnelAuthenticationMethod = VpnAuthenticationMethod.Eap;
            vpnProfile.UserAuthenticationMethod = VpnAuthenticationMethod.Eap;
            foreach (var s in epdg)
            {
                vpnProfile.Servers.Add(s);
            }

            vpnProfile.EapConfiguration = GetEapXmlString();

            // Adds the profile using the management api.
           status = await vpnMa.AddProfileFromObjectAsync(vpnProfile);
            Debug.WriteLine($"Add profile: {status}");
            TextBlockLog.Text += $"Add profile: {status}\r\n";

            await Task.Delay(1000);

            op = vpnMa.ConnectProfileAsync(vpnProfile);
            status = await op;
            Debug.WriteLine($"Connect succeeded: {status}");
            TextBlockLog.Text += $"Connect profile: {status}\r\n";


        }


  public static string GetEapXmlString()
        {
            //string template = "<EapHostConfig xmlns=\"http://www.microsoft.com/provisioning/EapHostConfig\"><EapMethod><Type xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">25</Type><VendorId xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</VendorId><VendorType xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</VendorType><AuthorId xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</AuthorId></EapMethod><Config xmlns=\"http://www.microsoft.com/provisioning/EapHostConfig\"><Eap xmlns=\"http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1\"><Type>25</Type><EapType xmlns=\"http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1\"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>d2 d3 8e ba 60 ca a1 c1 20 55 a2 e1 c8 3b 15 ad 45 01 10 c2 </TrustedRootCA><TrustedRootCA>d1 76 97 cc 20 6e d2 6e 1a 51 f5 bb 96 e9 35 6d 6d 61 0b 74 </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns=\"http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1\"><Type>13</Type><EapType xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1\"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>d2 d3 8e ba 60 ca a1 c1 20 55 a2 e1 c8 3b 15 ad 45 01 10 c2 </TrustedRootCA><TrustedRootCA>d1 76 97 cc 20 6e d2 6e 1a 51 f5 bb 96 e9 35 6d 6d 61 0b 74 </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\">true</PerformServerValidation><AcceptServerName xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\">false</AcceptServerName><TLSExtensions xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\"><FilteringInfo xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3\"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled=\"true\"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>true</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns=\"http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2\">true</PerformServerValidation><AcceptServerName xmlns=\"http://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2\">false</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>";
            string template = "<EapHostConfig xmlns =\"http://www.microsoft.com/provisioning/EapHostConfig\"><EapMethod><Type xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">13</Type><VendorId xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</VendorId><VendorType xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</VendorType><AuthorId xmlns=\"http://www.microsoft.com/provisioning/EapCommon\">0</AuthorId></EapMethod><Config xmlns=\"http://www.microsoft.com/provisioning/EapHostConfig\"><Eap xmlns=\"http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1\"><Type>13</Type><EapType xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1\"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>false</DisableUserPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>b6 ea bf ba 48 be 09 c9 50 4f c6 ea 9b f5 74 dc a9 01 56 62 </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\">false</PerformServerValidation><AcceptServerName xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\">false</AcceptServerName><TLSExtensions xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2\"><FilteringInfo xmlns=\"http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3\"><CAHashList Enabled=\"true\"><IssuerHash>b6 ea bf ba 48 be 09 c9 50 4f c6 ea 9b f5 74 dc a9 01 56 62 </IssuerHash></CAHashList></FilteringInfo></TLSExtensions></EapType></Eap></Config></EapHostConfig>";
            //TODO: Create propper XML here
            string result = template;

            return result;
        }
```
