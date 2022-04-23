# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple  680x0 Operating System.

For docs see: [Documentation Contents](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/contents.md)

Imagine an Operating Environment designed from the ground up to be small, fast, responsive, and radically simple.  Not just simple in its function, also simple to program for and to use.  This is the design goal of YASDOE, which to date has been a single person project over the last 10 years, starting in June of 2012 and finally being released to the world starting in May of 2022 (with some things ahead of this).

Designed to be easy to use.  YASDOE is modeled after some well known User Interfaces, taking to mind what people report liking about using each one.  Help is easy to obtain without looking awayfrom what you are doing.  Everything within the OS is well documented on how to do what you wish to do.  A good amount of effort has went into testing with people that are poor at using computers to help improve the user experience for any level of user.  The Windowing System is designed to be very responsive and intuitive, the CLI is intended to be easy to use with extreme power.

Provides a powerful work environment.  While it is easy to use, it is also very powerful.  Nothing is off limits to the user, and the features provided to improve workflow are very dynamic allowing more power than any one person can think of all the uses for.  In a fasion similar to some other OS's the intent is to provided the tools to use togather to do any number of tasks, each tool by itself is quite simple in nature, when used togather (very simply) there potential is exponential.

Designed to be completely understandable by any single programmer.  The API is very easy to understand, easy to use, and implemented with a very simple and usable ABI.  The algorithms used to implement each function, provided by the OS proper and its included libraries, are well documented, and in total can be understood by a single programmer.  All data structures are simple by design.

Anything and Everything.  YASDOE provides the programmer great power, including the ability to revecter any OS or library call, even for just a single task if wished.  While doing so it still provides a simple way to accomplish most things.

Stable and Reliable.  Well maybe not litterally, this is a prealpha state OS at this point.  Though the features of per task memory protection without slowing anything down, most system libraries run in User Mode, thus enhancing potential stability.  As such as bugs are found and fixed this is one OS that will become more and more stable with time.

A project of dedication.  I have been dedicated to YASDOE for ten years now, and have every intention of pushing on as long as I am alive.  This has become more than just another fun project, it has become a true dedication to create and continue to improve a good usable modern OS that is actually simple enough to use, program for, and understand in full.  With the goals mentioned above, as well as that of keeping the codebase as small as reasonable while providing all the extra functionality, this is an OS that should progress to continue to do better every month for the rest of its existence.  Being a truly Open Source project, without any restrictions on the use of the codebase, YASDOE is meant to live in one form or another for a long time, so long as at least one person has some interest in this OS it will live on.

The initial version is a neat concept.  The OS in all versions moving forward will run on 680x0 CPUs, though that presents an interesting issue of there being very few modern 680x0 systems.  The solution is to have an emulation layer that runs below the OS, emulating the 68030 CPU.  The CPU is emulation is designed to be as fast as I can get it running on bare HW or small Operating Systems, with the first verison being hosted on RISC OS.  I have written also a simple bare metal layer that allows for running YASDOE on the HW of the BCM2835 Single Board Desktop Computers, at what point that will be released is to be seen.

Very Portable. As most of the OS runs on the 680x0 CPU, porting becomes quite easy, if you are familiar enough with how the CPU emulation works and the target System it is easy to port the emulation layer to the target.  It is prefered to keep as much of the drivers 680x0 native as possible, though there is a means of using drivers written for the host CPU if this is absolutely needed (as it is for one driver used for the BCM2835 version).  As a note to the level of portability there is already a work in progress to update the 680x0 emulation layer and RISC OS hosted version to run on older ARM CPU's, without using big endian and without using the [b]rev[/b] instruction, thus allowing it to run on RiscPC and higher end A-Series RISC OS HW.

As to ease the fact that some of the native HW drivers for YASDOE are still a bit lacking in some areas (the focus was more the OS than the drivers till now), the first release will be designed to run hosted on top of RISC OS.  This is accomplished by using device drivers that go through RISC OS instead of to bare HW.  This has been a method of developing the OS, and as such is the best tested and most stable at this time.  As the HW drivers become more stable they will be released, and eventually a stable enough to be usable version will be able to run without being hosted on another OS.

# Where we Came From:

From the mid 1980s (1986) I have been an Amiga, and Atari ST/TT series user.  From the lat 1980s I have been a RISC OS user.  I continue to use RISC OS and Amiga OS to this day, though I admit my love for RISC OS is less than it used to be.  Amiga OS has always had a close place in my life, and likely always will.  As an Amiga user I am one of the purest that prefers the hunk format and non-linking (at runtime) shared libraries, this is a well known devide (the other side being the elf supporters) in the Amiga World.

Naturally I have had a hand in Amiga related projects in the past.  Was also involved in an 80x86 32-bit PMODE Operating System project that never got very far (because it was a commercial interest) in the late 1990s.

A bit more than 11 years ago, I had nearly given up on new RISC OS capable HW that could reasonable run with good support.  That changed in 2011 when first I heard about the BeagleBoard, then shortly thereafter about a new project from England that intends to create affordable computers.  This second project caught my eye quickly as a pre-release version of there ARM based computers was already running RISC OS.  So when this project released this new HW in 2012, based on the BCM2835 SoC, I decided to give RISC OS an extension to my usage.

Before long I was writing some bare metal programs on the RPi, this is where YASDOE began life (initially without a name).  This just seemed natural as we have always written bare metal programs for our computers.  Many 8-bitters, as well as Amigians, and Atarians have written a lot of bare metal code, running witout the aid of the OS, this is our nature in a way.  These little toys quickly came together once enough was available to support the strange USB of the BCM2835 based SBC, and before the end of 2012 was a proper working OS.

The concepts of keeping the system small, fast, responsive, usable, understandable, all began in 2012 as it went from bare metal emulation to a full blown 680x0 Operating System.  The YASDOE name is much newer, only being figured out in March of 2022 for the purpose of needing a name to release the project under.

# Ten Years?

If it is a small and simple system why did it take ten years?

YASDOE has had many parts written three or more time to improve the simplicity, make it smaller, and / or make it easier to use.  Writing an OS intended to be simple, small, fast, lightweight, easy to use, and responsive takes a lot of thought in how to implement things, especially when you are really serious about all these goals.  There may be component rewrites in the future to further improve the implementations, though the API / ABI is set in stone now.

Now YASDOE is at a point that it works, and has a stable API and ABI, so it is ready to be released.  I hope others enjoy YASDOE as it is updated.

## Notes:

NOTE 0A: There does exist one ARM native version, though it has never been as complete as the 680x0 version, and as it is crunch time on getting the release on github, I made the decision to focus only on the 680x0 version.

NOTE $0B: To assemble the 680x0 assembly sources you need Devpac 3 or later.  While I use the version for Atari TOS other 680x0 versions should work.

NOTE $0C: To Compile the C sources you need either Pure C or AHCC on an Atari ST/TT/Falcon series computer (or emulator).  Care has been taken to assure that the source should be able to compile with a 680x0 targetting Small C compiler as well, this includes using only integer variables and K&R type function definitions and declarations (also a personal rebelion to the crazy over-evolution of newer C standards).

NOTE $0D: Primary executable and library format is that of the Atari TOS (no name I know of).  Also provides some support for Amiga Hunk Files (work in progress).

NOTE $FF: I need a spell checker badly.  Perhaps should be editing this on RISC OS (!Zap has a spell checker).