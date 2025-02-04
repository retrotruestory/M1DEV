# Magic-1 Boot Process
By Bill Buzbee

On power-up or reset, interrupts are disabled, paging is disabled and the machine begins executing code in supervisor mode at address 0x0000.

With paging disabled, Magic-1 sees only 64K bytes of memory in the “device” space.  As currently implemented, the first 32K bytes of address 
are covered by overlapping a 27C256 EPROM and a 62256 SRAM.  The devices are wired in such that addresses 0x4000..0x7FFF always SRAM, and 
addresses 0x0000..0x3FFF cover either the SRAM or the EPROM depending on the setting of the ROM/RAM switch.  Normally, the switch is set to 
the ROM position.  The only time you’d use the RAM position is if you were toggling in a bootstrap program using the front panel.

Note that Magic-1 is hard-wired to locate its interrupt vector starting at address 0x0000 in data space.  This seems like a conflict when 
paging is disabled because because execution must start at 0x0000.  However, things work out OK.

Also, note that addresses 0xFF80 through 0xFFFF in data space are hard-wired to the UARTS, real-time clock, POST code display, IDE interface, 
front panel data switches and the Wiznet device.  See workspace/M1Dev/root/usr/include/magic1.h for the current assignments.

Currently, the boot ROM contains the bootloader found in the software image at:

	workspace/M1Dev/non_minix/bootloader

The very first code to execute resides in the file:

	workspace/M1Dev/non_minix/bootloader/bcrt0.s

Look for the following code:

	cseg
_start:
_interrupt_vector:
	sbr	over_ivec
	defw	unhandled_exception	; IRQ5 (RTC) 
	defw	unhandled_exception	; IRQ4 (unassigned)

Each interrupt vector is 2-bytes wide.  However, interrupt vector 0 is never used (it is reserved as part of the “fetch” microcode 
sequencing).  So, we are able to use that space for a 2-byte branch over the interrupt vector.

Execution then continues:

over_ivec:
	; On power-up or reset, we should already be interrupts off and
	; system mode, but go ahead and make sure before we do anything
	; else.
	;
	; For this loader, we're going to be as simple and compact
	; as possible.  All I/O will be busy wait - no interrupts
	ld.16	a,0x0000
	copy	msw,a		; interrupts off, system mode

		; Set up the kernel stack
	ld.16	a,stack_start
	copy	sp,a

		; Set the data base pointer (dp) to zero
	ld.16	a,dp_start
	copy	dp,a

		; go to C code, should not return
	call	_main	; with interrupts off

The remainder of bcrt0.s contains short assembly utility routines.  The primary work is now done in the source file:

	monitor/M1Dev/non_minix/bootloader/bloader.c

The primary job of the boot loader is to set up and enable paging, and perform basic I/O via the serial port and IDE interface.  
Note: when looking at this file you will see references to a CF (Compact Flash) card interface.  This is part of an experimental 
board that I developed.  It is not part of the regular Magic-1 schematics and can be ignored.

Starting at main() in bloader.c, our first task is to enable paging.  See: setup_address_space().  This is a somewhat tricky 
process, but the code should be sufficiently commented.

Once this is done, we initialize the serial ports, real-time clock, ide interface and then print out a banner.  Note that I’ve 
scattered to_post(x) calls throughout the code to help debug the boot process in case the serial port isn’t working as expected.

The primary job of the bootloader is to load either the second-stage Minix loader or the old Magic-1 monitor from disk.  When I 
developed this code, I chose the simplest file system possible: fixed locations for directory and files.  Sector 2 of the disk 
holds the image table, which shows the names and attributes of 8 possible images.  The images themselves are stored on the IDE 
drive in fixed 128K byte buckets on the drive.

The bootloader has the ability to read in new images from the serial port as “Intel Hex” text, and then write them to the ide drive.   
Examine the Magic-1 software build image for files ending in “.hex” for examples, as well as the tohex and fromhex utilities.

When developing Magic-1, I built up the IDE and Compact Flash images manually.  I don’t really remember the exact process, so I 
would strongly recommend starting with an existing image rather than a blank CF card.  Currently, I use 256 MB CF cards.   
The first partition is for the bootloader and original Magic-1 monitor, followed by 3 Minix partitions.  Here’s the output of 
the Minix “part” partition utility:

  Select device       ----first----  --geom/last--  ------sectors-----
    Device             Cyl Head Sec   Cyl Head Sec      Base      Size        Kb
    /dev/c0d0                         980   16  32
                         0    0   0   979   15  31         0    501760    250880
Num Sort   Type
 0*  p0  76 MAGIC1       0    1   0    40    0  31        32     20480     10240
 1   p1  81 MINIX       40    1   0   296    0  31     20512    131072     65536
 2   p2  81 MINIX      296    1   0   552    0  31    151584    131072     65536
 3   p3  81 MINIX      552    1   0   808    0  31    282656    131072     65536

SanDisk SDCFJ-256                      

The first 32 sectors are reserved for the bootloader, p0 is used by the monitor I used before getting Minix working, and 
the last 3 partitions are for Minix.  Note that in 16-bit Minix, file systems can be no larger than 64 Mbytes.

Anyway, back to the bootloader.  Here’s what the display should look like after power-on/reset:

 - - - - - - - - - - - - - - - -
Magic-1 boot loader, Version 3.4 - Minix
 - - - - - - - - - - - - - - - -

Master IDE drive: SanDisk SDCFJ-256, LBA supported, 245 MB
Slave IDE drive: SanDisk SDCFB-64, LBA supported, 61 MB

Active drive: Master IDE drive
Hit any key for menu .
=============================================
    Magic-1 boot loader command summary
          Version 3.4 - Minix
---------------------------------------------
S - Set active drive
P - Show image table
3 - Display drive info
L - [p] Load boot image (Intel hex)
Z - [p] Set default boot image
D - [p] Delete boot image
B - Boot an image
R - Read image table from disk
W - [p]Write boot images to disk
Q - [p]Toggle pre-boot pause on zero switches
V - Toggle [kernel] verbose mode
H/? - Display this help screen
=============================================
Magic-1 boot loader [Master IDE Drive] # 

You’d normally then execute the “r” command to read in the image table, and then “p” to print it out.  
Here’s what it might look like:

Magic-1 boot loader [Master IDE Drive] # r
Magic-1 boot loader [Master IDE Drive] # p
Available boot images:
   Slot 0 : "Milo 3.3", PID = 2, Split - Default image
   Slot 1 : "Mon11.0", PID = 3, Split
   Slot 2 : "Mon12.0", PID = 4, Split
   Slot 3 : Free : 5
   Slot 4 : Free : 6
   Slot 5 : Free : 7
   Slot 6 : Free : 8
   Slot 7 : Free : 9
Magic-1 boot loader [Master IDE Drive] # 


The “Milo 3.3” is the Minix loader, while Mon11.0 and Mon12.0 are two versions of the original Magic-1 monitor.

The source code for the Minix loader is:
	workspace/M1Dev/non_minix/minixloader

The source code for the Monitor is:
	workspace/M1Dev/non_minix/monitor

To execute any of these images, use the “b” command.  For example, to run the monitor:

Magic-1 boot loader [Master IDE Drive] # b
Available boot images:
   Slot 0 : "Milo 3.3", PID = 2, Split - Default image
   Slot 1 : "Mon11.0", PID = 3, Split
   Slot 2 : "Mon12.0", PID = 4, Split
   Slot 3 : Free : 5
   Slot 4 : Free : 6
   Slot 5 : Free : 7
   Slot 6 : Free : 8
   Slot 7 : Free : 9
Image table slot to boot? 2
................................................................................................................................

Master IDE drive: SanDisk SDCFJ-256, LBA supported, 245 MB
Slave IDE drive: SanDisk SDCFB-64, LBA supported, 61 MB








-------------------------------------------------------------------------------

            M     M                                            1
            MM   MM    aa     gggg      i     cccc            11
            M M M M   a  a   g    g     i    c    c          1 1
            M  M  M  a    a  g          i    c       -----     1
            M     M  aaaaaa  g  ggg     i    c                 1
            M     M  a    a  g    g     i    c    c            1
            M     M  a    a   gggg      i     cccc           11111
                     
                     Magic-1 HomebrewCPU TTL Minicomputer
                        Bill Buzbee, Half Moon Bay, CA
                   Tuesday, September 24 2024 - 04:51:08 PM
                        Magic-1 OS/Monitor Version 12.0
-------------------------------------------------------------------------------
 ** Welcome!  Take a look around, and then sign the guestbook
 ("X" then number for Guestbook - ?/H for Help)

Magic-1 # 

Using the “?” command, we can see the Monitor options:

Magic-1 # ?
===============================================================================
|                     Magic-1 monitor command summary                         |
---------------------------------------|---------------------------------------
|       Normal Commands                |       Password Protected Commands    |
---------------------------------------|---------------------------------------
| 2 - Display current time             | 0 [p] Timer interrupts off           |
| 3 - Display IDE hard drive info      | 1 [p] Timer interrupts on            |
| 6 - Seconds since UTC 00:00 1/1/1970 | L [p] Load program (Intel Hex fmt)   |
| 8 - Say Hi!                          | D [p] Delete program                 |
| 9 - Display message of the day       | W [p] Write program to disk          |
| P - Show available programs          | V [p] Toggle verbose kernel messages |
| X - Execute program                  | Y [p] Delete file                    |
| R - Read program directory from disk | C [p] Copy disk image to/from flash  |
| U - Show uptime stats                | T [p] Launch background task         |
| F - Display file directory           | K [p] Kill background task           |
| Z - Toggle stacktrace on <ctl>-G     | 4 [p] Lock process into memory       |
| B - Operate on disk partitions       | 7 [p] Reboot                         |
| <control>-G - Display task status    | E [p] Toggle TTY status & reset uarts|
| <control>-C - Kill foreground task   | G Boot Minix (experimental)          |
| H or ? - Display this help screen    | S [p] Set time/date                  |
===============================================================================
Magic-1 # 

Note that some of these commands, such as “G Boot Minix” probably no longer work.

Let’s reset the machine and go back to the bootloader.

One additional feature of the bootloader is that it can be configured with a default boot image.  
Once the machine is reset, the bootloader waits for input from the serial port.  If there is no input after 60 seconds, 
the bootloader will automatically boot the default image.  This allows Magic-1 to restart after a power outage.

Now, let’s boot Minix this time.  From the bootloader, we read the image table and them boot “Milo”:

Magic-1 boot loader [Master IDE Drive # r
Magic-1 boot loader [Master IDE Drive] # b
Available boot images:
   Slot 0 : "Milo 3.3", PID = 2, Split - Default image
   Slot 1 : "Mon11.0", PID = 3, Split
   Slot 2 : "Mon12.0", PID = 4, Split
   Slot 3 : Free : 5
   Slot 4 : Free : 6
   Slot 5 : Free : 7
   Slot 6 : Free : 8
   Slot 7 : Free : 9
Image table slot to boot? 0
................................................................................................................................

 - - - - - - - - - - - - - - - -
Minix Loader, Version 3.3
 - - - - - - - - - - - - - - - -

Master IDE drive: SanDisk SDCFJ-256, LBA supported, 245 MB
Slave IDE drive: SanDisk SDCFB-64, LBA supported, 61 MB

Booting default image in  60
# 

I hit <return> after Milo came up, which stopped the “Booting default image” countdown.  Just like the bootloader, 
the Minix loader also has a default image and timeout.

The Minix loader (Milo) can be found at:

	workspace/non_minix/minixloader

The Minix booting process is a bit ugly.  We have to tell it which Minix partition to boot, and also set up some environment variables.  
To make it a little easier, these variables are stored in a special location on the disk (and I don’t recall where that is - look at 
the source code if you are interested).

The Milo commands can be listed by entering “?”

# ?
Commands:  set unset device dir ls super partition quit bye cat help ? save clear read verbose default curr boot b 
# 

Look at the milo source code for full descriptions of these commands.  The key ones we need are:
device: tell Milo which partition we want to boot
set: set an environment variable
b: boot the current device

I generally use partition 1 as a recovery partition, partition 2 as the primary partition and partition 3 for extra data storage.

So, to boot Minix you would first type:

# device c0d0p2
Device c0d0p2[1] is current device

In Minix, partitions are described by the triple controller, disk, partition.  In our case c0 is Magic-1’s IDE interface, d0 is the 
IDE master disk (d1 is the slave), and p2 is partiton 2.

Besides identifying the boot partition, you also need to set several environment variables using the “set” command.  
You can also save these using the “save” command.  To see the current values, use the “set” command without any arguments:

# set
imagedev=771
rootdev=771
ramsize=600
memory=20000:3e0000
bootdir=/minix/
defaultdev=c0d0p2
bootopts=-n
# 

I tell myself that someday I’ll clean this code up, but probably won’t.  The environment variables are a little awkward.  
Here’s a brief description:

Imagedev,rootdev: The value here, 771, is in decimal.  But in hex it is 0x0303.  This corresponds to the major and minor 
device numbers of /dev/c0d0p2.  Looking at the block device files in Minix /dev we see:

# ls -l /dev/c0d0*
brw------- 1 root  operator  3,   0 Nov 11  2021 /dev/c0d0
brw------- 1 root  operator  3,   1 Oct 20  2007 /dev/c0d0p0
brw------- 1 root  operator  3,   2 May 22  2022 /dev/c0d0p1
brw------- 1 root  operator  3,   3 Apr 30  2019 /dev/c0d0p2
brw------- 1 root  operator  3,   4 Oct 20  2007 /dev/c0d0p3
# 

So, if you wanted to boot partition 1 of the IDE master disk, you should set imagedev and rootdev to decimal 770, which is 0x0302.

The next variable is “ramsize”.  This set the number of 2K pages to allocate to a RAM disk.  
My version of Minix allows for 3 ramdisks, and you’d allocate them here as ramdisk, ramdisk1 and ramdisk2.   
They would appear on the system as /dev/ram, /dev/ram1 and /dev/ram2.  To use them, you’d “mkfs /dev/ram” 
and them mount /dev/ram somewhere.

Next is “memory”.  This tells Minix what physical memory is available for use.  It is normally set as “memory=20000:3e0000”. 
Memory up to 0x20000 is used during the Minix boot process, so we reserve it.

“bootdir” tells the loader where in the file system on the boot disk we can find the system files.  
The files needed are kernel, fs, mm, init and mapper.

“defaultdev” is there for Milo, and tells which partition to boot if we time out.

“bootopts” are flags for /init/rc.  The one I use are:
   s - single-user mode
   n - disable networking
   r - disable ramdisk

See workspace/M1Dev/root/etc/rc for example usage.
Finally, here’s an example of booting Magic-1 from reset into Minix with ramdisk enabled, but networking disabled:


 - - - - - - - - - - - - - - - -
Magic-1 boot loader, Version 3.4 - Minix
 - - - - - - - - - - - - - - - -

Master IDE drive: SanDisk SDCFJ-256, LBA supported, 245 MB
Slave IDE drive: SanDisk SDCFB-64, LBA supported, 61 MB

Active drive: Master IDE Drive
Hit any key for menu .
=============================================
    Magic-1 boot loader command summary
          Version 3.4 - Minix
---------------------------------------------
S - Set active drive
P - Show image table
3 - Display drive info
L - [p] Load boot image (Intel hex)
Z - [p] Set default boot image
D - [p] Delete boot image
B - Boot an image
R - Read image table from disk
W - [p]Write boot images to disk
Q - [p]Toggle pre-boot pause on zero switches
V - Toggle [kernel] verbose mode
H/? - Display this help screen
=============================================
Magic-1 boot loader [Master IDE Drive] # r
Magic-1 boot loader [Master IDE Drive] # b
Available boot images:
   Slot 0 : "Milo 3.3", PID = 2, Split - Default image
   Slot 1 : "Mon11.0", PID = 3, Split
   Slot 2 : "Mon12.0", PID = 4, Split
   Slot 3 : Free : 5
   Slot 4 : Free : 6
   Slot 5 : Free : 7
   Slot 6 : Free : 8
   Slot 7 : Free : 9
Image table slot to boot? 0
................................................................................................................................

 - - - - - - - - - - - - - - - -
Minix Loader, Version 3.3
 - - - - - - - - - - - - - - - -

Master IDE drive: SanDisk SDCFJ-256, LBA supported, 245 MB
Slave IDE drive: SanDisk SDCFB-64, LBA supported, 61 MB

Booting default image in  60
# device c0d0p2
Device c0d0p2[0] is current device
# b


 *********** Minix boot **************

Booting from c0d0p2:/minix/
Loading kernel: 26 text start 64, 4 data start 90, 22 bss starting 94
..........................
,,,,;;;;;;;;;;;;;;;;;;;;;;||||||
Loading mm: 12 text start 122, 1 data start 134, 14 bss starting 135
............
,;;;;;;;;;;;;;;|||||||||||||||||
Loading fs: 19 text start 166, 2 data start 185, 25 bss starting 187
...................
,,;;;;;;;;;;;;;;;;;;;;;;;;;|||||
Loading mapper: 3 text start 217, 1 data start 220, 4 bss starting 221
...
,;;;;|||||||||||||||||||||||||||
Loading init: 4 text start 252, 1 data start 256, 1 bss starting 257
....
,;||||||||||||||||||||||||||||||
 Here we go!
================================================



Relocating remap_supervisor from 0x1FFE to 0xEABC, len 186
Relocating switch_to_minix from 0x6E to 0xEB76, len 4
Relocating code_pte from 0x27 to 0xEB7A, len 9
Relocating data_pte from 0x30 to 0xEB83, len 9
Jumping to remap supervisor page table and launch Minix
Start_phys_page:64, ssp:0xEAAE, new_sp:0xF000, tgt_location:0xFABC
Total memory size: 3968 Kbytes
Minix 2.0.4  Copyright 2001 Prentice-Hall, Inc.

Mapper is alive
SanDisk SDCFJ-256                      

Mapper is intialized

Memory size = 3968K   MINIX = 448K   RAM disk = 1200K   Available = 2320K

Tuesday, September 24 2024 - 05:44:12 PM GMT
Multiuser startup in progress.
Setting up /bin as ramdisk
/dev/ram is read-write mounted on /mnt
/dev/ram unmounted from /mnt
/dev/ram is read-write mounted on /bin
Skipping network initialization

Minix  Release 2 Version 0.4

Magic1 login: 
