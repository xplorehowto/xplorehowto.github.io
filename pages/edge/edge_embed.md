---
title: Edge Computing - Embedded Systems
keywords: edge, embedded
tags: [edge, embedded]
sidebar: edge_sidebar
permalink: /edge_embed
folder: edge
---

## Introduction

Embedded system consists of computer hardware and software, and physical parts, 
designed to perform a specific task.

{% include image.html file="edge/embed_components.JPG" url="#" 
  caption="Components of a typical embedded system; 
  <br/>[Source: Software Engineering for Embedded Systems; Ref below;]" 
  max-width=400%}

## Build Process

{% include image.html file="edge/embed_buildprocess.jpg" url="#" 
  caption="Build Process; (A) desktop application; (B) embedded system; 
  <br/>[Source: Software Engineering for Embedded Systems; Ref below;]" 
  max-width=900%}

### Compilation Toolchain

{% include image.html file="edge/embed_compile.jpg" url="#" 
  caption="Modern compilation toolchain; 
  <br/>[Source: Software Engineering for Embedded Systems; Ref below;]" 
  max-width=500%}
  
  
## Hardware Abstraction Layers (HAL)

Embedded system development is about programming at the hardware level but
accessing hardware via the hardware abstraction layers (HALs), an *interface* 
between hardware and software so that applications can be device independent. 
The HAL encapsulates the peripherals of a microcontroller, and several API 
implementations are provided at different levels of abstraction. 

{% include image.html file="edge/embed_hals.jpg" url="#" 
  caption="Hardware Abstraction Layers; 
  <br/>[Source: Software Engineering for Embedded Systems; Ref below;]" 
  max-width=500%}


## Embedded Development

To learn embedded development, it's best to have access to 
[development board](/edge_embed_dev). Embedded development requires 
some understanding of tasks typically handle by operating system.

The following instructions were extracted from "Software Engineering for 
Embedded Systems, 2nd Edition, by Mark Kraeling, Robert Oshana".

- Choose the hardware platform, and understand the hardware details from the
  following documents:
  - Platform User Guide - contains how to initialize the platform and access 
    peripherals; platform block diagram, reset details, board schematics, and 
    connector pinouts; For example: [NXP KW41Z](https://www.nxp.com/products/wireless/thread/kinetis-kw41z-2.4-ghz-dual-mode-bluetooth-low-energy-and-802.15.4-wireless-radio-microcontroller-mcu-based-on-arm-cortex-m0-plus-core:KW41Z?tab=Documentation_Tab){:target="_blank"}
  - Processor datasheet - aka reference guide, will refer to CPU architecture 
    data sheet containing hardware-specific details, such as voltages and 
    frequencies, bus timing, and any low-level details applicable to the 
    system reset, system initialization, clocking, etc. 
    For example: [NXP KW41Z](https://www.nxp.com/docs/en/data-sheet/MKW41Z512.pdf){:target="_blank"}

- Figure out how to initialize the system and  program the peripherals, which 
  requires knowledge of both hardware and software. Embedded hardware providers 
  typically include: preconfigured initialization code with the SDK, and sample 
  runtime codes. For example, [NXP MCUXpressoIDE](http://www.nxp.com/mcuxpresso/sdk){:target="_blank"}
  The SDK also provides the required cross-development tools (C compiler, 
  linker, debugger, etc.), set of header files, libraries, and sample projects. 
  These files provide utility functions to configure and use the peripherals 
  contained in the device.

- Install the SDK and development IDE

- Download the debugger; such as JTAG debug connection. 
  Connect the reference board to your workstation using the USB cable. 
  You may be prompted to install device drivers to support the JTAG connection. 
  With the board connected, right-click on the project in the project explorer 
  and select “Debug As >”.  
  The debugger will reset the target processor, download the binary image to 
  the target, insert a temporary breakpoint at main(), and release the 
  processor from reset. The processor will execute the startup code (memory and 
  variable initialization, etc.) and then halt execution at the temporary 
  breakpoint at main(). At this point the debugger IDE can be used to single 
  step, set breakpoints, examine variables, etc. To execute the program at 
  full speed, press the “F8” function key. The main program will run. 
  To terminate the debug session, press the “CTRL-F2” key.
  
- Understanding system reset;  
  All embedded processors have a well-defined mechanism to handle the power-on 
  reset event. However, the details of these mechanisms will vary based on many 
  factors: CPU architecture, SoC manufacturer, and a long list of optional 
  settings. These settings specify the boot device, bus settings, single-chip 
  mode, clock sources, etc. There are also many ways these settings can be 
  implemented. One way is to use pull-up resistors on specific I/O or bus pins. 
  These pins are read shortly after reset and determine the optional settings 
  for that SoC. After the settings are determined, these pins assume their 
  primary functions. Another method employed on some SoCs is to read the 
  settings from a specific location in flash memory.
    
  Once the processor has come out of reset with the correct configuration, 
  the boot software is then required to initialize many different subsystems. 
  These initialization steps will be very specific to the SoC being used, 
  the way the device is configured, and which peripherals will be needed by 
  the operating system and/or application software. There are several sources 
  that provide working examples of boot software. These examples can often be 
  found in the semiconductor supplier’s SDKs, commercial RTOS vendor’s SDKs, 
  and open source projects like Linux (www.yoctoproject.org) and 
  FreeRTOS (www.freertos.org). Reading sample boot code operations and 
  identifying the appropriate sections in the previously mentioned 
  documentation is an excellent way to learn how a reference platform like 
  the FDRM-KW41Z is configured and initialized at boot time.

- Understand clock configuration  
  The clocking subsystems on modern embedded SoCs are very complex. 
  The Reference Manual contains the detailed information needed to properly 
  configure the clocks.
  
- Learn I/O Pin Configuration and Initialization

- Learn Interrupt Handlers
  One of the peripherals most commonly used in embedded designs is the timer. 
  Many of the larger, highly integrated SoCs will contain multiple types of 
  timers, and often support different operating modes and capabilities. 
  Some are designed as periodic interrupt timers (PIT) and can be used to 
  generate interrupts at a constant rate, and others generate periodic 
  waveforms (PWM) or time the rise and fall of input signals (input capture). 
  Other types of timer models can function as counters, using internal or 
  external signals as the event to be counted.


## References 

- Software Engineering for Embedded Systems, 2nd Edition, by Mark Kraeling; 
  Robert Oshana; see OReilly Safari online;
  
- [](){:target="_blank"}