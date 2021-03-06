<p align="center"><img class="center" src =https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/logos/logo_gcwzero_clut224.png></p>

# POCKETGO2 ROGUE CFW

Oficial firmware for Pocketgo 2

# update firmware 1.0.3: <br>
https://github.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/releases/tag/v1.0.3

# update firmware 1.0.2: <br>
https://github.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/releases/tag/v1.0.2

# update firmware 1.0.1: <br>
https://github.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/releases/tag/v1.0.1

## Changelog:<br>

### 1.0.3:<br>

1. Fixed and updated SDL2 libraries.
2. Insert Scriptrunner app, now you can format the external sdcard in fat32, exfat or ext3 in the console.
3. Fixed errors in games that not run.
4. Fixed R2 time reactions.
5. Recompiled PCSX4ALL
6. Fixed Gmenu2x duplicate icons when this is edit

### 1.0.2:<br>

1. Fix clock hour reset when poweroff the console.
2. Gmenu2x now can show two type of previews (put in /(romsdir)/.previews/).
3. ajust the joystick (again).

### 1.0.1:<br>

1. Updated the file system, partition and expansion scripts again.
2. Gmenu2x analog stick control is removed
3. Adjusted the battery.
4. Update of the Stock Clock application with a new redesign. thanks to Rafa Vico (https://github.com/RafaVico)
![](https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/screenshots/screenshot011.png)
![](https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/screenshots/screenshot012.png)
5. Text editor, corrected opk buttons. thanks to Rafa Vico (https://github.com/RafaVico)
6. Added the hardware tester POCKETGO 2. thanks to Rafa Vico (https://github.com/RafaVico)
![](https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/screenshots/screenshot008.png)
![](https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/screenshots/screenshot009.png)
![](https://raw.githubusercontent.com/Ninoh-FOX/POCKETGO2_ROGUE_CFW/master/screenshots/screenshot010.png)

# features:

1. Support to read the second sdcard in fat32, exFAT, ntfs, ext4 (recommended) and ext3 format.

NOTE: for that the ext4 sdcard works, you need format this from command lines since the console, if you go to use the pc, then format in ext3.

2. Added key combinations with the power button:
+ POWER + VOL + or VOL-: Adjust the brightness of the screen.
+ POWER + SELECT: Close the current application.
+ POWER + START: Restart the console.
+ POWER + B: The analog stick will work as DPAD.
+ POWER + A: Change the aspect ratio with the screen in Hardware mode.
+ POWER + R1: Mouse emulation (Stick is movement and the L2 and R2 buttons the buttons)
+ POWER + DPAD up / dowm: Adjust the sharpness.
+ POWER + X: Take a screenshot.
    
3. In Gmenu2x the power button can turn the screen off or on.

4. You can change the cpu to maximum or minimum in gmenu2x for the opk, the same to change the name, description, icon and file filter.

# Installation:

For a correct installation, the first time it is advisable to flash the sd_image in an sdcard with Win32DiskImager for example, too you need format the sdcard two times with SD Formatter before of flasher the sdcard.

https://sourceforge.net/projects/win32diskimager/

if W32DI NOT WORK fine, try them https://www.balena.io/etcher/ or you can type in a terminal the follow command: 

sudo dd if=sd_image.bin of=/dev/(sdcard_partition)

https://www.sdcard.org/downloads/formatter/

One time that the program finish, put the sd in the console, NOT RESIZE THE PARTITION FROM PC!! The firmware has a script for auto resize!!

You can also use flasher.opk for the same, but it takes much longer and being a console that has the SD1 (TF1) of the system at hand because I do not see it really necessary, even so, it is in the release. If you would like to use it, it is advisable to put it in the apps folder of the SD2 (TF2).

For future updates you will only need to use the update.opk, which is used just like any application launched from GMENU2X. You can use it in both the apps folder of SD1 (TF1) or SD2 (TF2).

# BUILDING the code:

First you need a pc or vm with Debian 9.11 64 bits.

### Pre-Build Steps ###

$ sudo apt-get update

$ sudo apt-get install bison flex gettext texinfo wget cpio python unzip mercurial subversion libncurses5-dev libc6-dev-i386 bzr squashfs-tools
## you need a javac compiler, (i.e. sudo apt-get install gcj-4.9-jdk)

### Build Steps ###

## Enter the directory where you want to clone the git repo
## This assumes that you have a clean buildroot/dl and buildroot/output directory 

$ git clone https://github.com/Ninoh-FOX/toolchain.git

$ cd toolchain

$ make rg350_defconfig BR2_EXTERNAL=board/opendingux

$ make

# To generate upgrade image

$ . board/opendingux/gcw0/make_upgrade.sh

======================================================


To build and use the buildroot stuff, do the following:

1) run 'make menuconfig'
2) select the packages you wish to compile
3) run 'make'
4) wait while it compiles
5) Use your shiny new root filesystem. Depending on which sort of
    root filesystem you selected, you may want to loop mount it,
    chroot into it, nfs mount it on your target device, burn it
    to flash, or whatever is appropriate for your target system.

You do not need to be root to build or run buildroot.  Have fun!

Offline build:
==============

In order to do an offline-build (not connected to the net), fetch all
selected source by issuing a

$ make source

before you disconnect.
If your build-host is never connected, then you have to copy buildroot
and your toplevel .config to a machine that has an internet-connection
and issue "make source" there, then copy the content of your dl/ dir to
the build-host.

Building out-of-tree:
=====================

Buildroot supports building out of tree with a syntax similar
to the Linux kernel. To use it, add O=<directory> to the
make command line, E.G.:

$ make O=/tmp/build

And all the output files (including .config) will be located under /tmp/build.

More finegrained configuration:
===============================

You can specify a config-file for uClibc:

$ make UCLIBC_CONFIG_FILE=/my/uClibc.config

And you can specify a config-file for busybox:

$ make BUSYBOX_CONFIG_FILE=/my/busybox.config

To use a non-standard host-compiler (if you do not have 'gcc'),
make sure that the compiler is in your PATH and that the library paths are
setup properly, if your compiler is built dynamically:

$ make HOSTCC=gcc-4.3.orig HOSTCXX=gcc-4.3-mine

Depending on your configuration, there are some targets you can use to
use menuconfig of certain packages. This includes:

$ make HOSTCC=gcc-4.3 linux-menuconfig

$ make HOSTCC=gcc-4.3 uclibc-menuconfig

$ make HOSTCC=gcc-4.3 busybox-menuconfig

Please feed suggestions, bug reports, insults, and bribes back to the
buildroot mailing list: buildroot@buildroot.org

Build the kernel:
===============================

Download this git
Go to kenel folder.

$ make ARCH=mips pocketgo2_defconfig

$ make ARCH=mips vmlinuz.bin -j4

$ make ARCH=mips modules -j4

$ ./create_modules_fs.sh

