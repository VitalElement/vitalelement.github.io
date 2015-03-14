---
layout: posts
category: networking
title: Network Integration
author: James Walmsley
email: james@fullfat-fs.co.uk
---

We've completed initial work on our full-featured TCP/IP stack integration's, and its the first API level feature
which expresses itself with complete POSIX compliance.

# Simplified Network Interface Model

BitThunder espouses a separation of concerns principle throughout all levels of its design. Its of no surprise
that the network interface model adheres to this principle also. Network Interface drivers must only take care
of sending and receiving buffers of data, and signaling and responding to a small set of "netif" and "mac"
events.

Above the netif drivers sits a network manager, which handles all network buffers and interface initialisation
and configuration.

<div class="note info">
  <h5>Which TCP/IP stack?</h5>
  <p>
	We are using the Lightweight TCP/IP stack, but have designed the integration in such a way that this can easily
	be replaced. In the future we'll add support for uIP also, allowing users to switch between the 2 implementations
	using Kconfig.
  </p>
</div>

Currently the the TX and RX channels are managed together, but we aim to separate these data-paths completely very
soon. This should mean that e.g. data can be received while the TX channel is saturated and vice-versa.

# PHY Configuration Interface
Currently we have not defined the MDIO transport interface, but we shall add a simplified interface similar to the
I2C sub-system that allows PHY drivers to be easily associated with MAC devices.

We shall also attempt to make this interface similar to the Linux API, so that PHY drivers can easily be ported
between the two systems.

# Speed Results

On a Stellaris board we could achieve a TX throughput rate of 1.65 MB/second using the full TCP/IP socket API.
We shall provide UDP bandwidth shortly as this will be higher.

It doesn't sound like much, but this is quite an impressive result for such a low-powered micro-controller,
and we are looking to further optimise the netif driver to improve this further.
