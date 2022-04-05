---
layout: single
title: Architecture
overview: true
permalink: /architecture/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
toc_sticky : true
---
## Introduction

KNX IoT Point API stack is an open-source, reference implementation of the KNX IoT Point API specification.

## Stack Assumptions

The assumptions of the stack is to abstract as much functionality as possible.
This way the code that a manufactorer needs to write should be as small as possible.
Hence the stack has an API to create a device and add resources to the device.
Each resource represents a datapoint belonging to a function block.
A resource will have a GET (read) and a POST (write/update) handler.

## Stack Features

![Stack features](/assets/images/knxstack-v1.png)

* OS agnostic: The stack and modules work cross-platform (pure C code) and execute in an event-driven style.
  The stack interacts with lower level OS/hardware platform-specific functionality through a set of abstract interfaces.
  This decoupling of the common  standards related functionality from platform adaptation code promotes ease of long-term maintenance and evolution of the stack through successive releases of the KNX IoT Point API specifications.

* Porting layer: The platform abstraction is a set of generically defined interfaces which elicit a specific contract from implementations.
  The stack utilizes these interfaces to interact with the underlying OS/platform.
  The simplicity and boundedness of these interface definitions allow them to be rapidly implemented on any chosen OS/target.
  Such an implementation constitutes a "port". ![porting layer](/assets/images/porting.png)

* message pump: All sending and received message are handled via a message pump.
  This means that no threading, semaphores or critical sections are used in the code. The message pump is dependend on the OS.
  The message pump is most of the time created in main. Examples of Windows and Linux main are supplied.
  Note that most of the examples are using compiler defines so that the examples can run on Linux and Windows.

* Callbacks: When there is specific functionallity that needs a manufactorer implementation, Callbacks are implemented in the stack.
  Typical functionality that is manufactorer dependend:

  * device (application) configuration
  * device reset
  * device restart
  * device software update
  * device host name

  Having a callback implemented in the stack avoids that the stack has to be changed to add specific application or manufactorer depended code.

## Next steps

Go to the [source](https://github.com/KNX-IOT/KNX-IOT-STACK)
