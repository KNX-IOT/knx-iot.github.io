---
layout: single
title: Getting Started with Device Simulation
overview: true
permalink: /gs_device_simulation/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

The Getting started with KNX IoT Point API Device Simulation guide shows how to:

- Get the source code
- Compile the source code (stack examples)
  - compile a LSAB commandline application (actuator)
    called `lsab_minimal_all`.
  - compile a LSSB commandline application (sensor - push button)
    called `lssb_minimal_all`.

This Getting started guide does not need any specific hardware.

### Requirements for Device Simulation

- Windows or Linux based PC

## Steps

### build the stack examples on Windows

1. [Build on Windows](/building_windows/)

   Build the stack by following the [Build on Windows](/building_windows/).

   When everything is build then the executables will be available at folder:
   `\out\build\x64-Debug\apps`

   Note that the folder might be different due to the visual studio configuration.

1. Run the application from the command line

   by doing the following steps:
   1. Go to folder `\build\apps`
   1. Start an executable (files with extention .exe) by double clicking an execuable.

    A Popup might appear to grant the device network access.
    ![windows defender](/assets/images/windows_defender.png)
    Accept the network work access.

    The KNX device is now running.
