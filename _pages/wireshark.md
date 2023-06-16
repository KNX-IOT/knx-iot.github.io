---
layout: single
title: Getting Started with Wireshark
overview: true
permalink: /wireshark/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

Wireshark is a tool to analyze network traffic.
Since KNX-IOT is all about IPV6 network traffic, wireshark can be used to analyze the network traffic of KNX-IOT.

## Setup of Wireshark

Download and install wireshark from:

[wireshark](https://www.wireshark.org/)

## Usage (sniffing on PC)

1. Start wireshark

   This should now be an option in the start menu.

   This should open the following start screen:
   ![wireshark main](/assets/images/wireshark_main.png)
   This shows the availble network interfaces.
   For communication on the same pc select the loop back adapter.
   This can be used when the virtual devices are running on the same PC.

   Note: For capturing traffic between PC and other (physical) devices other interfaces needs to be selected, this depends on the PC and network configuration.

2. The data is being captured.
3. When enough data is captured one can stop capturing by pressing the `red` button.
4. To analyse the communication: 
   select a packet with protocol `OSCORE`. This is the security protocol used by KNX-IOT.
   To be able to see the encrypted data one should add the OSCORE security keys. This can be done via the popup menu structure below:
   ![wireshark oscore](/assets/images/wireshark_oscore.png)

5. The security credentials needs to be entered in the `Security Context` popup window.
   ![wireshark credentials](/assets/images/wiresshark_securitycontexts.png)
   To add credentials press the `+` sign at the bottom of the window
   This action creates a new line and one can add the SenderID & Recipient id of the traffic (take the sender and recipient id from wireshark).
   The master secret needs to come from the application.

6. When the credentials are entered then the stream can be decoded.
   The contents of the stream is visualized as a tree in the packet window. The tree can be expanded by pressing the tree sign (`>`).
   ![wireshark decoded](/assets/images/wireshark_decoded.png)
   To make the OSCORE (decoded) payload visible one should press `Object Security for Constrained Restful Environments`.
   Toe make the CBOR content visible one should press the
   `Consise Binary Object Representation`. The CBOR has different levels and can be expanded further.
   To understand CBOR, please take a look at [cbor.me](https://cbor.me/).

   If the credentials are not correctly entered, then the stream can't be decrypted and message `[Expert Info (Warning/Undecoced): Security context not set - can't decrypt]` is shown instead.



## Usage (sniffing on Thread)

   [Thread sniffer](https://github.com/Cascoda/cascoda-sdk/blob/master/posix/app/sniffer/README.md#configuring-wireshark)
