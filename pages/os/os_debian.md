---
title: OS - Linux Debian
keywords: os, linux, debian
tags: [os, linux, debian]
sidebar: os_sidebar
permalink: /os_debian
folder: os
---

## Overview

Debian is a free and open source operating system based on linux kernel.
Many OS are based on the Debian including: Ubuntu, Mint & Raspbian.

## Hardware

### Check processor architecture

```
dpkg --print-architecture
```

### Date & Time

```
date
date "+%H:%M:%S"
```

### Timezone
```
# set in 
/etc/timezone
```

## Manage User & Group

### Find a user's UID or GID
```
id <username>
# id
id -u <username>

# gid
id -g <username>

# all the groups a user belongs to
id -G <username>

# find all
cat /etc/passwd
cat /etc/group
```

### Modify user account
```
# add user to group
usermod <username> -aG <groupname>
```

### Add user
```
# add user and create the home directory for the user
# group with the same name also created
useradd -m <username>
useradd -m <username> -p <password>

# add user with group; so that group of the same name NOT created
useradd -m <username> -g <groupname>

# add user BUT not create home directory, and not allowed to login
useradd -M -L <username>

# add user with a specific id; a group of SAME "name and id" is also created 
useradd -M <username> -u 1883
```

### Add group
```
groupadd <groupname>
cat /etc/group
```

### Delete user and group
```
# delete user from a group
deluser <username> <groupname>

# delete user with no home directory, no login
userdel <username>

# delete regular user with password, home dir, login, files, etc. 
passwd -l <username>
tar -zcvf /nas/backup/account/deleted/v/<username>.$uid.$now.tar.gz /home/<username/

pgrep -u <username>
ps -fp $(pgrep -u <username>)
killall -KILL -u <username>
find /var/spool/at/ -name "[^.]*" -type f -user <username> -delete
crontab -r -u <username>
lprm <username>
find / -user <username> -print
find / -user <username> -exec chown newUserName:newGroupName {} \;
userdel -r <username>

# delete group
groupdel <groupname>
```

### chmod and chown

#### - Make shell file executable:
```
chmod +x <filename>
```

#### - Change owner user of file:
```
chown <userName> <filename>
```

#### - Change owner group of file:
```
chown :<groupName> <filename>
``` 

#### - Change both owner user and group of file:
```
chown <userName>:<groupName> <filename>
chown -R <userName>:<groupName> <foldename>
```


## Package Management

`apt` is debian package management.  

Debian maintains a list of links to repository that `apt-` or `apt-get` can
download from. The list(s) is stored in a file `/etc/apt/sources.list`, and
in a directory containing the list files. These files are merged at runtime
to form the complete list. Therefore, the content format of these files are 
exactly the same.
  
The benefits for allowing list of files in the `sources.list.d` folder are:
ease of configuration and automation. For example, to disable a repository that
is listed on a file, you can just remove the file instead of manipulating the 
main list (i.e. `sources.list`).

Also see:
  
- [How apt-get works](https://unix.stackexchange.com/questions/377736/how-does-apt-get-really-work)

### - List of apt repositories
```
grep ^[^#] /etc/apt/sources.list /etc/apt/sources.list.d/*
```
  
Example of the default content of `/etc/apt/sources.list` for raspbian
```
deb http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
```
  
and `/etc/apt/sources.list.d/debian.list`
```
deb http://archive.raspberrypi.org/debian/ stretch main ui
# Uncomment line below then 'apt-get update' to enable 'apt-get source'
#deb-src http://archive.raspberrypi.org/debian/ stretch main ui
```
  
Also see:  

- [How to add apt repos in Ubuntu](https://tecadmin.net/add-apt-repository-ubuntu/)

- Also see `man sources.list` for details.

### - List of installed packages
```
dpkg -l

dpkg --get-selections | grep python3-picamera
```

### - Web-based tool to search apt packages

- https://www.debian.org/distrib/packages

- https://aur.archlinux.org/packages/


### - Install package
```
apt-get install <packageName> --no-install-recommends
```

Notes:
- Do not consider recommended packages as a dependency for installing
- during package search, gathers the list required packages, recommended 
  packages, and suggested packages
- The *required packages* are dependencies so their installation is mandatory
- The *recommended packages* will be installed by default unless the 
  `--no-install-recommends` is specified or turned off in the 
  `/etc/apt/apt.conf`
- The *suggested packages* is not installed by default. 

### - References

- https://www.howtoforge.com/linux-dpkg-command/
  - additional `dpkg` features & how-to


## How-to

### Setting Environment vars

```
export K3S_URL="https://rpik3ssvr:6443"
```

- Preset environment variables
```
echo $HOME
```

### Configure program to run at boot

Old school mechanism for starting python program, `svc.py` at boot:
- add it to `/etc/rc.local`
- make sure `rc.local` runs at boot time
- must be setup as root. 

setup commands:
```
sudo chmod 755 /etc/rc.local
sudo nano /etc/rc.local

# in the editor; scroll to the bottom & add one line

ifup eth0
 
/usr/bin/python /home/svc.py &
  
exit 0

# exit nano editor CTL-X

sudo /etc/rc.local
```

## `/etc`

### apt Repository list
```
/etc/apt/sources.list
/etc/apt/sources.list.d/*
```

### rc.local
```
/etc/rc.local
```
[Example - setup startup program](os_debian##configure-program-to-run-at-boot)


### Timezone
```
/etc/timezone
```
[Example - Setting Timezone](os_debian#timezone)




## References 

- [The Linux Documentation Project](http://www.tldp.org/guides.html){:target="_blank"}  
  compilation of books, references, etc.; all free; MUST visit;
  
- [](){:target="_blank"}