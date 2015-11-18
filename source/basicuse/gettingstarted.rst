*Current as of November 4th, 2015, version 0.167*

An Introduction to MAME
=======================

MAME is an acronym which stands for Multi Arcade Machine Emulator. MAME documents and reproduces through emulation the inner components of arcade machines, computers, consoles, chess computers, calculators, and many other types of electronic amusement machines. As a nice side-effect, MAME allows to use on a modern PC those programs and games which were originally developed for the emulated machines.

At one point there were actually two separate projects, MAME and MAME. MAME covered arcade machines, while MAME covered everything else. They are now merged into the one MAME.

MAME is mostly programmed in C with some core components in C++. MAME can currently emulate over 550 individual systems from the last 5 decades. [todo: get a better number, with the MAME merger, it's gotta be over 3000 by now..]


Purpose of MAME
===============

The primary purpose of MAME is to preserve decades of arcade, computer, and console history. As technology continues to rush forward, MAME prevents these important “vintage” systems from being lost and forgotten.


Systems Emulated by MAME
========================

[todo: Do we still want to rely on outside sources for system list/compatibility? If the site's still good and reliable, up to date, etc..]

ProjectMESS contains a complete list of the systems currently emulated. As you will notice, being supported does not always mean that the status of the emulation is perfect. You may want 

1. to check the status of the emulation in the wiki pages of each system, accessible from the drivers page (e.g. for Apple Macintosh, from the page for the mac.c driver you can reach the pages for both **macplus** and **macse**),
2. to read the corresponding **sysinfo.dat** entry in order to better understand which issues you may encounter while running a system in MAME (again, for Apple Macintosh Plus you have to check this entry). 

Alternatively, you can simply see the status by yourself, launching the system emulation and taking a look to the red or yellow warning screen which appears before the emulation starts, if any. Notice that if you have information which can help to improve the emulation of a supported system, or if you can directly contribute fixes and/or addition to the current source, you can follow the instructions at the contact page or post to the MAME Message Board.


Supported OS
============

The current source code can be directly compiled under all the main OSes: Microsoft Windows (both with DirectX native support and with SDL support), Linux, FreeBSD, Mac OSX, and OS/2. Also, both 32-bit and 64-bit executable can be built with no difficulties. [todo: with 32-bit compiles on Windows becoming problematic, we may want to note that Win32 may be EOL soon..]


Installing MAME
===============

Microsoft Windows
-----------------

You simply have to download the latest binary archive available from www.mamedev.org and to extract its content to a folder. You will end up with many files (below you find explanations about some of these), and in particular with MAME.EXE. This is a command line program. The installation procedure ends here. Easy, isn't it?


Other Operating Systems
-----------------------

In this case, you can either look for pre-compiled (SDL)MAME binaries (e.g. in the repositories of your favorite Linux distro) which should simply extract all the needed files in a folder you choose, or compile the source code by yourself. In the latter case, see our section on compiling MAME.


System Requirements
===================

[todo: Find out what we're compiling to these days..]

MAME is written in fairly generic C/C++, and has been ported to numerous platforms. Over time, as computer hardware has evolved, the MAME code has evolved as well to take advantage of the greater processing power and hardware capabilities offered.

The official MAME binaries are compiled and designed to run on a standard Windows-based system. The minimum requirements are:

* Any MMX-capable AMD or Intel processor (Pentium III or later recommended for current versions)
* Windows 98 or later (Windows 2000 or later preferred)
* DirectX 5.0 or later (included with all versions of Windows 98 or later)
* A DirectDraw or Direct3D capable graphics card
* Any DirectSound capable sound card

Of course, the minimum requirements are just that: minimal. You may not get optimal performance from such a system, but MAME should run. Modern versions of MAME require more power than older versions, so if you have a less-capable PC, you may find that using an older version of MAME may get you better performance, at the cost of lowered accuracy and fewer supported systems.

As of MAME 0.106 and later, MAME will take advantage of 3D hardware for compositing artwork and scaling the games to full screen. To make use of this, you should have a modern Direct3D 8-capable video card with at least 16MB of video RAM.

Around the same time, MAME added minimal multi-processor support, if you use the -mt flag. This means that some of the video processing can be done on a second CPU core if it is available. To take advantage of this, you should run MAME on a dual core (or greater) system.

Keep in mind that even on the fastest computers available, MAME is still incapable of playing some systems at full speed. The goal of the project isn't to make all system run speedy on your system; the goal is to document the hardware and reproduce the behavior of the hardware as faithfully as possible.


BIOS Dumps and Software
-----------------------

Most of the systems emulated by MAME requires a dump of the internal chips of the original system. These can be obtained by extracting the data from an original unit, or finding them (at your own risk) in the WorldWideWeb. Being copyrighted material, MAME does not come with any of these.

Also, you may want to find some software to be run on the emulated machine. Again, Google and other search engines are your best friends. MAME does not provide any software to be run on the emulated machines because it is very often (almost always, in the case of console software) copyrighted material.