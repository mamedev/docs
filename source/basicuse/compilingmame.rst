Compiling MAME
==============

.. _compiling-MAME:

All Platforms
-------------

* Whenever you are changing build parameters, (such as switching between a SDL-based build and a native Windows renderer one, or adding tools to the compile list) you need to run a **make REGENIE=1** to allow the settings to be regenerated. Failure to do this will cause you very difficult to troubleshoot problems.
 
* If you want to add various additional tools to the compile, such as *CHDMAN*, add a **TOOLS=1** to your make statement, like **make REGNIE=1 TOOLS=1**
 
* You can do driver specific builds by using *SOURCES=<driver>* in your make statement. For instance, building Pac-Man by itself would be **make SOURCES=src/mame/drivers/pacman.cpp REGENIE=1** including the necessary *REGENIE* for rebuilding the settings.
 
* Speeding up the compilation can be done by using more cores from your CPU. This is done with the **-j** parameter. *Note: the maximum number you should use is the number of cores your CPU has, plus one. No higher than that will speed up the compilation, and may in fact slow it down.* For instance, **make -j5** on a quad-core CPU will provide optimal speed.
 
* Lastly, tiny builds of MAME are good for debugging a single driver during development. This can be done by **make tiny** and as always remember that REGENIE is needed any time you're making changes to what you want to compile.
 
Putting all of these together, we get a couple of examples:

Rebuilding MAME for just the Pac-Man driver, with tools, on a quad-core (e.g. i5 or i7) machine:

| **make SOURCES=src/mame/drivers/pacman.cpp REGENIE=1 -j5**
| 

Rebuilding MAME on a dual-core (e.g. i3) machine:

| **make -j3**
| 


Microsoft Windows
-----------------

Here are specific notes about compiling MAME for Microsoft Windows.

* Refer to `the MAME tools site <http://mamedev.org/tools/>`_ for the latest toolkit for getting MAME compiled on Windows.

* You will need to download the toolset from that link to begin. Periodically, these tools are updated and newer versions of MAME from that point on will **require** updated tools to compile. 

* You can do compilation on Visual Studio 2015 (if installed on your PC) by using **make vs2015**. This will always regenerate the settings, so **REGENIE=1** is *not* needed.

* Make sure you get SDL 2 2.0.3 or 2.0.4 as earlier versions are buggy.


Fedora Linux
------------

You'll need a few prerequisites from your distro. Make sure you get SDL2 2.0.3 or 2.0.4 as earlier versions are buggy.

**sudo yum install gcc gcc-c++ SDL2-devel SDL2_ttf-devel libXinerama-devel qt5-qtbase-devel qt5-qttools expat-devel fontconfig-devel**

Compilation is exactly as described above in All Platforms.


Debian and Ubuntu (including Raspberry Pi and ODROID devices)
-------------------------------------------------------------

You'll need a few prerequisites from your distro. Make sure you get SDL2 2.0.3 or 2.0.4 as earlier versions are buggy.

**sudo apt-get install git build-essentials libsdl2-dev libsdl2-ttf-dev libfontconfig-dev qt5-default**

Compilation is exactly as described above in All Platforms.


Arch Linux
----------

You'll need a few prerequisites from your distro.

**sudo pacman -S base-devel git sdl2 gconf sdl2_ttf gcc qt5**

Compilation is exactly as described above in All Platforms.


Apple Mac OS X
--------------

You'll need a few prerequisites to get started. Make sure you're on OS X 10.9 Mavericks or later. You will NEED SDL2 2.0.4 for OS X.

* Install **Xcode** from the Mac App Store
* Launch **Xcode**. It will download a few additional prerequisites. Let this run through before proceeding.
* Once that's done, quit **Xcode** and open a **Terminal** window
* Type **xcode-select --install** to install additional tools necessary for MAME

Next you'll need to get SDL2 installed.

* Go to `this site <http://libsdl.org/download-2.0.php>`_ and download the *Mac OS X* .dmg file
* If the .dmg doesn't auto-open, open it
* Click 'Macintosh HD' (or whatever your Mac's hard disk is named) in the left pane of a **Finder** window, then open the **Library** folder and drag the **SDL2.framework** folder from the SDL disk image into the **Frameworks** folder

Lastly to begin compiling, use Terminal to navigate to where you have the MAME source tree (*cd* command) and follow the normal compilation instructions from above in All Platforms.

It's possible to get MAME working from 10.6, but a bit more complicated:

* You'll need to install clang-3.7, ld64, libcxx and python27 from MacPorts
* Then add these options to your make command or useroptions.mak:

| 
| OVERRIDE_CC=/opt/local/bin/clang-mp-3.7
| OVERRIDE_CXX=/opt/local/bin/clang++-mp-3.7
| PYTHON_EXECUTABLE=/opt/local/bin/python2.7
| ARCHOPTS=-stdlib=libc++
| 
