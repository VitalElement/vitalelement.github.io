---
layout: docs
title: Syslog
next_section: usage-rules
permalink: /docs/api/syslog/
header_path: os/include/syslog/bt_printk.h
source_path: os/src/syslog/bt_printk.c
---

The syslog allows a accurately time-stamp diagnostic messages to be log to the kernel system log.
Usually this causes the message to be placed in the syslog buffer and written to the boot-logger.

However its also possible to redirect the the syslog buffer to the filesystem or any device
supporting charachter streams.

<div class="note info">
  <h5>Notes</h5>
  <p>
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
      <td><p><code><a href="{{ site.url }}/docs/api/syslog/bt_kprint/">BT_kPrint()</a></code></p></td>
      <td><p>
		Adds "printf" style message to the syslog.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
