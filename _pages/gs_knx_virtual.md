---
layout: single
title: Getting Started with KNX IoT Virtual
overview: true
permalink: /gs_knx_virtual/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

The Getting started with KNX IoT Virtual guide shows how to:

- get the source code
- compile the source code

This Getting started guide does not need any specific hardware.

### What is KNX IoT Virtual

This are 2 sample applications with GUI:

- LSAB : a switch actuator (light)
- LSSB : a push button (light toggle)

Hence they can be configured as a small installation.
Each device has 4 channels.

The PB has 4 push button and 4 feedback widgets.
![push button application](/assets/images/knx-iot_virtual-PB.png)

The SA has buttons to indicate if the light is turned on or off and a mechanism to introduce a fault.
![switch actuator application](/assets/images/knx-iot_virtual-SA.png)

### Requirements for KNX IoT Virtual

- Windows (or Linux) based PC
- install wxWidgets on the development machine

## Steps

### Get the source code and build on Windows

1. [Get the code](https://github.com/KNX-IOT/KNX-IOT-Virtual)
   Clone the code

   ```bash
   git clone https://github.com/KNX-IOT/KNX-IOT-Virtual.git
   ```

2. Build on Windows

   ```bash
   mkdir build
   cd build
   cmake .. -DwxWidgets_ROOT_DIR=c:/wxWidgets-3.1.5
   # open visual studion with the created knx-virtual.sln
   # build the solution
   ```

   When everything is build then the executables will be available at folder:
   `\out\build\x64-Debug\apps`

   Note that the folder might be different due to the visual studio configuration.

3. go to folder \build\apps
   start an executable (files with extention .exe) by double clicking an execuable.
   A Popup might appear to grant the device network access.
   ![windows defender](/assets/images/windows_defender.png)
   Accept the network work access.

   The KNX device is now running.
