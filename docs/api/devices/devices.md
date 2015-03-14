---
layout: docs
title: Device Manager
next_section: usage-rules
permalink: /docs/api/devices/
header_path: os/include/devman/bt_devman.h
source_path: os/src/devman/bt_devman.c
---


# User-space API

The following table lists all functions related to the device manager API.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>API</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/devices/bt_deviceopen/">BT_DeviceOpen()</a></code></p></td>
      <td><p>
		Opens a device based on its device name. This is equivalent to opening devices with BT_Open() using
		a /dev/{name} path.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview

The bitthunder device manager makes extensive use of the linker to create tables of devices and their associated
drivers. This allows drivers to be removed by simply not compiling and linking the relevant driver into the kernel.

This separation between device and driver encourages drivers to be written in a portable style,
where no assumptions are made about register address or other resources.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

See the driver interface under:

<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_device.h"><code>os/include/interfaces/bt_if_device.h</code></a>
