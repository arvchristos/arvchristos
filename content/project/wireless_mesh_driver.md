---
title: Wireless mesh sensor network driver
date: '2018-02-15'
draft: false
description: Project in the context of NTUA Operating Systems Laboratory course.
tags:
  - c
  - driver
  - device
  - university

---

*Wirlesh mesh sensor character device driver for Operating Systems Laboratory course of Electrical and Computer Engineering School of NTUA Athens.*
*You can find the project code on [GitHub](https://github.com/arvchristos/oslab-ntua/tree/master/mesh_driver)*

This exercise contains the implementation of a character device driver for a wireless network of sensors. Those sensors are connected in a mesh network and provide data to e central collecting station. Each of those sensors collects brightness, temperature as well as sensor battery voltage levels. The sensors are collecting data and send it to the central station through a serial over USB connection. During the development process, the school didn't provide every team the set of sensors required. However, the mesh system was built inside the lab and we were provided a QEMU virtualmachine that exported a socket connection to the central device to the virtual local serial device `/dev/ttyS0`.  