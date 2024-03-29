The view that is presented here is that of the author of YASDOE, and one that is largely shared by some other Desktop ARM Computer users that the Author knows and speaks with about such things in the South-West United States of America.

# What is ARM, One View:

ARM is the CPU series that uses a 32-bit Instruction word, and implements the Instruction Set of the ARMv2, with some updates.  That is the core CPU, not any of the Coprocessors that are accessed by way of Coprocessor Instructions (like FPE, VFP, NEON, etc), coprocessors are just that, seperate from the CPU processors (even if they mix logic on die with the CPU, still a coprocessor).

Thumb is **NOT** ARM, Jazzle is **NOT** ARM, etc.

ARM is a simple ISA that has been lost to the company that now maintains the name.  ARM is what we saw with the ARMv2 (first widely available version), ARMv3, and ARMv4 implementations.  It can be argued that ARM is still alive in the ARMv5 and ARMv6 devices, and the author agrees with this, while these newer ISA's have some things that border on going to far, they are still at there core ARM devices.  ARMv7 is ARM like, though it depracates some instructions, making it not count (there are useful ARMv7 cores, the ones that still have the full 32-bit ARM ISA and still have SWAP).

There are three classes of ARM CPU's.  First are those that have a 24-bit PC and thus a 26 bit effective address range for Instruction acces, with the other bits of R15 being used for the current mode and flags.  Second are those that can operate with the 24-bit PC that uses the other bits for flags and mode, though can also operate with 32-bit PC in R15 with the PSR accessed seperately.  Third are those that can only work with a 32-bit PC that fills R15 and keeps the PSR seperate.  These are the only three groups that count as ARM.

Any of the other stuff that ARM Ltd. has come up with is **NOT ARM**.  That is to say that Tuumb, Thumb2, TumbEE, Jazzle, AARCH64, etc are **NOT ARM** .  Some of these are CISC like preprocessing devices that process a different ISA into the core ISA, some are just useless, and some are a different ISA altogether.  When you create a new incompatible ISA you create a new CPU with a new name so the ISA is known, at least this is how everyone else does it, ARM Ltd. should learn from the rest of the world on that one.

If the author understands correctly Thumb was requested by another company originally, under the thought of increasing code density.  Considering that the other company in question was using M680x0 series CPU's before ARM, and later added PowerPC CPU's it makes little sense, as ARM was very close in code density in most cases to the M680x0 (sometimes greater code density than the 680x0 series), and almost always higher code density than the PowerPC.

So the author likes ARM, true ARM that is.  The author does **not** like the other ISA based CPU's that wrongly have the name of ARM put on them, they are not ARM.
