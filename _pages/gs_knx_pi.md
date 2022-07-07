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
- Pi Hat info:
  - https://pinout.xyz/pinout/display_o_tron_hat
  - https://github.com/pimoroni/displayotron

To create a demonstrator 2 Pi and 2 hats are needed:
one to act as a push button and the other one acting as a light:

![demo setup](/assets/images/knx-demo-pi-hat.png)

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


## Checking if the applications run correctly


### check Pi-Hat drivers

run the application `pi-hat`

- LCD should turn on
   - should show the IP address


### check network connectivity

Note that KNX IoT Point API is IPV6 based.

#### send IPV6 ping to the other PI

The command is `ping`

if ping is success full then communication is possible

#### send IPV6 ping from windows pc to Pi's

if ping is success full then communication is possible

#### disable virtual box (if running)

check if your machine is running a virtual box
if so:

- shutdown the running virtual machine
- disable the ethernet connection of the virtual box 


#### virus scanner

If your virus scanner is known to interfer with network traffic.
Disable to avoid issue.


#### send multicast from windows pc to Pi's

if ping is success full then discovery of the KNX-IOT devices is possible


### configure the devices (from a Windows Machine)

- download the zip from GitLab
- unzip the file in a folder
- open the README.md file
- follow the instructions about configuring the 2 devices.

## Check networking connectivity on Thread

The network interface is wpan0

### check if wpan0 interfaces are up and running

```bash
ifconfig
```
should list IPV6 adresses for the WPAN0 interface.
If no IPV6 adrss 

### restart wpan0


sudo systemctl restart wpantund.service

### list system logs

sudo journalctl




