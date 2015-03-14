---
layout: docs
title: Time & Timers
next_section: usage-rules
permalink: /docs/api/timers/
header_path: os/include/timers/bt_timers.h
source_path: os/src/timers/bt_timers.c
---

The timer, system-timer and time sub-system provides APIs for managing hardware & software timers,
as well allowing the user to query the system-clock or high-resolution timer.

The API also provides access to real-time (as in the current time) using RTC sources, as well syncing
the subsystem regularly with an RTC.

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
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_getkerneltime/">BT_GetKernelTime()</a></code></p></td>
      <td><p>
		Get's the current kernel time in us.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/gpio/bt_getkerneltick/">BT_GetKernelTick()</a></code></p></td>
      <td><p>
		Get's the current kernel tick, usually ms units but depends on scheduler periodicity.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Hardware Timer API.

# Software Timer API.

# Time API.

# Design Overview

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
