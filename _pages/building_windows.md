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
- Installed software:
  - git
  - visual studio
  - cmake
    - python
    - perl
  - wxWidgets (for KNX IoT Virtual)
  
  If the software is not installed please follow the instructions [here](Installing-the-dependencies).

## Build steps

1. Getting the code
   clone the repo to a local folder

   ```bash
   # do from your working folder
   git clone https://github.com/KNX-IOT/KNX-IOT-STACK.git
   ```

1. Build the code with visual studio

   - Open visual studio
     - Open cmake project by:

     - menu -&gt; file -&gt; open -&gt; Cmake

       ![VisualStudio](/assets/images/visualstudio-cmake.png)

     - select the CMakefile.txt from the working folder `<working folder>\KNX-IOT_STACK`
     - wait until visual studio prepared the project

1. Use visual studio to build the executables:

   - menu -&gt; build -&gt; Build All (Ctrl+shift+B)

   - The executables are created in the project.

    The executables can be found in folder:
    `\KNX-IOT-STACK\out\build\x64-Debug`

    Note: The actual path of the executables is dependend on the visual studio configuration.

1. Debug an application

   - toolbar -&gt; Select Startup Item -&gt; down button
     - Select item (for example: LSSB_minimal_all.exe)
     - press the debug symbol (or F5)
     - A commandline window will appear with the logging of the KNX application

## Build architecture

The Build architecture (win32 or x86) is dependend on the visual studio installation.

## Installing the dependencies

### git

git can be obtained from:

https://git-scm.com/download/win

- Download the file that is appropriate for your machine

  example: `64-bit Git for Windows Setup`
- Install the software (e.g. run the downloaded installer)

one should now have windows explorer integration to:

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

#### Installing wxWidgets on Windows

Download wxwidgets from (installer source code):
https://www.wxwidgets.org/downloads/

- Install the contents on the recommended folder (e.g. c:\wxWidgets-3.1.5)
- Build wxwidgets with visual studio:
  
  - Open c:\wxWidgets-3.1.5\build\msw\wx_vc16.sln (or take the highest number available)
  - Accept convert solution suggestion: convert solution to newer version studio
  - Build the solution for:
    - static Win32 library for Debug & Release
    - static x64 library for Debug & Release

### Cmake information

More information on Cmake and Visual studio can be found [here](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170).
