# Board Support Packages

A Board Support Package(BSP) includes a set of device drivers that are specific to the components/silicon used in the board. These are provided by the component vendors / silicon vendors, mostly in the form of .inf and associated .sys/.dll files. A BSP is a collection of drivers/settings required to run IoT Core on a hardware platform. These are provided by the hardware vendors/silicon vendors.

There are two steps to creating your own BSP:

First, find where you can get BSPs for supported platforms below.
Second, learn how to create your own BSP by following the steps listed in the IoT Manufacturing guide.

## Raspberry Pi BSP
Steps to create the drivers :

1. Check out ms-iot/bsp project.
2. Build the bcm2386 solution (Release or Debug)
    * You can also download the prebuilt binaries from rpibsp_wm.zip.
3. Launch IoTCoreShell, select arm
   * In ms-iot/bsp project folder, run tools\binexport.cmd Release (or) Debug C:\RPiBSP to export the binaries to C:\RPiBSP folder. If you are using prebuilt binaries, you can skip this step and unzip the binaries to C:\RPiBSP.
   * Run C:\RPiBSP\build.cmd to create the cabs in the build output folder (iot-adk-addonkit\Build\arm\pkgs)
   * Run buildpkg all to process all cab files

## Intel BSPs
### Apollo Lake / Braswell / Cherry trail
The BSP supporting Apollo Lake is available at Apollo Lake BSP.

The BSP supporting Braswell/Cherry trail are available at Braswell BSP.

Follow the steps below to use this BSP with the Windows 10 ADK release 1709 (16299) with iot-adk-addonkit version 4.0 or later.

1. Download the BSP package and install
2. Copy files from C:\Program Files (x86)\Intel IoT\Source-<arch> to iot-adk-addonkit\Source-<arch>
3. Launch IoTCoreShell, select arch (x64 / x86) as required
4. In the IoTCoreShell, run the below command to convert the BSP files to latest format and build
    * run .\bsptools\<bspname>\convert.cmd
    * buildbsp <bspname>
5. For serial support (FILL IN BLANK HERE with Win8 Drivers??)

### KabyLake

## Qualcomm BSPs
### DragonBoard 410C
DragonBoard drivers are available at DragonBoard 410C Software under Windows 10 IoT Core section.

Steps to create the drivers :

1. Download the *_db410c_BSP.zip and extract to a folder say C:\download\DB410c_BSP
2. Launch IoTCoreShell, select arm
    * Run .\bsptools\QCDB410C\export.cmd C:\download\DB410c_BSP C:\MyBSPs\QCDB410C to export the required bsp cab files to a directory say C:\MyBSPs\QCDB410C.
    * set BSPPKG_DIR=C:\MyBSPs\QCDB410C to specify the location of the bsp cabs. See the BSPFM.xml file for the cab files it looks for in BSPPKG_DIR.
    * Run buildpkg all to create the oem packages
    * Run buildimage <productname> <test> or <retail> to build the image
