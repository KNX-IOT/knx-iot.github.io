---
layout: single
title: Getting Started with building your own device
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
  - [See information about building on Linux](building_linux).
  - [See information build building on Windows](building_windows).

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

The basics of the concept of data points and functional blocks is explained [here](knx_ipa.md#functional-blocks--data-points).

Each resource type is represented by a URI (Uniform Resource Identifier) which uniquely maps the resource's data point type with a functional block type. For example, the resource type with URI `urn:knx:dpa.421.61` represents a data point type of 61 in functional block type 421. This makes it so that a data point type can be uniquely located, because the resource type indicates which functional block the data point type belongs to. For example, if there was also a data point type 61 in a functional block type 422, then the URI for both resource types (the one having the data point type in fb 421 and 422) will be different, even though the data point type itself is the same.

A KNX device can have multiple instances of the same functional block type (e.g. multiple instances of functional block type 421), each containing the same data point types (e.g. data point type 61). Therefore, each data point instance within a functional block instance needs to be given a unique instance identifier in order to distinguish it from the other instances. This is done by calling the function `oc_resource_set_function_block_instance()`. Note: If there is only one instance of a functional block type, then that function doesn't need to be called, and the instance id will be set to 0 by default.

The following diagram illustrates the hierarchical relationship between functional blocks and data points, as well as the mapping to resources.

```
 /f
  |--- /f/<fb0>            < - functional block 1
  |        |--- p/o_1_1    <-- data point 1 of fb 1
  |        |--- p/o_2_2    <-- data point 2 of fb 1
  |
  |--- /f/<fb1>            < - functional block 2
  |        |--- p/o_3_3    <-- data point 1 of fb 2
  |        |--- p/o_4_4    <-- data point 2 of fb 2
```

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
