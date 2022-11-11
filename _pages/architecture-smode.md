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

The run-time operation of KNX is (standard) s-mode communication.
The s-mode messages are sent by sensors and interpreted by actuators, according to their configuration.
The s-mode messages are sent to a single device or group of devices, the sender does not know who is receiving the message.
In that sense, the sensor sending an s-mode message is performing a publish (of the publish/subscribe paradigm).
The actuator is receiving the message without prior information on where the message is comming from, (i.e. implementing the subscribe of the publish/subscribe paradigm)
Note that multiple sensors and actuators can be active (configured) in a KNX system.

An s-mode message is a group communication message that contains the following info :

- Sender individual addres (sia)
- Group address (ga)
- The value of data point in the message (value)
- Transport flags (st)
  - "r" read
  - "w" write
  - "rp" response (on a read)

There are 2 notations for s-mode messages in the specifications:

- JSON notation
- JSON notation with integer keys

```bash
s-mode message in json notation

{ "sia": <sia>, "s": { "st": <st>, "ga": <ga>, "value": <value> } }

s-mode message in json notation with integer keys)

{ 4: <sia>, 5: { 6: <st>, 7: <ga>, 1: <value> } }

```

Note: On the wire, s-mode messages represented using JSON notation with integer keys are encoded using CBOR. This ensures that the messages are small.

The s-mode messages are secured with OSCORE.

## Stack Features

The stack supports sending and receiving of s-mode messages.
The routing of the s-mode messages is implemented in the stack.

The routing of the s-mode messages outside the device is achieved via the Group Object Table.
The Group Object table translates between the Group Ids and the url to be used.

The device that implements a sensor will have to implement a resource (datapoint) with the GET function.
The stack supplies a function that will retrieve the data from the resource and send out the s-mode message with the value of the datapoint.
Since the function to send an s-mode message is generic, one of the arguments of the function is the url of the datapoint.

![s-mode send](https://github.com/KNX-IOT/KNX-IOT-STACK/raw/master/images/sequence_send_s-mode.png)

The device that implements an actuator (e.g. receives messages) will have have to implement the data point as resources with the function POST.
The stack will translate the group address via the group object table to the url of the datapoint.
The POST of the datapoint implementation is called with the actual value of the s-mode message. The implementation of the POST needs to do the actual actuation of the hardware (e.g. turn on/off a light).



![s-mode receive](https://github.com/KNX-IOT/KNX-IOT-STACK/raw/master/images/sequence_receive_s-mode.png)
