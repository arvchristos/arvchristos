---
title: Matching /dev/hidraw* devices with physical devices
date: '2019-10-04T00:07:30+03:00'
draft: true
---
> During development of ContourUSB device driver (I' ve dedicated [a post](/project/contourusb/) for this one) I had a hard time detecting the hidraw device created for the meter. I' ve been suggested to just print all available hidraw devices (pseudo files), then plug the meter and re-print hidraw devices to detect which one was just created. While this worked I wasn't really thrilled with the approach. So I created this simple following script.

This is a short tutorial about how to match `/dev/hidraw*` devices to physical ones. For this purpose, we are going to use sysfs (or anything else I could put here). Specifically, the following is a simple bash script that prints the hidraw device entries with their related device:

```bash
code here
```

Example output:

```bash
output here
```
