---
layout: single
title: Getting Started with KNX IoT on a Pi
overview: true
permalink: /gs_knx_pi/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

The Getting started with KNX IoT PI guide shows how to:

- get the source code
- compile the source code

This Getting started guide does require specific hardware.

### What is KNX IoT PI

This are 2 sample applications with GUI:

- LSAB (knx_iot_sa_pi): a switch actuator (light)
- LSSB (knx_iot_pb_pi): a push button (light toggle)

Hence they can be configured as a small installation.
Each device has 4 channels.

The PB has 4 push buttons and 4 feedback leds.
The SA has 4 leds for acting as a light

More info can be found on [GitHub](https://github.com/KNX-IOT/KNX-IOT-Virtual)

### Requirements for KNX IoT Pi

- Raspberry Pi 3b or 4
- Pi Hat
  - https://pinout.xyz/pinout/display_o_tron_hat

To create a demonstrator: 2 Pi and 2 hats are needed.

## Steps

### Get the source code and build

1. [Get the code]([/building_windows/](https://github.com/KNX-IOT/KNX-IOT-Virtual))
   Clone the code

   ```bash
   git clone https://github.com/KNX-IOT/KNX-IOT-Virtual.git
   ```

2. Build on Pi

   ```bash
   mkdir build
   cd build
   cmake .. 
   make -j4
   ```

3. go to folder \build\apps
   start an executable (files with no extention) by double clicking an executable.
   The KNX device is now running.

## Note

The actual code to talk to the HAT is in python.
However the C code is made in such way that button presses are received from Python and that LEDS can be toggled.