---
title: Python
author: paulmon
ms.author: paulmon
ms.date: 08/13/2019
ms.topic: article
description: Learn how to install Python on a device running Windows 10 IoT Core
keywords: windows iot, python
---

# Python
Python is a scripting language that is popular for system automation and machine learning (ML).
You can learn more about Python at [python.org](https://www.python.org/).

## Using Python on x64
To install Python on Windows IoT Core:
1. Download the Python nuget package, and then install the files using [PowerShell](../connect-your-device/PowerShell.md).

```powershell
Invoke-WebRequest https://globalcdn.nuget.org/packages/python.3.7.4.nupkg -OutFile c:\data\python.zip
Expand-Archive C:\data\python.zip -DestinationPath c:\python_temp
move C:\python_temp\tools c:\python
rd C:\python_temp -Recurse -Force
del C:\data\python.zip
```

2. Add Python to the system path.

```powershell
cmd /c 'setx PATH "%PATH%";c:\python;c:\python\scripts /M'
$env:Path += ";c:\python;c:\python\scripts"
```

3. Ensure that the current version of pip is installed

```powershell
python -m pip install --upgrade pip
```

## Try out [Azure IoT Hub Python SDKs v2 - PREVIEW](https://github.com/Azure/azure-iot-sdk-python-preview) on x64

1. First install the SDK.

```powershell
python -m pip install azure-iot-device
```

In the output for the `pip install` there may be errors: `Download error for https://files.pythonhosted.org/`.  
If you see this then, otherwise skip to `Set up an IoT Hub and create a Device Identity`:
1. Navigate to `https://files.pythonhosted.org/` in your favorite browser. Inspect the web site's certificate and noticed that it issued by `GlobalSign`.
2. Create a directory named `c:\test`.
3. Run `certmgr.msc` from a command prompt on a desktop Windows machine.  
4. Navigate to `Trusted Root Certification Authorities` in the treeview.  Expand the node and choose `Certificates`.
5. In the right pane find the `GlobalSign Root CA`, right-click and select `All Tasks` > `Export`.  Note that there are multiple GlobalSign certs and I identified this one by trying each one, one at a time.
6. In the dialog that pops up click `Next`.
7. Select `DER encoded binary X.509 (.CER)` (this should be the default) and click `Next`.
8. In the `File name:` edit box type `c:\test\GlobalSign Root CA.cer`

![Certificate Export Wizard](../media/Python/global_sign_cert.png)

9. Click `Next`.
10. Click `Finish`.
11. Copy `c:\test\GlobalSign Root CA.cer` to the device by running the following command on your desktop machine:

```powershell
net use X: \\host\c$ /user:host\administrator
md X:\test
copy "c:\test\GlobalSign Root CA.cer" X:\test
```

12. On the device import the certificate into the root store using [PowerShell](../connect-your-device/PowerShell.md).

```powershell
certmgr -add "c:\test\GlobalSign Root CA.cer" -s root -r localMachine -c
```

13. Try to install the `azure-iot-device` again

``` powershell
python -m pip install azure-iot-device --no-color
```

### Set up an IoT Hub and create a Device Identity
14. Install the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) (or use the [Azure Cloud Shell](https://shell.azure.com/)) and use it to [create an Azure IoT Hub](https://docs.microsoft.com/en-us/cli/azure/iot/hub?view=azure-cli-latest#az-iot-hub-create).

    ```bash
    az iot hub create --resource-group <your resource group> --name <your IoT Hub name>
    ```
    * Note that this operation make take a few minutes.

15. Add the IoT Extension to the Azure CLI, and then [register a device identity](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-device-identity-create)

    ```bash
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name <your IoT Hub name> --device-id <your device id>
    ```

16. [Retrieve your Device Connection String](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot/hub/device-identity?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-device-identity-show-connection-string) using the Azure CLI

    ```bash
    az iot hub device-identity show-connection-string --device-id <your device id> --hub-name <your IoT Hub name>
    ```

    It should be in the format:
    ```
    HostName=<your IoT Hub name>.azure-devices.net;DeviceId=<your device id>;SharedAccessKey=<some value>
    ```

### Send a simple telemetry message

17. [Begin monitoring for telemetry](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-iot-ext/iot/hub?view=azure-cli-latest#ext-azure-cli-iot-ext-az-iot-hub-monitor-events) on your IoT Hub using the Azure CLI

    ```bash
    az iot hub monitor-events --hub-name <your IoT Hub name> --output table
    ```

18. On your device, set the Device Connection String as an enviornment variable called `IOTHUB_DEVICE_CONNECTION_STRING`.

    ### Windows
    ```cmd
    set IOTHUB_DEVICE_CONNECTION_STRING=<your connection string here>
    ```
    * Note that there are **NO** quotation marks around the connection string.

    ### Linux
    ```bash
    export IOTHUB_DEVICE_CONNECTION_STRING="<your connection string here>"
    ```


```powershell
cmd /c "if not exist c:\test md c:\test"
Invoke-WebRequest https://raw.githubusercontent.com/Azure/azure-iot-sdk-python-preview/master/azure-iot-device/samples/simple_send_d2c_message.py -OutFile c:\test\simple_send_d2c_message.py
```

