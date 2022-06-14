# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

PLEASE SEE: [The YASDOE WIKI](https://github.com/David-SWUSA-RISCOS/YASDOE/wiki) For more information

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple ARM, and 680x0 Operating System.

---

**I apologize** I apologize to anyone waiting to see YASDOE.  I repeated a mistake I had made before, the mistake of attempting to move awayfrom ARM and RISC OS, this mistake has delayed things in the release of YASDOE.   The Wiki needs a lot of rewriting to get back to the version as it was initialy to be released (an Amiga Like library based calling convention OS, that is preemptive multitasking, and has a RISC OS like API).

I messed up, and my mess up has caused me to revamp a lot of code, and rewrite a lot of documentation, just to have to undo these changes once I realized my mistake.  Though it does have the advantage that YASDOE is a lot better than it would have been, no more central kernel, everything a lot simpler instead.  I am still trying to improve the use of region based clipping in a WIMP style Windowing System (takes some work), as the WIMP API, and programs that use it assume multiple rectangle clipping.

---

**UPDATE:** The RISC OS Hosted version is workable, need to redo some things do to small changes made, though no need to worry about HW support anymore on the [ARM](./docs/WhatIsARM.md) target (RISC OS provides that, essentially using RISC OS as a HAL for YASDOE).

**UPDATE:** The [ARM](./docs/WhatIsARM.md) Version is back.  I like the real ARM ISA too much not to continue that branch.  Wish I had not moved away from that, just allowed political crud to influence mmy decisions on development for a short time.  The ARM ISA as implemented in the ARMv2, ARMv3, ARMv4 is a great ISA, and still useful into ARMv5 and ARMv6 (so long as you ignore Thumb (Thumb sucks), ignore Jazzle, etc), the core ARM ISA is still and always will be great.  Remember that VFP is a cooprocessor (VFP code is explicitly coprocessor instructions, dispatching to CP10/CP11(if you need proof look at the opcodes)).

