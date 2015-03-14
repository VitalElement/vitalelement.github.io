---
layout: docs
title: Processes and Threads
next_section: usage-rules
permalink: /docs/api/process/
header_path: os/include/gpio/bt_gpio.h
source_path: os/src/gpio/bt_gpio.c
---

The process manager is responsible for keeping track of all processes in the system, and
all their associated threads, memory and other resources.

# Process API

The following table lists all functions related to the process manager API.

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
      <td><p><code><a href="{{ site.url }}/api/process/bt_createprocess/">BT_CreateProcess()</a></code></p></td>
      <td><p>
		Creates a BitThunder process.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_destroyprocess/">BT_DestroyProcess()</a></code></p></td>
      <td><p>
		Destroys a BitThunder process.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_getprocesshandle/">BT_GetProcessHandle()</a></code></p></td>
      <td><p>
		Gets the handle of the current process.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Thread API

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
      <td><p><code><a href="{{ site.url }}/api/process/bt_createthread/">BT_CreateThread()</a></code></p></td>
      <td><p>
		Creates a new thread.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_getthreadhandle/">BT_GetThreadHandle()</a></code></p></td>
      <td><p>
		Get the handle of the currently executing thread.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_threadsleep/">BT_ThreadSleep()</a></code></p></td>
      <td><p>
		Causes the current thread to sleep for the specified time..
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_threadsleepuntil/">BT_ThreadSleepUntil()</a></code></p></td>
      <td><p>
		Causes the current thread to sleep until a specified time in the future.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/process/bt_threadyield/">BT_ThreadYield()</a></code></p></td>
      <td><p>
		Yields the processor to allow execution of another thread or process.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Kernel-space / Driver API

# Design Overview
The primary object of execution in BitThunder is a thread. A process is simply an abstraction that allows the grouping
of 1 or more threads together into a system (or application).

A process usually takes responsibility for a major task in a BitThunder system, and should require little or no
communication with other processes. Although there are some IPC constructs available.

Processes always contain at least 1 thread,

On full-featured platforms (like Xilinx Zynq) this abstraction can be optionally enforced by enabling MMU and virtual memory
support. In such cases, attempts to access pointers in memory not allocated to that process will result in a seg-mentation fault
and the process will be closed and all resources free'd and cleaned.

If configured, a BitThunder process can be restarted automatically by the BitThunder watchdog system.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
