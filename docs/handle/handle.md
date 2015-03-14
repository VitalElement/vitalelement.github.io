---
layout: docs
title: Handle Manager
next_section: usage-rules
permalink: /docs/api/handle/
header_path: lib/include/handles/bt_handle.h
source_path: lib/src/handles/bt_handles.c
---

The handle manager, in co-operation with the process manager, is responsible for managing BT_HANDLE objects and
their associated handles.

# Handle Manager API.

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
      <td><p><code><a href="{{ site.url }}/api/handle/bt_closehandle/">BT_CloseHandle()</a></code></p></td>
      <td><p>
		Causes a HANDLE to be correctly closed, and free'd up.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Kernel-mode API.

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
      <td><p><code><a href="{{ site.url }}/api/bt_createhandle/">BT_CreateHandle()</a></code></p></td>
      <td><p>
		Allocates handle memory and associates a handle with the relevant process.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview
The handle manager forms lists of all handles associated with each process.
All handles contain a BT_HANDLE_HEADER structure, which contains pointers to the relevant interface implementations,
e.g. function pointers for writing data to the handle etc.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}
