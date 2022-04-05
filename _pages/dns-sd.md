# DNS-Based Service Discovery within KNX-IoT

The KNX-IoT features Multicast DNS based Service Discovery. KNX servers
advertise their KNX Serial Number, KNX Individual Address and KNX Installation
IDs using PTR Resource records, which can be discovered using Multicast DNS.
This enables KNX-IoT devices to be discoverable on the local network with
essentially zero configuration.

## Dependencies

On Ubuntu & Debian systems, you must install `avahi-utils` package before DNS-SD
will work within the KNX-IoT stack.

## Hostname

The KNX-IoT specification mandates that the hostname of a KNX device must be in
the format {serialnumber}.knx.local. However, modifying the hostname of a
computer from within a C program is highly intrusive and it requires superuser
privileges, so the KNX-IoT stack does not do this by default. 

In order to be KNX-IoT compliant, products must ensure that their hostname
obeys the {serialnumber}.knx.local format. On Ubuntu & Debian based systems,
this can be done by overwriting the contents of the /etc/hostname - the change
will take place upon the next reboot.

## Discovery Example

Devices in programming mode advertise the _ia0 subtype, which can be discovered
by avahi-browse as folows:

```
$ avahi-browse -rt _ia0._sub._knx._udp
+ enp6s0 IPv6 000003                                        _knx._udp            local
+ enp6s0 IPv4 000003                                        _knx._udp            local
= enp6s0 IPv6 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
```

Devices can also be discovered based on their serial number. Note that the
advertised service for the serial number is prefixed with an underscore.

```
$ avahi-browse -rt _000003._sub._knx._udp
+ enp6s0 IPv6 000003                                        _knx._udp            local
+ enp6s0 IPv4 000003                                        _knx._udp            local
= enp6s0 IPv6 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
```

After programming, devices can be discover based on their IA & IID. In the
example below, the device lives on Installation ID 5, with an individual
address of 1. Note that discovery using _ia0 is no longer successful.

```
$ avahi-browse -rt _ia5-1._sub._knx._udp
+ enp6s0 IPv6 000003                                        _knx._udp            local
+ enp6s0 IPv4 000003                                        _knx._udp            local
= enp6s0 IPv6 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [2a00:23a8:89b:da00:ba27:ebff:fed5:c652]
   port = [5683]
   txt = []
= enp6s0 IPv4 000003                                        _knx._udp            local
   hostname = [000003.knx.local]
   address = [192.168.202.161]
   port = [5683]
   txt = []
$ avahi-browse -rt _ia0._sub._knx._udp
$
```