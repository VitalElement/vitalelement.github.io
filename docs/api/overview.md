---
layout: docs
title: Overview
next_section: usage-rules
permalink: /docs/api/overview/
---

Most of the API documented here is the native BitThunder API. This is the best API to use
for small and memory-constrained devices. (Bare-metal).

BitThunder is designed to scale and adapt to different systems, and the native BitThunder API is
always available, even in the high-end configurations. It is guaranteed that all software using the native
API will work across all devices that can support the used features.

The API is available through direct linking, when the application and the kernel are combined together,
and also through a system-call mechanism.

When linking applications through the system-call interface, it becomes possible to upgrade embedded applications
separately from the kernel, and vice-versa.

On more powerful platforms, BitThunder can also expose other personalities via the system-call mechanism.
E.g. we aim to have a fully featured POSIX "personality" available. Some features like networking,
expose directly a native POSIX compliant API.
