---
layout: single
title: DNS discovery
overview: true
permalink: /DNS/

sidebar:
  nav: "arch_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---

## DNS-Based Service Discovery within KNX IoT

The KNX-IoT features Multicast DNS based Service Discovery. KNX servers
advertise their KNX Serial Number, KNX Individual Address and KNX Installation
IDs using [PTR Resource records](https://datatracker.ietf.org/doc/html/rfc1035#section-3.3.12),
which can be discovered using Multicast DNS. This enables KNX-IoT devices to
be discoverable on the local network with essentially zero configuration.

### Dependencies

On Ubuntu & Debian systems, you must install `avahi-utils` package before DNS-SD
will work within the KNX-IoT stack.

On Windows, you will need to install Bonjour, which can be done using the Chocolatey
package manager: `choco install bonjour`

### Hostname

The KNX-IoT specification mandates that the hostname of a KNX device must be in
the format {serialnumber}.knx.local. However, modifying the hostname of a
computer from within a C program is highly intrusive and it requires superuser
privileges, so the KNX-IoT stack does not do this by default. 

In order to be KNX-IoT compliant, products must ensure that their hostname
obeys the {serialnumber}.knx.local format. On Ubuntu & Debian based systems,
this can be done by overwriting the contents of the /etc/hostname - the change
will take place upon the next reboot.

### Discovery Example

Devices in Programming Mode (as defined in the KNX-IoT Point API specification
section 2.5.3.9) advertise the _ia0 subtype, which can be discovered by
avahi-browse as folows:

```bash
$ avahi-browse -rt _ia0._sub._knx._udp
+ enp6s0 IPv6 00FA10010700                                        _knx._udp            local
+ enp6s0 IPv4 00FA10010700                                        _knx._udp            local
= enp6s0 IPv6 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
```

Devices can also be discovered based on their serial number. Note that the
advertised service for the serial number is prefixed with an underscore.

```bash
$ avahi-browse -rt _00FA10010700._sub._knx._udp
+ enp6s0 IPv6 00FA10010700                                        _knx._udp            local
+ enp6s0 IPv4 00FA10010700                                        _knx._udp            local
= enp6s0 IPv6 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
```

After programming, devices can be discover based on their IA (Individual
Address) & IID (Installation ID). The KNX Point API Specification defines the
subtype for programmed devices as follows:
_ia{installationid}-{ia}._sub._knx._udp

In the example below, the device lives on
Installation ID 5, with an individual address of 1.

```bash
$ avahi-browse -rt _ia5-1._sub._knx._udp
+ enp6s0 IPv6 00FA10010700                                        _knx._udp            local
+ enp6s0 IPv4 00FA10010700                                        _knx._udp            local
= enp6s0 IPv6 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 00FA10010700                                        _knx._udp            local
   hostname = [00FA10010700.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
```

