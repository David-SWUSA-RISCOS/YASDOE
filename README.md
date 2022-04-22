![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple ARM and 680x0 Operating System.

Imagine an Operating Environment designed from the ground up to be small, fast, responsive, and radically simple.  Not just simple in its function, also simple to program for and to use.  This is the design goal of YASDOE, which to date has been a single person project over the last 10 years, starting in June of 2012 and finally being released to the world starting in May of 2022 (with some things ahead of this).

Designed to be easy to use.  YASDOE is modeled after some well known User Interfaces, taking to mind what people report liking about using each one.  Help is easy to obtain without looking awayfrom what you are doing.  Everything within the OS is well documented on how to do what you wish to do.  A good amount of effort has went into testing with people that are poor at using computers to help improve the user experience for any level of user.  The Windowing System is designed to be very responsive and intuitive, the CLI is intended to be easy to use with extreme power.

Provides a powerful work environment.  While it is easy to use, it is also very powerful.  Nothing is off limits to the user, and the features provided to improve workflow are very dynamic allowing more power than any one person can think of all the uses for.  In a fasion similar to some other OS's the intent is to provided the tools to use togather to do any number of tasks, each tool by itself is quite simple in nature, when used togather (very simply) there potential is exponential.

Designed to be completely understandable by any single programmer.  The API is very easy to understand, easy to use, and implemented with a very simple and usable ABI.  The algorithms used to implement each function, provided by the OS proper and its included libraries, are well documented, and in total can be understood by a single programmer.  All data structures are simple by design.

Anything and Everything.  YASDOE provides the programmer great power, including the ability to revecter any OS or library call, even for just a single task if wished.  While doing so it still provides a simple way to accomplish most things.

Stable and Reliable.  Well maybe not litterally, this is a prealpha state OS at this point.  Though the features of per task memory protection without slowing anything down, most system libraries run in User Mode, thus enhancing potential stability.  As such as bugs are found and fixed this is one OS that will become more and more stable with time.

A project of dedication.  I have been dedicated to YASDOE for ten years now, and have every intention of pushing on as long as I am alive.  This has become more than just another fun project, it has become a true dedication to create and continue to improve a good usable modern OS that is actually simple enough to use, program for, and understand in full.  With the goals mentioned above, as well as that of keeping the codebase as small as reasonable while providing all the extra functionality, this is an OS that should progress to continue to do better every month for the rest of its existence.  Being a truly Open Source project, without any restrictions on the use of the codebase, YASDOE is meant to live in one form or another for a long time, so long as at least one person has some interest in this OS it will live on.

The initial version is a cool hybrid of implementation.  The target being Single Board Computers based on the BCM2835 SoC, the physical CPU is an ARM1176, though the OS runs mostly on a 68030 compatible CPU.  This is accomplished through the use of a very effecient Emulation layer, that runs under the OS.  To aid in keeping the speed high, the 68030 style PMMU is emulated by translating the 68K page tables into ARM page tables.  It is still possible to run ARM native libraries and binaries, though these are not considered native format to the OS.

As to ease the fact that some of the native HW drivers for YASDOE are still a bit lacking in some areas (the focus was more the OS than the drivers till now), the first release will be designed to run hosted on top of RISC OS.  This is accomplished by using device drivers that go through RISC OS instead of to bare HW.  This has been a method of developing the OS, and as such is the best tested and most stable at this time.  As the HW drivers become more stable they will be released, and eventually a stable enough to be usable version will be able to run without being hosted on another OS.

# Ten Years?

If it is a small and simple system why did it take ten years?

YASDOE has had many parts written three or more time to improve the simplicity, make it smaller, and / or make it easier to use.  Writing an OS intended to be simple, small, fast, lightweight, easy to use, and responsive takes a lot of thought in how to implement things, especially when you are really serious about all these goals.  There may be component rewrites in the future to further improve the implementations, though the API / ABI is set in stone now.

Now YASDOE is at a point that it works, and has a stable API and ABI, so it is ready to be released.



FOOTNOTE: I need a spell checker badly.
