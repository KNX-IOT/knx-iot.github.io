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

The python scripts are a set of applications that can perform tasks to interact with an KNX IoT Point API Device.
Typical interactions are:

- [Searching for a device or multiple devices](#list_devices.py).
- [Configuring a device](#list_devicespy)
- [Issuing s-mode messages](#s-modepy)
- [Listening to s-mode messages](#sniffer-s-modepy)
- [Resetting a device](#reset_devicepy)

Each python script has the -h option to show the command line parameters.

Typical all scripts require to indicate to which device the command is issued. e.g. use the option -sn the serial number of the device.

### Downloading the python scripts

The python scripts can be downloaded from the [release page of the KNX IoT Stack](https://github.com/KNX-IOT/KNX-IOT-STACK/releases)

The files to download and unzip are:

- python_release_no_security.zip
  (scripts with security disabled)
- python_release_security.zip
  (scripts with security enabled)

The scripts should be run from the folder `<install folder>\python_apps`.

### list_devices.py

Python script to list the device, issuing:

- Discovery of device with internal address using query : if=urn:knx:ia.[ia]
- Discovery of device in programming mode using query : if=urn:knx:if.pm
- Discovery of device with a serial_number using query : ep=urn:knx:sn.[serial_number]
- Discovery of device using a group_address using query : d=urn:knx:g.s.[group_address]
- Discovery with query : rt=urn:knx:dpa.*

To show all options:
```bash
python list_devices.py -h
```

### programming_mode.py

Python script to issue set a specific device (via serial_number) in programming mode.

To show all options:

```bash
python programming_mode.py -h
```

Note: to discover a device in programming mode, use [list_devices.py](#list_devicespy)

### install_config.py

Python script to configuring a device.

The script will issue the following commands:

- Discovery a device with a specific sn
- Performing device individualization by setting the:
  - internal address (ia)
  - installation id (iid)
- Setting the device in `loading` state
  - configure Group Object Table
  - configure the Publisher Table
  - configure the Recipient Table
  - configure parameters
  - Set the device in `loaded` state
- Retrieve the finger print

The flow is depicted in the following diagram:
![configuration steps](https://raw.githubusercontent.com/KNX-IOT/KNX-IOT-STACK/master/images/ets_sequence_setup.png)

To show all options:

```bash
python install_config.py -h
```

Example to configure:

- Device with serial number 000003
- Setting the internal adress on 1
- Using the LSAB_config.json input file for all other configurations
  
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
- recipient table: Key = "recipient"
- publisher table: Key = "publisher"
- access token table: Key = "auth"
- parameter (table): Key = "memparameter"

Example config data for ia and idd:

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

The group object table contains the following json tags.

- "id" : identifier in the group object table
- "href" : the href of the point api url
- "ga": the array of group addresses
- "cflags" : the communication flags (as strings),
  the cflags array will be converted into the bit flags.

| JSON Tag | CBOR tag |
|----------| ------------|
| "id"     | 0 |
| "href"   | 11 |
| "ga"   | 7 |
| "cflags"   | 8 |

Example :

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

The Publisher table contains the array of json objects for an Publisher entry.
Note that the ia (and path) needs to be defined or the url.
if ia is defined and path is not there, the path will have the default value ".knx".

- "id" : identifier in the group object table
- "ia" : internal address of the target device
- "ga" : the array of group addresses
- "path" : the optional path to send the commands too.
- "url" : the unicat url to send the command too

| JSON Tag | CBOR tag |
|----------| ------------|
| "id"     | 0 |
| "ia"   | 12 |
| "iid"      | 26            |
| "fid"      | 25            |
| "grpid"    | 13            |
| "path"     | 112           |
| "url"      | 10            |
| "ga"       | 7             |
| "con"      | -             |

Example:

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

The Recipient table contains the array of json objects for an Recipeint entry.
Note that the ia (and path) needs to be defined or the url.
If ia is defined and path is not there, the path will have the default value ".knx".

- "id" : identifier in the group object table
- "ia" : internal address of the target device
- "ga" : the array of group addresses
- "path" : the optional path to send the commands too.
- "url" : the unicat url to send the command too

| JSON Tag | CBOR tag |
|----------| ------------|
| "id"     | 0 |
| "ia"   | 12 |
| "iid"      | 26            |
| "fid"      | 25            |
| "grpid"    | 13            |
| "path"     | 112           |
| "url"      | 10            |
| "ga"       | 7             |
| "con"      | -             |

Example:

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

- "id" : identifier of the entry
- "profile" : oscore (2)
- "scope"  : either list of integers for group scope or list of access (if) scopes

The oscore information is layered: cnf & osc as json objects:

- "cnf":"osc":"id": the oscore identifier
- "cnf":"osc":"ms" : the master secret (32 bytes)
- "cnf":"osc":"contextId" : the OSCORE context id

| JSON Tag  | CBOR tag |
|-----------| ---------|
| "id"      | 0        |
| "profile" | 28       |
| "scope"   | 26       |
| "cnf"     | 8        |
| "osc"     | 4        |
| "ms"      | 2        |
| "contextId"  | 6     |

Example

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

The parameter information:

- "value": The value of the data (e.g. will be translated to CBOR)
- "href": The href of the endpoint for the parameter

| JSON Tag  | CBOR tag |
|-----------| ---------|
| "value"   | 1        |
| "href"    | 11       |

Example:

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

### s-mode.py

Python script to issue an s-mode command.

- has option to set the various values in the command.

To show all options:

```bash
python s-mode.py 
```

### sniffer-s-mode.py

Python script to listen to s-mode commands.

- has option to set iid and max group number

To show all options:

```bash
python sniffer-s-mode.py -h
```

### reset_device.py

Python script to reset the device.
The script will issue the following commands:

- Discovery with a specific serial number
- POST to /a/sen with the reset command

To show all options:

```bash
python reset_device.py -h
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