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

KNX IoT Point API is based on IPv6. Hence an IPv6-based network needs to be available to connect to.
This introduction is how to commision the Thread device on the Thread network.
This is needed before KNX IoT Point API configuration starts (e.g. download tables and setup the security)

## Prerequisites

- Thread Border Router
  - [Cascoda Border Router](https://www.cascoda.com/products/border-router/)
  - [Kirale Border Router](https://www.kirale.com/products/ktbrn1/)
- Thread-based device
  - [Cascoda Chili2D](https://www.cascoda.com/products/module/chili2/)
  - [Kirale KTDG102](https://www.kirale.com/products/ktdg102/)
  - [Nordic nRF52840](https://www.nordicsemi.com/Products/Development-hardware/nrf52840-dongle)
- Android phone
- Wi-Fi connection

## Essential information

- Thread network information
- Device information
  - EUI64 & Joiner credential
  - QR code (same information)

## Steps to commision a device on the network

1. Connect the Thread Border Router to the larger Wi-Fi network.

1. Install the [thread commissioning app](https://play.google.com/store/apps/details?id=org.threadgroup.commissioner&hl=en&gl=US)

1. Open the Thread application on the phone.
   - note that the phone needs to be connnected to the Wi-Fi network.
     The same Wi-Fi network that is used with the Thread Border Router.

1. Select a Border Router in the application.

1. Select adding a device.
   - Select scan QR code, if you have an QR code.
     - Wait until commisioning is finished.
   - Select enter connect code.
     - Enter EUI64 & joiner credential.
     - Wait until commisioning is finished.

Note: the QR code encodes a string which is formatted as shown in the following example: `v=1&&eui=0000b57fffe15d68&&cc=J01NU5`.

## More information

Thread topology explained:
[Thread topology](https://www.threadgroup.org/BUILT-FOR-IOT/Commercial#NetworkTopology)
