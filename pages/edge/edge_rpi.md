---
title: Edge Computing - Raspberry Pi
keywords: edge, embedded
tags: [edge, embedded, rpi]
sidebar: edge_sidebar
permalink: /edge_rpi
folder: edge
---

## Introduction

Website: [raspberrypi.org](https://www.raspberrypi.org/)

### Models

{% include image.html file="edge/rpi_models_tbl.PNG" url="#" 
    caption="Raspberry Pi Models; 
    [Source: wikipedia]" 
    max-width=800%}

- Quick way to identify the model on RPi
```
cat /sys/firmware/devicetree/base/model
```

Output:
```
Raspberry Pi 3 Model B Plus Rev 1.3
```

- To identify CPU hardware model and revision
```
cat /proc/cpuinfo
```

Output:
```
processor       : 0
model name      : ARMv7 Processor rev 4 (v7l)
BogoMIPS        : 38.40
Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
CPU implementer : 0x41
CPU architecture: 7
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 1
model name      : ARMv7 Processor rev 4 (v7l)
BogoMIPS        : 38.40
Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
CPU implementer : 0x41
CPU architecture: 7
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 2
model name      : ARMv7 Processor rev 4 (v7l)
BogoMIPS        : 38.40
Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
CPU implementer : 0x41
CPU architecture: 7
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 3
model name      : ARMv7 Processor rev 4 (v7l)
BogoMIPS        : 38.40
Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
CPU implementer : 0x41
CPU architecture: 7
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

Hardware        : BCM2835
Revision        : a020d3
Serial          : 00000000e5337702
Model           : Raspberry Pi 3 Model B Plus Rev 1.3
```

### Pin Layout & GPIO

{% include image.html file="edge/rpi_pins_gpio.png" url="#" 
    caption="Raspberry Pi Pins & GPIO; 
    [Source: raspberrypi.org]" 
    max-width=600%}

- The pin layout can also be displayed on the running RPi by opening 
  the terminal and issue:
```
pinout
```

Output:
```
'--------------------------------.
| oooooooooooooooooooo J8     +====
| 1ooooooooooooooooooo  PoE   | USB
|  Wi                    oo   +====
|  Fi  Pi Model 3B+ V1.3 oo      |
|        '----.               +====
| |D|    |SoC |               | USB
| |S|    |    |               +====
| |I|    '----'                  |
|                   |C|     +======
|                   |S|     |   Net
| pwr        |HDMI| |I||A|  +======
'-| |--------|    |----|V|-------'

Revision           : a020d3
SoC                : BCM2837
RAM                : 1024Mb
Storage            : MicroSD
USB ports          : 4 (excluding power)
Ethernet ports     : 1
Wi-fi              : True
Bluetooth          : True
Camera ports (CSI) : 1
Display ports (DSI): 1

J8:
   3V3  (1) (2)  5V
 GPIO2  (3) (4)  5V
 GPIO3  (5) (6)  GND
 GPIO4  (7) (8)  GPIO14
   GND  (9) (10) GPIO15
GPIO17 (11) (12) GPIO18
GPIO27 (13) (14) GND
GPIO22 (15) (16) GPIO23
   3V3 (17) (18) GPIO24
GPIO10 (19) (20) GND
 GPIO9 (21) (22) GPIO25
GPIO11 (23) (24) GPIO8
   GND (25) (26) GPIO7
 GPIO0 (27) (28) GPIO1
 GPIO5 (29) (30) GND
 GPIO6 (31) (32) GPIO12
GPIO13 (33) (34) GND
GPIO19 (35) (36) GPIO16
GPIO26 (37) (38) GPIO20
   GND (39) (40) GPIO21

For further information, please refer to https://pinout.xyz/
```

- For interactive pinout diagram, go to https://pinout.xyz/

  
In addition to IO, the GPIO pins are used for a variety of functions, such as:
PWM (pulse-width modulation), SPI, I2C and Serial. See *source* below for 
details.

*Source*: [raspberrypi.org - GPIO](https://www.raspberrypi.org/documentation/usage/gpio/)

  
### Power Up

RPi does not have BIOS. Diagnostic during booting will be based solely on the
various LEDs on the board. For all models of RPi:
- LED1: Green (labeled ACT) means SD card is connected
- LED2: Red (labeled PWR) means getting 3.3 V power, and should remain on
  
During booting sequence, the LED2 will flicker on then off, pause a moment, 
then pulse on and offf again as the boot code read off the SD card.

Refer to  
[How to fix Raspberry Pi boot problems](https://www.techradar.com/how-to/computing/how-to-fix-raspberry-pi-boot-problems-1310697)
for more details on the booting LEDs on/off sequences.


## Installation Raspbian OS

### Download the Raspbian OS binary

*Source*: [raspberrypi.org - Download](https://www.raspberrypi.org/downloads/)


### Prepare Raspbian OS on microSD card

*Source*: [Installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)


### Prepare Raspbian OS on USB Flash drive or SSD

USB mass storage boot is available out of the box on Raspberry Pi 2B v1.2, 3A+, 
3B, and 3B+ only. Support for RPi 4B in will be available in future software 
update (Per Nov 2019). **Note:** an extra step is needed for RPi 3A+ and 3B only
to enable USB host boot mode, by setting the USB host boot mode bit in the OTP 
(one-time programmable) memory.

References:

- [USB mass storage boot](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md)

### Headless Install - Finding the IP address

When installing Raspbian OS on RPI using *headless* setup, meaning RPi is not
connected to external monitor and keyboard but it has been preconfigured with
wifi setup and SSH, the IP address needs to be identified for making the SSH
connectionb.

- TBD 

### Raspbian OS version

- Check on device raspbian os version
```
uname --all
```

Output:
```
Linux raspberrypi 4.19.75-v7+ #1270 SMP Tue Sep 24 18:45:11 BST 2019 armv7l GNU/Linux
```
Note: 
- 4.19 corresponds to Debian 10 (Buster); 
- part of 4.9 & 4.14 corresponds to Debian 9 (Stretch) 

  
*Source*: [Raspbian](https://en.wikipedia.org/wiki/Raspbian)

## Setup

### Change hostname

The hostname should be letters 'a' to 'z' (upper or lower), digits '0' to '9', and 
the dash '-'.
  
Reboot is needed. 

- Change from terminal
  The `hostname` is in the `/etc/hostname`; the file contains one line only, 
  the hostname. 
```
sudo nano /etc/hostname
# change the intended hostname
```

- [Alternative] Change using raspi-config; select “Hostname” from the menu.


### SSH Keys

- TBD

- On windows
```
ls -l ~/.ssh/id_rsa.pub
```

- Copy to RPI
```
ssh-copy-id pi@raspberrypi.local
```
  
### Increase Swap Space

Increasing swap space is commonly done prior to compilation of native code, 
such as C/C++, to prevent compilation hanging due to out of memory especially 
in the multi-core complation setup.

- Swap file is defined in `/etc/dphys-swapfile`; edit the `CONF_SWAPSIZE` 
  variable in this file: 

```bash
# default value
#CONF_SWAPSIZE=100

# increase to 1024MB or 2048MB, for example
CONF_SWAPSIZE=1024
```

- Restart the service

```bash
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

- *WARNING:* for RPi running microSD card, increase swap space may result in
  shorter lifetime of the SD card due to heavy used. 
  Refer to [How to change Raspbian swapfile size](https://www.bitpi.co/2015/02/11/how-to-change-raspberry-pis-swapfile-size-on-rasbian/) for more details.

- Now ready for multi-core compilation; 

```bash
# running four cores
make -j4

# running single core
make
```

### Install Touchscreen Keyboard - Matchbox

**Prerequisite**:
- Raspbian desktop image (not lite)

- Install
```
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install --no-install-recommends matchbox-keyboard
```

- The keyboard can be started from Menu > Accesories > Keyboard

*Source*: [Matchbox Keyboard - Raspberry Pi Touchscreen Keyboard](https://thepihut.com/blogs/raspberry-pi-tutorials/matchbox-keyboard-raspberry-pi-touchscreen-keyboard)

## Backup Raspbian microSD 

RPI OS runs on microSD card which has a shorter lifetime than, for example, 
physical hard drive. Therefore, backing up the entire microSD card to a file
(`.img` file) is highly recommended to prevent failure at the least desired 
time, like in a middle of critical half-finished project.
  
For Windows, use [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)

Reference:
- https://raspberry-projects.com/pi/pi-operating-systems/win32diskimager


## Tips & Tricks

### Useful commands

- Info
```
info
```

Output:
```
File: dir,      Node: Top,      This is the top of the INFO tree.

This is the Info main menu (aka directory node).
A few useful Info commands:

  'q' quits;
  'H' lists all Info commands;
  'h' starts the Info tutorial;
  'mTexinfo RET' visits the Texinfo manual, etc.

* Menu:

Basics
* Common options: (coreutils)Common options.
* Coreutils: (coreutils).       Core GNU (file, text, shell) utilities.
* Date input formats: (coreutils)Date input formats.
* File permissions: (coreutils)File permissions.
                                Access modes.
* Ed: (ed).                     The GNU line editor
* Finding files: (find).        Operating on files matching certain criteria.
[...]
```

## Cloud hosting of RPi

Cloud hosting of Raspberry Pi at:
https://www.mythic-beasts.com/order/rpi


## Troubleshooting

### [Issue] Installing numpy

Installation of 
**Error:**

```bash
sudo apt update
pip3 install numpy
python3
>>> import numpy
Traceback (most recent call last):
[...]
ImportError: libf77blas.so.3: cannot open shared object file: No such file or directory
```

**Setup:** 
- raspbian stretch (2019-04-08-raspbian-stretch)
- fresh install + docker (19.03.1, build 74b1e89)

**Resolution:**

```bash
pip3 uninstall numpy
sudo apt install libatlas3-base
sudo pip3 install numpy
```

**Reference:**
- [Issue installing numpy python3](https://www.raspberrypi.org/forums/viewtopic.php?t=207058)