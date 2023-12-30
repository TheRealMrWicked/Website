---
layout - default
title - Magisk Utilities
description - "Documentation for the Magisk Utilities Program."
nav_order - 2
---

# Magisk Utilities
A program that automates various tasks related to rooting/patching Android devices using
Magisk.

## Main Functions
### dependencies()
```
Downloads the dependencies needed for the other functions to work correctly:
adb - Used to communicate with a connected Android device.
Samfirm.NET - Used to download the Firmware from Samsung's servers.
Magiskboot - Used to patch Android .img files.
```

### adbroot(bootimage)
```
Arguments:
bootimage - The .img file to be patched.

Transfers the supplied file, as well as the magisk dependencies to the connected Android
device using adb. It then runs the original boot_patch.sh script on device to patch the
file and transfers the patched file back to the computer.
```

### localroot(bootimage, prefix)
```
Arguments:
bootimage - The .img file to be patched.
prefix - Used to run commands depending on the OS.

A rewrite of Magisk's boot_patch.sh, it uses Magiskboot to patch .img files on the
computer, it functions very similar except there is one issue. Magisk need to write
SELINUX rules in a partition, and the partition to be used is determined by the magisk 
binaries in Android. However, this is impossible because this function is running on
a desktop OS, and is unaware of the partition statuses.

**NOTE - Based on the information above it is highly recommended to connect the device
over adb, to use the "adbroot" function. If you still want to continue with local
patching, ensure that you reinstall Magisk using the "Direct Install Method" in the
Magisk app after flashing the boot image.**
```

### patchrecovery(recoveryimage, prefix)
```
Arguments:
recoveryimage - The .img file to be patched.
prefix - Used to run commands depending on the OS.

Patches the recovery file of Samsung devices to re-enable fastbootd mode.

**NOTE - This should only be run on recovery images from Samsung devices that launched
with Android 10 (API Level 29) or higher. If you are unsure you can either research it
or use the "samsungroot" function (-sr argument).**
```

### samsungdownload(prefix)
```
Arguments:
prefix - Used to run commands depending on the OS.

Uses "adb getprop" to retrieve the model, region, serial number and the first Android
version of a connected device. If a device is not connected or not made by Samsung
it will notify the user accordingly. It then downloads the latest Firmware for the
respective model of device using SamFirm.NET into the "Firmware" folder.
```

### samsungroot(prefix)
```
Arguments:
prefix - Used to run commands depending on the OS.

Runs the "samsungdownload" and "adbroot" functions to download and root the boot image
file for a connected Samsung device.
```

## Utility/Miscellaneous Functions
### decompress(file, prefix)
```
file - The file to be decompressed to a .img.
prefix - Used to run commands depending on the OS.

Decompresses files to the .img format using Magiskboot.
```

### help()
```
Displays a help message.
```

### oscheck()
```
Determines if the OS is supported.

Returns a prefix for commands.
```

### unzip(zip, srcfile, dstfile)
```
Arguments:
zip - The zip file to extract the file from.
srcfile - The file that is being extracted from the zip.
dstfile - The name and location to place the extracted file.

Extracts a specific file from a zip.
```

### wildcardrename(oldname, newname)
```
Arguments:
oldname - The orginal name of the file or folder.
newname - The new name of the file or folder.

Uses pattern matching (wildcards) to rename files.
```

### bulkdelete(filetype, directory)
```
Arguments:
filetype - The type of files to delete.
directory - The location of the files to be deleted.

Deletes all files of a given type, in a specific directory.
```

### moveallfiles(src, dst)
```
Arguments:
src - Orginal directory of files.
dst - New directory to place files into.

Moves all files from a given directory to a new one.
```