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

The Getting started with Device Simulation guide shows how to:
- get the source code
- compile the source code
- create an LSAB and LSSB application
- configure the installation

This Getting started guide does not need any specific hardware.

#### requirements

- Windows or Linux based PC

## Steps

### Get the source code and build on windows

1. [Build on Windows](building_windows)

   When everything is build then the executables will be available at folder:
   `\out\build\x64-Debug\apps`

   Note that the folder might be different due to the visual studio configuration.

2. go to folder \build\apps
   start an executable (files with extention .exe) by double clicking an execuable.
   A Popup might appear to grant the device network access.
   ![windows defender](/assets/images/windows_defender.png)
   Accept the network work access.
   
   The KNX devics is now running

