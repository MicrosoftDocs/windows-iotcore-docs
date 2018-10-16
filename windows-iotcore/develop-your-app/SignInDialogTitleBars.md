---
title: Configure the title bar height for sign in dialog boxes
author: johntasler
ms.author: jtasler
ms.date: 09/13/2018
ms.topic: article
description: Learn how to configure the title bar height for sign in dialog boxes in Windows 10 IoT Core, version 1809. 
keywords: Windows 10 IoT Core, msa, aad, titlebar, close, cancel, headed, web, account, WebAccountManagement, sign-in , sign
---

# Title bars for sign in dialogs

By design, Windows 10 IoT Core does not display an application frame around your application's window
\- you get the full screen. However, in version 1809, several system dialog boxes have been given a
title bar containing close button to allow the user to cancel out of them, even when the content of
the dialog box provides no cancel button.

## Sign in dialog boxes

The dialogs that have this feature added are the identity dialogs - for signing in to Microsoft
Accounts (MSA) and Azure Active Directory (AAD). These can be used in your application as shown
in the [Web Account Management sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WebAccountManagement)
in the [Microsoft UWP app samples repo](https://github.com/Microsoft/Windows-universal-samples).

## Configuring the title bar height

The title bar has a default height of 25 pixels, and can be set to any greater value up to 50 pixels. Any value
greater than 50 will be clamped to 50. The height can be less than 25, but consider the possibly negative effect
on the user's experience when deciding the height of the close button.

As an example, to set the title bar height to 32 pixels, in PowerShell you could do the following:
```powershell
# Note that we're only using the variable to make the sample code more narrow
Set-Variable IoTRootKey "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension"
Set-ItemProperty -Path "$IoTRootKey\Experiences\TitleBar" -Name Height -Type DWord -Value 32
```

> [!NOTE]
> For creating an OEM image, the preferred mechanism for setting registry values is with the
> `OEMInput.xml` file discussed in
> [Runtime customizations](/windows-hardware/manufacture/iot/oscustomizations#runtime-customizations)
