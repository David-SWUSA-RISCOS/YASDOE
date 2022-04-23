# The 680x0 Emulation on RISC OS Hosted ARM Systems.

_Note: This document is in the process of being retyped from the original messed up copy.  Please forgive the time taken_

This document details the specifics for the RISC OS hosted version, for the details of the emulation layer propper pleas refer to:
[ARM Hosted 680x0 Emulation Layer](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/68kemu/arm68kemu.md)

The RISC OS hosted version runs single tasking from the view of RISC OS, thus stopping any other tasks until it is quit out of.  This allows us to use page mapping calls into RISC OS to work with pages as mapped from the 68030 PMMU pagetables.

The call for continuing translation on RISC OS hosted Systems is:  **SWI EMU68K_ContTrans**

When **SWI EMU68K_ContTrans** is called it uses the return address to determine the location in the address table, then uses the 68K address to continue from as stored in the translation address table.

For translating page tables we just use calls to map the page tables in RISC OS, very simple indeed.

If needed (such as for drivers) OS calls can be made using OS_CallASWI, which is mapped to TRAP #7 on the 680x0 side.  When calling a RISC OS SWI from the emulated code registers D0 through D7 map to ARM Registers R0 through R7, and registers A0 and A1 map to ARM registers R8 and R9.  The SWI number to call should be placed in A3 (which gets copied for the call).  This allows the 680x0 drivers to make use of RISC OS system calls, and is only allowed for code that is mapped in the address range 0x00F00000 through 0x00FFFFFF in the 680x0 address space (the top MB of the low 24bits of the address space).  Addresses are translated automatically for SWI calls the emulator knows about (which are only the ones needed by the current drivers).

## TODO:

Need to add a list of SWI calls that the Emulator knows about.  Need to expand on some of the description given above, and give a little more detail.  Need to improve the discription a bit.