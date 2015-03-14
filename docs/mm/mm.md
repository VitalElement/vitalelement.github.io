---
layout: docs
title: Memory Manager
next_section: usage-rules
permalink: /docs/api/mm/
header_path: os/include/syslog/bt_printk.h
source_path: os/src/syslog/bt_printk.c
---

The memory manager is responsible for managing all memory within BitThunder. For systems with MMU's the mm,
is also responsible for managing all virtual memory mappings for each process.

# User-space Memory Allocation API.

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
      <td><p><code><a href="{{ site.url }}/api/mm/malloc/">malloc()</a></code></p></td>
      <td><p>
		POSIX compliant malloc implementation.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/mm/free/">free()</a></code></p></td>
      <td><p>
		POSIX compliant free implementation.
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
      <td><p><code><a href="{{ site.url }}/api/mm/bt_kmalloc/">BT_kMalloc()</a></code></p></td>
      <td><p>
		Allocates arbitrary amounts of memory for use in the kernel, e.g. drivers etc.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/mm/bt_kfree/">BT_kFree()</a></code></p></td>
      <td><p>
		Frees a kernel memory allocation.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/mm/bt_ioremap/">bt_ioremap()</a></code></p></td>
      <td><p>
		Remaps a physical address to a usable virtual address. THIS MUST BE USED EVEN WITH NO MMU.
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Page Allocation

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
      <td><p><code><a href="{{ site.url }}/api/mm/bt_page_alloc/">bt_page_alloc()</a></code></p></td>
      <td><p>
		Allocates page-aligned, page multiples of atleast the requested size.
      </p></td>
    </tr>

	<tr>
      <td><p><code><a href="{{ site.url }}/api/mm/bt_page_free/">bt_page_free()</a></code></p></td>
      <td><p>
		Frees page-aligned memory as requested from bt_page_alloc().
      </p></td>
    </tr>

  </tbody>
</table>
</div>

# Design Overview
The memory manager has a few different implementations which are used depending on the kernel configurations.

## Basic MM
Typical micro-controller applications use a mono-lithic, space-efficient heap.
The heap consists of a free linked list, and the heap structure is stored within the heaps memory
directly. This means its possible for threads/processes to cause heap corruption.

## Powerful MM (Page based and Virtual Memory Management)
In these more powerful systems with MMUs, its possible to configure support for page based memory allocations
and optionally virtual memory if desired.

The page based allocator becomes the lowest-level memory allocator on which the kernel heap, and process heaps
are based.

The kernel heap is really efficient SLAB based algorithm, with all O(1) constant time operations.

# To be implemented:

  * mmap()
  * User-space heaps.

# In progress

  * vmalloc() api - Virtual memory allocation and mappings.

# Further Reading

The full API is defined under:

{% include api/header-path.md %}

See the implementation under:

{% include api/source-path.md %}

<a href="{{ site.gh-blob-url }}/os/src/mm/slab.c"><code>os/src/mm/slab.c</code></a>
<a href="{{ site.gh-blob-url }}/os/src/mm/bt_page.c"><code>os/src/mm/bt_page.c</code></a>
