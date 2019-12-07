---
title: Edge Computing - Raspberry Pi
keywords: edge, embedded
tags: [edge, embedded, rpi]
sidebar: edge_sidebar
permalink: /edge_rpi
folder: edge
---

## Introduction

Website: [raspberrypi.org](https://www.raspberrypi.org/){:target="_blank"}

### Models

{% include image.html file="edge/rpi_models_tbl.PNG" url="#" 
    caption="Raspberry Pi Models; 
    [Source: wikipedia]" 
    max-width=800%}

Quick way to identify the model on RPi
```bash
cat /sys/firmware/devicetree/base/model
```
Output:
```
Raspberry Pi 3 Model B Plus Rev 1.3
```

To identify CPU hardware model and revision
```bash
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

The pin layout can also be displayed on the running RPi by opening 
the terminal and issue:
```bash
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

Also checkout the web-based interactive pinout diagram, go to 
[https://pinout.xyz/](https://pinout.xyz/){:target="_blank"}

    
In addition to IO, the GPIO pins are used for a variety of functions, such as:
PWM (pulse-width modulation), SPI, I2C and Serial. 
See [raspberrypi.org - GPIO](https://www.raspberrypi.org/documentation/usage/gpio/){:target="_blank"}
for more details.

  
### Power Up

RPi does not have BIOS. Diagnostic during booting will be based solely on the
various LEDs on the board. For all models of RPi:
- LED1: Green (labeled ACT) means SD card is connected
- LED2: Red (labeled PWR) means getting 3.3 V power, and should remain on
  
During booting sequence, the LED2 will flicker on then off, pause a moment, 
then pulse on and offf again as the boot code read off the SD card.
  
[How to fix Raspberry Pi boot problems](https://www.techradar.com/how-to/computing/how-to-fix-raspberry-pi-boot-problems-1310697){:target="_blank"}
provides more details about the booting LEDs on/off sequences.


## Installation Raspbian OS

### Download the Raspbian OS binary

The [raspberrypi.com Download](https://www.raspberrypi.org/downloads/){:target="_blank"}
page provides download for Raspbian OS and links to other OS*es* such as:
Windows 10 IoT Core, OSMC, Mozilla Web Thing, etc.

The latest version of Raspbian can be found [here](https://www.raspberrypi.org/downloads/raspbian/){:target="_blank"}. 
The **older versions** can be found on the
[download archive](http://downloads.raspberrypi.org/raspbian/images/){:target="_blank"}
  
There are three packages to choose from depending on usage, and they varies in size:
- Raspbian Buster with desktop and recommended software
- Raspbian Buster with desktop
- Raspbian Buster Lite; 

The *Lite* version is suitable for server or most edge devices that does not need 
access to UI during operation but access using 
[*headless mode*](https://en.wikipedia.org/wiki/Headless_software){:target="_blank"}.
  
<span class="label label-default">Instructions:</span> 
- Download the Raspbian OS *ZIP* file to a **computer** from
  [Raspberry Pi download](https://www.raspberrypi.org/downloads/raspbian/){:target="_blank"}; 

{% include note.html content="Don't unzip the file. It will later be red as is 
using the balenaEtcher tool." %}

### Prepare Raspbian OS 

Two types of media for storing the OS image are discussed below:
- the default raspberry microSD card
- external USB Flash drive or SSD 

#### Writing the OS image to microSD card

**Notes:** 
- Choosing the size of microSD card:
  - For SD card *up to 32 GB*, flashing to SD card can be easily done using 
    **Etcher** as discussed below. 
    [Source](https://www.raspberrypi.org/documentation/installation/installing-images/README.md){:target="_blank"}

  - For SD card of *64GB or larger*, also known as *SDXC card*, it needs to be
    formatted with the *exFAT filesystem*. Please refer to
    [SDXC formatting](https://www.raspberrypi.org/documentation/installation/sdxc_formatting.md){:target="_blank"}
    for more detailed discussion.

- balenaEtcher is the recommended tool to write OS image, for its ease of use. 

<span class="label label-default">Instructions:</span> 
- Follow [Installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md){:target="_blank"}

- The quick checklist is as follow:  
  - If not already, download the latest version of 
    [balenaEtcher](https://www.balena.io/etcher/){:target="_blank"}
    and install it.
  - Insert the SD card to the SD card reader; most laptops has built in reader
  - Run balenaEtcher and follow four steps below:
    - Select the downloaded zip file OS image from the laptop hard drive
    - Select the SD card you wish to write your image to
    - Review & review again the selections

      {% include warning.html content="Please **ENSURE** the selected SD drive is the intended drive.
      Special caution especially when you have more than one drive. 
      The next step will wipe out all the existing data in the drive and **irreversible!**" %}
  
    - Once you are confident, Click `Flash!` to start writing OS files to the SD card

  - Flashing takes a while. Once complete, the boot drive may not be visible 
    on Windows 10 laptop until the SD card is ejected & re-inserted. 
    The boot drive should be visible on, for example `D:` drive or other, 
    depending on the drive setup on the laptop.
  - Next, proceed with [Preboot Setup](#pre-boot-setup)


#### Writing the OS image to USB Flash drive or SSD

USB mass storage boot is available out of the box on Raspberry Pi 2B v1.2, 3A+, 
3B, and 3B+ only. Support for RPi 4B in will be available in future software 
update (Per Nov 2019). **Note:** an extra step is needed for RPi 3A+ and 3B only
to enable USB host boot mode, by setting the USB host boot mode bit in the OTP 
(one-time programmable) memory.

<span class="label label-default">Instructions:</span> 
- *TBD*

Source: 
[USB mass storage boot](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md){:target="_blank"}

### Pre-boot Setup

The OS media can be provisioned prior to starting the 
[*first boot*](#first-boot-on-raspberry-pi) on the RPi.
The pre-boot setup is to do away with the need for RPi to be connected to 
monitor and keyboard during the first boot process, and RPi will be ready in
*headless* mode after bootup. 
  
Headless mode means RPi can be access remotely
from another computer using `ssh` but it requires the "ssh server" and "wifi" 
to be enabled on RPi. 
  
Pre-boot setup is commonly done on the raspbian lite OS
because it does not have the desktop UI installed, and it is typically not 
connected to keyboard or monitor, and accessed from remote computer using `ssh`.
This is a typical edge devices setup. The preboot setup involves creating 
new file or modifying existing file on the boot drive. 
The content of the boot drive will be copied to the OS folder during
*first boot* process.
  
<span class="label label-default">Instructions - Windows:</span>
- The following instructions are to be performed on the computer or laptop

- Open file explorer, make sure the boot drive is 
  visible; for example, `D:` drive or other depending on the computer drive 
  setup. If the boot drive is not visible, ejected & re-inserted the microSD
  card. Otherwise, the microSD card may not be flashed properly.

- **Enabled wifi network** - create a blank file named `wpa_supplicant.conf` in 
  boot drive. This file enables the OS to connect to the specified wireless 
  network. 
  - Open command prompt in Admin mode, run the following 
    command, which creates a blank *wpa_supplicant.conf* in the `boot`
    drive
    
    {% include warning.html content="the following command assumes the
    microSD card is connected as drive letter E" %}

    ```
    C:\>fsutil file createnew E:\wpa_supplicant.conf 0
    ```
    
    {% include note.html content="the file can also be created directly 
    from File Explorer; or copy existing file to the microSD card." %}
    
  - open text editor and add the following to *wpa_supplicant.conf* file
    ```
    country=US
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    network={
      ssid="<wifiSSID>"
      psk="<wifiPassword>"
      key_mgmt=WPA-PSK
    }
    ```
    replace `<wifiSSID>` and `<wifiPassword>` with values from the target wifi.
    Depending on the country & wifi router type, adjust `country=US` and
    `key_mgmt=WPA-PSK` accordingly.
    
    See [Rapsberry Pi guide on wireless](https://www.raspberrypi.org/documentation/configuration/wireless/){:target="_blank"}

- **Enabled SSH connection** to RPi from other computer after first boot to 
  perform additional configurations or administration tasks, or application 
  setup. 
  - For Windows, in the same command prompt, run the following command, 
    which creates a blank file named `ssh` in the `boot` drive. 
    
    {% include warning.html content="the following command assumes the
    microSD card is connected as drive letter E" %}
    ```
    C:\>fsutil file createnew E:\ssh 0
    ```

- **Configure GPU memory allocation** as follows:
  - if running Raspbian desktop OS, skip this step
  - if running Raspbian desktop OS with Pi Camera attached, see the next step
    for how to allocate `gpu_mem`
  - if running Raspbian lite OS, the `gpu_mem` allocation can be set to the lowest
    or 16 MB

- **Enable Pi Camera** [Optional] - edit `config.txt` file and add the 
  following lines:
  ```
  start_x=1
  gpu_mem=128           
  disable_camera_led=1
  ```
  - need at 128 MB GPU memory
  - optional, to turn-off the led while camera in use, set to 
    `disable_camera_led=1`

  - Next proceed to the [first boot](#first-boot-on-raspberry-pi)


### First boot on Raspberry Pi

<span class="label label-default">Instructions:</span> 
- Perform the following instructions on the raspberry pi

- Insert the SD card into the Rapsberry Pi and **start the first boot** process
  - For RPi with connected monitor, mouse and keyboard, proceed to login using
    the UI
  - For headless RPi, not connected to monitor, mouse and keyboard,
    use SSH client software, such as [putty](https://www.putty.org/){:target="_blank"}, 
    to connect to RPi, as discussed next below.
    
- [Optional] **SSH connection** to headless RPi. Since the RPi is headless,
  there is no visual way to know if the booting process is complete.
  Luckily, the raspbian OS has been pre-configured by default with the
  hostname equals to `raspberrypi`, and the raspbian buster OS comes
  with preinstalled Multicast Domain Name Service (mDNS) called `avahi-daemo`.
  Therefore, you should be able to `ping` or `ssh` the host using the hostname.
  A reply to the `ping` indicates the boot process has completed and ready for
  `ssh` connection
  ```
  ping raspberrypi
  ```
  
  Output:  
  ```
  Pinging raspberrypi.attlocal.net [192.168.1.105] with 32 bytes of data:
  Reply from 192.168.1.105: bytes=32 time=5ms TTL=64
  Reply from 192.168.1.105: bytes=32 time=5ms TTL=64
  Reply from 192.168.1.105: bytes=32 time=5ms TTL=64
  Reply from 192.168.1.105: bytes=32 time=6ms TTL=64

  Ping statistics for 192.168.1.105:
      Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
  Approximate round trip times in milli-seconds:
      Minimum = 5ms, Maximum = 6ms, Average = 5ms
  ```

- **Login** using the default (userid, password) = (pi, raspberry)
  and start post-configure RPi using the `sudo raspi-config` including: change password, 
  setup country, language, timezone, keyboard.


### Headless Install - Finding the IP address

When installing Raspbian OS on RPI using *headless* setup, meaning RPi is not
connected to external monitor and keyboard but it has been preconfigured with
wifi setup and SSH, the IP address needs to be identified for making the SSH
connection.

- TBD 

### Raspbian OS version

Check on device raspbian os version
```bash
uname --all
```

Output:
```
Linux raspberrypi 4.19.75-v7+ #1270 SMP Tue Sep 24 18:45:11 BST 2019 armv7l GNU/Linux
```
Note: 
- 4.19 corresponds to Debian 10 (Buster); 
- part of 4.9 & 4.14 corresponds to Debian 9 (Stretch) 

  
Source: [Raspbian](https://en.wikipedia.org/wiki/Raspbian){:target="_blank"}

## Setup

### Change hostname

The hostname should be letters 'a' to 'z' (upper or lower), digits '0' to '9', and 
the dash '-'.
  
Reboot is needed. 
  
From the terminal, change the `hostname` in the `/etc/hostname` file; 
the file contains one line only, and it's the hostname. 
```bash
sudo nano /etc/hostname
# change to the intended hostname
```
  
[Alternative] Change using raspi-config; select “Hostname” from the menu.


### Generate SSH Keys and Transfer to remote host 

Create cryptographic SSH private/public keys to SSH connect to RPi without
entering username and password.

<span class="label label-default">Instructions - Windows:</span>
- On the Windows computer, generate the SSH keys
  ```
  cd /Users/<username>/.ssh
  # create the .ssh folder if it does not exist 
  ssh-keygen -t rsa
  ```

- Choose no passphrase when asked and accept the default filename of `id_rsa`.
  This creates both the id_rsa *private key file* and *public key file*. 
  Keep the private key on the safe place, and copy the public key to the 
  host to be connected to, i.e., RPi.
  ```
  cd /Users/<username>/.ssh
  dir id_rsa.pub
  ```

- Copy the public key to RPi using WinSCP as described [here](#scp---secure-copy)
  - After WinSCP login to RPi, the left column shows the folders on the local
    Windows host; the right column shows the folders on the remote host, RPi.
  - On the local host (left column), navigate to the `/Users/<username>/.ssh`; the
    public key, `id_rsa.pub`, should be visible
  - On the RPi host (right column), navigate to `~/.ssh`
  - drag the file from left to right
  - after successful copy, rename the file, `id_rsa.pub`, to `authorized_keys`;
  - if the `authorized_keys` file already exists then need to append the content
    of `id_rsa.pub`, to `authorized_keys` by right clicking each file to open it
    using the built-in editor, and copy & paste the content.
  - Note: on the debian linux host, the key can be copied directly from the
    local to remote host using:
    ```
    ssh-copy-id pi@raspberrypi.local
    ```

- Now, [SSH client](#ssh-1) (putty) and [SCP client](#scp---secure-copy) (WinSCP)
  can be setup to connect without using username/password

Source: 
- [SSH without password](https://www.tunnelsup.com/ssh-without-password/){:target="_blank"}
- [Setting up ssh keys on RPi](https://www.raspberrypi-spy.co.uk/2019/02/setting-up-ssh-keys-on-the-raspberry-pi/){:target="_blank"}

  
### Increase Swap Space

Increasing swap space is commonly done prior to compilation of native code, 
such as C/C++, to prevent compilation hanging due to out of memory especially 
in the multi-core complation setup.

<span class="label label-default">Instructions:</span>
{% include warning.html content="increase swap space may result in
  shorter lifetime of the SD card due to heavy used" %}

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

- Now ready for memory intensive task such as multi-core compilation; 
  ```bash
  # running four cores
  make -j4

  # running single core
  make
  ```

Source: [How to change Raspbian swapfile size](https://www.bitpi.co/2015/02/11/how-to-change-raspberry-pis-swapfile-size-on-rasbian/){:target="_blank"}

### Mount USB Drive

Tasks related to mounting USB drive include:
- format the drive
- mount the drive
- unmount

#### Format USB drive 

<span class="label label-default">Instructions:</span>
- Identify which device is the USB stick by removing it (if it is plugged in) 
  and then reconnect it. This will generate some messages about the device in 
  the system messages file. View the last few lines to identify your device.  
  The USB device will be named something like sda, sdd, etc.
  ```bash
  cat /var/log/messages | tail -n 50
  ```
    
  Unnless there are other usb drives, it should be `/dev/sda`

- RPi will automatically mount USB drive
  ```bash
  cd /media
  ls -al usbdisk
  ```

- Check the partition on the USB disk using `fdisk` command
  ```bash
  sudo fdisk /dev/sda
  ```

  Output:
  ```
  Welcome to fdisk (util-linux 2.33.1).
  Changes will remain in memory only, until you decide to write them.
  Be careful before using the write command.


  Command (m for help):
  ```

- Enter `p` to see all the partitions that already exist
  ```
  Disk /dev/sda: 57.9 GiB, 62176362496 bytes, 121438208 sectors
  Disk model: Ultra Fit
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 512 bytes
  I/O size (minimum/optimal): 512 bytes / 512 bytes
  Disklabel type: dos
  Disk identifier: 0x00000000

  Device     Boot Start       End   Sectors  Size Id Type
  /dev/sda1       21952 121438207 121416256 57.9G  c W95 FAT32 (LBA)

  Command (m for help):
  ```

- **Delete** all the partitions by entering `d`
  ```
  Selected partition 1
  Partition 1 has been deleted.

  Command (m for help):
  ```

- Create **new partition** and use the USB drive as a single partition 
  by typing `n` and follow the output below:
  ```
  Partition type
     p   primary (0 primary, 0 extended, 4 free)
     e   extended (container for logical partitions)
  Select (default p):
  ```

  - press `enter` to accept "p" as primary, and the output:
    ```
    Partition number (1-4, default 1):
    ```

  - press `enter` to accept single partition, and the output:
    ```
    First sector (2048-121438207, default 2048):
    ```

  - press `enter` to accept the default 2048, and the output:
    ```
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-121438207, default 121438207):
    ```

  - press `enter` to accept the default `121438207`, and the output:
    ```
    Created a new partition 1 of type 'Linux' and of size 57.9 GiB.

    Command (m for help):
    ```

  - enter `w` to write the new partition table and `exit` fdisk


- **Create a filesystem** using the `mkfs` command

  - **Note:**
    - `vfat` file system enable to use the USB drive on a PC or a Mac too, BUT
       cannot change permission once mounted
    - `ext4` is a new filesystem that has become the defacto standard of most 
      Linux distros today
    - `ext3` is just ext2 with journal

  - There is one partition, so must put the partition number to the end of the 
    device name:
    ```bash
    sudo mkfs.ext4 /dev/sda1
    ```

  - To be clean, physically eject the drive and then re-insert it

  - Next mount the drive as described below

Source:  
[Formatting and Mounting a USB Drive from a Terminal Window](https://thepihut.com/blogs/raspberry-pi-tutorials/17699796-formatting-and-mounting-a-usb-drive-from-a-terminal-window){:target="_blank"}


#### Mount USB flash drive

Raspbian OS will auto-mount USB flash drive soon after it is plugged-in.
It will be mounted on `/media/<??>`.
  
**To change to a different mount point**
<span class="label label-default">Instructions:</span>
- create a mount point
  ```bash
  sudo mkdir /media/usbdisk
  ```

- make `pi` the owner and group if not already
  ```bash
  sudo chown -R pi:pi /media/usbdisk
  ```

- mount the usb drive to `/media/usbdisk` mount point
  ```bash
  sudo mount /dev/sda1 /media/usbdisk -o uid=pi,gid=pi
  ```


**Setup to auto-mount after reboot**
The mount point will not persist after reboot so `auto-mount` needs to be setup.

- find the UUID for sda1, if the first usb
  ```bash
  ls -l /dev/disk/by-uuid/
  ```
  Example output with the `UUID=0116-FA8D`:
  ```
  total 0
  lrwxrwxrwx 1 root root 10 Nov 18 13:49 0116-FA8D -> ../../sda1
  lrwxrwxrwx 1 root root 15 Nov 18 13:49 0C61-73F5 -> ../../mmcblk0p1
  lrwxrwxrwx 1 root root 15 Nov 18 13:49 43f2d0bb-83be-464f-94d0-9a751f376c64 -> ../../mmcblk0p2
  ```

- edit `/etc/fstab`
  ```bash
  sudo nano /etc/fstab

  # add at the end
  UUID=0116-FA8D /media/usbdisk vfat auto,nofail,noatime,users,rw,uid=pi,gid=pi 0 0
  ```

  **Note:**
  - Use UUID rather than the device node (`/dev/sda1`) as the device node can change 
  across reboots especially if drives are added or removed.  
  - Include "nofail" in the mount options to prevent the Pi hanging if it is booted 
  without the drive attached.  



#### Unmount USB Drive
```bash
sudo umount /media/usbdisk
```

### Auto Start App/Svc after boot

Assume there is a python script, `push_hold_shut.py`, in the home directory.

```bash
sudo nano /etc/rc.local
# add the program
~/push_hold_shut.py &
```


### Install Touchscreen Keyboard - Matchbox

**Prerequisite**:
- Raspbian desktop image (not lite)

- Install
```bash
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install --no-install-recommends matchbox-keyboard
```

- The keyboard can be started from Menu > Accesories > Keyboard

*Source*: [Matchbox Keyboard - Raspberry Pi Touchscreen Keyboard](https://thepihut.com/blogs/raspberry-pi-tutorials/matchbox-keyboard-raspberry-pi-touchscreen-keyboard){:target="_blank"}

## Backup Raspbian microSD 

RPI OS runs on microSD card which has a shorter lifetime than, for example, 
physical hard drive. Therefore, backing up the entire microSD card to a file
(`.img` file) is highly recommended to prevent failure at the least desired 
time, like in a middle of critical half-finished project.
  
For Windows, use [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/){:target="_blank"}

Source: [Win32DiskImager](https://raspberry-projects.com/pi/pi-operating-systems/win32diskimager){:target="_blank"}


## Connect to RPi

### SSH using Putty and PuttyGen Key Generator

Putty is a free SSH client that can be downloaded from 
[here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html){:target="_blank"}

<span class="label label-default">Instructions:</span>
- Start putty; the main screen is the "PuTTY Configuration" window.
- Enter "Host Name (or IP address)"
- Click SSH radio button for "Connection type"
- Use default Port=22
- Enter a session name to save the configuration
- [Optional] setup SSH key for connection without username/password
  - Click Connection - Data; enter "Auto-login username" with the username to
    login to RPi; for example, `pi`
  - Click Connection - SSH - Auth, on the "Private key file for authentication"
    browse to find the private key in the putty ppk format. Otherwise, 
    jump to the next step to convert the OpenSSH private key (`id_rsa`) to
    putty ppk format using the PuttyGen application.
  - To save, click Session, then click Save to save the setup into the session
    config file for later reuse.
- [Optional] Convert the private key, `id_rsa` to putty `ppk` format; both the ssh client
  (putty) and the scp client (WinSCP) that we will use later to connect to 
  headless RPi need the putty `ppk` format.
  - as part of putty ssh client installation, the "puttyGen" key generator is
    also installed; use the puttygen to convert the private key to ppk format
  - Open puttygen
  - On the top menu, click "Conversions" and then "Import" 
  - Select the private key (e.g., `id_rsa`); enter the "Key passphrase" and 
    "Confirm passphrase" fields if provided when generating the key, 
  - go to File and click "Save private key" to save the key to disk in PuTTY 
    format (as a .ppk file)
 


### SCP - Secure Copy

Use `SCP` to tranfer file from a computer or laptop to RPi. 
The SCP client application needs to be installed on the laptop.
  
Example, to copy file `domain.crt` to RPi host `192.168.1.134` for `pi` user 
and store it at the home directory:
```
scp domain.crt pi@192.168.1.134:
```

For Windows computer, download and setup the free 
[Windows SCP](https://winscp.net/eng/index.php){:target="_blank"}
<span class="label label-default">Instructions:</span>
- Open WinSCP
- On the "Session"
  - File Protocol = SCP
  - Host name: <enter IP address of RPi>
  - Port: 22
  - User name: <enter user name>
  - Password: <enter password>
- Setup Tunnel otherwise WinSCP will fail to connect and it will
  keep trying and slowing down the computer network;
  - Click Edit to enable "Advanced" button; in the "Advanced Site Settings";
  - On the left-hand nav, click Connection - Tunnel, setup the following:
  - Check "Connect through SSH tunnel"
  - Enter `hostname`, `port`, `username` and `password`
- [Optional] Setup SSH key for connection without username/password
  - Click Edit to enable "Advanced" button; in the "Advanced Site Settings";
  - On the left-hand nav, click SSH - Authentication, setup the following:
  - Enter the "Authentication parameters" - "Private key file" (`id_rsa.ppk` or 
    `id_rsa`); WinSCP needs Putty formatted private key, `id_rsa.ppk`, but it 
    will take and convert the OpenSSH `id_rsa` private key file to the Putty 
    format automatically.
  - On the left-hand nav, click Connection - Tunnel, setup the following:
  - Enter the "Tunnel authentication parameters" - "Private key file";
    enter the `id_rsa.ppk` file, the same one used for the authetntication above 
  - click OK
- Click "Save"

Source: [Secure Copy](https://www.raspberrypi.org/documentation/remote-access/ssh/scp.md){:target="_blank"}


## Useful commands

### - Info
```bash
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

### - Disk Usage
Disk usage; `-h` - human readable; `-s` - summary;
```bash
du -hs
```
Output:
```
48k
```
  
Disk Free
```bash
df -h
```
Output:
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        30G  1.4G   27G   5% /
devtmpfs        428M     0  428M   0% /dev
tmpfs           433M     0  433M   0% /dev/shm
tmpfs           433M  5.9M  427M   2% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           433M     0  433M   0% /sys/fs/cgroup
/dev/mmcblk0p1  253M   52M  201M  21% /boot
tmpfs            87M     0   87M   0% /run/user/1000
```

### - RAM Usage
State of memory
```bash
free -h
```
Output
```
              total        used        free      shared  buff/cache   available
Mem:          864Mi        50Mi       740Mi       5.0Mi        74Mi       758Mi
Swap:          99Mi          0B        99Mi
```
Note: [increase swap space](#increase-swap-space)

## Cloud hosting of RPi

Cloud hosting of Raspberry Pi at:
[Mythic Beast](https://www.mythic-beasts.com/order/rpi){:target="_blank"}


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
- [Issue installing numpy python3](https://www.raspberrypi.org/forums/viewtopic.php?t=207058){:target="_blank"}
