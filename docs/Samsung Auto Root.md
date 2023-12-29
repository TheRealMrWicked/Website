---
layout: default
title: Samsung Auto Root
description: "Documentation for Samsung Auto Root."
nav_order: 3
---

# Samsung Auto Root
A program written in batch and bash that automates the process of patching the boot and recovery images on a Samsung device.

## Functions
The program is broken down into various functions they are listed below.

### dependencies()

The program downloads the dependencies it needs to function which are as follows:
adb - Used to communicate with the phone.
Samfirm.NET - Used to download the Firmware from Samsung's servers.
Magiskboot - Used to patch the .img files.

### download()

Next adb is used to collect data from the device, so the correct firmware is downloaded, 4 commands are run:

**adb shell getprop ro.product.model** - Returns the model number of the phone. e.g (SM-A546E)

**adb shell getprop ril.matchedcsc** - Returns the region code of the phone. e.g (AWS)

**adb get-serialno** - Returns the serial number of the phone. e.g (123456789)

**adb shell getprop ro.product.first_api_level** - Returns the first API Level (Android Version) of the phone.

If the device is not connected or the device is not made by Samsung the program will report accordingly.

Using the data from adb, the program uses [SamFirm.NET](https://github.com/jesec/SamFirm.NET) to download the data from Samsung's servers.

### patchboot()

Finally, the programs extracts the downloaded contents and extracts the boot.img.lz4/init_boot.img.lz4 file(s)
and transfers them along with the magisk binaries and [scripts](https://github.com/topjohnwu/Magisk/tree/master/scripts)
to the device over adb. Then it runs the scripts which inturn patch the .img files. They are then transfered to the 
computer where they are compressed into .tar file.