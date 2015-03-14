---
layout: docs
title: Watchdog
next_section: usage-rules
permalink: /docs/api/watchdog/
---

The BitThunder watchdog service will allow processes to be created with watchdog monitoring enabled.
In the case they stop responding, e.g. a dead-lock, infinite loop, or some other serious condition like
a segmentation fault, then BitThunder can automatically cleanup all associated resources and restart the
offending process.

Obviously this feature depends on certain hardware capabilities like MMU etc.

On MMU less systems, the watchdog can cause a reset of the entire device if desired.
