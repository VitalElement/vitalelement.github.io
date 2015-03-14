---
layout: docs
title: BT_CreateProcess()
permalink: /docs/api/process/bt_createprocess/
header_path: os/include/process/bt_process.h
source_path: os/src/process/bt_process.h
---

Creates a new process.

<div class="note info">
  <h5>Notes</h5>
  <p>Depending on the platform and its supported features, e.g. MMU availabilty a process will have different levels of security.
  Processes should always be programmed with the assumption that they are completely isolated from all other processes.
  To create a non-isolated thread, use the BT_CreateThread() api.
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
