---
layout: docs
title: BT_kPrint()
permalink: /docs/api/syslog/bt_kprint/
header_path: os/include/syslog/bt_printk.h
source_path: os/src/syslog/bt_printk.c
---

Pushes a "printf" style message onto the system-log.

<div class="note info">
  <h5>Notes</h5>
  <p>
	This function affects the syslog state, and output depends on the syslog driver used.
	On systems with a file-system this may simply push a message to a file buffer.
	During early-boot, syslog messages are written directly to the BootLogger device.
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
      <td><p><code>format</code></p></td>
      <td><p>
		printf style format string.
      </p></td>
    </tr>

	<tr>
      <td><p><code>...</code></p></td>
      <td><p>
		Variables required to create the format string.
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
