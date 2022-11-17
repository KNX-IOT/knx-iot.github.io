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

This page describes Getting Started with KNX IoT Point API development on Windows.
The build system enviroment is Cmake, so one can use:

- Visual Studio
- nmake (from the commandline)

## Prerequisites 

- Windows (10) machine
- Installed software:
  - git
  - Visual Studio
  - cmake
    - Python 
  
## Installing the dependencies

You can skip this section if you already have all the dependencies.

### git

git can be obtained from:

https://git-scm.com/download/win

- Download the file that is appropriate for your machine

  example: `64-bit Git for Windows Setup`
- Install the software (e.g. run the downloaded installer)

one should now have windows explorer integration to:

- Git Gui Here (to push data)
- Git Bash Here (a bash shell for commandline git)

### CMake

CMake has the following dependencies that needs to be installed:
- Perl 
- Python 
- cmake itself

#### Python 

Building and configuring wxWidgets with CMake requires Python. 

If Python is not installed then install it via a Windows installer available at:

https://www.python.org/downloads/

To check if Python is installed:

```bash
# do in a bash window (e.g. Git bash)
which python
# result should be
# <some path>/python
```

### Visual Studio

download Visual Studio from :

https://visualstudio.microsoft.com/downloads/

Install the package which includes C++ (Desktop development with C++).

### Cmake information

More information on Cmake and Visual Studio can be found [here](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio?view=msvc-170).

## Build steps

1. Make sure you have the full environment installed
   1. [git](#git)
   2. [Visual Studio with C++](#VisualStudio)
   3. [CMake](#CMake)

2. Getting the code
   clone the repo to a local folder

   From GitHub:

   ```bash
   # do from your working folder
   git clone --recurse-submodules https://github.com/KNX-IOT/KNX-IOT-STACK.git
   # do cd into the created folder
   cd KNX-IOT-STACK
   ```

   or from GitLab:

   ```bash
   # do from your working folder
   git clone --recurse-submodules https://gitlab.knx.org/shared-projects/knx-iot-point-api-public-stack.git
      # do cd into the created folder
   cd knx-iot-point-api-public-stack
   ```

3. Build the code with Visual Studio

   - Open Visual Studio
     - Open cmake project by:

     - File -&gt; Open -&gt; Cmake

       ![VisualStudio](/assets/images/visualstudio-cmake.png)

     - Select the CMakefile.txt from the working folder `<working folder>\KNX-IOT_STACK` or  `<working folder>\ knx-iot-point-api-public-stack`
     - Wait until Visual Studio prepared the project

4. Use Visual Studio to build the executables:

   - Build -&gt; Build All (Ctrl+shift+B)

   - The executables are created in the project.

    The executables can be found in folder:
    `\KNX-IOT-STACK\out\build\x64-Debug`

    Note: The actual path of the executables is dependent on the Visual Studio configuration.

5. Debug an application

   - Select Startup Item -&gt; down button
     - Select item (for example: LSSB_minimal_all.exe)
      ![SelectItem](/assets/images/vs_select_startup.png)

     - Press the debug symbol (green "play button"), or F5
     - A commandline window will appear with the logging of the KNX application

## Build architecture

The Build architecture (win32 or x86) is dependent on the Visual Studio installation.
