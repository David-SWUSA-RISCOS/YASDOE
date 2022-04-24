# YASDOE Inspiration.

Direct Inspiration for YASDOE comes from a number of other Operating Systems that I am familiar with:


* **Amiga OS** : To many things are demonstrated by Amiga OS and helped in the creation of YASDOE.  See the Amiga OS section below.
* **Atari TOS** : Simplicity put to good use, proving complexity is not required.
* **Atari MiNT** : Demonstrates how simply a good Kernel and OS can be written, and what to avoid to keep speed.
* **RISC OS** : Some of the concepts on easy means of redirection of verious system functions, as well as Drag and Drop.
* **The X Windowing System** : Shows Some lessons about how to do things.
* **BeOS** : Some of the GUI concepts came of use in the design of YASDOE.
* **X-GUI** : Showed some light on simple methods to do some things in a GUI.
* **Ancient Unix** : Provided a base concept of how to ease the applications while improving the overall system.
* **Zerro-GUI** : As I wrote this in 1993 through 1995, it inspired me through the experience gained in its creation.
* **ProDOS** : From this we get the concept of using "/" as the root of the forest, and having each volume and file device be the first level under that.
* **PlayerKit** : From this old (1979) program comes the inspiration of line wise clipping, and non-continous clipping areas.
* **Macintosh System Software** : From this we get the concept of compressing line wise clipping to save space.  Also an alternative means of storing the **.info** data (do not need a seperate file, can use a secondary data stream on the file).

There are other influences as well, though these are the major ones.  The breif descriptions in this list are just to show major the points, below are sections for each of these and how they effected the creation and design of YASDOE.


---
## Amiga OS:

From Amiga OS comes a great amount of the inspiration behind YASDOE, from the Microkernel, to direct call libraries, up to the GUI task, and through the multi-state icons.  Amiga OS is one Operating System I have very heavily used, and thus it is natural for it to be a large part of the inspiration of YASDOE.

We get the concept of kernel lists for everything from Amiga OS.  This is heavily used in YASDOE to simplify resource tracking, which is a core feature of YASDOE.

The CLI is largely modeled after that of Amiga OS, with largely the same command set though not quite the same rules for device level objects.  Thus easy to learn commands, that many already know from other Operating Systems are the norm.  Also many of the low level utilities common to Amiga OS have been cloned, such as **ed** .  Then there are the scripts used, including one named **startup-sequence** and one named **user-startup** among others.

The user experience of the Windowing System will remind one of Amiga OS in a number of ways.  From windows having dynamic focus (depth in stack does not effect focus), to using right mouse clicks to bring up in place menus for the program being used (OK more MagicMenu, though what Amiga User does not use MagicMenu).  Also has the ability to specify background images for the backdrop, each directory or sub-tree, etc.  The Windowing System is lower level than the CLI, the CLI relies on the Windowing System in order to run.

The use of a **.info** file for specifying the properties of files that are visable in the desktop environment comes from the Amiga world.  As does the use of two state icons.

The means of keeping applications responsive, even when they are too busy, is inspired by Amiga Intuition.  In fact the Window Manager is a very similar to that of Intuition, almost though not quite a clone.  This includes the way the Window Manager runs as a task of its own, how it calls directly into application space to handle events, etc.

Also our DOS.LIBRARY is heavily modeled on that of AmigaOS.  This includes the default filesystem, that takes a number of ideas from Amiga FFS, though does a few things a little better for speed.  There is also support for using colon appended device names, like in AmigaOS, even though this is not the native filespec for YASDOE.  Likewise our timestamps are very much like those in FFS, allowing for at least 5.7 million years before they roll over (take that 32-bit nix timestamps :) ).


---
## Atari TOS:

Atari TOS is the source of our binary format, as the binary format is very simple and easy to work with.  The VDI was also of huge inspiration in the implementation of the GRAPHICS.LIBRARY of YASDOE.


---
## Atari MiNT:

Atari MiNT is the inspiration for some of the API, as well as for the method of multiple file system support.  In MiNT they are called File System Translaters, in YASDOE they are called FS Libraries.  The functional concept is nearly identical.

MiNT shows a wrapper API to allow easing porting some applications from other platforms, especially from unix like platforms.  As such a lot of the API for the NIXISH.LIBRARY of YASDOE was inspired by MiNT.

There are also a few things about how some things have been done in MiNT that show us things that are very slow.  This has improved in newer versions of MiNT, though the lessons still stand.  This is also part of the reason for the MiNT divide among Atarians.


---
## RISC OS:

From RISC OS we get the inspiration for the optional Application Directories.  In RISC OS these are done by indicating a pling, in YASDOE it is a property stored in the directories **.info** file (so no limits on the name).  YASDOE prefers single file applications and files, though allows for the use of application-directories and file-resource-directories.

Also from RISC OS come some of the tricks of WindowManagement that make life just a little easier.

Then there is the support for dragging a files icon to a directory display window to specify where to save said file.  This also works for transfering files between applications, very much like it does in RISC OS.  It has been found that this is an easier way for a lot of users to realize where the file is really found in the mass storage device file system (as using standard file requesters often users do not note where they save things).

Also the way that RISC OS is specific about being able to revector many calls has been an inspiration to the universal vectorization abilities of YASDOE.


---
## X Windowing System:

The X Windowing System was an extradorinary accomplishment for its time and environment.  When people used a large computer from relitively small terminals and there was a need to display graphical applications running on the large system on there terminal, this was the day of X.  Though for running applications on your desktop computer (where everything including the display is on the same computer) X is terribly ineffecient, and much of the XLib and XCB API is designed around the needs of remote displays.

So we can learn what works well with remote displays is a terrible idea for a Desktop Computer.  This lessen is taken deaply in YASDOE. There is the beginings of an XLib, though it is only an API abstraction running directly on the local systems Windowing System.


---
## X-GUI

While no features of X-GUI were used in YASDOE (beyond those shared with other Windowing Systems), X-GUI was still an inspiration.  The inspiration being the fact that a very complete Windowing System can be written in a very high level BASIC in fairly little code.  It shows an effeciency of design that is rare to see.


---
## Ancient Unix:

The Unix Philosophy in its pure form has guided a lot of the creation of YASDOE.  Even though YASDOE is very far from being an Unix like system, the Unix Philosophy is still a great thing in most ways.


---
## Zerro-GUI:

Zerro-GUI was a series of toy GUIs I wrote in the early 1990s to learn the concepts of implementing a complete Windowing System.  There were a few versions from the view of how Window Management was handled, so I could learn as much as possible.  This project is what taught me the core concepts of most forms of Window Managemet (including 'Compositing Window Management' even though we did not yet use that term).

As these systems were my first Window Managers of any kind (I was stil quite young), they have had an influence on most things I have created.


---
## ProDOS:

From ProDOS we get the directory format.  Instead of using a single tree like Unix we use a forest, though the volumes and devices are all under the highest level / .  The format being a slash followed by the device followed by any FS path (on FS devices) with directories sepperated by slashes.  This is a simple format to work with, as well as to implement.  This format also simplifies porting of applications from a verity of different OS's that use different means of seperating directories, use different roots (some a forest some a single tree), and use different seperatere for device specs.


---
## PlayerKit:

PlayerKit was an early example of a software Sprite Engine for 8-bit personal computers (specifically the Apple II).  For sprite masking it used line cliping, using inversion point offsets to define an area that could be non-continouse.  This was very convient for sprites, though even more useful in windowing systems later.


---
## Macintosh System Software:

The Macintosh System software, despite it's limitations, has some very good concepts on how to do many things.  From the use of handles in application local memory management to help preven application heap memory fragmentation, on to some of the graphics primitives, and continuing into the use of resource forks.  These were all good features, and to a degree all features of YASDOE as a result.

YASDOE is able to optionally store the information normally in the **.info** file of an application in a secondary data stream (fork) of the file.  YASDOE also has a structured set of different data-types that can be in this information, allowing easy OS managed access to the resources.

The Compression of line based inversion point clipping that QuickDraw taught us (and is finally out of pattent) is a very good way to improve the speed of arbitrary shaped possibly non-continous clipping, as well as saving memory.  And YASDOE uses this compression for its ClipAreas.

Memory allocation is recommended to be done by handle.  This allows YASDOE to defragment the memory within a given applications heap.  YASDOE takes it a step further by further by allowing the movement of the application blocks, so long as the code obeys the rules of being position independant and using the App base pointer provided by the OS, thus making the application heap effectively a handle allocation that can be itself moved in memory.  This also allows for the possibiliity of a version of yasdoe that does not have a PMMU without having issues with memory fragmentation.  There is of course provision for applications that are unable to change there base address once running, though these can still cause memory fragmentation.
