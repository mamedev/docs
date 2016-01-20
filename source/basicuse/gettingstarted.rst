An Introduction to MAME
=======================

MAME is an acronym which stands for Multi Arcade Machine Emulator. MAME documents and reproduces through emulation the inner components of arcade machines, computers, consoles, chess computers, calculators, and many other types of electronic amusement machines. As a nice side-effect, MAME allows to use on a modern PC those programs and games which were originally developed for the emulated machines.

At one point there were actually two separate projects, MAME and MESS. MAME covered arcade machines, while MESS covered everything else. They are now merged into the one MAME.

MAME is mostly programmed in C with some core components in C++. MAME can currently emulate over 32000 individual systems from the last 5 decades.


Purpose of MAME
===============

The primary purpose of MAME is to preserve decades of arcade, computer, and console history. As technology continues to rush forward, MAME prevents these important “vintage” systems from being lost and forgotten.


Systems Emulated by MAME
========================


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

You simply have to download the latest binary archive available from http://www.mamedev.org and to extract its content to a folder. You will end up with many files (below you will find explanations about some of these), and in particular **MAME.EXE**. This is a command line program. The installation procedure ends here. Easy, isn't it?


Other Operating Systems
-----------------------

In this case, you can either look for pre-compiled (SDL)MAME binaries (e.g. in the repositories of your favorite Linux distro) which should simply extract all the needed files in a folder you choose, or compile the source code by yourself. In the latter case, see our section on compiling MAME.


System Requirements
===================

MAME is written in fairly generic C/C++, and has been ported to numerous platforms. Over time, as computer hardware has evolved, the MAME code has evolved as well to take advantage of the greater processing power and hardware capabilities offered.

The official MAME binaries are compiled and designed to run on a standard Windows-based system. The minimum requirements are:

* Intel Core series CPU or equivalent, at least 2.0 GHz
* 32-bit OS (Vista SP1 or later on Windows, 10.9 or later on Mac)
* 4 GB RAM
* DirectX 9.0c for Windows
* A DirectDraw, Direct3D, or OpenGL capable graphics card
* Any DirectSound capable sound card/onboard audio

Of course, the minimum requirements are just that: minimal. You may not get optimal performance from such a system, but MAME should run. Modern versions of MAME require more power than older versions, so if you have a less-capable PC, you may find that using an older version of MAME may get you better performance, at the cost of greatly lowered accuracy and fewer supported systems.

MAME will take advantage of 3D hardware for compositing artwork and scaling the games to full screen. To make use of this, you should have a modern Direct3D 8-capable video card with at least 16MB of video RAM.

HLSL or GLSL special effects such as CRT simulation will put a very heavy load on your video card, especially at higher resolutions. You will need a fairly powerful modern video card, and the load on your video card goes up exponentially as your resolution increases. If HLSL or GLSL are too intensive, try dropping your output resolution.

MAME also has minimal multi-processor support, if you use the **-mt** flag. This means that some of the video processing can be done on a second CPU core if it is available. To take advantage of this, you should run MAME on a dual-core (or greater) system.

Keep in mind that even on the fastest computers available, MAME is still incapable of playing some systems at full speed. The goal of the project isn't to make all system run speedy on your system; the goal is to document the hardware and reproduce the behavior of the hardware as faithfully as possible.


BIOS Dumps and Software
-----------------------

Most of the systems emulated by MAME requires a dump of the internal chips of the original system. These can be obtained by extracting the data from an original unit, or finding them (at your own risk) in the WorldWideWeb. Being copyrighted material, MAME does not come with any of these.

Also, you may want to find some software to be run on the emulated machine. Again, Google and other search engines are your best friends. MAME does not provide any software to be run on the emulated machines because it is very often (almost always, in the case of console software) copyrighted material.


Using MAME
----------


If you are a new MAME user, you could find this emulator a bit complex at first. Let's take a moment to talk about softlists, as they can simplify matters quite a bit. If the content you are trying to play is a documented entry on one of the MAME softlists, starting the content is as easy as

    **mame.exe** *<system>* *<software>*

For instance:

    **mame.exe nes metroidu**

will load the USA version of Metroid for the Nintendo Entertainment System.


Alternatively, you could start MAME with

	**mame.exe nes**
	
and choose the *software list* from the cartridge slot. From there, you could pick any softlist-compatible software you have in your roms folders. Please note that many older dumps of cartridges and discs may either be bad or require renaming to match up to the softlist in order to work in this way.


If you are loading an arcade board or other non-softlist content, things are only a little more complicated:


The basic usage, from command line, is

	**mame.exe** *<system>* *<media>* *<software>* *<options>*

where

* *<system>* is the shortname of the system you want to emulate (e.g. nes, c64, etc.)
* *<media>* is the switch for the media you want to load (if it's a cartridge, try **-cart** or **-cart1**; if it's a floppy disk, try **-flop** or **-flop1**; if it's a CD-ROM, try **-cdrom**)
* *<software>* is the program / game you want to load (and it can be given either as the fullpath to the file to load, or as the shortname of the file in our software lists)
* *<options>* is any additional command line option for controllers, video, sound, etc.

Remember that if you type a <system> name which does not correspond to any emulated system, MAME will suggest you some possible choices which are close to what you typed; and if you don't know which <media> switch are available, you can always launch

	**mame.exe** *<system>* **-listmedia**

If you don't know what *<options>* are available, there are a few things you can do. First of all, you can check the command line options section of this manual. You can also try one of the many :ref:`frontends` available for MAME.


Alternatively, you should keep in mind the following command line options, which might be very useful on occasion:


	**mame.exe -help**

tells what MAME is the basic structure of MAME launching options, i.e. as explained above.


	**mame.exe -showusage**

gives you the (quite long) list of available command line options for MAME. The main options are described, in the :ref:`universal-command-line` section of this manual.


	**mame.exe -showconfig**

gives you a (quite long) list of available configuration options for MAME. These configuration can always be modified at command line, or by editing them in mame.ini which is the main configuration file for MAME. You can find a description of some configuration options in the :ref:`universal-command-line` section of the manual (in most cases, each configuration option has a corresponding command line option to configure and modify it).


	**mame.exe -createconfig**

creates a brand new **mame.ini** file, with default configuration settings. Notice that mame.ini is basically a plain text file, hence you can open it with any text editor (e.g. Notepad, Emacs or TextEdit) and configure every option you need. However, no particular tweaks are needed to start, so you can basically leave most of the options unaltered.


Once you are more confident with MAME options, you may want to configure a bit more your setup. In this case, keep in mind the order in which options are read; see :ref:`advanced-multi-CFG` for details.

