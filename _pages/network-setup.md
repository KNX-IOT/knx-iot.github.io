---
layout: single
title: Getting Started with Thread
overview: true
permalink: /getting_started_network/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

KNX IoT Point API is based on IPV6. Hence an IPV6 based network needs to be available to connect too.
This introduction is how to commision the thread device on the thread network.
This is needed before KNX IoT Point API configuration starts (e.g. download tables and setup the security)

### Prerequisites

- Thread Border router
- Thread based device
- android phone
- Wifi connection

### Essential information

- Thread network information
- Device information
  - EUI64 & Joiner credential
  - QR code (same information)

## Steps to commision a device on the network

1. Connect the Thread border router to the larger network, e.g. making sure there is wifi

1. Install the [thread application](https://play.google.com/store/apps/details?id=org.threadgroup.commissioner&hl=en&gl=US)

1. open the thread application on the phone
   - note that the phone needs to be connnected to the wifi network.
     The same wifi network that is used with the Thread border router.

1. select a border router in the application.

1. select adding a device
   - select scan QR code, if you have an QR code
     - wait until commisioning is finished
   - select enter connect code
     - enter EUI64 & joiner credential
     - wait until commisioning is finished

Note the QR code of the commisioning app: example:
v=1&&eui=0000b57fffe15d68&&cc=J01NU5

## More information

Thread topology explained:
[Thread topology](https://www.threadgroup.org/BUILT-FOR-IOT/Commercial#NetworkTopology)
