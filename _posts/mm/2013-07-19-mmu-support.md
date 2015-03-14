---
layout: posts
category: memory
title: Memory Management and Virtual Memory Support
author: James Walmsley
email: james@fullfat-fs.co.uk
---

Today, BitThunder officially became a "real" operating system.
I now managed to add basic MMU (memory management unit) support. Its not, and never will be
a requirement of course, but for those projects that can support this you'll get a lot!

# Memory Map
During boot, the kernel now sets up a default set of page tables. (Section entries on ARM).
This mirrors the inital executable at address 0xC000_0000 (just like Linux), and then the
boot code carefully jumps to the "next" instruction but in its true address space.

{% highlight c %}
+-------------------------+	0xFFFF_FFFF
|                         | \
|                         | |
|                         | |
| Remapped I/O regions    | |
|                         |  }- High-Memory (Permanent Kernel Region).
| Allocatable Mem Pages   | |
|                         | |
| BT Kernel Text Section  |/
+-------------------------+	0xC000_0000
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
| Unmapped                |
| Process Address Space   |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
|                         |
+-------------------------+	0x0000_0000
{% endhighlight %}

# IO Remapping

Turning on the MMU with an initial mapping on the ARM was trivial. (I'll blog about this later).
The biggest issue now was that the entire kernel was running completely isolated, there
was no-longer any access to hardware. That means none of the drivers could be utilised
to create a kernel tick or print anything to stdout.

To solve this issue I created a bt_ioremap() api function. The function is used just like the ioremap
function in the linux kernel. bt_ioremap() can only create section mappings, (e.g. 1MB regions).
This might be over-simple, but it reduces the page-table walk dramatically, something that is important
when using hardware in a real-time system.

After all a real-time process in BitThunder may use any driver in the system, and those drivers
must not alter the real-time characteristics of the calling process.

# Page Allocation

Currently I have not had time to implement page allocation, but this is coming very soon!
I am currently planning to have a distinction between hard real-time and soft real-time processes,
of which both will come in 2 flavours.

## Hard Real-time

All processes that are hard-realtime based will only be able to map section sized (top-level page entries)
into their respective memory spaces. This is to prevent table walking, and reduce TLB misses.

### Hard Kernel Bound Processes

This variation uses kernel address space, these processes will have full system access, and a bug in these
will cause the entire system to kernel panic. The advantage is that this process address space is permanently
mapped. TLB misses are therefore less likely, especially if the process is regularly active.

These processes can call the Kernel level API's directly, and reduce the overhead of system calls.
Of course system calls will also work in this mode.

### Hard Isolated processes

This variation creates a full process address space, and completely isolates the process from 
other processes and the kernel's internal data. These processes can only use devices or OS services
through a system call mechanism.

## Soft Real-time

These processes are very much like those on a standard linux system. The scheduler is still real-time
but here we have a full page table, therefore increased page walking and TLB misses will occur.

### Soft Kernel Bound

The same as hard kernel bound processes, except a normal page table is used allowing PAGE_SIZE memory
allocation granularity.

### Soft Isolated processes

These are the same as the hard isolated processes, but with a full page table for fine-grained memory
control. These are just like Linux processes but on a real-time scheduler.
Again they must use system calls to utilise OS services etc.

Most processes should be soft isolated process variants.


