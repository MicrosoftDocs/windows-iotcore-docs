---
title: Cortana on IoT Core
author: zhuridartem
ms.author: artemz
ms.date: 08/28/2017
ms.topic: article
description: Learn how to get started and install updates for Cortana on Windows IoT Core.
keywords: windows iot, Cortana, voice, AI, digital assistant, language

---

# Cortana on IoT Core

Cortana is a personal digital assistant working across all your devices to help you in your daily life. She learns about you; helps you get things done by completing tasks; interacts with you using natural language in a consistent, contextual way; and always looks out for you. Cortana has a consistent visual identity, personality, and voice.

IoT Core is an edition of Windows 10 and is optimized for small-footprint and low-cost IoT devices. Cortana is enabled on IoT Core in the Windows 10 Creators Update. It is in preview now. 

Cortana on IoT Core will focus on commercial scenarios in the future. Updates will come soon. 

> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/Cortana-on-Windows-10-IoT-Core/player]

To use Cortana:

-   The device must have internet connection.

-   The user must have a Microsoft account (MSA) which is in the form of
    [alias@outlook.com, alias@hotmail.com](mailto:alias@outlook.com,%20alias@hotmail.com) or <alias@live.com>.

-   The user is required to sign in using their MSA on the device to utilize Cortana.

-   The device must have a display.

-   A microphone and speaker are required for speech interaction with Cortana.

-   An OEM must follow the guidance provided for the design and development of audio input devices outlined in the [Microsoft Speech Platform](https://msdn.microsoft.com/en-us/library/windows/hardware/dn915051(v=vs.85).aspx) Specification.

## Use the Cortana Function on IoT Core

This document describes how to enable and utilize Cortana on IoT Core. Makers and OEMs can now leverage the capabilities of Cortana to build even smarter, connected IoT devices.

### Hardware List

Windows 10 IoT Core can be run on a [list of IoT devices](../learn-about-hardware/SuggestedBoards.md).

Any microphone and speaker you select to use with the your IoT devices should work with Cortana. For better speech recognition
quality, here is a recommended list of hardware that has been tested.

**Microphone**

* Blue Snowball iCE Condensier Microphone, Carioid 
* Sound Tech CM-1000USB Table Top Conference Meeting Microphone with omni-directional stereo
* Microsoft LifeCam HD 3000

**Speaker**
* Logitech S150 USB Speakers

**USB Hub**
* Depending on your IoT device, you may need a USB hub to connect the
    peripherals (including a mouse and a keyboard)

## Getting Started

To get started with Cortana on Windows 10 IoT Core, a few additional set up steps are necessary.

### Install [Windows 10 IoT Core Dashboard](https://developer.microsoft.com/en-us/windows/iot/Downloads).

### Flash the IoT Device

[Flash your IoT Core device](https://developer.microsoft.com/en-us/windows/iot/getstarted) with the correct image. If you have trouble finding the image for
your IoT device, please go to [Windows Insider Preview Downloads](https://www.microsoft.com/en-us/software-download/windowsiot) page.

### Install Update

Once the image boots up, please open Device Portal for your device and install updates. To do this, enter `http://[device
IP]:8080/#Windows%20Update` in a browser and click on **Check for
Updates**. Apply any updates if they are available. The update process will take approximately 30-40 minutes. 
Once the updates have been downloaded and installed, click on **Restart Now**.

![Install update](../media/CortanaOnIoTCore/InstallUpdate1.png)

![Install update](../media/CortanaOnIoTCore/InstallUpdate2.png)

![Install update](../media/CortanaOnIoTCore/InstallUpdate3.png)

### Set Up the Peripherals

Connect the microphone and speakers into the USB port on your device. If
necessary, use a USB hub.

Once connected, adjust the microphone and speaker settings in Device Portal. To do this, enter `http://[device
IP]:8080/#Device%20Settings` in a browser. Under **Audio Control**, check that the microphone and speakers displayed are the ones
that are physically connected. In the image below, the speakers show **Speakers (2- USB AUDIO)** which is the **Logitech USB Speakers** and the microphone shows **Desktop Microphone (Microsoft LifeCam HD-3000)** which is the **Microsoft LifeCam HD 3000**.

Adjust the volume settings for both to be within the range of 40-70%
(Double-check that the Microphone setting is not 0.0)

![Audio setup](../media/CortanaOnIoTCore/AudioSetup.png)

> [!NOTE]
> This next step is only for Dragonboard 410c.

###  Dragonboard Only : Disable Audio Driver

To enable USB audio, you will need to disable the Qualcomm audio driver.
To do this, simply run this command in a PowerShell window under the IoT
Device administrator account:

`devcon disable "AUDD\\QCOM2468"`

### Launch Cortana

Now it’s time to launch Cortana!

During the first boot, right after Wi-Fi setting, Cortana consent will
pop up to ask for permission. To accept, click **Sure**, Cortana will be launched when you say
“Hey Cortana”. 

> [!IMPORTANT]
> If you deny consent, Cortana will not work. If you skip the acceptance, you need to go to Device Portal to enable Cortana later.

![Constent from Cortana](../media/CortanaOnIoTCore/Consent.png)

MSA sign in will pop up after consent. If you'd like to sign in, follow
her instructions on the sign in page.

Cortana should work now if you accept the Consent.

If Cortana still doesn’t work, please do the following instructions to
turn on Cortana manually.

### Start Cortana on Boot

Enter Device Portal again - to do this, enter: 
`http://<deviceIP>:8080/\#Device%20Settings` into a browser. Under Device
Settings, scroll to the bottom and check **"Start Cortana on Boot"** if it is not checked. Restart the device (top right corner of the browser
has a Power button with Restart option)


![Start Cortana](../media/CortanaOnIoTCore/StartCortana.png)

### Grant Consent

Go to Apps Manager under Device Portal - to do this, enter:
`http://<device IP>:8080/\#Apps%20manager` into a browser.
Under the list of App Names, you should see **Search** or **Cortana**.
If it's stopped, start the app (under the Actions drop down box, select
**Start**). Cortana will launch on your IoT Device

If it's your very first time launching Cortana, it will ask for consent.
To accept, click **Sure**:

> [!IMPORTANT]
> If you deny consent, Cortana will not work. 

![Consent from Cortana](../media/CortanaOnIoTCore/Consent2.png)

If you deny consent at first and want to use Cortana later, you could go
to Device Settings in the IoTCoreDefaultApp to turn on Cortana.

![Start Cortana](../media/CortanaOnIoTCore/EnableKws.png)

### Sign into MSA

Signing in with your MSA will help Cortana provide more personalized
context in her responses to you. If you deny log in, Cortana will still
work but her responses will just be more generalized.

If you'd like to sign in, follow her instructions on the sign in page.

Sign in page will only be launched at the first time you ask Cortana to
do any personal information related action. If you click ‘Maybe later’,
it will be popped up next time when you ask personal information related
question.

![Signing into MSA](../media/CortanaOnIoTCore/MSASignIn.png)

###  Sign out of MSA

If you want to sign out your MSA, please go to Device Settings in the IoTCoreDefaultApp, click ‘About Me’, then the account icon at the bottom to
sign out.

![Signing out of MSA](../media/CortanaOnIoTCore/MSASignOut.png)

### Invoking and Stopping Cortana

You can now try Cortana.

To start Cortana, say "Hey Cortana" to your microphone. Cortana on IoT
Core will now launch and you can start to talk to her. Here are some
sample queries:

Hey Cortana, What's the weather today?

Hey Cortana, what is the traffic in Seattle?

Hey Cortana, what is the stock price for Microsoft?

If you stop talking to Cortana, she will be dismissed. To start her up
again, say "Hey Cortana" followed by your query. To stop Cortana, say
"Hey Cortana, stop" to your microphone.

## Integrate Cortana in your Products

To learn more about changing settings for region and user or speech language to build Cortana enabled products, please read our [Command Line Utils](../manage-your-device/CommandLineUtils.md) documentation.

> [!NOTE]
> Cortana will only work when region, UI language and speech
language are coherent, e.g.: `region = CA`, `UI language = en-CA` and `speech
language = en-CA`.

### Cortana Feature ID

There is one [feature ID](<https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/iot/iot-core-feature-list>) for Cortana, `<Feature>IOT_CORTANA</Feature>` that an OEM needs to add this feature ID in their OEMInput XML. To enable ‘Start Cortana on Boot’ in an image, just add `<Feature>IOT_CORTANA_OBSCURELAUNCH></Feature>`; in OEMInput XML.

### Cortana Consent

OEM should add the following snippet into their own code to make sure
that consent will be launched before the user uses Cortana.

```
// Microsoft recommends replacing **QuerySourceSecondaryId=IoT** with
**QuerySourceSecondaryId=IoT\_MANUFACTURER\_DEVICE**.

// For example **QuerySourceSecondaryId=IoT\_YourCompanyName\_Toaster**

 var uri = new
 Uri(@"ms-cortana://CapabilitiesPrompt/?RequestedCapabilities=InputPersonalization,Microphone,Personalization&QuerySourceSecondaryId=IoT&QuerySource=Microphone&DismissAfterConsent=True");
 var success = await Windows.System.Launcher.LaunchUriAsync(uri);
```

### Enable Voice Activation (Keyword Spotting)

Keyword spotting, it is software keyword spotter which detects when the
user says “Hey, Cortana” .

OEM has the flexibility to decide when to enable KWS. For example, OEM
wants to enable KWS only when proximity sensor detects someone is
nearby. 

OEM will be able to set whether Cortana can be
activated by voice (listen to “Hey Cortana”). These API will only be
available in Embedded Mode to UWP applications.

Embedded mode is a restricted device mode that enables a device to gain
access to features and APIs that are otherwise restricted in UWP,
including: 

-   Background applications (aka CBT or headless apps)

-   Use of the lowLevelDevice capability APIs

-   Use of systemManagement capability APIs

The Windows.Services.Cortana.CortanaSettings will provide the following

-   An API to check if Cortana is available

-   An API to check if user has consent to voice activation for Cortana

-   an API to control Cortana voice activation (listening to “Hey
    Cortana”). 

IoT OEM has a UWP app that enables voice activation (Cortana can listen
to “Hey Cortana”) when user is close to a device. The sample below shows
how to do that.

```
private void OnUserProximitySensorApproach()

{ // leave if Cortana isn't available

  if (!Windows.Services.Cortana.CortanaSettings.IsCortanaAvailable)
 
  {
 
  return;
 
  }
 
  // enable voice activation if allowed and not already done
 
  if
  (!Windows.Services.Cortana.CortanaSettings.HasUserConsentToVoiceActivation)
 
  {
 
  // voice activation isn’t allowed by user
 
  //
 
  // Note that, user consent can be obtained by launching
 
  // ms-cortana://CapabilitiesPrompt/?RequestedCapabilities

  // =InputPersonalization,Microphone&QuerySource=

  // Microphone&QuerySourceSecondaryId=IoT
 
  return;

}

else if
(!Windows.Services.Cortana.CortanaSettings.IsVoiceActivationEnabled)

{

  Windows.Services.Cortana.CortanaSettings.IsVoiceActivationEnabled =
  true;

}

}
```

### Cortana on Windows 10 IoT Core Capabilities

Cortana on IoT Core offers reactive
experiences in the Windows 10 Creators Update. A reactive experience
occurs when the user initiates commands to cut through multiple steps to complete a task. Reactive information is provided in response to a
query.

Cortana is extensible. In addition to the native skills supported by the
Cortana application, developers can create their own skills to allow
Cortana to do more.

-   With the Windows 10 Creators Update, the following capabilities of
    Cortana will be enabled on IoT Core.

    -   Cortana skills sample list	   - Reminder, To-do list, Traffic/Restuarant, Chit Chat, Dictionary, Finance, Health,News, Reference, Show Times, Calculator, Weather, Entity look up, Events, Sports,Time zone, etc.


-   Catered to devices with small- or medium-sized screens (e.g. thermostat or refrigerator), provide a voice response with optimized visual content.

-   Leverages the audio pipeline provided in the Windows 10 operating system which supports linear microphone arrays. Audio input devices should conform to the guidance outlined in the [Microsoft Speech Platform](https://msdn.microsoft.com/en-us/library/windows/hardware/dn915051(v=vs.85).aspx).

-   To wake-up Cortana the user says “Hey, Cortana.” Keyword Spotting (KWS) runs locally to receive the voice input and complete the analysis. The audio is only sent to the cloud once the keyword is spotted. User consent is needed before enabling KWS. The KWS is optimized by the Windows Speech Platform and supports multiple
    languages and regions.

-   Will support en-US only.

### Cortana Extensibility

Cortana custom skill provides the extensible capability for Cortana. The experts control the end-to-end experience, while Cortana brokers to relevant applications, websites, services and bots. Custom skills are created by developers, for example, OEM partners or ISVs.

OEMs can write a [Voice Command Definition application](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CortanaVoiceCommand) that allows to add local commands to Cortana.

