---
layout: docs
title: I2C Subsystem
next_section: usage-rules
permalink: /docs/api/i2c/
header_path: os/include/interfaces/bt_dev_if_i2c.h
source_path: os/src/interfaces/bt_dev_if_i2c.c
---

The I2C sub-system mirrors closely the linux api.

# User-space API

The following table lists all functions related to the I2C subsystem API.

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
      <td><p><code><a href="{{ site.url }}/docs/api/i2c/bt_i2c_transfer/">BT_I2C_Transfer()</a></code></p></td>
      <td><p>
		Sends I2C "messages" on the specified I2C bus.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/i2c/bt_i2c_mastersend/">BT_I2C_MasterSend()</a></code></p></td>
      <td><p>
		Sends data to an I2C_CLIENT.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/i2c/bt_i2c_masterreceive/">BT_I2C_MasterReceive()</a></code></p></td>
      <td><p>
		Receives data from an I2C_CLIENT.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Kernel-space / Driver API

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
      <td><p><code><a href="{{ site.url }}/docs/api/i2c/bt_i2c_registerbuswithid/">BT_I2C_RegisterBusWithID()</a></code></p></td>
      <td><p>
		Registers an I2C bus controller using the specified bus id.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview



## I2C Bus device descriptors


# Interrupts

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

<a href="{{ site.gh-blob-url }}/os/include/devman/bt_i2c.h"><code>os/include/devman/bt_i2c.h</code></a>
