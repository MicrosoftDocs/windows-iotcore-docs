---
title: Windows Virtual Shields for Arduino Overview
author: saraclay
ms.author: saclayt
ms.date: 09/13/17
ms.topic: article
ms.prod: Windows
ms.technology: IoT
description: Learn how to set up Windows Virtual Shields for Arduino and build your first Windows 10 IoT Core app.
keywords: windows iot, WVSA, Windows Virtual Shields, Arduino, app
---

> [!NOTE]
> You are viewing archived documentation. AllJoyn is no longer supported by Windows 10 IoT. For questions, please open an issue on GitHub or leave us feedback in the comments below.

# Set up Windows Virtual Shields for Arduino

## Overview
If you’ve used an [Arduino](https://www.arduino.cc), you’re familiar with the concept of a shield. Each shield has a specialized purpose (e.g. a temperature shield, an accelerometer shield), and building a device with multiple shields can be complex, costly, and space-inefficient. Now imagine that you can use a low-cost Windows Lumia Phone as a compact set of shields. Your Arduino sketch would be able to access hundreds of dollars worth of sensors and capabilities in your Windows Phone through easy-to-use library calls.

This is exactly what the Windows Virtual Shields for Arduino library enables for developers. And that’s not the best part - this technology works on all Windows 10 devices, so you can use the sensors and capabilities on your PC or Surface as well. Also, the Arduino can offload computationally expensive tasks like speech recognition and web parsing to the Windows 10 companion device!

Let's learn how to setup hardware and software to work with Windows Virtual Shields for Arduino.


## 1. Get your Windows 10 device ready for developing projects using Windows Virtual Shields for Arduino.

In this section of the tutorial, you'll prepare a Windows 10 device of your choice by loading it with the Windows Virtual Shields for Arduino application - this Universal Windows Application allows you to use your device as a "virtual shield" for an Arduino board.  This results in some powerful possibilities for Makers, allowing them to utilize voice recognition, touch screens, and the computational power of Windows with relative ease.

### Hardware
The Windows Virtual Shields for Arduino application can run on any Windows 10 device, but this tutorial will explain setup with a Windows Phone.

*What you need* 
 Windows Phone running Windows 10 - we recommend the [Lumia 520](http://www.microsoft.com/en-us/mobile/phone/lumia520) or [Lumia 635](http://www.microsoft.com/en-us/mobile/phone/lumia635).

*Set up your Windows Phone*

If your phone is not already running Windows 10, there are options to install preview versions of the software.  Windows Phone 8 users can go to the Microsoft Store app to download the "Windows Insider" application - this app allows the user to opt into receiving Windows 10 Technical Previews as updates.  Follow the prompts and instructions upon opening the app, and continue once your phone is successfully running Windows 10.

### Software

There are two options for installing the Windows Virtual Shields for Arduino UWP app on your Windows Phone.  Downloading the app is the easier, quicker choice.

* Download the app from the Microsoft Store
* Sideload the app using a PC and Visual Studio

*Option 1: Download the app from the Microsoft Store*

Follow this [link](https://www.microsoft.com/store/apps/9nblgggz0mld) to the Microsoft Store page for Windows Virtual Shields for Arduino, download the application, and then install. You can then open the application to ensure it runs properly.  Your device is now setup to be used as a "virtual shield" for an Arduino!  You can proceed to the next page.

*Option 2: Sideload the app using a PC and Visual Studio*
_What you need_
* Visual Studio 2017 to sideload the Windows Virtual Shields for Arduino app onto a developer-unlocked phone.
* This [repository](https://github.com/ms-iot/virtual-shields-universal) containing the code for the Windows Virtual Shields for Arduino application.  Either clone the repository or download it as a ZIP on your local disk.  If you're not familiar with git and want to do a proper clone, follow the instructions [here](https://help.github.com/articles/cloning-a-repository).

_Set up Visual Studio 2017_
1. Install Visual Studio 2017 with the Windows 10 Developer Preview tools from [dev.windows.com](https://developer.microsoft.com/en-us/windows/downloads).  We recommend the free Community Version of Visual Studio, but both Enterprise and Professional will work as well.  If you already have Visual Studio installed, skip to the next step.
2. In Visual Studio, load the Shield.sln from the repository downloaded in the "What you need" section above.
3. Ensure your Windows 10 device (in this case a Windows Phone) is developer-unlocked. [This page](https://msdn.microsoft.com/en-us/library/windows/apps/dn614128.aspx) explains how to unlock Windows Phone 8.1, 8, and 7.1; however, the steps are the same for Windows 10 phones.
4. Plug your Windows 10 device into your computer and deploy the Shield.sln program to your device.  To do this, deploy to a "Local Machine", and be sure to set the architecture of the device as "ARM".
5. Run the newly-installed Windows Virtual Shields for Arduino application on your phone to ensure the deploy was successful.  Your Windows 10 device is now setup to be used as a virtual shield!

## 2. Set up your Arduino to use the Windows Virtual Shields for Arduino library 
With our Windows 10 companion device properly set up, let's get our Arduino ready to use the Windows Virtual Shields for Arduino library. You can establish a connection between your Arduino and your Windows 10 "virtual shield" over USB, Bluetooth, or Wi-Fi. This particular tutorial will explain how to complete setup using a Bluetooth connection, but feel free to experiment with the other options.

### Hardware
*What you need*
* Arduino Uno or compatible device
* Connecting wires
* A PC used to upload your Arduino sketches
* Standard A to Standard B USB - needed to upload sketches to your Arduino device
* Optional: Bluetooth module - only needed if you choose to connect by Bluetooth.
* Optional: Wi-fi module - only needed if you choose to connect by wi-fi.

* Set up your Arduino
1. Prepare the Bluetooth module if necessary (the Bluetooth module may need to have headers soldered onto it).
2. Except for the one different noted below, connected the Bluetooth module to the Arduino per [the wiring diagram](https://learn.sparkfun.com/tutorials/using-the-bluesmirf/hardware-hookup).

  * Difference: Use pins 0 and 1 instead of 2 and 3:
    * The Bluetooth TX should connect to pin 0 (Arduino RX or RX0).
    * The Bluetooth RX should connect to pin 1 (Arduino TX or TX1).

### Software
*What you need*
* Arduino IDE 1.6 or better
* ArduinoJSON library
* [This repository](https://github.com/ms-iot/virtual-shields-arduino), which contains the example sketch which will run on the Arduino.

*Set up your Arduino IDE*
* Download and install the Arduino IDE, then launch the program.
* Verify that you have the correct Arduino board selected under *Tools > Board*.
* Verify that you have the correct COM Port selected under *Tools > Port*. The name of the board should appear next to each option, making it much easier to choose the correct option.

*Set up the ArduinoJSON library*
* From the [ArduinoJson repository](https://github.com/bblanchon/ArduinoJson), clone the repository or download the zip.
* Place the whole repository into your libraries folder (i.e. `Documents\Arduino\libraries\ArduinoJson\`).

*Set up the Windows Virtual Shields for Arduino Library*
* Clone [this repository](https://github.com/ms-iot/virtual-shields-arduino) or download the ZIP. If you're not familiar with git and want to do a proper clone, follow the instructions [here](https://help.github.com/articles/cloning-a-repository/).
* Copy the "VirtualShield" folder, found in the "Arduino\Libraries" folder of the repository you just downloaded, to your Arduino library folder (i.e. `Documents\Arduino\libraries\VirtualShield\`).

*Test your setup*
* From the Arduino IDE, go to the menu item *File -> Examples -> Virtual Shield -> HelloWorld-Speech-Eventing*. This should load the speech-recognition based Hello World example we're using for this tutorial.
* Before uploading the sketch to your Arduino, temporarily remove the Bluetooth TX and RX wires from the Arduino (there is only one serial port shared between the USB and Bluetooth - the Bluetooth interferes with the upload).
* Upload the sketch by pressing the "Upload" button in the IDE.
* Replace the Bluetooth TX and RX wires into the Arduino pins (Bluetooth TX to Arduino RX (or RX0) and Bluetooth RX to Arduino TX or (TX1)).
* On the phone (or other Windows device) you prepared on the previous page, pair to the Bluetooth device on your Arduino in the Bluetooth settings. If you're using the BlueSMiRF, the default pin code is 1234. 

> [!NOTE]
> The red blinking light on the BlueSMiRF continues to blink red after a successful pairing. This is expected. It only turns green after a connecting with the Windows Virtual Shields for Arduino application.


## 3. Write your first app: Hello, Blinky! 

### Hello World speech-enabled LED example
With your Windows Phone (or potentially any Windows 10 device!) and your Arduino prepared as detailed in the previous steps of this tutorial, you're now ready to try our sample.

1. Prepare your Arduino board by hooking up an LED with a resistor to pin 8.
2. Make sure that your Arduino is still uploaded with the HelloWorld-Speech-Eventing sample, and then plug the Arduino into a power supply.
3. Run the Windows Virtual Shields for Arduino app on the Windows Phone you prepared previously.
4. If everything has been setup properly, your phone should connect to your Arduino sketch and welcome you with an audio cue. You can now say 'on' or 'off' to your Windows 10 device to switch the LED on your Arduino between on and off!

### Arduino Wiring Sketch: Hello World example

```C++
#include <ArduinoJson.h>

#include <VirtualShield.h>
#include <Text.h>
#include <Speech.h>
#include <Recognition.h>

VirtualShield shield;	          // identify the shield
Text screen = Text(shield);	      // connect the screen
Speech speech = Speech(shield);	  // connect text to speech
Recognition recognition = Recognition(shield);	  // connect speech to text

int LED_PIN = 8;

void recognitionEvent(ShieldEvent* event)
{
  if (event->resultId > 0) {
    digitalWrite(LED_PIN, recognition.recognizedIndex == 1 ? HIGH : LOW);
    screen.printAt(4, "Heard " + String(recognition.recognizedIndex == 1 ? "on" : "off"));
    recognition.listenFor("on,off", false);	    // reset up the recognition after each event
  }
}

// when Bluetooth connects, or the 'Refresh' button is pressed
void refresh(ShieldEvent* event)
{
  String message = "Hello Virtual Shields. Say the word 'on' or 'off' to affect the LED";

  screen.clear();
  screen.print(message);
  speech.speak(message);

  recognition.listenFor("on,off", false);	// NON-blocking instruction to recognize speech
}

void setup()
{
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN, LOW);

  recognition.setOnEvent(recognitionEvent);	// set up a function to handle recognition events (turns auto-blocking off)
  shield.setOnRefresh(refresh);

  // begin() communication - you may specify a baud rate here, default is 115200
  shield.begin();
}

void loop()
{
  shield.checkSensors();		    // handles Virtual Shield events.
}
```


