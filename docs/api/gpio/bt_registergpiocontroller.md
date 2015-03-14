---
layout: docs
title: BT_RegisterGpioController()
permalink: /docs/api/gpio/bt_registergpiocontroller/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

<div class="note warning">
  <h5>Kernel Mode API</h5>
  <p>This API is only available in kernel-mode code. It is used to register a GPIO driver implementation.</p>
</div>

Registers a GPIO driver with the GPIO sub-system via a driver generated BT_HANDLE.

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
      <td><p><code>ulBaseGPIO</code></p></td>
      <td><p>
		GPIO base number, from which this GPIO controller will respond to. I.e. for the driver this is GPIO.0.
      </p></td>
    </tr>

	<tr>
      <td><p><code>ulTotalGPIOs</code></p></td>
      <td><p>
		The total number of GPIO lines that this driver instance will manage.
      </p></td>
    </tr>

	<tr>
      <td><p><code>hGPIO</code></p></td>
      <td><p>
		The GPIO driver/controller handle, and generated in the driver's probe function.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Returns

BT_ERR_NONE on success.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

See the driver interface under:

<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_dev_if_gpio.h"><code>os/include/interfaces/bt_dev_if_gpio.h</code></a>
