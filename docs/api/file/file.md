---
layout: docs
title: File I/O
next_section: usage-rules
permalink: /docs/api/fs/file/
header_path: os/include/fs/bt_file.h
source_path: os/src/fs/bt_file.c
---

# User-space API

The following table lists all functions related to using open File HANDLE's.

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
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_read/">BT_Read()</a></code></p></td>
      <td><p>
		Reads data from the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_write/">BT_Write()</a></code></p></td>
      <td><p>
		Writes data to the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_getc/">BT_GetC()</a></code></p></td>
      <td><p>
		Get a character from the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_putc/">BT_PutC()</a></code></p></td>
      <td><p>
		Write a character to the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_seek/">BT_Seek()</a></code></p></td>
      <td><p>
		Seeks the file offset pointer of the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_tell/">BT_Tell()</a></code></p></td>
      <td><p>
		Gets the current position of the file offset pointer of the specified file handle.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/docs/api/fs/bt_gets/">BT_GetS()</a></code></p></td>
      <td><p>
		Gets a string (a line) from the specified file handle.
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

See the driver interface under:

<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_fs.h"><code>os/include/interfaces/bt_if_fs.h</code></a>
<a href="{{ site.gh-blob-url }}/os/include/interfaces/bt_if_file.h"><code>os/include/interfaces/bt_if_file.h</code></a>
