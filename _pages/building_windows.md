---
layout: single
title: Building on Windows
overview: true
permalink: /building_windows/


toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

This page describes Getting Started with KNX-IOT development on windows.
The build system enviroment is Cmake, so one can use:
- visual studio
- nmake (from the commandline)

### prerequisits

- windows (10) machine
- installed:

  - git
  - visual studio


## build steps

1. Getting the code
   clone the repo to a local folder

  ```bash
  # do from your working folder
  git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git
  ```

Note: the clone is needed for the subprojects.

1. build the code with visual studio

- open visual studio
- open cmake project by:

  - file -&gt; open -&gt; Cmake

    ![VisualStudio](/assets/images/visualstudio-cmake.png)

- select the CMakefile.txt from the working folder
- wait until visual studio prepared the project
- use visual studio to build & run the example applications


## build architecture

The build architecture (win32 or x86) is dependend on the visual studio installation.


## Cmake information

more information on Cmake and Visual studio can be found [here](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170)

