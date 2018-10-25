---
title: Configure your headed device with the Windows 10 IoT Core on-screen keyboard
author: johntasler
ms.author: jtasler
ms.date: 09/13/2018
ms.topic: article
description: Learn about the new on-screen keyboard and how to configure it in Windows 10 IoT Core, version 1809. 
keywords: Windows 10 IoT Core, touch, keyboard, osk, onscreen, on-screen, sip, input, ime, headed, dictation, voice, speech
---

# On-screen keyboard for headed devices

In Windows 10 IoT Core, version 1809, the on-screen keyboard component has changed significantly, and
for the better! IoT Core now uses the same touch keyboard components as the desktop edition of Windows.

## New features
The new keyboard implementation provides the following benefits to your headed device development:

* [The entire set of Windows keyboard language layouts](#windows-keyboard-language-layouts)
* [Support for input scopes (e.g., Email Address, Numeric PIN, Search Field, etc.)](#support-for-input-scopes)
* [Input Method Editor (IME)](#input-method-editor-ime)
* [Non-obscured text input fields](#non-obscured-text-input-fields)
* [Dictation mode](#dictation-mode)
* [A selection of user interface preferences](#user-interface-configuration)

## Feature packages

For prototyping (development) images, the on-screen keyboard feature is already included, but you will need to
enable it from Device Settings in the [Windows Device Portal](../manage-your-device/deviceportal.md#iot-specific-features).

For commercialization, the following optional feature packages will add the on-screen keyboard to your image:
* IOT_SHELL_ONSCREEN_KEYBOARD
* IOT_SHELL_ONSCREEN_KEYBOARD_FOLLOWFOCUS

> [!TIP]
> For more information about IoT Core Features,
> see [IoT Core Feature List](/windows-hardware/manufacture/iot/iot-core-feature-list)
> and [IoT Core manufacturing guide](/windows-hardware/manufacture/iot/iot-core-manufacturing-guide).

## Windows keyboard language layouts

With this release, the supported language layouts has expanded to include the full set of those
available in the desktop Windows edition. To allow your users to select between different language layouts,
you would typically include selection UI in your application's Settings area. The following API is provided
to enable your application to set the language that the on-screen keyboard will use:

[Windows.Globalization.Language.TrySetInputMethodLanguageTag](/uwp/api/windows.globalization.language.trysetinputmethodlanguagetag)

An example of this API can be seen in the [IoTCoreDefaultApp sample application](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/IoTCoreDefaultApp),
in the [LanguageManager.cs](https://github.com/Microsoft/Windows-iotcore-samples/blob/develop/Samples/IoTCoreDefaultApp/CS/IoTCoreDefaultApp/Presenters/LanguageManager.cs) file.

## Support for input scopes

In previous releases, only the EmailSmtpAddress input scope was available. In this release, the full set
of input scopes are available. The following topic explains input scopes and how to use them in your applications:

[Use input scope to change the touch keyboard](/windows/uwp/design/input/use-input-scope-to-change-the-touch-keyboard)

## Input Method Editor (IME)

This release provides an Input Method Editor, which is required for any language that has more graphemes than there
are keys on the keyboard, such as Chinese, Japanese, and Korean.

## Non-obscured text input fields

In previous releases, the touch keyboard might obscure the focused text field so that the user was unable to see what
they were typing. This release fixes this problem by automatically scrolling the text field into view so that it's
no longer obscured by the touch keyboard.

## Dictation mode

When the input language is set to the OS language, which is the default, the voice recognition input feature is available.
To show the dictation button in the keyboard, refer to the following section on
[User Interface configuration](#user-interface-configuration).

## User Interface configuration

The on-screen keyboard provides several configurable options for its user interface. These are configured via the registry.
During development you can use [PowerShell](/windows/iot-core/connect-your-device/powershell) or
[Secure Shell (SSH)](/windows/iot-core/connect-your-device/ssh). For creating an OEM image, the preferred mechanism for
setting registry values is the `OEMInput.xml` file discussed here:

[Runtime customizations](/windows-hardware/manufacture/iot/oscustomizations#runtime-customizations)

> [!NOTE]
> Most of the registry settings documented here will take effect while the on-screen keyboard is visible.
> This allows you during development to easily try different combinatations of settings values,
> immediately seeing the resulting changes in real time. If a setting does not take effect immediately,
> you will need to reboot the device in order to see the changes to the keyboard UI.

### Keyboard Height

By default, the touch keyboard will use the lower 45% of the screen's height. This may appear too large or small on your
device, depending on its size and resolution. You can adjust the height up to a maximum of two-thirds the height
of the screen. Any value not in range will be clamped into range. Because this is specified as a floating point value,
it allows for pixel-level precision. Simply apply the following formula to calculate the percentage:

`percentage = (100 * <desired_pixel_height>) / <screen_height>`

As an example, to change the height to 56.783%, you would set the following registry value:
```console
set OskRootKey=HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\OSK
reg.exe ADD "%OskRootKey%" /v MaxHeightPercentage /t REG_SZ /d "56.783" /f
```
or from PowerShell:
```powershell
set OskRootKey "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\OSK"
cd $OskRootKey
Set-ItemProperty -Path . -Name MaxHeightPercentage -Type String -Value 56.783
```

> [!NOTE]
> The registry value type must be a String (`REG_SZ`), so that the fractional values can be represented with.
> a decimal point. Using DWord (`REG_DWORD`) will _not_ work, even for whole number percentages.

### Additional preferences

The remaining set of preferences are String values in the Preferences subkey:
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\OSK\Preferences
```

| Registry Value               | Default Value      | Description                                                                                         |
| ---------------------------- | ------------------ | --------------------------------------------------------------------------------------------------- |
| AudioFeedback_Disabled       | "0"                | "0" enables the key click audio feedback; "1" disables it.                                          |
| Dictation_Disabled           | "1"                | "0" shows the dictation (voice recognition) button; "1" hides it.<br/> (see note below)             |
| KeyboardModeEnabled_full     | "0"                | "0" disables the full keyboard mode; "1" enables it.                                                |
| KeyboardModeEnabled_narrow   | "1"                | "0" disables the narrow keyboard mode; "1" enables it.                                              |
| KeyboardModeEnabled_wide     | "1"                | "0" disables the wide keyboard mode; "1" enables it.                                                |
| ModeOrder                    | "wide;narrow;full" | The order (from left to right) in which the modes are listed in the mode drop-down menu, if enabled |
| SettingsMenuKey_Collapsed    | "0"                | Hides the mode drop-down menu. Set this to "1" if only one mode is enabled.                         |
| Paste_Disabled               | "0"                | "0" shows the Paste button; "1" hides it.<br/> Change takes effect after reboot.                    |
| CloseButton_Disabled         | "0"                | "0" shows the Close button; "1" hides the Close button<br/> Change takes effect after reboot.       |
| EmojiKeyEnabled              | "0"                | "0" hides the Emoji key; "1" shows it, allowing the user to enter Emoji characters.                 |

> [!NOTE]
> Dictation mode requires a speech package to be installed for the selected input language, as well as an
> audio input device. If a matching speech packages is not installed, the dictation button will not be shown.
> 
> All images include the en-US speech language. Other speech packages are installed as optional features.
> For more information about IoT Features, see [IoT Core Feature List](/windows-hardware/manufacture/iot/iot-core-feature-list)
> and [IoT Core manufacturing guide](/windows-hardware/manufacture/iot/iot-core-manufacturing-guide).

As an example, to enable only `wide` keyboard mode, in PowerShell you could do the following:
```powershell
set OskRootKey "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\IoTShellExtension\OSK"
cd $OskRootKey
mkdir Preferences
cd Preferences
Set-ItemProperty . -Name KeyboardModeEnabled_full -Value "0"      # Optional, since the default is "0"
Set-ItemProperty . -Name KeyboardModeEnabled_narrow -Value "0"
Set-ItemProperty . -Name KeyboardModeEnabled_wide -Value "1"      # Optional, since the default is "1"
Set-ItemProperty . -Name SettingsMenuKey_Collapsed -Value "1"
```
