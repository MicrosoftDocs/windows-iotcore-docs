---
title: Network packet capture
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use Microsoft Message Analyzer to enable network packet capture
keywords: windows iot, network packet, network packet capture, Microsoft Message Analyzer, PowerShell
---

# Network packet capture

You can use [Microsoft Message Analyzer](http://www.microsoft.com/en-us/download/details.aspx?id=44226) to capture, display, and analyze protocol messaging traffic on your Windows 10 IoT Core device.

![Message Analyzer](../media/NetworkPacketCapture/message-analyzer.png)

## Prerequisites

Working PowerShell Connection (Step 1 to 8 described at [PowerShell](../connect-your-device/PowerShell.md).

## Set up your device

In order to connect to your device using Message Analyzer, you need to first rename your device.  This can be done through [SSH](../connect-your-device/SSH.md) or 
[PowerShell](../connect-your-device/PowerShell.md) using the `setcomputername` command.

![PowerShell Rename Device](../media/NetworkPacketCapture/powershell-rename-device.png)

After you rename your device, reboot the device to apply the name change.

## Turn off the firewall

Connect to your device using PowerShell or SSH and run the following command to disable the firewall.
    
    netsh advfirewall set allprofiles state off
    
## Connect to your device using Message Analyzer

Now that your device is set up, let's connect to it using Microsoft Message Analyzer.

1. Download the [Microsoft Message Analyzer](http://www.microsoft.com/en-us/download/details.aspx?id=44226).
2. Open Message Analyzer.
3. Click on `New Session`.

    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer-new-session.png)
4. In the window that opens, click on the `Live Trace` button.
    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer-live-trace.png)
5. Click on the `Edit...` button.
    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer-edit-button.png)
6. Replace Localhost with the name of your IoT device, and enter the administrator user name and password.  Then click `OK`.
    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer-edit-target-computers.png)
7. Click on the `Select a trace scenario` dropdown and select `Local Network Interfaces`.
    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer-trace-scenario.png)
8. Click the `Start` button.
9. You should start to see the messages going through the network interfaces on your device.
    ![Message Analyzer](../media/NetworkPacketCapture/message-analyzer.png)
10. After you start the trace through Message Analyzer, you can also view the ETW messages from the packet capture driver in your device's [web interface](DevicePortal.md).  To do this, go to the ETW tab of the web interface, select `Microsoft-Windows-NDIS-PacketCapture` from the `Registered providers` dropdown menu and click the `Enable` button.
    ![Message Analyzer](../media/NetworkPacketCapture/web-etw.png)    
