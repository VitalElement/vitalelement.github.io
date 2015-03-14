---
layout: docs
title: GPIO Subsystem
next_section: usage-rules
permalink: /docs/api/gpio/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

The GPIO sub-system in BitThunder is very straight-forward and simple to use.
Throughout the entire system GPIOs are addressed using a GPIO number/flag space.

Depending on your system/application GPIO flags can be mapped and aliased within this
address space. Usually primary GPIOs start at 0, but thats just a convention.

GPIO are accesible to all, and no BT_HANDLE is associated or exported to user-space.
Therefore its possible to have multiple processes conflicting, and controlling the same
GPIO by mistake.

<div class="note info">
  <h5>GPIO Anarchy</h5>
  <p>
	Having the GPIO API in this way makes its usage very simple, and most BitThunder systems are currently
	closed embedded systems. However we intend to extend the API later to allow a process to LOCK a GPIO
	to itself, and only make use of the GPIO pin using a special HANDLE based API.
  </p>
</div>

# User-space API

The following table lists all functions related to the GPIO subsystem API.

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
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_gpioget/">BT_GpioGet()</a></code></p></td>
      <td><p>
		Gets the current state of a GPIO line.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_gpioset/">BT_GpioSet()</a></code></p></td>
      <td><p>
		Sets a GPIO line to the desired state.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_gpiogetdirection/">BT_GpioGetDirection()</a></code></p></td>
      <td><p>
		Gets the direction / mode of a GPIO line.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_gpiosetdirection/">BT_GpioSetDirection()</a></code></p></td>
      <td><p>
		Sets the direction / mode of a GPIO line.
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
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_registergpiocontroller/">BT_RegisterGpioController()</a></code></p></td>
      <td><p>
		Registers a GPIO controller driver with the GPIO sub-system.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview

The BitThunder GPIO subsystem is simple, and all operations on a standard system are relatively cheap. There is
an O(n) cost, where n = number of registered GPIO controllers, to resolve GPIO numbers to the correct driver
implementation.

The GPIO api is not meant to be a high-performance API for doing bit-banging, or accurately timed PWM signals,
bit mostly for setting board MUXs, or LEDs, or chip-selects.

Those wanting to do high-performance GPIO access should write a driver that utilises the GPIO registers
directly in kernel-mode. E.g. a bit-banged I2C bus driver should be implemented directly.

# Interrupts

The driver interface implements interrupt hooking, and this will be later exposed to user-space and other kernel-mode
drivers.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

See the driver interface under:

<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_dev_if_gpio.h"><code>os/include/interfaces/bt_dev_if_gpio.h</code></a>
