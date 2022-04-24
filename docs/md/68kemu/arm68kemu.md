## ARM Hosted 680x0 Emulation Layer

_Note: This document is in the process of being retyped from the original messed up copy.  Please forgive the time taken_

The 680x0 Emulation layer is a simple lazy JIT layer that translates up to a branch that exceeds already translated code, and inserts a call to the translator to continue translation.  The translator keeps a table of points where the code translation left off in the 68K original and the ARM translation for quick continuation, as multiple points may be end of translation points.  All data load / store address are treated as pointing to the memory of the 680x0 copy of the code.

The code is translated from 680x0 instructions to ARM instructions directly, except for code that uses the PMMU.  There are three versions of the ARM hosted emulation core, one translates to little endian data ARM code for the ARMv6 or newer (uses the REV instruction), one does the same for older ARM CPUs, and one that runs in big endian ARM mode.  The big endian ARM version is the fastest, though also the most buggy, the one for older ARM CPUs is the slowest do to needing 4 instructions to perform a byteswap, and the one for ARMv6 and newer using the REV instruction is nearly a third as fast as the host CPU in terms of instructions per second.

For more information on the specifics of how PMMU instructions are handled, please see the host specific document (as it varies depending on the host method).

The translation takes place by first fetching the first 16-bits of the next instruction (first word in 680x0 terms), then it decodes the opcode, fetching any needed additional words in the process.  Once decode it dumps the ARM code generated to the correct part of the ARM side code buffer, and repeats until it reaches a branch that goes outside the translated area.  The ending branch is replaced with a call to the translator so translation can continue.  The translator keeps a table of ARM and 680x0 code addresses for each stop point and each branch target, using said table to figure out where to translate to and from.

The exact details of the call made to continue translation depend on the Host details (RISC OS, BareMetal, or other).  So please return to the documentation contents to find those details for your system.

When data is fetched or stored by instructions, if running in Big Endian it is directly fetched, if running in little endian on an ARMv6 or newer it will preform the correct byteswap for the size of data being fetched inserting an REV or similar.  If running on an ARMv4 or earlier (sorry ARMv5 not supported) it will perfom the byteswap by the two or four instruction byteswap instructions that are well known (2 instructions for 16-bit byteswap and 4 for 32-bit byteswap).  The additional code needed to load or store data when running on the older CPUs is the reason for the extreme slowdown (about 8 times slower than the host in worse case).

For each data transfer the address used is from the 680x0 address space.  Thus relitive address are adjusted correctly, and absolute addresses are relitive to BASE680x0.  When the Emulator is running the ARM side register R11 always contains BASE680x0.  BASE680x0 refers to address 0 as seen from the 680x0 code.  The translated code running in the ARM side buffer is outside the 680x0 address space.

## Register Assignments:

680x0 Registers are mostly assigned directly to ARM registers, though not all.  The focus is on the most used of the 680x0 registers, thus normally we have:
 
* R0-R4 = D0-D4
* R5-R9 = A0-A4
* R13   = A7
* R11-R12 = Emulator temp usage registers.
* R10   = pointer to CPUBlock structure.

This covers the most common usage cases, as 680x0 code uses mostly D0-D4 and A0-A3.  The remaining registers are in the CPUBlock Structure in RAM (which should be in the L1 cache do to use).

## Things Requiring Special Consideration:

There are a few things that require special consideration, do to the nature of the differences between the 680x0 and the ARM CPU's.  Among these are the handling of the stack, for which we must generate a little extra code for every access of A7 on the 680x0 (R13 on the ARM).

A7 is the stack pointer on the 680x0 for most applications.  Thus A7 is assigned to the R13 stack, though there are times that the R13 stack must be ARM word alligned.  Most 680x0 applications keep the stack 16-bit alligned, we need 32-bit alligned for many things.  Thus when operating on the stack we insert code to keep the stack 32-bit alligned, and it is a good idea to figure that the code uses as much as 2 times as much stack space as the 680x0 equilivent.  Like the ARM the choice of registers for the stack is just a convention commonly used on the 680x0 CPUs, any Address register could be used as the stack.

As for the PC (R15 on ARM, implicit on 680x0) is not an issue, as the method code is translated keeps its allignment correct.

## TODO:

Need to add some pseudo code to help illistrate the function.  Need to add some actuall code to further illistrate the function.