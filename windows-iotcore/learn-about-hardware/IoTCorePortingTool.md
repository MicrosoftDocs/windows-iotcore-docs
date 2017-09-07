---
title: Windows 10 IoT Core API Porting Tool
author: saraclay
ms.author: saclayt
ms.date: 08/28/2017
ms.topic: article
description: Learn how to use the Windows 10 IoT Core API Porting Tool to estimate porting costs.
keywords: windows iot, API porting tool, API porting, binaries
---

# Windows 10 IoT Core API Porting Tool

Windows 10 IoT Core only supports a subset of the Win32 and .Net API surface area available on various prior versions of Windows. This tool will scan your binaries and give you a report of the APIs these binaries use that aren't available and give suggestions for possible replacements. This will both help with estimating the cost of a port to IoT Core as well as help you along the way.


## Usage

The Windows 10 IoT Core API Porting Tool can be found in the [ms-iot/iot-utilities](https://github.com/ms-iot/iot-utilities) github repository.  Download the [repository zip](https://github.com/ms-iot/iot-utilities/archive/master.zip) and copy the IoTAPIPortingTool folder to your local machine.  Open **IoTAPIPortingTool.sln** in Visual Studio 2017 and build the project.  This will generate `IotAPIPortingTool.exe`.

You can use the tool by running `IoTAPIPortingTool.exe <Application path> [-os]`.

*  `<Application path>` exe of application that porting tool is used for

*  `-os` should be specified if you are not planning to use UWP.  By default, the tool validates your binaries against the Windows UWP platform.

> [!NOTE] 
> IoTAPIPortingTool.exe must be run from a Visual Studio Developer Command Prompt. You need to navigate to the folder that contains the IotAPIPortingTool.exe. 

        Sample command: C:\IoTAPIPortingTool\bin\Debug>IoTAPIPortingTool.exe C:\Sample\Sample.exe -os 

## Output

The tool will generate a comma separated values (csv) file in same folder that contains the `IotAPIPortingTool.exe`. The file is named `IoTAPIPortingTool.csv` (or, `IoTAPIPortingToolOS.csv` if -os is specified) and a summary will be on the command line. Open the `.csv` file in Excel to analyze the complete output.
