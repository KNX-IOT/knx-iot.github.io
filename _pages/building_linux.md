---
layout: single
title: Building on Linux
overview: true
permalink: /building_linux/


toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

This page describes Getting Started with KNX-IOT development on Linux.

Note this also applies to Raspberry Pi.

prerequisits:

- Linux machine
- installed:

  - git
  - gcc
  - cmake environment

1. build the code on Linux

```bash

# Clone the Stack
git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git

# go into the create repo
cd KNX-IOT-STACK

- # Make a working directory (named anything)
mkdir build
cd build 

# Create a build directory for native build, and build the SDK
cmake ..
make -j12
# Built for current system! To change configuration, the 'ccmake .' command can be used

#Go back to working directory
cd ..

```
