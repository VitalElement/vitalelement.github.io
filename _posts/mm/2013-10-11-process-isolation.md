---
layout: posts
category: memory
title: New release and Full process Isolation
author: James Walmsley
email: james@fullfat-fs.co.uk
---

So its a little while since I last blogged about bitthunder, and there's been a lot of huge changes and improvements.
Most importantly, v0.8.0 (2-acetoxybezoic acid) [for the non-chemists thats Aspirin] has been released, bringing full 
process isolation and a proper virtual memory manager. The release also replaces the original page allocator with a
much faster and more simple implementation.

# Whats new in 0.8.0

  * VM Manager allowing full isolation of process memory contexts.
  * Improved page allocator.

# VM Manager sub-system.

