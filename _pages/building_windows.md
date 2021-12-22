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

## prerequisits

- windows (10) machine
- installed:

  - git
  - visual studio

1. Getting the code
   clone the repo to a local folder

  ```bash
  # do from your working folder
  git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git
  ```

1. build the code with visual studio

- open visual studio
- open cmake project by:

  - file -&gt; open -&gt; Cmake

- select the CMakefile.txt from the working folder
- wait until visual studio prepared the project
- use visual studio to build & run the example applications


## Cmake information

more information on Cmake and Visual studio can be found at:

https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170

