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

The run-time operation of KNX is s-mode communication.
An s-mode message is a group communication message that contains the following info :

- Sender individual addres (sia)
- Group number (ga)
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
The routing of these messages is implemented in the stack.

The routing of the s-mode messages outside the device is achieved via the Group Object Table. The Group Object table translates between the Group Ids and the url to be used.

The device that implements a sensor (i.e. sends data) will have to use specific function to s-mode messages and implement resources with GET.
For sending an s-mode message, the url of the device resource is used. The logic will do a GET on that resource to fetch the value to be sent in each s-mode message.

![s-mode send](https://github.com/KNX-IOT/KNX-IOT-STACK/raw/master/images/sequence_send_s-mode.png)

The device that implements an actuator (i.e. receives data) will have have to implement resources with POST to receive the value.
For receiving, the url is translated to the local url on the device. On this url the POST command is called (similar as a regular CoAP POST) with the received value of the s-mode message.

![s-mode receive](https://github.com/KNX-IOT/KNX-IOT-STACK/raw/master/images/sequence_receive_s-mode.png)
