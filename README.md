# YASDOE

YASDOE a Simple ARM and 680x0 Operating System

YASDOE stands for Yet Another Simple Desktop Operating Environment.

Designed to be an easy to understand, easy to use, easy to program for, small Preemptive Multitasking, Protected Memory, Microkernel based Operating System with a very responsive Windowing System and simple CLI, YASDOE is a personal pasion of a project. Starting in 2012 YASDOE began to take form as I learned to program for a then new ARM based computer on the bare metal. Over the last 10 years YASDOE has become a usable Operating System, that I am ready to share with the world.

The ARM Version provides support for both big-endian ARM binaries as well as 680x0 binaries written for YASDOE.  The 680x0 on ARM version provides support for both as well, though more limited in the support of ARM binaries.  A native 680x0 version for non-ARM computers is a future extension.

The version that is being released at this time is the 680x0 on ARM version, this version is the most complete at this time.  This version runs a JIT emulation of the 68030 CPU with the entire OS, Drivers, and most libraries and and applications being compiled / assembled to run on the 68030 CPU.  For memory protection the 68030 PMMU is emulated by translating the page tables from 68K format into ARM format, thus the memory protection does not incure any additional hit.

To start with the versions released will use drivers that allow running hosted in RISC OS.  This is do to the fact that there are still a number of things not yet complete for the native running version, and as such it is a better experience with the RISC OS hosted version.  The most notable difference is that the hosted version supports TCP/IP networking which is still to come in the native version.

This document will improve over time, this version is just to give a quick overview, and have something in the repo until I get code uploaded.
