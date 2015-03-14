---
layout: docs
title: Semaphores & Mutex's
next_section: usage-rules
permalink: /docs/api/semaphore/
header_path: os/include/process/bt_mutex.h
source_path: os/src/process/bt_mutex.c
---

Provides synchronisation objects between threads.
Later this API will allow named objects on the file-system, and for objects to be passed
between processes.

# Mutex API

The following table lists all functions related to the Mutex API.

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
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_createmutex">BT_CreateMutex()</a></code></p></td>
      <td><p>
		Creates a mutex, and returns a handle to the mutex object.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_pendmutex/">BT_PendMutex()</a></code></p></td>
      <td><p>
		Causes the current thread to sleep until the specified mutex is released / signalled.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_releasemutex/">BT_ReleaseMutex()</a></code></p></td>
      <td><p>
		Releases (signals) the specified mutex.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_pendmutexrecursive/">BT_PendMutexRecursive()</a></code></p></td>
      <td><p>
		Causes the current thread to sleep until the specified mutex is released. Does not block if current thread owns the mutex.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_releasemutexrecursive/">BT_ReleaseMutexRecursive()</a></code></p></td>
      <td><p>
		Releases a recursive mutex.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Mutex Kernel Mode API

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
      <td><p><code><a href="{{ site.url }}/api/semaphore/bt_releasemutexfromisr/">BT_ReleaseMutexFromISR()</a></code></p></td>
      <td><p>
		Releases a Mutex from an ISR context.
      </p></td>
    </tr>

  </tbody>
</table>
</div>


# Semaphore API

Currently the semaphore API has not been exposed.

# Kernel-space / Driver API

# Design Overview
These APIs are simply wrappers to the underlying tasking kernel used, usually FreeRTOS.
However direct implementations may be provided when using the BtKernel when available.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
