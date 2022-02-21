---
layout: single
title: Architecture
overview: true
permalink: /architecture/

sidebar:
  nav: "doc_nav"

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
toc_sticky : true
---
## Introduction

KNX-IOT stack is an open-source, reference implementation of the KNX-IOT specification.

## Stack Features

![Stack features](/assets/images/knxstack-v1.png)

* OS agnostic: The stack and modules work cross-platform (pure C code) and execute in an event-driven style.
  The stack interacts with lower level OS/hardware platform-specific functionality through a set of abstract interfaces. This decoupling of the common  standards related functionality from platform adaptation code promotes ease of long-term maintenance and evolution of the stack through successive releases of the KNX-IOT specifications.
  ![porting layer](/assets/images/porting.png)

* Porting layer: The platform abstraction is a set of generically defined interfaces which elicit a specific contract from implementations.
  The stack utilizes these interfaces to interact with the underlying OS/platform. 
  The simplicity and boundedness of these interface definitions allow them to be rapidly implemented on any chosen OS/target. 
  Such an implementation constitutes a "port".

## Next steps

Go to the [source](https://github.com/KNX-IOT/KNX-IOT-STACK)
