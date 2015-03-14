---
layout: docs
title: BT_GpioSet()
next_section: api/gpio/bt_gpiogetdirection
permalink: /docs/api/gpio/bt_gpioset/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

Sets the state of the specified GPIO.

<div class="note info">
  <h5>Notes</h5>
  <p>

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
      <td><p><code>bValue</code></p></td>
      <td><p>
		BT_TRUE or BT_FALSE.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Returns

BT_TRUE or BT_FALSE to represent the GPIO's current state.
On error, BT_FALSE is returned, and pError can be tested.


# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:
{% include api/source-path.md %}
