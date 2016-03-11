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

* *Refer to http://mamedev.org/tools/ for the latest toolkit for getting MAME compiled on Windows.*

* You will need to download the toolset from that link to begin. Periodically, these tools are updated and newer versions of MAME from that point on will **require** updated tools to compile. 

* You can do compilation on Visual Studio 2015 (if installed on your PC) by using **make vs2015**. This will always regenerate the settings, so **REGENIE=1** is *not* needed.