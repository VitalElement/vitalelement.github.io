---
layout: posts
title: Building GCC / GNU Toolchain for Windows
author: James Walmsley
author_email: james@fullfat-fs.co.uk
category: misc
---

I've been trying to sucessfully compile GCC for Windows to allow me to maintain a Windows version of the BTDK
(BitThunder development kit). Well the documentation on the internet describing how to do this is thin and far between.
The good news is that I've finally managed to create one.

# Strategies
Most guides talk about setting up MSYS and MinGW or cygwin or some other native Windows build environment. I explicitly do NOT
recommend this approach. Its extremely slow and tedious, you will simply waste months of your life!

The approach I eventually settled for is to cross-compile for Windows on Linux (Ubuntu 14.10). To do this I use the excellent MXE
cross compile environment.

The build involves the following steps:

1. Clone and build MXE.
2. Configure build environment.
3. Clone and build binutils-gdb
4. Download and build libgmp (4.3.2)
5. Download and build libmpfr (2.4.2)
6. Download and build libmpc (0.8.1)
7. Clone and build gcc (stage 1).
8. Clone and build newlib.
9. Clone build gcc (final stage).

## 1. Get and Install MXE

{% highlight bash %}
git clone git://github.com/mxe/mxe.git
cd mxe
git checkout stable
make
{% endhighlight %}

Now wait for a really long time... You don't actually need the whole environment to be built, but it will come in useful.

## 2. Build Variables & Environment

    PATH   : Path must include the mxe binary path:
{% highlight bash %}
export PATH=/path/to/mxe/usr/bin:$PATH
{% endhighlight %}

    TARGET	    : This is the target type, e.g. arm-unknown-eabi or arm-eabi-bt
	PREFIX      : Where the toolchain will reside on the system. E.g. /opt/btdk
	HOST        : The type of system that will host the compiler (Windows in our case).
	BUILD       : The type of system that is being used to build the toolchain.
	PKGVERSION  : A toolchain package name/version.

	BTDK uses the following defaults:

{% highlight bash %}
export TARGET=arm-unknown-eabi
export PREFIX=/opt/mytoolchain
export HOST=i686-pc-mingw32
export BUILD="$(config.guess)"
export PKGVERSION="mytoolchain v1.0.0"
{% endhighlight %}

## 3. Building Binutils (ld gas nm gdb etc)

{% highlight bash %}
git clone git://sourceware.org/git/binutils-gdb.git
mkdir build-binutils
cd build-binutils
../binutils-gdb/configure --host=${HOST} --build=${BUILD} --target=${TARGET} \
                          --prefix=${PREFIX} --enable-interwork --enable-multilib \
                          --enable-target-optspace --with-float=soft --disable-werror \
                          --with-pkgversion=${PKGVERSION}
make
sudo make install
{% endhighlight %}

### Patch / Fix for Binutils
Currently the build tree contains a fix for compiling for windows, but MXE is good enough not to need it.
If the build complains something like:

{% highlight bash %}
mxe/usr/lib/gcc/i686-pc-mingw32/4.8.1/../../../../i686-pc-mingw32/lib/libncurses.a(lib_tputs.o):lib_tputs.c:(.text+0x780): multiple definition of `tputs'
windows-termcap.o:mytoolchain/binutils-gdb/gdb/windows-termcap.c:62: first defined here
{% endhighlight %}

The simply open the file gdb/windows-termcap.c

Comment out the tputs() function, or apply the following patch:

{% highlight bash %}
diff --git a/gdb/windows-termcap.c b/gdb/windows-termcap.c
index 7c258cf..e7d5fa3 100644
--- a/gdb/windows-termcap.c
+++ b/gdb/windows-termcap.c
@@ -57,14 +57,14 @@ tgetstr (char *name, char **area)
   return NULL;
 }

-int
+/*int
 tputs (char *string, int nlines, int (*outfun) ())
 {
   while (*string)
     outfun (*string++);

   return 0;
-}
+}*/

 char *
 tgoto (const char *cap, int col, int row)
{% endhighlight %}

You can apply it by saving it into a .patch file and ...

{% highlight bash %}
cd ../binutils-gdb
git apply binutils.patch
cd ../build-binutils
make
sudo make install
{% endhighlight %}

There's also a problem with the install target, of binutils it cannot find the ranlib tool for some reason. You can fix this with the following patch:

{% highlight bash %}
# Obviously adjust the path to your actual mxe ranlib binary :D
sed -i 's:i686-pc-mingw32-ranlib:/home/wl/develop/tools/mxe/usr/bin/i686-pc-mingw32-ranlib:g' Makefile sim/Makefile sim/arm/Makefile
sudo make install
{% endhighlight %}

You should now have a full gdb and binutils for windows:

{% highlight bash %}
tree ${PREFIX}/bin/
/opt/mytoolchain/bin/
├── arm-unknown-eabi-addr2line.exe
├── arm-unknown-eabi-ar.exe
├── arm-unknown-eabi-as.exe
├── arm-unknown-eabi-c++filt.exe
├── arm-unknown-eabi-elfedit.exe
├── arm-unknown-eabi-gdb.exe
├── arm-unknown-eabi-gprof.exe
├── arm-unknown-eabi-ld.bfd.exe
├── arm-unknown-eabi-ld.exe
├── arm-unknown-eabi-nm.exe
├── arm-unknown-eabi-objcopy.exe
├── arm-unknown-eabi-objdump.exe
├── arm-unknown-eabi-ranlib.exe
├── arm-unknown-eabi-readelf.exe
├── arm-unknown-eabi-run.exe
├── arm-unknown-eabi-size.exe
├── arm-unknown-eabi-strings.exe
└── arm-unknown-eabi-strip.exe

0 directories, 18 files
{% endhighlight %}

## 4. Build libgmp
Yup building these libraries is boring, but its probably the safest option in the long run
(trust me I wasted hours of my life trying to make this all link with pre-compiled versions in mingw32, mxe is probably better
but lets just use my working method :D )

{% highlight bash %}
wget https://gmplib.org/download/gmp/gmp-4.3.2.tar.bz2
tar xvf gmp-4.3.2.tar.bz2
mkdir build-gmp
cd build-gmp
../gmp-4.3.2/configure --host=${HOST} --build=${BUILD} --prefix=$(pwd)/../libgmp \
                       --disable-shared --enable-static --without-readline --enable-cxx
make
# We install into ../libgmp/ so we don't need sudo.
make install
{% endhighlight %}

## 5. Build libmpfr

{% highlight bash %}
wget https://ftp.gnu.org/gnu/mpfr/mpfr-2.4.2.tar.bz2
tar xvf mpfr-2.4.2.tar.bz2
mkdir build-mpfr
cd build-mpfr
../mpfr-2.4.2/configure --host=${HOST} --build=${BUILD} --prefix=$(pwd)/../libmpfr \
                        --with-gmp=$(pwd)/../libgmp --disable-shared --enable-static
make
make check
make install
{% endhighlight %}

## 6. Build libmpc
{% highlight bash %}
wget http://www.multiprecision.org/mpc/download/mpc-0.8.1.tar.gz
tar xvf mpc-0.8.1.tar.gz
mkdir build-mpc
cd build-mpc
../mpc-0.8.1/configure --host=${HOST} --build=${BUILD} --prefix=$(pwd)/../libmpc \
                       --with-gmp=$(pwd)/../libgmp --with-mpfr=$(pwd)/../libmpfr \
                       --disable-shared --enable-static
make
make install
{% endhighlight %}

## 7. Build GCC - Stage 1

Building GCC for Windows is the most complex part of this cross-compile.

{% highlight bash %}
git clone git://gcc.gnu.org/git/gcc.git
cd gcc
git checkout gcc-4_9_0-release
mkdir build-gcc
cd build-gcc
../gcc/configure --host=${HOST} --build=${BUILD} --target=${TARGET} --prefix=${PREFIX} \
                 --enable-interwork --enable-multilib --enable-languages="c" \
                 --with-newlib --without-headers --disable-shared --disable-libssp \
                 --with-gnu-as --with-gnu-ld --disable-nls \
                 --with-pkgversion=${PKGVERSION} --with-gmp=$(pwd)/../libgmp \
                 --with-mpfr=$(pwd)/../libmpfr --with-mpc=$(pwd)/../libmpc
make all-gcc
sudo make install-gcc
#make all-target-libgcc             # Cannot build using the Windows compiler in Wine on linux.
#sudo make install-target-libgcc    # Solution is to copy the libraries produced when building the toolchain for linux.
{% endhighlight %}

You'll find that at this point building libgcc and libstdc++ etc will actually fail. I finally realised that actually it doesn't matter
from this point on. You don't actually need to compile anything further with the Windows toolchain at this point.

Simply use the libraries as compiled by your native linux cross compiler, and copy them into your windows cross-compiler appropriately.

### Fixes or Patches for GCC 4.9.0

Currently you'll probably get a cannot find arm-unknown-eabi-gcc error when the build system attempts to dump the compiler
specs. To work around this, you can apply the following patch:

{% highlight bash %}
sed -i 's:$(GCC_FOR_TARGET) -dumpspecs > tmp-specs:./xgcc$(exeext) -dumpspecs > tmp-specs:g' gcc/Makefile
make all-gcc
sudo make install-gcc
make all-target-libgcc
sudo make install-target-libgcc
{% endhighlight %}

At this stage you should have a working cross-compiler. As long as you don't use any standard libraries at all, then you can
build a working kernel. In fact you should be able to use such a compiler to build BitThunder.

You can even use this compiler to build your own libc and then manually link with it.

For most purposes a basic libc is useful, and its really convenient to use e.g. the BTDK which uses a ported version of
newlib to provide a complete libc implementation on top of bitthunder.

## 8. Build Newlib

Again the secret is to simply copy the libraries produced by linux to the Windows toolchain folders.

## 9. Finalise GCC.

Not 100% sure what this stage does. I think it creates a arm-eabi-bt/bin/gcc.exe etc. In anycase I don't think they are needed,
and you can always copy the bin/arm-eabi-bt-gcc.exe files to the appropriate place manually.

