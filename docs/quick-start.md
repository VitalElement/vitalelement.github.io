---
layout: docs
title: Quick-Start
next_section:
permalink: /docs/quick-start/
---

This guide will attempt to provide a guide to getting bitthunder building on your development system.
The guide is based around the RaspberryPi, but should be very similar for all other supported platforms.

# Cloning BitThunder

You can clone the latest sources from:
{% highlight bash %}
git clone https://github.com/jameswalmsley/bitthunder.git
# Or using SSH (if your a github member).
git clone git@github.com:jameswalmsley/bitthunder.git
{% endhighlight %}

The public master branch aims to stay relatively stable, so you should always be able to build from it.

# Requirements

## DBUILD
BitThunder includes its own make based build system. Its only real dependency is python. There must be a python
interpreter in the path. Version 2.7 is known to work.

DBUILD is responsible for managing dependencies effectively. Its called DBUILD because its like dark-matter, very mysterious!

## Kconfig-frontends
BitThunder uses the Kconfig system taken from the Linux kernel. Kconfig is simply brilliant, so we borrowed it.
Thanks kernel.org!

Build as follows:

{% highlight bash %}
git clone https://github.com/jameswalmsley/kconfig-frontends.git
# Or using SSH (if your a github member).
git clone git@github.com:jameswalmsley/kconfig-frontends.git
# Note this is a mirror of:
# http://ymorin.is-a-geek.org/projects/kconfig-frontends

cd kconfig-frontends
./bootstrap
./configure
make
sudo make install
{% endhighlight %}

### Debian / Ubuntu Package List
build-essentials
autoconf
libtool
gperf
flex
bison
libncurses-dev

sudo ldconfig

# Building BitThunder

Building BitThunder should now be relatively straight-forward...

{% highlight bash %}
cd bitthunder
make menuconfig
{% endhighlight %}

Now configure your system.
For example when building for the raspberry pi:

	Build System:
    -> Change toolchain-prefix to location of your compiler:
       e.g.
	   		/opt/codesourcery/bin/arm-none-eabi-

    System Architecture:
    -> Select ARM
    -> Select BCM2835 Chip variant

	   Linking:
	   -> Enable RAM
	   -> RAM Start Addess = 0x8000
 	   -> RAM length = 0x01000000
  	   	  # Thats 16Mb, but you could also set it to 128mb.

Exit and save the configuration. Due to a small problem with Kconfig you now have to run
menuconfig once more.

    make menuconfig

Simply exit and save the config file.

To build:

    make

In the case of raspberry pi, this should compile and produce binaries under

    bsp/arm/raspberrypi

    kernel.img  -- A raw binary for loading directly in memory.
	kernel.elf  -- JTAG loadable elf file with full debug info.
	kernel.list -- A disassembly of the kernel.
	kernel.map  -- A map of the kernel.


<div class="note info">
  <h5>The build folder</h5>
  <p>Also note the build folder in the bsp. This is where all the objects, intermediates and dependency files are placed.
This makes it possible to build different BSPs independently without having to clean everything. -- nice!</p>
</div>

Hopefully you'll get a nice flashing LED on the Pi if it works.
