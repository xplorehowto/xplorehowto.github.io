---
title: Edge Computing - Raspberry Pi
keywords: edge, embedded
tags: [edge, embedded, rpi]
sidebar: edge_sidebar
permalink: /edge_rpi
folder: edge
---

## Introduction

Compilation of tips, tricks, troubleshooting issues, etc.


## Tips & Tricks

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

### Backup raspbian SD 

RPI OS runs on microSD card which has a shorter lifetime than, for example, 
physical hard drive. Therefore, backing up the entire microSD card to a file
(`.img` file) is highly recommended to prevent failure at the least desired 
time, like in a middle of critical half-finished project.
  
For Windows, use [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/)

Reference:
- https://raspberry-projects.com/pi/pi-operating-systems/win32diskimager

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