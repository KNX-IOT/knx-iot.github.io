---
layout: single
title: What is KNX IoT Point API
overview: true
permalink: /knx_ipa/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## Introduction

The KNX IoT Point API is an extension of the suite of KNX physical transmission medias.
The KNX IoT Point API is part of [KNX IoTech](https://www.knx-iotech.org/) as part 3.10.5.
The transmission media is IPv6 hence future proofing KNX and can be used on a variety of phyiscal transports.
The KNX IoT Point API products can be used with existing KNX products in a single system.
For example it can be combined with existing product on Twisted Pair (TP), KNXnet/IP using IPV4 and KNX-RF using radio transmission on 868 MHz.
KNX IoT Point API is an evolution of the KNX system and being IPV6 it can be used with various networking mechanisms.

The most common usage of KNX is using the TP variant using cables.

| ![Knx bus diagram ](/assets/images/OIP.jpg) |
|:--:|
| <b>KNX bus diagram</b>|

Resulting in using large cabinets to hook up all the devices.

| ![Knx bus cabinet ](/assets/images/knx-cabinet.jpg) |
|:--:|
| <b>KNX cabinet</b>|

The most interesting one is Thread, capable of creating a large area, wireless meshed IPV6 network.
Using Thread based devices will reduce the typical KNX bus wiring.

### Technical Background

KNX IoT Point API is a new specification in the KNX system specifications group.
e.g. 3_10_5 KNX IoT Point API.

The specification describes:

- A new transport layer based on IPV6, e.g. suitable for [Thread based networks](https://www.threadgroup.org/).
- A new communication/message protocol using [CoAP](https://www.rfc-editor.org/rfc/rfc7252) and [CBOR](https://www.rfc-editor.org/rfc/rfc8949.html).
- Using the same functional blocks as the other KNX transport layers.
- Using the same s-mode message semantics as the other KNX transport layers.
- Using the same configuration data to configure which device is talking to which device.

Hence KNX IoT Point API conveyes the same semantic data on the transport layer as an KNX TP implementation.
therefore the interworking between KNX IoT Point API and the other KNX technologies is garanteed.

#### Functional Blocks / Data points

The application domain in KNX is described by functional blocks. The Functional Blocks are a consistent set of data points that describe the domain.
There can be mandatory and optional data points in a functional block.
Functional Blocks are described in the KNX specification volume 7: Application descriptions.

An example of a functional block is Light Switching Sensor Basic (LSSB), which provides hardwired inputs or local push-button/HMI functionality to trigger output messages to control the On/Off status

Since the LSSB is a Sensor, it sends out the triggers to the Acutators FB Light Switching Actuator Basic (LSAB) or FB Light Dimming Actuator Basic (LDAB).
Next to the data point that sends out these triggers, there is another data point that receives status feedback messages from light switching/dimming actuators.


#### Configuration Data

The KNX devices needs to be configered, e.g. for sensor data points, the Management Client (MaC) needs to set up in the Tables:

- Which group address is being used to send the data
- Which multicast address is being used to communicate
- Whether it allowed to send the message
- The data point is identified by the MaC by its url

For the actuator data points, the Management Client (MaC) needs to set up:

- Which group address is being used for receiving the data
- Which multicast address is being used to communicate
- Whether the data is to be interpreted (acted upon) by the device
- The data point is identified by the MaC by its url

#### IPV6

IPV6 can run over different cables and can be used wireless.
Ethernet cables like CAT6 can be used for wired networking, also an option to use PoE (Power over Ethernet) to power devices connected via Ethernet cables.
Next to wired solutions, IPV6 can run over Wifi and [Thread based networks](https://www.threadgroup.org/).

#### What is new

- The KNX IoT Point API is secured (on Application layer) by default.
- Mandatory software update mechanism included.

### How to combine KNX TP and KNX IoT Point API

Since KNX IoT is semantic equivalent as another KNX transport layer, interworking between KNX IoT Point API and KNX/TP and KNXnet/IP is possible through an `iot router`.
The `iot router` converts messages from KNX/TP (or KNXnet/IP) to KNX IoT Point API messages.

| ![Knx iot router ](/assets/images/iot-router.jpg) |
|:--:|
| <b>KNX IoT Router</b>|

### What are the advantages of KNX IoT Point API?

The advantages of KNX IoT Point API is that the new technology is IPV6 ready and is using the latest (newest) IETF technologies in the specifications.
The stack implementing the KNX IoT Point API therefore is quite small and can run on MCU devices with only 100kb of memory.
Also due to the usage of the latest IETF technologies in the specification is secure by design.

[Thread](https://www.threadgroup.org/) based devices can be made with KNX IoT Point API.
Advantages of Thread are:

- Meshed networking, e.g. covering a large area.
- Using the same radio across the world, e.g 1 product that can be used/sold in all regions of the world.
- Low power end devices, devices can go to sleep and reattach to the network when waking up.
