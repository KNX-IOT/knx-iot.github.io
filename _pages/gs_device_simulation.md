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

The getting started with KNX IoT Point API Device Simulation guide shows how to:

- Get the source code
- Compile the source code (stack examples)
  - compile an LSAB commandline application (actuator)
    called `lsab_minimal_all`.
  - compile an LSSB commandline application (sensor - push button)
    called `lssb_minimal_all`.

This Getting started guide does not need any specific hardware.

## Requirements for Device Simulation

- Windows or Linux based PC

## Steps

### Build the stack examples on Windows

1. [Build on Windows](/_pages/building_windows.md)

   Build the stack by following the [Build on Windows](/_pages/building_windows.md).

   When everything is built, the executables will be available in the folder:
   `\out\build\x64-Debug\apps`.

   Note that the folder might be different due to the Visual Studio configuration.

1. Run the application from the command line

   1. Go to the folder where the executables were built in the previous step.
   2. Start an executable (files with extention .exe) by double clicking an execuable.

    A Popup might appear to grant the device network access.
    ![windows defender](/assets/images/windows_defender.png)
    Accept the network work access.

    The KNX device is now running.
