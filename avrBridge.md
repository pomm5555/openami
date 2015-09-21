
# Requirements #
Note that this has been tested with Mac OSX only.
Depending on your target platform you'll need the following:

## Cross Platform (userpace-driver) ##
Note: This hasn't yet been tested on Windows

  1. Netbeans >= 6.5.x
  1. XCode Development Tools
  1. libusb
  1. OBDev's Crosspack (AVR-Macpack before)

## PC-Linux (kernel-driver) ##
  1. 2.6 Kernel
  1. kernel headers matching your target kernel

## Embedded Linux (kernel-driver) ##
Note: although we're currently only supporting OpenWRT here, the drivers should compile on other systems as well.

  1. OpenWRT - kernel 2.4 & 2.6 are supported
  1. a buildroot environment ready to build the driver for your specific target

# Getting the Sources #
you can check out the complete source-tree here:

hg clone https://avrbridge.openami.googlecode.com/hg/ openami-avrbridge



# Building the Drivers #
## Firmware ##
**avrBridgeFirmware (target: atmega8)**

Basically here is not much to do, just check the makefile if the path set to ROOT matches your system. Also you have to adjust the programmer (here usbasp) or make flash wont work.
```
ROOT = ”/usr/local/CrossPack-AVR/bin”
AVRDUDE = $(ROOT)/avrdude -c usbasp -p $(DEVICE)
```
then just open a terminal cd into the avrBridgeFIRMWARE directory and use make to build the firmware and make flash to flash the avr.

## Host ##

### Cross-Platform ###
**[libavrBridgeC](libavrBridgeC.md)**

Here are a couple of things to do, first fire up netbeans and open the avrBridgeC project, then do the following:

1. open up the makefile, (avrBridgeC/nbproject/Makefile-Debug.mk) and check if all variables pointing to libusb like LDLIBSOPTIONS=/usr/local/lib/libusb.dylib match your libusb installation.

2. open up avrBridgeC.c and check if the following include matches your system.
```
#include ”/usr/local/CrossPack-AVR/include/usb.h”;
```
3. make sure to set the usb- vendor and product ids according to your usb device. I use the free one provided by Obdev.
```
#define USBDEV_SHARED_VENDOR 0x16C0
#define USBDEV_SHARED_PRODUCT 0x05DC
```
now the project should compile.

**[libavrBridgeJNA](libavrBridgeJNA.md)**

Just make sure the jvm can find the libAvrBridgeC.dylib, produced by avrBridgeC. You can do this by setting the system property jna.library.path to the library's absolute location. Open the project in netbeans and adjust the following line:
```
System.setProperty(“jna.library.path”, ”/Users/ka010/share/workspace/avrBridge/avrBridgeC/dist/Debug/GNU-MacOSX”);
```
### PC Linux ###
**[kmod-avrBridge-x86-2.6]**

  1. cd avrBridgeMOD/modue\_sysfs
  1. make
  1. sudo insmod avrBridge\_usbfs.ko
  1. dmesg should show:
```
usbcore: registered new interface driver avrBridge
attache avrBridge device
dmesg should show: avrBridge 2-2:1.0: avrBridge device now attached
ls /sys/bus/usb/drivers/avrBridge/2-2\:1.0 
adc0 adc1 adc2 adc3	adc4 adc5 bAlternateSetting bInterfaceClass	bInterfaceNumber bInterfaceProtocol bInterfaceSubClass bNumEndpoints bus dac0 dac1 dac2	driver	modalias pin portB portC portD power subsystem supports_autosuspend uevent
```

### Embedded Linux ###
**[kmod-avrBridge-openWRT-2.6]**

**[kmod-avrBridge-openWRT-2.4]**

# Building the Hardware #
## Schematics ##

![http://sites.google.com/site/newwiki/Home/metaboard/Bild%202.png](http://sites.google.com/site/newwiki/Home/metaboard/Bild%202.png)

## Parts ##
  1. atmega8 (dip)
  1. ic-sockel 28pin
  1. 16mhz quarz + 2x 22pf Folienkondensator oder 16mhz Quarzoszillator
  1. USB-B Buchse (right?)
  1. 2x 68ohm Widerstand
  1. 2x 100nf
  1. 2x 10uf

# Getting Started #
## Let it blink ##
## I/O Configuration ##
## Read/Write I/O ##
## ADC/DAC ##
# Advanced Topics #
# Demos #
# Sensors/Actors #
## Power Swich ##
## Motion Detector ##
## Photo Resistor ##
# API Reference #