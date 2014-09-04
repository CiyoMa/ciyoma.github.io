---
layout: post
category: Pintos
tags: [Pintos, Operating System, Stanford]
---

Pintos is an educational operating system developed by Stanford University. Below is a tutorial to install pintos on Ubuntu 12.04

Pintos code has been written to run on Unix based systems, so you can install it on Mac, Ubuntu and other linux distribution.

###Prerequisites

The following packages need to be installed on your system:

1.  GCC

2.  GNU binutils

3.  Perl

4.  GNU make

5.  QEMU; "If QEMU is not available, Bochs can be used, but its slowness is frustrating." 

6.  GDB

install them by

    sudo apt-get install gcc binutils perl make qemu gdb

###Installation

NOTE: $HOME will refer to your home directory, wherever you create a folder for pintos. 

####PLEASE CHANGE $HOME TO YOUR ACTUAL PATH!!!

Once the prerequisites have been installed, do the following steps:

1.  Download Pintos:

	Download the pintos source code on github. Extract it in some directory, say $HOME/stanford .

2.  Set GDBMACROS

	Open the script 'pintos-gdb' (in $HOME/stanford/pintos/src/utils) in any text editor. Find the variable GDBMACROS and set it to point to $HOME/stanford/pintos/src/misc/gdb-macros .

	####Remember to replace $HOME with the actual path.

3.  Compile the utilities

	Change to the utils folder, if not already there, and compile the utilities by typing

		make

	on the terminal.

	If you get an error saying "Undefined reference to ‘floor' ", make the following changes; edit 'Makefile' in the current directory and replace "LDFLAGS = -lm" by "LDLIBS = -lm". Recompile now, it will work.

4.  Edit Make.vars in /threads

	Edit the file 'Make.vars' in the 'threads' directory ( $HOME/stanford/pintos/src/threads ); change the last line to:
		SIMULATOR = --qemu

5.  Compile Pintos kernel

	Change to the 'threads' directory, if not already there, and run 'make' to compile the pintos kernel.

6.  Edit the pintos utility

	Make these changes in the 'pintos' file at $HOME/stanford/pintos/src/utils/':

    	a) On line number 103, change 'bochs' to 'qemu'.
    	b) On line number 259, change 'kernel.bin' to the actual path at '$HOME/stanford/pintos/src/threads/build/kernel.bin'.

7.  Edit pintos.pm file

	Open the file '$HOME/stanford/pintos/src/utils/Pintos.pm' in the editor and at line number 362, change "loader.bin" to the actual path to the file at '$HOME/stanford/pintos/src/threads/build/loader.bin'.

8.  Create qemu link

	You need to create a link to the QEMU executable on your system; these will generally be found in '/usr/bin'. If it is not there search the $PATH folders for it. Whichever directory you find it, change to that directory and type the following command:

    	ln -s qemu-system-i386 qemu

	####IF YOUR SYSTEM IS 64-BITS USE FOLLOWING CODE INSTEAD

    	ln -s qemu-system-x86_64 qemu

	This will create a link 'qemu' to the QEMU executable.

	Restart the terminal for changes to take effect.

9.  Run Pintos

	Go to the 'utils' directory at '$HOME/stanford/pintos/src/utils/' and run pintos with the following command:

	pintos run alarm-multiple

10. Copy utils from $HOME/stanford/pintos/src/utils to $HOME/stanford/pintos/bin

11. Add pintos to $PATH

        $ export PATH=$PATH:$HOME/standford/pintos/bin

    Now you are all set to get hacking away with Pintos.

    try 
        pintos run alarm-multiple

###Acknowledgement
[This](http://krharsha.blogspot.com/2013/08/pintos-installation.html) is the site that got me started. I encountered some errors by krharsha's tutorial but fix it in bold text.

[This](http://computercalledvarun.wordpress.com/2013/02/03/pintos-on-ubuntu/) is the site recommended by [Professor Wilson](http://www.ccs.neu.edu/home/cbw/)

###For Pintos installation on Northeastern CCIS machine
After you copy and untar the pintos.tar.gz file to the "stanford" folder I said at the begining of this post from "/course/cs5600sp13". [INSTRUCTION HERE](http://www.ccs.neu.edu/home/cbw/5600/pintos/pintos_1.html#SEC1)

1. Create a .bash_profile file under your home folder. write

        export PATH=${PATH}:$HOME/standford/pintos/bin:/course/cs5600sp13/bin:/course/cs5600sp13/pintos/bin

2. Restart your terminal

3. Do the qemu/boches, kernel.bin/loader.bin name modifying things as the part above in your "stanford" folder. Exactly the same steps above, except installing and linking qemu, since professor have already put them in /course/cs5600sp13/bin and /course/cs5600sp13/pintos/bin.

4. Congratulations! pintos installed!
