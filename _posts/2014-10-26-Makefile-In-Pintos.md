---
layout: post
category: Pintos
tags: [Pintos, Operating System, Stanford]
---

We finished Project 1 thread scheduling last month and Project 2 user program early this week.

And there are many small things about makefile and other project files to notice.

###Can't format disk

When we were swiching from project 1 to project 2, pintos always yield "can not find option '-f'" exception. 

We found the reason is that the when building kernel, pintos doesn't define USERPROG.

Instead of manually define USERPROG in hard code, we can change the kernel.bin and loader.bin path in pintos and pintos-pm file under the bin folder, to the one under the userprog/build folder.

Thanks Ruiyang for detecting that.

###Can't make check & weird stack layout

The pintos source code in 2013spr folder is different from the code for 2014fall!

Make sure to add the following lines to shutdown_power_off() in devices/shudown.c after the serial_flush(); Make check issue solved.

/* ACPI power-off */

outw (0xB004, 0x2000);

for system call, the 2013spr code introduce a weird stack layout. That is because the assembly in src/lib/user/syscall.c use "g" as register argument instead of "r"!

"r"  means assign a general register  register for the argument,  "g" means  to assign  any register,  memory  or immediate integer for this.

###How to add more file to makefile

We just begin our project 3: virtual memory. It is an open-end project, and the vm folder is almost empty. When we want to put new file on it, we need to add the .c file in src/Makefile.build.

###How to run individual test cases

Go to the build folder for the project you want to do the test, enter make tests/abc.result where abc is the test name. For example in userprog project, if we want to make check args-many, we can type in 
"make tests/userprog/args-many.result".
