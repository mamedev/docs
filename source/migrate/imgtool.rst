Imgtool - *A generic image manipulation tool for MAME*
======================================================

*Current as of November 4th, 2015, version 0.167*


Imgtool is a tool for the maintenance and manipulation of disk and other types of images that MAME users need to deal with.  Functions include retrieving and storing files and CRC checking/validation.

Imgtool is part of the MAME project.  It shares large portions of code with MAME, and its existence would not be if it were not for MAME.  As such, the distribution terms are the same as MAME.  Please read the MAME license thoroughly. 

**Some portions of Imgtool are Copyright (c) 1989, 1993 The Regents of the University of California.  All rights reserved.**

Using Imgtool
=============

Imgtool is a command line program that contains several "subcommands" that actually do all of the work.  Most commands are invoked in a manner along the lines of this:

	**imgtool <subcommand> <format> <image> ...**

* **<subcommand>** is the name of the subcommand
* **<format>** is the format of the image
* **<image>** is the filename of the image

Example usage:
	imgtool dir coco_jvc_rsdos myimageinazip.zip
	
	imgtool get coco_jvc_rsdos myimage.dsk myfile.bin mynewfile.txt
	
	imgtool getall coco_jvc_rsdos myimage.dsk


Further details vary with each subcommand.  Also note that not all subcommands are applicable or supported for different image formats.

*Certain Imgtool subcommands (info, crc, good) make use of the CRC files, so if you use these commands, make sure that your CRC directory is set up.*


Imgtool Subcommands
===================

**create**

	**imgtool create <format> <imagename> [--(createoption)=value]**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name

	
	Creates an image

**dir**

	**imgtool dir <format> <imagename> [path]**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name

	Lists the contents of an image

**get**

	**imgtool get <format> <imagename> <filename> [newname] [--filter=filter] [--fork=fork]**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Gets a single file from an image

**put**

	**imgtool put <format> <imagename> <filename>... <destname> [--(fileoption)==value] [--filter=filter] [--fork=fork]**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Puts a single file on an image (wildcards supported)

**getall**

	**imgtool getall <format> <imagename> [path] [--filter=filter]**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Gets all files off an image

**del**

	**imgtool del <format> <imagename> <filename>...**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Deletes a file on an image

**mkdir**

	**imgtool mkdir <format> <imagename> <dirname>**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Creates a subdirectory on an image

**rmdir**

	**imgtool rmdir <format> <imagename> <dirname>...**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Deletes a subdirectory on an image

**readsector**

	**imgtool readsector <format> <imagename> <track> <head> <sector> <filename>**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	Read a sector on an image and output it to specified <filename>

**writesector**
	
	**imgtool writesector <format> <imagename> <track> <head> <sector> <filename>**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name

	Write a sector to an image from specified <filename>

**identify**

	* <format> is the image format, e.g. coco_jvc_rsdos
	* <imagename> is the image filename; can specify a ZIP file for image name
	
	**imgtool identify <imagename>**

**listformats**

	Lists all image file formats supported by imgtool

**listfilters**

	Lists all filters supported by imgtool

**listdriveroptions**

	**imgtool listdriveroptions <format>**

	* <format> is the image format, e.g. coco_jvc_rsdos
	
	Lists all format-specific options for the 'put' and 'create' commands



Imgtool Filters
===============

Filters are a means to process data being written into or read out of an image in a certain way.  Filters can be specified on the get, put, and getall commands by specifying --filter=xxxx on the command line.  Currently, the following filters are supported:

**ascii**

	Translates end-of-lines to the appropriate format

**cocobas**

	Processes tokenized TRS-80 Color Computer (CoCo) BASIC programs

**dragonbas**

	Processes tokenized Tano/Dragon Data Dragon 32/64 BASIC programs

**macbinary**

	Processes Apple MacBinary-formatted (merged forks) files
	
**vzsnapshot**

	[todo: VZ Snapshot? Find out what this is....]

**vzbas**

	Processes Laser/VZ Tokenized Basic Files

**thombas5**

	Thomson MO5 w/ BASIC 1.0, Tokenized Files (read-only, auto-decrypt)

**thombas7**

	Thomson TO7 w/ BASIC 1.0, Tokenized Files (read-only, auto-decrypt)

**thombas128**

	Thomson w/ BASIC 128/512, Tokenized Files (read-only, auto-decrypt)

**thomcrypt**

	Thomson BASIC, Protected file encryption (no tokenization)

**bm13bas**

	Basic Master Level 3 Tokenized Basic Files
	
Imgtool Format Info
===================

  =======================  ========================================================
  amiga_floppy             Amiga floppy disk image (OFS/FFS format)
  apple2_do_prodos_525     Apple ][ DOS order disk image (ProDOS format)
  apple2_nib_prodos_525    Apple ][ Nibble order disk image (ProDOS format)
  apple2_po_prodos_525     Apple ][ ProDOS order disk image (ProDOS format)
  apple35_2img_prodos_35   Apple ][gs 2IMG disk image (ProDOS format)
  apple35_dc_mac_hfs       Apple DiskCopy disk image (Mac HFS Floppy)
  apple35_dc_mac_mfs       Apple DiskCopy disk image (Mac MFS Floppy)
  apple35_dc_prodos_35     Apple DiskCopy disk image (ProDOS format)
  apple35_raw_mac_hfs      Apple raw 3.5" disk image (Mac HFS Floppy)
  apple35_raw_mac_mfs      Apple raw 3.5" disk image (Mac MFS Floppy)
  apple35_raw_prodos_35    Apple raw 3.5" disk image (ProDOS format)
  coco_dmk_os9             CoCo DMK disk image (OS-9 format)
  coco_dmk_rsdos           CoCo DMK disk image (RS-DOS format)
  coco_jvc_os9             CoCo JVC disk image (OS-9 format)
  coco_jvc_rsdos           CoCo JVC disk image (RS-DOS format)
  coco_os9_os9             CoCo OS-9 disk image (OS-9 format)
  coco_vdk_os9             CoCo VDK disk image (OS-9 format)
  coco_vdk_rsdos           CoCo VDK disk image (RS-DOS format)
  concept                  Concept floppy disk image
  cqm_bml3                 CopyQM floppy disk image (Basic Master Level 3 format)
  cqm_fat                  CopyQM floppy disk image (FAT format)
  cqm_mac_hfs              CopyQM floppy disk image (Mac HFS Floppy)
  cqm_mac_mfs              CopyQM floppy disk image (Mac MFS Floppy)
  cqm_os9                  CopyQM floppy disk image (OS-9 format)
  cqm_prodos_35            CopyQM floppy disk image (ProDOS format)
  cqm_prodos_525           CopyQM floppy disk image (ProDOS format)
  cqm_rsdos                CopyQM floppy disk image (RS-DOS format)
  cqm_vzdos                CopyQM floppy disk image (VZ-DOS format)
  cybiko                   Cybiko Classic File System
  cybikoxt                 Cybiko Xtreme File System
  d88_bml3                 D88 Floppy Disk image (Basic Master Level 3 format)
  d88_fat                  D88 Floppy Disk image (FAT format)
  d88_mac_hfs              D88 Floppy Disk image (Mac HFS Floppy)
  d88_mac_mfs              D88 Floppy Disk image (Mac MFS Floppy)
  d88_os9                  D88 Floppy Disk image (OS-9 format)
  d88_prodos_35            D88 Floppy Disk image (ProDOS format)
  d88_prodos_525           D88 Floppy Disk image (ProDOS format)
  d88_rsdos                D88 Floppy Disk image (RS-DOS format)
  d88_vzdos                D88 Floppy Disk image (VZ-DOS format)
  dsk_bml3                 DSK floppy disk image (Basic Master Level 3 format)
  dsk_fat                  DSK floppy disk image (FAT format)
  dsk_mac_hfs              DSK floppy disk image (Mac HFS Floppy)
  dsk_mac_mfs              DSK floppy disk image (Mac MFS Floppy)
  dsk_os9                  DSK floppy disk image (OS-9 format)
  dsk_prodos_35            DSK floppy disk image (ProDOS format)
  dsk_prodos_525           DSK floppy disk image (ProDOS format)
  dsk_rsdos                DSK floppy disk image (RS-DOS format)
  dsk_vzdos                DSK floppy disk image (VZ-DOS format)
  fdi_bml3                 Formatted Disk Image (Basic Master Level 3 format)
  fdi_fat                  Formatted Disk Image (FAT format)
  fdi_mac_hfs              Formatted Disk Image (Mac HFS Floppy)
  fdi_mac_mfs              Formatted Disk Image (Mac MFS Floppy)
  fdi_os9                  Formatted Disk Image (OS-9 format)
  fdi_prodos_35            Formatted Disk Image (ProDOS format)
  fdi_prodos_525           Formatted Disk Image (ProDOS format)
  fdi_rsdos                Formatted Disk Image (RS-DOS format)
  fdi_vzdos                Formatted Disk Image (VZ-DOS format)
  hp48                     HP48 SX/GX memory card
  imd_bml3                 IMD floppy disk image (Basic Master Level 3 format)
  imd_fat                  IMD floppy disk image (FAT format)
  imd_mac_hfs              IMD floppy disk image (Mac HFS Floppy)
  imd_mac_mfs              IMD floppy disk image (Mac MFS Floppy)
  imd_os9                  IMD floppy disk image (OS-9 format)
  imd_prodos_35            IMD floppy disk image (ProDOS format)
  imd_prodos_525           IMD floppy disk image (ProDOS format)
  imd_rsdos                IMD floppy disk image (RS-DOS format)
  imd_vzdos                IMD floppy disk image (VZ-DOS format)
  mess_hd                  MESS hard disk image
  pc99fm                   TI99 Diskette (PC99 FM format)
  pc99mfm                  TI99 Diskette (PC99 MFM format)
  pc_chd                   PC CHD disk image
  pc_dsk_fat               PC floppy disk image (FAT format)
  psionpack                Psion Organiser II Datapack
  td0_bml3                 Teledisk floppy disk image (Basic Master Level 3 format)
  td0_fat                  Teledisk floppy disk image (FAT format)
  td0_mac_hfs              Teledisk floppy disk image (Mac HFS Floppy)
  td0_mac_mfs              Teledisk floppy disk image (Mac MFS Floppy)
  td0_os9                  Teledisk floppy disk image (OS-9 format)
  td0_prodos_35            Teledisk floppy disk image (ProDOS format)
  td0_prodos_525           Teledisk floppy disk image (ProDOS format)
  td0_rsdos                Teledisk floppy disk image (RS-DOS format)
  td0_vzdos                Teledisk floppy disk image (VZ-DOS format)
  thom_fd                  Thomson .fd disk image, BASIC format
  thom_qd                  Thomson .qd disk image, BASIC format
  thom_sap                 Thomson .sap disk image, BASIC format
  ti990hd                  TI990 Hard Disk
  ti99_old                 TI99 Diskette (old MESS format)
  ti99hd                   TI99 Harddisk
  v9t9                     TI99 Diskette (V9T9 format)
  vtech1_vzdos             Laser/VZ disk image (VZ-DOS format)
  =======================  ========================================================


Driver specific options for module 'amiga_floppy':

No image specific file options

Image specific creation options (usable on the 'create' command):


================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--density        dd/hd                          Density
--filesystem     ofs/ffs                        File system
--mode           none/intl/dirc                 File system options
================ ============================== =============================================================




Driver specific options for module 'apple2_do_prodos_525':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1                              Heads
--tracks         35                             Tracks
--sectors        16                             Sectors
--sectorlength   256                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple2_nib_prodos_525':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1                              Heads
--tracks         35                             Tracks
--sectors        16                             Sectors
--sectorlength   256                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple2_po_prodos_525':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1                              Heads
--tracks         35                             Tracks
--sectors        16                             Sectors
--sectorlength   256                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_2img_prodos_35':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_dc_mac_hfs':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_dc_mac_mfs':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_dc_prodos_35':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_raw_mac_hfs':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_raw_mac_mfs':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'apple35_raw_prodos_35':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         80                             Tracks
--sectorlength   512                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================


Driver specific options for module 'coco_dmk_os9':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ =============================== =============================================================
Option           Allowed values                  Description
---------------- ------------------------------- -------------------------------------------------------------
--heads          1-2                             Heads
--tracks         35-255                          Tracks
--sectors        1-18                            Sectors
--sectorlength   128/256/512/1024/2048/4096/8192 Sector Bytes
--interleave     0-17                            Interleave
--firstsectorid  0-1                             First Sector
================ =============================== =============================================================


Driver specific options for module 'coco_dmk_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================

Image specific creation options (usable on the 'create' command):

================ =============================== =============================================================
Option           Allowed values                  Description
---------------- ------------------------------- -------------------------------------------------------------
--heads          1-2                             Heads
--tracks         35-255                          Tracks
--sectors        1-18                            Sectors
--sectorlength   128/256/512/1024/2048/4096/8192 Sector Bytes
--interleave     0-17                            Interleave
--firstsectorid  0-1                             First Sector
================ =============================== =============================================================


Driver specific options for module 'coco_jvc_os9':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         35-255                         Tracks
--sectors        1-255                          Sectors
--sectorlength   128/256/512/1024               Sector Bytes
--firstsectorid  0-1                            First Sector
================ ============================== =============================================================


Driver specific options for module 'coco_jvc_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         35-255                         Tracks
--sectors        1-255                          Sectors
--sectorlength   128/256/512/1024               Sector Bytes
--firstsectorid  0-1                            First Sector
================ ============================== =============================================================


Driver specific options for module 'coco_os9_os9':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         35-255                         Tracks
--sectors        1-255                          Sectors
--sectorlength   128/256/512/1024               Sector Bytes
--firstsectorid  1                              First Sector
================ ============================== =============================================================



Driver specific options for module 'coco_vdk_os9':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         35-255                         Tracks
--sectors        18                             Sectors
--sectorlength   256                            Sector Bytes
--firstsectorid  1                              First Sector
================ ============================== =============================================================



Driver specific options for module 'coco_vdk_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         35-255                         Tracks
--sectors        18                             Sectors
--sectorlength   256                            Sector Bytes
--firstsectorid  1                              First Sector
================ ============================== =============================================================



Driver specific options for module 'concept':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'cqm_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'cqm_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'cqm_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'cybiko':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--flash          AT45DB041/AT45DB081/AT45DB161  Flash Type
================ ============================== =============================================================



Driver specific options for module 'cybikoxt':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'd88_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'd88_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'd88_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================

No image specific creation options


Driver specific options for module 'dsk_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'dsk_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'dsk_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'dsk_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'fdi_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'fdi_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'fdi_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'fdi_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'hp48':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ================================ =============================================================
Option           Allowed values                   Description
---------------- -------------------------------- -------------------------------------------------------------
--size           32/64/128/256/512/1024/2048/4096 Size in KB
================ ================================ =============================================================



Driver specific options for module 'imd_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'imd_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'imd_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'imd_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'mess_hd':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ================================================= =============================================================
Option           Allowed values                                    Description
---------------- ------------------------------------------------- -------------------------------------------------------------
--blocksize      1-2048                                            Sectors Per Block
--cylinders      1-65536                                           Cylinders
--heads          1-64                                              Heads
--sectors        1-4096                                            Total Sectors
--seclen         128/256/512/1024/2048/4096/8192/16384/32768/65536 Sector Bytes
================ ================================================= =============================================================


Driver specific options for module 'pc99fm':

No image specific file options

No image specific creation options


Driver specific options for module 'pc99mfm':

No image specific file options

No image specific creation options


Driver specific options for module 'pc_chd':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ====================================================================== =============================================================
Option           Allowed values                                                         Description
---------------- ---------------------------------------------------------------------- -------------------------------------------------------------
--cylinders      10/20/30/40/50/60/70/80/90/100/110/120/130/140/150/160/170/180/190/200 Cylinders
--heads          1-16                                                                   Heads
--sectors        1-63                                                                   Sectors
================ ====================================================================== =============================================================


Driver specific options for module 'pc_dsk_fat':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         40/80                          Tracks
--sectors        8/9/10/15/18/36                Sectors
================ ============================== =============================================================


Driver specific options for module 'psionpack':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--type           OB3/OPL/ODB                    file type
--id             0/145-255                      File ID
================ ============================== =============================================================


Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--size           8k/16k/32k/64k/128k            datapack size
--ram            0/1                            EPROM/RAM datapack
--paged          0/1                            linear/paged datapack
--protect        0/1                            write-protected datapack
--boot           0/1                            bootable datapack
--copy           0/1                            copyable datapack
================ ============================== =============================================================


Driver specific options for module 'td0_bml3':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'td0_fat':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_mac_hfs':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_mac_mfs':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_os9':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_prodos_35':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_prodos_525':

No image specific file options

No image specific creation options


Driver specific options for module 'td0_rsdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/data/binary/assembler    File type
--ascii          ascii/binary                   Ascii flag
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'td0_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


No image specific creation options


Driver specific options for module 'thom_fd':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          auto/B/D/M/A                   File type
--format         auto/B/A                       Format flag
--comment        (string)                       Comment
================ ============================== =============================================================

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         40/80                          Tracks
--density        SD/DD                          Density
--name           (string)                       Floppy name
================ ============================== =============================================================


Driver specific options for module 'thom_qd':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          auto/B/D/M/A                   File type
--format         auto/B/A                       Format flag
--comment        (string)                       Comment
================ ============================== =============================================================

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1-2                            Heads
--tracks         25                             Tracks
--density        SD/DD                          Density
--name           (string)                       Floppy name
================ ============================== =============================================================


Driver specific options for module 'thom_sap':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          auto/B/D/M/A                   File type
--format         auto/B/A                       Format flag
--comment        (string)                       Comment
================ ============================== =============================================================


Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1                              Heads
--tracks         40/80                          Tracks
--density        SD/DD                          Density
--name           (string)                       Floppy name
================ ============================== =============================================================


Driver specific options for module 'ti990hd':

No image specific file options

Image specific creation options (usable on the 'create' command):

================   ============================== =============================================================
Option             Allowed values                 Description
----------------   ------------------------------ -------------------------------------------------------------
--cylinders        1-2047                         Cylinders
--heads            1-31                           Heads
--sectors          1-256                          Sectors
--bytes per sector (typically 25256-512 256-512   Bytes Per Sector [Todo: This section is glitched in imgtool]
================   ============================== =============================================================


Driver specific options for module 'ti99_old':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--sides          1-2                            Sides
--tracks         1-80                           Tracks
--sectors        1-36                           Sectors (1->9 for SD, 1->18 for DD, 1->36 for HD)
--protection     0-1                            Protection (0 for normal, 1 for protected)
--density        Auto/SD/DD/HD                  Density
================ ============================== =============================================================


Driver specific options for module 'ti99hd':

No image specific file options

No image specific creation options


Driver specific options for module 'v9t9':

No image specific file options

Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--sides          1-2                            Sides
--tracks         1-80                           Tracks
--sectors        1-36                           Sectors (1->9 for SD, 1->18 for DD, 1->36 for HD)
--protection     0-1                            Protection (0 for normal, 1 for protected)
--density        Auto/SD/DD/HD                  Density
================ ============================== =============================================================



Driver specific options for module 'vtech1_vzdos':

Image specific file options (usable on the 'put' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--ftype          basic/binary/data              File type
--fname          intern/extern                  Filename
================ ============================== =============================================================


Image specific creation options (usable on the 'create' command):

================ ============================== =============================================================
Option           Allowed values                 Description
---------------- ------------------------------ -------------------------------------------------------------
--heads          1                              Heads
--tracks         40                             Tracks
--sectors        16                             Sectors
--sectorlength   154                            Sector Bytes
--firstsectorid  0                              First Sector
================ ============================== =============================================================



  
[todo: fill out the command structures, describe commands better. These descriptions came from the imgtool.txt file and are barebones]
[todo: merge the two lists better]