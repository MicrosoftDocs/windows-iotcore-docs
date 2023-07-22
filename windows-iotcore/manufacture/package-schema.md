---

description: Windows Universal OEM Package Schema
ms.assetid: cbae6949-ccfe-4015-a9b0-a269f6f30d5a
MSHAttr: 'PreferredLib:/library'
title: Windows Universal OEM Package Schema

ms.date: 09/02/2017
ms.topic: article


---

# Windows Universal OEM Package Schema

You can manually edit your packages using the Universal OEM Package Schema.

[Creating Windows Universal OEM Packages](create-packages.md)



## Schema
Only the common elements and attributes are documented here.  

To get the full schema run "pkggen /universalbsp /wmxsd:.", then open **WM0.XSD** with Visual Studio.  

### identity

|Attribute |Type   |Required|Macro |Notes |
|----------|-------|--------|------|------|
|owner     |string |*       |      |      |
|name      |string |*       |*     |      |
|namespace |string |        |*     |      |
|buildWow  |boolean|        |      |Default = false, set to true to generate WOW packages|
|legacyName|string |        |*     |Uses the specified name as the package name overriding the default name (owner-namespace-name.cab).|

```xml
<identity name="FeatureName" namespace="FeatureArea" owner="OEM" buildWow="false"/>
```

### onecorePackageInfo

|Attribute      |Type                                 |Required|Macro |Notes                                                       |
|---------------|-------------------------------------|--------|------|------------------------------------------------------------|
|targetPartition|MainOS  Data  UpdateOS  EFIESP  PLAT |*       |      |If onecorePackageInfo is not specified, Default = MainOS    |
|releaseType    |Production   Test                    |        |      |If onecorePackageInfo is not specified, Default = Production|

```xml
<onecorePackageInfo targetPartition="MainOS" releaseType="Production"/>
```

### file

|Attribute     |Type   |Required|Macro |Notes                                                                             |
|--------------|-------|--------|------|----------------------------------------------------------------------------------|
|source        |string |*       |*     |                                                                                  |
|destinationDir|string |        |*     |destinationDir must start with one of the following built in runtime macros below.|
|name          |string |        |      |used to rename the source file                                                    |
|buildFilter   |string |        |      |                                                                                  |

destinationDir must start with:
- $(runtime.bootDrive)
- $(runtime.systemDrive)
- $(runtime.systemRoot)
- $(runtime.windows)
- $(runtime.system32)
- $(runtime.system)
- $(runtime.drivers)
- $(runtime.help)
- $(runtime.inf)
- $(runtime.fonts)
- $(runtime.wbem)
- $(runtime.appPatch)
- $(runtime.sysWow64)
- $(runtime.mui)
- $(runtime.commonFiles)
- $(runtime.commonFilesX86)
- $(runtime.programFiles)
- $(runtime.programFilesX86)
- $(runtime.programData)
- $(runtime.userProfile)
- $(runtime.startMenu)
- $(runtime.documentSettings)
- $(runtime.sharedData)
- $(runtime.apps)
- $(runtime.clipAppLicenseInstall)
- If not specified, the default is $(runtime.system32) 

To see the directories that map to these locations, see C:\Program Files (x86)\Windows Kits\10\tools\bin\i386\pkggen.cfg.xml.

```xml
<file buildFilter="(not build.isWow) and (build.arch = arm)" name="output.dll" source="$(_RELEASEDIR)\input.dll" destinationDir="$(runtime.system32)"/>
```

### regKey

|Attribute      |Type   |Required|Macro |Notes |
|---------------|-------|--------|------|------|
|keyName        |string |*       |*     |keyName must start with $(hklm.system), $(hklm.software), $(hklm.hardware), $(hklm.sam), $(hklm.security), $(hklm.bcd), $(hklm.drivers), $(hklm.svchost), $(hklm.policies), $(hklm.microsoft), $(hklm.windows), $(hklm.windowsnt), $(hklm.currentcontrolset), $(hklm.services), $(hklm.control), $(hklm.autologger), $(hklm.enum), $(hkcr.root), $(hkcr.classes), $(hkcu.root), $(hkuser.default)| 
|buildFilter    |string |        |      |      |

To see the registry keys that map to these locations, see C:\Program Files (x86)\Windows Kits\10\tools\bin\i386\pkggen.cfg.xml.

```xml
<regKey buildFilter="buildFilter1" keyName="keyName1">
  <regValue buildFilter="buildFilter1" name="name1" value="value1" type="REG_SZ" />
</regKey>
```

### regValue

|Attribute      |Type   |Required|Macro |Notes  |
|---------------|-------|--------|------|-------|
|name           |string |        |      |Name of the value you are specifying. If not specified, the Default value in the key will be over-written|
|type           |string |*       |      |type must be one of these: REG_SZ, REG_MULTI_SZ, REG_DWORD, REG_QWORD, REG_BINARY, REG_EXPAND_SZ|
|value          |string |        |      |       |
|buildFilter    |string |        |      |       |

```xml
<regKey buildFilter="buildFilter1" keyName="keyName1">
  <regValue buildFilter="buildFilter1" name="name1" value="value1" type="REG_SZ" />
  <regValue buildFilter="buildFilter2" name="name2" value="value1,value2" type="REG_MULTI_SZ" />
  <regValue buildFilter="buildFilter3" name="name3" value="00000000FFFFFFFF" type="REG_QWORD" />
  <regValue buildFilter="buildFilter4" name="name4" value="FFFFFFFF" type="REG_DWORD" />
  <regValue buildFilter="buildFilter5" name="name5" value="0AFB2" type="REG_BINARY" />
  <regValue buildFilter="buildFilter6" name="name6" value="&quot;%ProgramFiles%\MediaPlayer\wmplayer.exe&quot;" type="REG_EXPAND_SZ" />
</regKey>
```

