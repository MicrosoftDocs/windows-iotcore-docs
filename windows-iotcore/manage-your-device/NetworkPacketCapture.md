---
title: Network packet capture
ms.date: 04/03/2023
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to use Microsoft Message Analyzer to enable network packet capture
keywords: windows iot, network packet, network packet capture, Microsoft Message Analyzer, PowerShell
---

# Network packet capture

> [!NOTE]
> Microsoft Message Analyzer has been [deprecated](/openspecs/blog/ms-winintbloglp/dd98b93c-0a75-4eb0-b92e-e760c502394f). Information contained below is for archival reference only.

You can use [Microsoft Message Analyzer](/message-analyzer/installing-and-upgrading-message-analyzer) to capture, display, and analyze protocol messaging traffic on your Windows 10 IoT Core device.

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

```cmd
netsh advfirewall set allprofiles state off
```

## Connect to your device using Message Analyzer

Now that your device is set up, let's connect to it using Microsoft Message Analyzer.

1. Download the [Microsoft Message Analyzer](/message-analyzer/installing-and-upgrading-message-analyzer).
1. Open Message Analyzer.
1. Click on `New Session`.

    ![Message Analyzer 1](../media/NetworkPacketCapture/message-analyzer-new-session.png)
1. In the window that opens, click on the `Live Trace` button.
    ![Message Analyzer 2](../media/NetworkPacketCapture/message-analyzer-live-trace.png)
1. Click on the `Edit...` button.
    ![Message Analyzer 3](../media/NetworkPacketCapture/message-analyzer-edit-button.png)
1. Replace Localhost with the name of your IoT device, and enter the administrator user name and password.  Then click `OK`.
    ![Message Analyzer 4](../media/NetworkPacketCapture/message-analyzer-edit-target-computers.png)
1. Click on the `Select a trace scenario` dropdown and select `Local Network Interfaces`.
    ![Message Analyzer 5](../media/NetworkPacketCapture/message-analyzer-trace-scenario.png)
1. Click the `Start` button.
1. You should start to see the messages going through the network interfaces on your device.
    ![Message Analyzer 6](../media/NetworkPacketCapture/message-analyzer.png)
1. After you start the trace through Message Analyzer, you can also view the ETW messages from the packet capture driver in your device's [web interface](DevicePortal.md).  To do this, go to the ETW tab of the web interface, select `Microsoft-Windows-NDIS-PacketCapture` from the `Registered providers` dropdown menu, and click the `Enable` button.
    ![Message Analyzer 7](../media/NetworkPacketCapture/web-etw.png)
