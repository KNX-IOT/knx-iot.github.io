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

For enroling a device the serial number and password needs to be known.

## KNX application format

The format is defined as: `KNX:S:serno;P:password`

where the fields are defined as:

- `KNX`: is a fixed prefix.
- `S`: means a KNX serial number follows, serno itself is encoded
       as 12 upper-case hexadecimal characters.
- `P`: means a password follows, password itself is just the KNX IoT Point API password;
       this works as the allowed password characters do not interfere with the
       separator characters colon and semicolon and are in the Alphanumeric range.

### Extended KNX application format

Since the QR code also can contain thread information the application format can be extended by prefixing the code. The delimiter is then &&. 
This allows to prefix the KNX application format with the QR info that is needed to enrole to thread network.
The Extended format then will be:

v=1&&eui=0000b57fffe15d68&&cc=J01NU5&&KNX:S:serno;P:password

- v : version of Thread QR code
- eui : eui of the thread device
- cc  : credential for onboarding

## KNX ISO format

The ISO 15418 standard specifies sets of Data Identifiers and Application Identifiers for the purpose of identifying encoded data, for example, in DMC codes. The following example shows an ISO 15418 encoded string w/ a device ASN and EUI64:

 `1PS55812-Y100+31POCT100.BR+2PFSA+16D20220512+43S015C00002D+3ZEUI:8CF681FFFE000001.P:ABCDEF.PA:994AC`

- 1P: SSN (order number)
- 31P: ASN (model) - planned to be removed to reduce print density for better scanning results
- 2P: Functional State -- 2PFSA for COMFORT products
- 16D: Production Date
- 41S: Serial Number -- 12-character hexadecimal KNX serial number
- 43S: Serial Number -- 10-character hexadecimal Siemens serial number
- 3Z: Free Text -- for custom data; . as field separator
- EUI: EUI-64
- P: Network Password (Thread joining Device Credential / default Commissioning Credential)
- PA: Application Password for SPAKE2+

In the case PA is absent, the Network Password is also used as Application Password (SPAKE2+)
