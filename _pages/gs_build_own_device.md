---
layout: single
title: Build your own device
overview: true
permalink: /build_own_device/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

KNX IoT Point API devices can be made with the [KNX-IOT-STACK repository](https://github.com/KNX-IOT/KNX-IOT-STACK). However, it is best practice to have a separate repository where applications can be developed on top of the stack, rather than building the applications within the same repository as the stack. For that reason, a simple [example application repository](https://github.com/KNX-IOT/Example-Application) has been created. 

This getting started guide provides instructions on how to use the example application repository, and what subsequent changes need to be made to develop a functional KNX IoT Point API application.

## Prerequisites

- Linux or Windows PC. The full list of prerequisites is available in the links below.
  - [See information about building on Linux](/_pages/building_linux).
  - [See information build building on Windows](/_pages/building_windows).

## Download and Build the Example Application

```bash
# Clone the repository 
git clone https://github.com/KNX-IOT/Example-Application.git
# Go into the cloned repo
cd Example-Application
# Make a build directory (named anything)
mkdir build
cd build 
# do the configuration step, to build the native make files
cmake ..
```

Then if you are using Linux:

```bash
make -j12
#  go back to the source directory
cd ..
```

If you are using Windows, open the `example-application.sln` file in Visual Studio, and Build Solution.

## Changing the application

The example application consists of a single datapoint for a push button. To change this, you can modify the following things:

- Resource type, e.g. what the resource exposes.
- Interfaces, what access control is wanted.
- GET/POST callbacks: functionality of the resource.
- Whether the resource can be read or written to via GET or POST.

### Adding additional resources

Additional resources are setup in the `register_resources()` function.
Each new resource will have:

1. Callbacks for handling GET and (optionally) POST.
2. Global varialbes: to handle incoming and outgoing data via the callbacks.
3. Some logic that interacts with the underlying hardware (out of scope of this document).
4. The option to store data persistently.

### Data point types

The KNX data points are mapped to resources.
Hence the value of a resource's "rt" member contains the data point types of KNX.
examples:

- urn:knx:dpa.421.61

### Data points and functional blocks

The information of the data point types are used to map the data points into a functional block. For example, data point `urn:knx:dpa.421.61` will belong to functional block `urn:knx:fb.421`. Since there can be multiple instances of the same functional block/data point, one can set the instance id on a resource. Default is instance 0, so that for a single occurrence of the data point this function does not have to be called.

The data point types dictate what kind of data will be exposed by the GET/POST functions.

Example of mapping of data point types and C variables:

|  KNX data type |  JSON type | C variable type |
|----------------| -----------| --------------- |
| B1             | boolean    | bool            |
| U8             | integer    | int             |
| F16            | number     | float/double    |
| A8             | string     | oc_string_t     |

See also section 2.5.122.5.13 Datatype Mapping of the KNX IoT Point API specification.

### Interfaces

The data points typically have the interfaces to grant (security) access control.
For data points, the following interfaces are defined:

- if.s (sensor interface) e.g. sending information
- if.a (actuator interface) e.g. receiving information that has to be acted upon.

Data points typically only have one interface type defined.
When the interface type `if.s` is implemented, the GET callback function has to be implemented.
When the interface type `if.a` is implemented, the GET and POST callback functions have to be implemented.
