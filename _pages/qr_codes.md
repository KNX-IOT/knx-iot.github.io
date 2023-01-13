---
layout: single
title: QR codes
overview: true
permalink: /qr_codes/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

For enroling a device the serial number and password needs to be known

The format is defined as: `KNX:S:serno;P:password`

where the fields are defined as:

- `KNX`: is a fixed prefix.
- `S`: means a KNX serial number follows, serno itself is encoded
       as 12 upper-case hexadecimal characters.
- `P`: means a password follows, password itself is just the KNX IoT Point API password;
       this works as the allowed password characters do not interfere with the
       separator characters colon and semicolon and are in the Alphanumeric range.
