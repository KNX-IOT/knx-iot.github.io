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

https://www.wireshark.org/

## Usage

1. Start wireshark

   This should now be an option in the start menu.

   This should the following start screen.
   ![wireshark main](/assets/images/wireshark_main.png)
   for communication on the same pc select the loop back adapter.
   This can be used when the virtual devices are running on the same PC.
2. The data is being captured
   select a OSCORE communication. This is the security protocol used by KNX-IOT.
   To be able to see the encrypted data one should add the OSCORE security keys. This can be done via the popup menu structure below:
   ![wireshark oscore](/assets/images/wireshark_oscore.png)

3. The security credentials needs to be entered in the `Security Context` popup window.
   ![wireshark credentials](/assets/images/wiresshark_securitycontexts.png)
   To add credentials press the `+` sign at the bottom of the window
   This action creates a new line and one can add the SenderID & Recipient id of the traffic (take the sender and recipient id from wireshark).
   The master secret needs to come from the application.

4. When the credentials are entered then the stream can be decoded.
   The contents of the stream can be made visible by pressing the ">" sign in the window at each level.
   ![wireshark decoded](/assets/images/wiresshark_decoded.png)
   To make the OSCORE (decoded) payload visible one should press `Object Security for Constrained Restful Environments`.
   Toe make the CBOR content visible one should press the
   `Consise Binary Object Representation`. The CBOR has different levels and can be expanded further.