---
layout: single
title: S-Mode functioning
overview: true
permalink: /architecture-smode/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
toc_sticky : true
---
## Introduction

The run time operation of KNX is s-mode communication.
An s-mode message is a group communication that contains info :

- group number
- the new value of the communication
- transport flags

The s-mode messages are secured with OSCORE.

## Stack Features

The stack supports sending and receiving of s-mode messages.
The routing of these messages is implemented in the stack.

The routing of the s-mode messages outside the device is achieved via the Group Object Table. The Group Object table translates between the Group Ids and the url to be used.

The device that implements as sensor (e.g. sending) will have to use specific function to s-mode messages and implement resources with GET.
For sending an s-mode message, the url of the device resource is used. The logic will do an GET on that resource to fetch the value to be send in each s-mode message.

![s-mode send](https://KNX-IOT.github.io/KNX-IOT-STACK/images/sequence_send_s-mode.png)

The device that implements an actuator (e.g. receives) will have have to implement resources with POST to receive the value.
For receiving the url is translated the local url on the device. On this url the POST command is called (similar as a regular CoAP POST) with the received value of the s-mode message.

![s-mode receive](https://KNX-IOT.github.io/KNX-IOT-STACK/images/sequence_receive_s-mode.png)
