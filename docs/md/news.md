# YASDOE NEWS:

## April 29th:

Bad-ish News: There does not apear to be much interest in YASDOE yet, and code will start going up soon (still targeting May 2nd).

Goodish news.  The core emulation layer is nearly ready to have its repo created, and then it should be fairly quick to get every version uploaded.

## April 29th:

Slowly plodding along in preperation to get some code up.  Also found a neglected project that may merit some interest in the distant future

## April 24th:

I can see the point that enough documentation is up to start posting sources to the YASDOE Repository.  The begining for everyone else is in sight at last.

The amount of documentation that has to be retyped is surprising in nature.  I had not realised I had messed up so much the first time through.

As I got thinking about the side project a little yesterday, I will note that GraFaDOE will be released after YASDOE is realeased to a completely usable point (including binaries).  GraFaDOE will be released under the **Unlicense**, as this is a well known nearly PD license (and truely PD where possible).

The goal is to get the stuff that can be used by other OS's documented and released first, as that will be the most immediate benifit.  Once that is done it should be quicker to get the rest of YASDOE into the repo.  Again remember the main bottleneck is getting the documentation ahead of anything released.

## April 23RD:

Considering a change in one element of the design of YASDOE.  Currently it relies on the abiltiy to use the PMMU to protect memory, this limits the hosts or the speed (either have to use a host that lets us play with the page mapping, or have to go pure software emulation on the 680x0).  As such, knowing it would only mean modifying a total of 14 lines of code (can remove the other stuff that becomes dead code later), I am considering making YASDOE use a flat, unprotected, memory model before it is released.

I personally have always prefered Operating Systems that use a flat memory space without protection.  Despite what many say this does not effect the security of the computer (unless a user runs a program that effects security, same issue even with memory protection (not going into this rant here)), and it does make some things a lot easier to work with.  This would also move a step closer to the great Amiga OS.

Doing this change would ease adding MINIX Hosted, BSD Hosted, Haiku OS hosted, and AROS Hosted versions of YASDOE.  It will also be helpful when it is time to port the core to CPUs other than the ARM (a lot of the 680x0 PMMU emulation is tightly tied to the ARM or RISC OS).  There have been many good operating systems on the 680x0 series of CPUs that run well and secure without any memory protection at all, including though not limited to SMSQ/E, TOS, AmigaOS, AROS, MiNT, Macintosh System Software, MP/M, CP/M, Human68k, OS-9, QDOS, Minerva, 68K/OS.

The idea of YASDOE being to only emulate the CPU, using drivers that interface to the Host System directly (if in another OS, uses the host OS, if on bare HW interfaces to the HW it runs on) makes for the possibility of also eventually porting other 680x0 Operating Systems to the 680x0 core of YASDOE.  It is probable that at some point I will split the 680x0 emulation core off into its own project so others can use it.

Beings attempting to be complete: As a side project I have worked on, in part to test ideas for YASDOE, I have another less complete OS (I am calling GraFaDOE) that uses the Emulation core from YASDOE already, one that provides an API and ABI that many people will be very familiar with.  So one could say that GraFaDOE is a side-effect of writing YASDOE, the reason it has a familiar API is that there was the need to not need special tools for testing ideas. Thus I chose to make GraFaDOE run programs written for a very well known 680x0 OS (that is GraFaDOE is a partial clone of a well known 680x0 OS).  The OS that GraFaDOE is a partial clone of uses A-Line traps for most OS Calls, and is known for its use of clipping areas using line based clipping and supporting irragular shaped non-continous clipping areas, it is also known for it's extremely versitile method of handling resource data accross the OS, Applications, and even Documents in a dynamic manner (hence making a great testbed).

Having played with Macintosh Computers of my own in the 1990s (and some owned by others before that), I can see another potential HW target for YASDOE.  The 680x0 and Old-World PowerPC based Macintosh computers are an easy potential target for future versions of YASDOE (as well as GraFaDOE).  This HW uses a simple framebuffer for the primary graphics, uses well documented HW for most things, and provides a lot of HW abstraction in the System ROM that we can take advantage of.

For reasons that I will not go into here I am becoming a bit of a skeptic about the future of Linux (and thus for now using Linux more).  I use Linux at this time, though I am also keeping my eye on other Operating Systems that others may migrate to in the future.  Like many that once used Macintosh System Software or AmigaOS on there main computer and Linux or Unix on a play or work computer, so I intend to migrate to using Linux (possibly replaced in future) on a play computer and YASDOE and GraFaDOE (to be anounced) on my main computers.

## April 22ND

Learned how to use **git** finally.  Started getting some of the documentation for YASDOE online (ended up having to rewrite most of it).

## April 21ST:

After 10 years of developing YASDOE I created a Github Repository to host YASDOE.  This gives the ability to share a great work that others may have an interest in.
