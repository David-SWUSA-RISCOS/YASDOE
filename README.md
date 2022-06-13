# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

PLEASE SEE: [The YASDOE WIKI](https://github.com/David-SWUSA-RISCOS/YASDOE/wiki) For more information

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple 65816, ARM, and 680x0 Operating System.

**UPDATE:** The RISC OS Hosted version is workable, need to redo some things do to small changes made, though no need to worry about HW support anymore on the ARM target (RISC OS provides that, essentially using RISC OS as a HAL for YASDOE).

**UPDATE:** The ARM Version is back.  I like the real ARM ISA too much not to continue that branch.  Wish I had not moved away from that, just allowed political crud to influence mmy decisions on development for a short time.  The ARM ISA as implemented in the ARMv2, ARMv3, ARMv4 is a great ISA, and still useful into ARMv5 and ARMv6 (so long as you ignore Thumb (Thumb sucks), ignore Jazzle, etc), the core ARM ISA is still and always will be great.  Remember that VFP is a cooprocessor (VFP code is explicitly coprocessor instructions, dispatching to CP10/CP11).

**UPDATE:** A successful boot on a 6502 computer with 256KB bank swiched RAM has been done.  This may help shape the future direction of YASDOE, potentially without the limits of only supporting 65816 and 68K.

YASDOE has changed directions radically, thankfully before any code was posted.  There will be continuing updates, though in the future only for 680x0 and 65816 based computers.  The choice to target 680x0 and 65816 based systems is down to the available software, as well as the abilities of the 2gs computer that are above and beyond those that are known as Mac.

The 680x0 series has a bright future, so does the 65816 (currently in the form of the WDC65C816S, as well as higher speed versions).

Part of the purpose of this project is to add to the potential implementation of extreme long term computing. As a CPU the 65816 is one of the best canidates for extreme long term computing, that is computing applications where the hardware and software must remain operational with minimal maintainence for centuries.  Long term computing is a big area of studdy for me, as we are on the edge of seeing deep space travel.  Also we live in a world where reducing all forms of waste is needed (we create way too much waste), keeping our computers in use for centuries will aid in reducing this waste.  Also if computers are used for centuries at a time we will actually have time to reach the limits of optimizing for these computers.

The future direction will be based on much of the existing code of YASDOE.  Specifically there will end up being two components of YASDOE, a ROM that is able to boot both YASDOE and Macintosh System Software (or GS/OS on the 65816 HW) and thus provides the needed toolsets, and the disk based system software intended to be compatible with the same.

Please refer to the YASDOE github wiki for more information.
