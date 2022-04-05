---
layout: single
title: Building on Windows
overview: true
permalink: /building_windows/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

This page describes Getting Started with KNX-IOT Point API development on windows.
The build system enviroment is Cmake, so one can use:

- Visual Studio
- nmake (from the commandline)

### prerequisits

- Windows (10) machine
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

     - menu -&gt; file -&gt; open -&gt; Cmake

       ![VisualStudio](/assets/images/visualstudio-cmake.png)

     - select the CMakefile.txt from the working folder
     - wait until visual studio prepared the project

1. use visual studio to build the executables:

   - menu -&gt; build -&gt; Build All (Ctrl+shift+B)

   - The executables are created in the project.

     The executables can be found in folder:
     `\KNX-IOT-STACK\out\build\x64-Debug`
     note that the actual path of the executables is dependend on the visual studio configuration.

1. debug an application

   - toolbar -&gt; Select Startup Item -&gt; down button
     - Select item (for example: LSSB_minimal_all.exe)
     - press the debug symbol (or F5)
     - A commandline window will appear with the logging of the KNX application

## build architecture

The build architecture (win32 or x86) is dependend on the visual studio installation.

## Cmake information

more information on Cmake and Visual studio can be found [here](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170)
