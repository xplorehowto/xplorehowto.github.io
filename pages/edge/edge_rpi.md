---
title: Edge Computing - Raspberry Pi
keywords: edge, embedded
tags: [edge, embedded, rpi]
sidebar: edge_sidebar
permalink: /edge_rpi
folder: edge
---

## Introduction

RaspberryPi...

## [Issue] Installing numpy

Installation of 
**Error:**
```
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

```
pip3 uninstall numpy
sudo apt install libatlas3-base
sudo pip3 install numpy
```

**Reference:**
- [Issue installing numpy python3](https://www.raspberrypi.org/forums/viewtopic.php?t=207058)