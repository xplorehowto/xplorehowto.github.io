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


## How-to

### Setting Environment vars

```
export K3S_URL="https://rpik3ssvr:6443"
```

- Preset environment variables
```
echo $HOME
```

## References 

- [The Linux Documentation Project](http://www.tldp.org/guides.html){:target="_blank"}  
  compilation of books, references, etc.; all free; MUST visit;
  
- [](){:target="_blank"}