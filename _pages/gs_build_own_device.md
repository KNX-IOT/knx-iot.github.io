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

KNX IoT Point API devices can be made with the KNX-IOT-STACK repo.
However is not a good practice to create individual applications inside the same repo.
To overcome that hurdle a simple example application repo is created.
This getting started guide give some instructions on how to use the example application repo and what subsequent changes needs to be made to make a functional KNX IoT Point API application.

### Prerequisites

- Linux or Windows (build) PC:

### Essential information

- Linux or windows (build) PC:

  - [See build on Linux](/building_linux)
  - [See build on Windows](/building_windows)

## Download and Build the Example Application

```bash
# Clone the Stack
git clone https://github.com/KNX-IOT/Example-application.git
# go into the create repo
cd Example-application
# Make a working directory (named anything)
mkdir build
cd build 
# do the configur step, e.g. build the native make files
cmake ..
# build (Linux) the application (including sdk), the -j is the amount of processors the build will be using
make -j12
# Go back to working directory
cd ..
```

## Changing the application

The example application consist of a single datapoint, the data point for a push button. To change the behaviour:

- resource type, e.g. what the resource exposes.
- interfaces, what access control is wanted.
- GET/POST callbacks: functionality of the resource
- implements what needs to be exposed as data point (GET) and needs to be set as data point (POST)

### Adding additional resources

Additional resources are setup in function `register_resources`.
Each new resource will have:

1. Callbacks for handling GET and (optionally) POST
2. Global varialbes: to handle data incomming and outgoing via the callbacks.
3. Some logic that interacts with the underlaying hardware (out of scope of this document)
4. Storing data as persistent data.

### Data points types

The KNX data points are mapped on resources.
Hence the resource "rt" values are the data point types of KNX.
examples:

- urn:knx:dpa.421.61
- DPT_Switch
- :dpt.value2UCount

### Data points and functional blocks

The information of the data point types are used to map the data points into a function block. For example data point `urn:knx:dpa.421.61` will belong to functional block `urn:knx:fb.421`. Since it is allowed to have multiple instances of the same functional block/data point, one can set the instance id on a resource. Default is instance 0, so that for a single occurance of the data point this function does not have to be called.

The data point types dictates what kind of data will be exposed by the GET/POST functions.

Example of mapping of data points and c variables :

|  KNX data type |  JSON type | C variable type |
|----------------| -----------| --------------- |
| B1             | boolean    | bool            |
| U8             | integer    | int             |
| F16            | number     | float/double    |
| A8             | string     | oc_string_t     |

see also section 2.5.122.5.13 Datatype Mapping of the KNX IoT Point API specification.

### Interfaces

The data points have typically the interfaces to grant (security) access control.
For data points the following interfaces are defined:

- if.s (sensor interface) e.g. sending information
- if.a (actuator interface) e.g. receiving information that has to be acted upon.

Typical for data points only 1 interface type is defined.
When the interface type if.s is implemented the GET callback function has to be implemented.
When the interface type if.a is implemented the GET and POST callback functions have to be implemented.
