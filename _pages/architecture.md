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

## Stack tenets 

The stack implements as much functionality as possible, and abstracts it away.
This way the code that a manufacturer needs to write should be as small as possible.
Hence the stack has an API to create a device and add resources to the device.
Each resource represents a datapoint belonging to a function block.
A resource will have a GET (read) and a POST (write/update) handler.
The resources will be used to send or receive s-mode messages and the unicast publish/subscribe messages.


## Stack Features

![Stack features](https://raw.githubusercontent.com/KNX-IOT/KNX-IOT-STACK/master/images/knxstack-v1.png)

* OS agnostic: The stack and modules work cross-platform (pure C code) and execute in an event-driven style.
  The stack interacts with lower level OS/hardware platform-specific functionality through a set of abstract interfaces.
  This decoupling of the common  standards-related functionality from platform adaptation code promotes ease of long-term maintenance and evolution of the stack through successive releases of the KNX IoT Point API specifications.

* Porting layer: The platform abstraction is a set of generically defined interfaces which elicit a specific contract from implementations.
  The stack utilizes these interfaces to interact with the underlying OS/platform.
  The simplicity and boundedness of these interface definitions allow them to be rapidly implemented on any chosen OS/target.
  Such an implementation constitutes a "port". ![porting layer](https://raw.githubusercontent.com/KNX-IOT/KNX-IOT-STACK/master/images/porting.png)

* message pump: All sending and receiving message are handled via a message pump.
  This means that no threading, semaphores or critical sections are used in the code. The message pump is dependent on the OS.
  The message pump is most of the time created in the main function of the application.
  Examples of Windows and Linux main functions are supplied.

  Note that most of the examples are using compiler defines so that the examples can run on Linux and Windows.

* Implements generic KNX IoT Point API infrastructure
  
  * KNX config information
    * installation id
    * individual address
    * serial number
    * Tables:
      * Group object Table
      * Publisher Table
      * Recipient Table
      * Security (auth/at) Table

  All configuration data is stored persistently.

* Data point API

    API to create a data point in a functional block

    * GET callback
    * POST callback (if needed)
    * Setting DPT (Data Point Type) and DPA (Data Point Annotation)

* Application callbacks: When there is specific functionality that needs a manufacturer implementation, callbacks are implemented in the stack.
  Typical functionality that is manufacturer dependent:

  * Device (application) configuration
  * Device reset
  * Device restart
  * Device software update
  * Device host name

  Having a callback implemented in the stack avoids that the stack has to be changed to add specific application or manufacturer dependent code.

## Next steps

1. Go to the [stack source](https://github.com/KNX-IOT/KNX-IOT-STACK)
1. Go to the [simple example](https://github.com/KNX-IOT/Example-Application)
