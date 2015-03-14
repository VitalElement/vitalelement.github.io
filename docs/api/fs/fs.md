---
layout: docs
title: File-system
next_section: usage-rules
permalink: /docs/api/fs/
header_path: os/include/fs/bt_fs.h
source_path: os/src/fs/bt_fs.c
---

# User-space API

The following table lists all functions related to the file-system manager API.

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
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_open/">BT_Open()</a></code></p></td>
      <td><p>
		Opens a handle to an object (file/device/fifo/socket ...) from the Virtual File-system.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_opendir/">BT_OpenDir()</a></code></p></td>
      <td><p>
		Opens a BT_HANDLE to a directory like object for traversing.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_getinode/">BT_GetInode()</a></code></p></td>
      <td><p>
		Get a BT_HANDLE for the i-Node associated with the specified path.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Kernel-mode API

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
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_registerfilesystem/">BT_RegisterFilesystem()</a></code></p></td>
      <td><p>
		Registers a file-system with the file-system manager.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_mount/">BT_Mount()</a></code></p></td>
      <td><p>
		Attempts to mount a file-system on the specified block-device. (Usually a Volume Handle).
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview

The filesystem is designed to provide a simple abstraction across all filesystems. Usually this means
a block based filesystem like FAT (FullFAT) or EXT, but can also be for pseudo-filesystems like the device
manager's devfs implementation.


# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

See the driver interface under:

<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_fs.h"><code>os/include/interfaces/bt_if_fs.h</code></a>
<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_file.h"><code>os/include/interfaces/bt_if_file.h</code></a>
<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_dir.h"><code>os/include/interfaces/bt_if_dir.h</code></a>
