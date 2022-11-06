---
layout: single
title: Building on Linux
overview: true
permalink: /building_linux/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

This page describes Getting Started with KNX IoT Point API development on Linux.

The build system is CMake.

Note this description also applies to development on a Raspberry Pi.

### Prerequisites 

The prerequisites are:

- Linux machine (or Pi)
- installed:

  - git
  - gcc
  - cmake environment

## Build steps GitHub

```bash
# Clone the Stack
git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git
# go into the create repo
cd KNX-IOT-STACK
- # Make a working directory (named anything)
mkdir build
cd build 
# do the configur step, e.g. build the native make files
cmake ..
# build the sdk, the -j is the amount of processor the build will be using
make -j12
#Go back to working directory
cd ..
```

Note: one can copy paste the contents above in a Linux terminal.

## Build steps GitLab

```bash
# Clone the Stack
git clone https://gitlab.knx.org/shared-projects/knx-iot-point-api-public-stack.git
# go into the create repo
cd knx-iot-point-api-public-stack
- # Make a working directory (named anything)
mkdir build
cd build 
# do the configur step, e.g. build the native make files
cmake ..
# build the sdk, the -j is the amount of processor the build will be using
make -j12
#Go back to working directory
cd ..
```

Note: one can copy paste the contents above in a Linux terminal.
