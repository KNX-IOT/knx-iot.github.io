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

This page describes Getting Started with KNX IoT Point API development on windows.
The build system enviroment is Cmake, so one can use:

- Visual Studio
- nmake (from the commandline)

### prerequisits

- Windows (10) machine
- installed:

  - git
  - visual studio
  - cmake
    - python
    - perl
  - wxWidgets (for KNX IoT Virtual)

## build steps

1. Getting the code
   clone the repo to a local folder

   ```bash
   # do from your working folder
   git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git
   # update the dependencies
   git submodule update --init --recursive
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

## installing the dependencies

### git

git can be obtained from:

https://git-scm.com/download/win

- download the file
- install the software

one should now have explorer integration to:

- Git Gui Here (to push data)
- Git Bash Here (a bash shell for commandline git)

#### perl

Building (e.g. configuring wxWidgets with Cmake) requires perl
If perl is not installed then install it via a Windows installer available at:

https://www.perl.org/get.html

To check if perl is installed:

```bash
# do in a bash window
which perl
# result should be
# /usr/bin/perl
```

#### python

Building (e.g. configuring wxWidgets with CMake) requires python

If python is not installed then install it via a Windows installer available at:

https://www.python.org/downloads/

To check if python is installed:

```bash
# do in a bash window
which python
# result should be
# <some path>/python
```

#### installing wxWidgets on Windows

download wxwidgets from (installer source code):
https://www.wxwidgets.org/downloads/

- install the contents on the recommended folder (e.g. c:\wxWidgets-3.1.5)
- build wxwidgets with visual studio:
  
  - open c:\wxWidgets-3.1.5\build\msw\wx_vc16.sln (or take the highest number available)
  - accept convert solution suggestion: convert solution to newer version studio
  - build the solution :
    - static Win32 library for Debug & Release
    - static x64 library for Debug & Release

### Cmake information

more information on Cmake and Visual studio can be found [here](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170)
