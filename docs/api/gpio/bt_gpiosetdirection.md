---
layout: docs
title: BT_GpioSetDirection()
next_section: api/gpio/bt_registergpiocontroller
permalink: /docs/api/gpio/bt_gpiosetdirection/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

Sets the mode / direction of the specified GPIO.

<div class="note info">
  <h5>Notes</h5>
  <p>
	Depending on the actual physical hardware, and the GPIO driver implementation for your platform,
	some modes may not be possible / available.
  </p>
</div>

# Parameters

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>

	<tr>
      <td><p><code>ulGPIO</code></p></td>
      <td><p>
		GPIO number of the GPIO line to be configured.
      </p></td>
    </tr>

	<tr>
      <td><p><code>eDirection</code></p></td>
      <td><p>
		ENUM: specifying the direction/mode to configure.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Returns

BT_ERR_NONE on success.

# Valid Directions
{% include api/gpio/directions.md %}

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
