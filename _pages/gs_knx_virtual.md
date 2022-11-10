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

This guide will walk you through how to get the source code for a KNX IoT Virtual device, and how to build it. No special hardware is required to run KNX IoT Virtual devices.

## What is KNX IoT Virtual

KNX IoT Virtual is a GUI-enabled simulation of a KNX device. This consists of two sample applications with GUI, which can be configured as a small installation:

- LSAB: a simulated switch actuator (light)
- LSSB: a simulated push button (light toggle)

Each device has 4 channels. The Push Button application has 4 push buttons and 4 feedback widgets.

![push button application](/assets/images/knx-iot_virtual-PB.png)

The Switch Actuator application has read-only buttons which indicate if the light is turned on or off, and a mechanism to introduce a fault.

![switch actuator application](/assets/images/knx-iot_virtual-SA.png)

More info on the applications can be found in the [KNX IoT Virtual repository](https://github.com/KNX-IOT/KNX-IOT-Virtual).

## Requirements for KNX IoT Virtual

Windows PC: [see information about building on Windows](/_pages/building_windows).

## Steps

1. [Clone the repository](https://github.com/KNX-IOT/KNX-IOT-Virtual)

   ```bash
   git clone https://github.com/KNX-IOT/KNX-IOT-Virtual.git
   cd KNX-IOT-Virtual
   ```

2. Build on Windows

   ```bash
   mkdir build
   cd build
   cmake .. -DwxWidgets_ROOT_DIR=c:/wxWidgets-3.1.5
   ```

3. Open Visual Studio with the created `knx-virtual.sln` located in the build directory.

4. Build the solution

   When everything is built, the executables will be available in the folder:
   `build\Debug`.

   Note that the folder might be different due to the Visual 
   Studio configuration.

3. Go to the folder where the executables were built in the previous step. 
   Start an executable (files with extension .exe) by double clicking it.
   A Popup might appear to grant the device network access.
   ![windows defender](/assets/images/windows_defender.png)
   Accept the network work access.

   The KNX device is now running.

## More info

For more information about KNX IoT Virtual, see the main [README file](https://github.com/KNX-IOT/KNX-IOT-Virtual#readme) of the KNX IoT Virtual repository.