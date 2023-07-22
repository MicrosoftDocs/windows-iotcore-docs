---

description: 'Update the time server on IoT Core devices'
MSHAttr: 'PreferredLib:/library'
title: 'Update the time server'

ms.date: 05/02/2017
ms.topic: article


---

# Update the time server

By default, IoT Core devices are setup to synchronize time from time.windows.com.  If you don’t have internet connectivity or behind a firewall, then you’ll need to synchronize the system time for your IoT Core devices to a time server reachable in your network.  You can change the time server or add multiple time servers using the information below.

## Update the server from a command line (for example, using a tool like PuTTY):

1.	 Identify the required NTP server(s) and make sure you can reach them from your network. For example, if time.windows.com, NTPServer1, NTPServer2 are the three desired NTP servers, make sure the following commands succeed when run on a Windows computer on the network before using in an IoT device:
     ```
     W32tm.exe /stripchart /computer:time.windows.com /samples:5
     W32tm.exe /stripchart /computer:NtpServer1 /samples:5
     W32tm.exe /stripchart /computer:NtpServer2 /samples:5
     ```

2.	Modify the W32Time service configuration on the IoT device to use your NTP time server(s).
    ```
    reg add HKLM\SYSTEM\CurrentControlSet\Services\w32time\Parameters /v NtpServer /t REG_SZ /d "time.windows.com,0x9 NtpServer1,0x9 NtpServer2,0x9 " /f >nul 2>&1
    ```

3.	Restart the time service
    ```
    net stop w32time
    net start w32time
    ```

4.	Verify the time servers from which the device is currently receiving time.If you restarted the time service, allow a minute or so before verifying the time service.
    ```
    W32tm.exe /query /peers
    ```

## Update the server in an IoT Core image

1.	Create a package definition file, and add it to the image. To learn more, see [Lab 1c: Add a file and a registry setting to an image](add-a-registry-setting-to-an-image.md). Sample script: 

	``` xml
    <regKeys>
        <regKey
            keyName="$(hklm.system)\CurrentControlSet\Services\w32time\Parameters">
            <regValue name="NtpServer" type="REG_SZ"
                value="time.windows.com,0x9 NtpServer1,0x9 NtpServer2,0x9" />
        </regKey>
    </regKeys>
    ```
