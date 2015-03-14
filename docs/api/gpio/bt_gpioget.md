---
layout: docs
title: BT_GpioGet()
next_section: api/gpio/bt_gpioset
permalink: /docs/api/gpio/bt_gpioget/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

Gets the current state of the specified GPIO.

<div class="note info">
  <h5>Notes</h5>
  <p>
	This function will always succeed when given a valid GPIO number.
	The provided pError value can be optionally provided and checked.
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
		GPIO number of the GPIO line to be tested.
      </p></td>
    </tr>

	<tr>
      <td><p><code>pError</code></p></td>
      <td><p>
		Pointer to a BT_ERROR variable. Can be NULL.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Returns

BT_TRUE or BT_FALSE.
On error, BT_FALSE will be returned, and the BT_ERROR code can be tested from the optionally provided
pError variable.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:
{% include api/source-path.md %}
