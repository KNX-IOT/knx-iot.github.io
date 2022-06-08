---
layout: single
title: Configuring Devices
overview: true
permalink: /gs_knx_config/

sidebar:
  nav: "gs_nav"

toc: true
toc_label: Table of Contents
toc_icon: cog
toc_sticky : true
---


## Introduction

When the KNX devices are running, they are running without a configuration.
Hence python scripts are provided that can configure the devices.
The scripts are using the serial number (of the device) to find the device on the network and talk to the device.

## Python scripts

The python scripts are a set of applications that can perform tasks that ETS can do.
for example:

- searching for devices
- issuing s-mode messages
- listening to s-mode messages
- configuring a device

Each python script has the -h option to show the command line parameters.

Note that the underlaying code is KNX.org owned.

### Downloading the python scripts

The python scripts can be downloaded from the [release page of the KNX IoT Stack](https://github.com/KNX-IOT/KNX-IOT-STACK/releases)

The files to download and unzip are:

- python_release_no_security.zip
  scripts with security disabled
- python_release_security.zip
  scripts with security enabled

All scripts should be run from the folder `<install folder>\python_apps`.

### reset_device.py

script to reset the device, issuing:

- discovery with serial number
- POST to /a/sen with the reset command

```bash
python reset_device.py -h
```

### list_devices.py

script to list the device, issuing:

- discovery of device with internal address using query : if=urn:knx:ia.[ia]
- discovery of device in programming mode using query : if=urn:knx:if.pm
- discovery of device with a serial_number using query : ep=urn:knx:sn.[serial_number]
- discovery of device using a group_address using query : d=urn:knx:g.s.[group_address]
- discovery with query : rt=urn:knx:dpa.*

```bash
python list_devices.py -h
```

### s-mode.py

script to issue an s-mode command

- has option to set the various values in the command.

```bash
python s-mode.py 
```

### sniffer-s-mode.py

script to listen to s-mode commands

- has option to set iid and max group number

```bash
python sniffer-s-mode.py 
```

### programming_mode.py

script to issue set a specific device (via serial_number) in programming mode

```bash
python programming_mode.py 
```

### install_config.py

script to configuring a device, issuing:

- discovery a device with a specific sn
- performing device individualization by setting the:
  - internal address (ia)
  - installation id (iid)
- setting the device in loading state
  - configure Group Object Table
  - configure parameters
- retrieving the finger print

```bash
python install_config.py -h
```

```bash
python install_config.py -sn 000003 -ia 1 -file LSAB_config.json
```

#### The configuration file

The configuration file is a json formatted file.
config data:

- installation id: key = "iid"
- individual address: key = "ia"
- group object table: Key = "groupobject"
- parameter (table): Key = "memparameter"
- recipient table: Key = "recipient" (not yet used)
- publisher table: Key = "publisher" (not yet used)
- access token table: Key = "auth" (not yet used)
- parameter (table): Key = "memparameter"

example config data for ia and idd
```bash
{
  "ia": 7,
  "iid": 5,
....
}
```

The content of the tables are the items in an array.
The items have the json keys (e.g. "id" instead of 0)
The application (in python) converts the json data in to data with integer keys and then convert the contents to cbor.

##### Group object table

The group object table contains the array of json objects for an Group Object Table entry.

- id (0): identifier in the group object table
- href (11) : the href of the point api url
- ga (7): the array of group addresses
- cflags (8) : the communication flags (as strings)
  the cflags array will be converted into the bit flags.

```bash
{
....
"groupobject" : [ 
    { "id": 1, "href": "p/push", "ga" :[1], "cflag" : ["w"] },
    { "id": 1, "href": "p/push", "ga" :[1], "cflag" : ["r"] }] 
....
}
```

##### Publisher table

The group object table contains the array of json objects for an Publisher entry.
note that this table contains the info of the sending side.
Note that the ia (and path) needs to be defined or the url.
if ia is defined and path is not there, the path will have the default value ".knx".

- id (0): identifier in the group object table
- ia (12) : internal address
- ga (7): the array of group addresses

```bash
{
....
"publisher" : [ 
      {
         "id": "1",
         "ia": 5,
         "ga":[2305, 2401],
         "path": ".knx",
     },
     {
         "id": "2",
         "url": "coap://<IP multicast, unicast address or fqdn>/<path>",
         "ga": [2305, 2306, 2307, 2308]
      }] 
....
}
```

##### Recipient table

The group object table contains the array of json objects for an Publisher entry.
note that this table contains the info of the receiving side.
Note that the ia (and path) needs to be defined or the url.
if ia is defined and path is not there, the path will have the default value ".knx".

```bash
....
{
"recipient" : [ 
    {
        "id": "1", ia": 5, "ga":[2305, 2401], "path": ".knx",
    },
    {
        "id": "2","url": "coap://<IP multicast, unicast address or fqdn>/<path>", 
        "ga": [2305, 2306, 2307, 2308]
      }] 
....
}
```

##### Access token table

The access token table contains the array of json objects for an auth/at entry.

- id (0): identifier of the entry
- profile (38): oscore (2) 
- scope (9) : either list of integers for group scope or list of access (if) scopes
- the oscore information is in 2 layers: cnf & osc as json objects
- cnf(8):osc(4):id(0) : the oscore identifier
- cnf(8):osc(4):ms(2) : the master secret (32 bytes)
- cnf(8):osc(4):contextId(6) : the OSCORE context id

```bash
{
....
"auth" : [ 
  {
     "id": "id1", 
     "aud": "xx", 
     "profile": 2, 
     "scope": [ 1, 2 , 3 ], 
     "cnf": {"osc" : { "id": "osc_1",  "ms" : "ms_1" }}
  },
  {
      "id": "id2", 
      "aud": "yyy", 
      "profile": 2,
      "scope": [ 4], 
      "cnf": {"osc" : { "id": "osc_2", "ms" : "ms_2" }}
  },
  {
      "id": "id3", 
      "aud": "yyy", 
      "profile": 2,
      "scope": [ "if.sec" ], 
      "cnf": {"osc" : { "id": "osc_3", "ms" : "ms_2" }}
  }
  ] 
....
}
```

##### Parameters

The parameters can be set on /p.

```bash
{
....
 "memparameter": [{
            "href": "/p/P-1/R-1",
            "value": "true"
        }, {
            "href": "/p/P-2/R-2",
            "value": "false"
        }, {
            "href": "/p/MD-2/M-1/MI-1/P-1/R-1",
            "value": "17"
        }, {
            "href": "/p/MD-2/M-1/MI-1/P-2/R-2",
            "value": "1"
        }, {
            "href": "/p/MD-2/M-2/MI-1/P-1/R-1",
            "value": "17"
        }, {
            "href": "/p/MD-2/M-2/MI-1/P-1/R-4",
            "value": "17"
        }, {
            "href": "/p/MD-2/M-2/MI-1/P-1/R-3",
            "value": "13.333"
        }
 ]
....
}
```

### Python versions

Please ensure that the version of Python you have installed matches the
architecture for which the project is built - if you are building using the
amd64 architecture you must install the 64-bit version of Python, and make sure
that it is available within your path. You can check your Python version using
`python -VV`

```powershell
> python -VV
Python 3.10.4 (tags/v3.10.4:9d38120, Mar 23 2022, 23:13:41) [MSC v.1929 64 bit (AMD64)]
```

If there is a mismatch, you will receive an error about the DLL not being a valid
Win32 application. The error informs you that there is a _mismatch_, it does not
mandate that you use 32-bit binaries. For instance, an AMD64 DLL can successfully
be used alongside a 64-bit Python interpreter.