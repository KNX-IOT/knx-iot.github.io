---
layout: single
title: Build your own device
overview: true
permalink: /gs_build_own_device/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

The Build your own device guide shows how to:

- get the source code :
  - The stack
  - Example application for development
- compile the application
- change the application to your needs

### What do you get

- an development application that exist of:
  - A main application
  - an initial set of data points
  - callbacks for:
    - handling device restart
    - handling device reset
    - setting the hostname
    - writing the sofware update data to file.
- build environment based on CMake
  - Capable of cross compiling
  - implemented ports to windows and Linux

## Steps

### Get the development repo

The development repo is outside of the KNX-IOT-STACK repo.
This avoids changing the build environment of the KNX-IOT-STACK.
The development repo is already setup that it builds the KNX-IOT-STACK automatically.

TODO

### build the example

TODO

### start changing the application

TODO