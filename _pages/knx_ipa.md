---
layout: single
title: What is KNX IoT Point API
overview: true
permalink: /knx_ipa/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## What is KNX IoT Point API

The KNX IoT Point API is an extention of the suite of KNX physical transmission medias.
The KNX IoT Point API products can be used with existing KNX products in a single system. KNX IoT Point API is an evolution of the KNX system.


### Technical Background

KNX IoT Point API is a new specification in the KNX system specifications group.
e.g. 3_10_5 KNX IoT Point API.

The specification describes:
- A new transport layer based on IPV6, e.g. suitable for [Thread based networks](https://www.threadgroup.org/).
- A new communication/message protocol using [CoAP](https://www.rfc-editor.org/rfc/rfc7252) and [CBOR](https://www.rfc-editor.org/rfc/rfc8949.html)
- using the same functional blocks as the other KNX transport layers
- using the same s-mode message semantics as the other KNX transport layers
- same configuration data to configure which device is talking to which device 

Hence KNX Iot Point API conveyes the same semantic data on the transport layer as an KNX TP implementation.
therefore the interworking between KNX IoT Point API and the other KNX technologies is garanteed.

#### What is new:

- The KNX IoT Point API is secured (on Application layer) by default.
- Mandatory software update mechanism included.


### How to combine KNX TP and KNX IoT Point API

Since KNX IoT is semantic equivalent as another KNX transport layer, interworking between KNX IoT Point API and KNX TP is possible through an `iot router`.
The `iot router` converts messages from TP (or IP) to KNX IoT Point API messages.

![iot router ](/assets/images/iot-router.jpg)

### What are the advantages of KNX IoT Point API?

The advantages is that the new technology is IPV6 ready. So [Thread](https://www.threadgroup.org/) based devices can be made with KNX IoT Point API.
Advantages of Thread are:

- Meshed networking, e.g. covering a large area
- Using the same radio across the world, e.g 1 product that can be used in all regions of the world
- Low power end devices, devices can go to sleep and reattach to the network when waking up.