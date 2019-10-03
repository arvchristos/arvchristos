---
title: Ascensia ContourUSB Python driver
date: '2019-09-25'
draft: false
description: Python driver implementation for Ascensia ContourUSB glucose meter.
tags:
  - driver
  - open_source
  - python
---
![](/images/uploads/contourusb.jpg)

## Introduction

I have used numerous glucose meters the last 20 years, but only lately I found interest in exporting statistics about my blood glucose levels. Most of the models provide a proprietary exporting tool that is AFAIK only for Windows. However, down to the connection interface level, all those devices use either USB or Serial connection. This fact led to the development of many libraries meant to interface and provide data export functionality for a number of devices, regardless of the underlying operating system. The most famous library of that kind is [glucometerutils](https://github.com/Flameeyes/glucometerutils) by [@Flameeyes](https://github.com/Flameeyes), implemented in Python.

`glucometerutils` already supports multiple manufacturers device. However, when I wanted to export readings from my Ascensia (formerly Bayer) ContourUSB meter I realized that no one had implemented the required module for `glucometerutils`. Having used this library for my Freestyle Libre, I already had my graph scripts ready to get data in this particular format. So I decided to write the driver myself.

## Requirements

The library already provides a common interface for all the meters. Specifically, varying by device, the supported functionality is outlined by the following commands:

```
* info - get info about device (e.g., software version, serial number)
* dump - extract all readings in specified format
* datetime - get or set datetime on meter
* zero - flush meter memory
```

The current implementation of ContourUSB driver only implements info and dump. However the rest of the commands are to be implemented in the future.

## ContourUSB protocol

Implementing a device driver from the ground up requires knowledge of the underlying communication protocol and this knowledge is _almost_ never open and accessible. Every device has its own protocol commands and conventions, making it difficult to create a universal supporting software, hence developers end up sniffing communication data while using the proprietary software provided by the manufacturer and reverse engineering the command set. In fact, @Flameeyes has created a [separate repository](https://protocols.glucometers.tech) where he tracks protocol details about all devices he, or other contributors, reverse engineered for `glucometerutils` driver implementations.

Fortunately, for Ascensia meters, Bayer decided that the possibilities that will arise by opening protocol details are far more than the commercial problems for the company. Protocol details are accessible for everyone at [Ascensia developer website](http://protocols.ascensia.com/Programming-Guide.aspx), so we will not spend any time describing the protocol used.

## Implementation
ContourUSB is recognized as a simple `hidraw` device and the pseudo-file `/dev/hidraw*` is used for read/write of data.Communication between host and glucose meter is based on frames of standard format. Those frames are byte strings and we use regular expressions to extract needed fields.

### `info`
ContourUSB provides device information via specific frames called `Header records` in standardized format. Among others, details include:

* Serial number
* Software version
* Measurement unit used
* Date and Time of meter
* Total records stored in meter memory
* Blood glucose ranges set by manufacturer/user
* Meter language

[This code segment](https://github.com/Flameeyes/glucometerutils/blob/d258a6813aa26b94b160374823f5498370e3358d/glucometerutils/support/contourusb.py#L194) stores Header record data for use in the info command.

### `dump`
ContourUSB exports all stored reading records in the so called `Download mode`. During this mode, readings are encapsuled in frames that include a checksum for validation checks, the reading value, its timestamp and any supplementary info such as labels about the reading. My implementation was based on [this](https://bitbucket.org/iko/glucodump/src/default/) repository that gets the meter to download mode and then reads each frame following while checking their checksums for validation. Each frame is parsed using the corresponding regular expression object and then provides (or better yields) data to the higher level functions of the driver for standard driver functionality. 
For more info consult the [corresponding code segment](https://github.com/Flameeyes/glucometerutils/blob/d258a6813aa26b94b160374823f5498370e3358d/glucometerutils/support/contourusb.py#L311).

## Conclusion
The driver implementation is included in the following commit:

* [Add driver implementation for Ascensia ContourUSB.](https://github.com/Flameeyes/glucometerutils/commit/48e89e53d9983312e36ae6c353da9b94fa46b590)

that was merged in the master branch of `glucometerutils`.

## Future work
Implementation of remote code functionality, provided by the protocol documentation, such as datetime set and memory flush is pending.

## Acknowledgements
The following people contributed valuable information for this project:
* Anders Hammarquist for [glucodump](https://bitbucket.org/iko/glucodump/src/default/)
* Alexander Schrijver for the driver outline and communication functions included in his previous try for the same device.
