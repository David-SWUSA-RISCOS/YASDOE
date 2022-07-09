# Inspiration For YASDOE:

***
THIS PAGE BEING UPDATED
***

The two things that got the project now known as YASDOE going back in 2012 were the potential challenge (with a new ARM based computer coming out) and the chance to show that preemptive multitasking can be very effecient (traditionally Cooperative Multitasking has shown more effecient).  By nature there is the inspiration that comes from the Operating Systems that the author has studdied over time.

## The Multitasking Question:

The argument of which is better, cooperative multitasking or Preemptive multitasking will go on forever.  No attempt is made to enter this argument here, as both have there advantages (even when combined with AMP or SMP for multiple CPU Cores).

Part of the goal of YASDOE is to show that Preemptive multitasking can be accomplished with nearly as little Overhead a Cooperative multitasking (though for obvious reasons never completely as little overhead).  We also wish to show the advantages of cooperative multitasking, which are more than most seem to realize (especially now that Preemptive Multitasking is so wide spread).

As such there is YASDOE, then there is SiBDOE.  These two Operating Systems contain a lot of shared code (around 98% shared code, give or take) and provide identical API and ABI with one another.  The only real difference is the multitasking model, with YASDOE being primarily Preemptive and SiBDOE being primarily Cooperative (with the ability to preempt an errant task).  Originally I was going to call both the same name with the difference noted, though decided that the multitasking model is enough to require a difference in naming and distributing.

## From Other Projects:

Herein we will look at the giants from which we may learn, and have had the most direct impact on the development of YASDOE.

Some of the low level inspiration for YASDOE comes from:

* Atari TOS:
* [Amiga OS:](http://wiki.amiga.org/index.php?title=Main_Page)
* [RISC OS:](https://www.riscosopen.org/content/)
* [Ancient Unix:](https://minnie.tuhs.org/UnixTree/)
* Zerro-GUI:
* PlayerKit:
* [Macintosh System Software:](https://main.system7today.com/)


---
### Atari TOS:

From Atari TOS we learn that any system can be cloned, or even just partially cloned.  Look at the number of GEMDOS replacements, VDI replacements, AES replacements, Whole TOS Replacements.

From TOS we also learn that anything can be done better if third parties put in the effort to so do.

Replacement parts of Atari TOS also reinforce the lesson that for desktop computing Cooperative Multitasking is usually a better option than Preemptive.  When SiBDOE (Simple & BASIC Desktop Operating Environment) gets anounced this will be made more clear, as it is the Cooperative Multitasking counterpart to YASDOE, and shares a lot of code with YASDOE.



---
### Amiga OS:

From Amiga OS we learn a lot.  This includes ways to keep things very simple while improving capabilities.

We also learn from the means of callbacks to deliver events to WIMP Icons (or as Amiga OS words it, delever events to Widgets).

Amiga OS provides the inspiration from BOOPSI, a simple means of OO that can be used in most procedural languages (no OO language needed).



---
### RISC OS:

This is the Operating System that has likely had the most effect on YASDOE of any of them.  From RISC OS come many ideas including:

* Universal Interapplication Drag & Drop (used for Inter App Communication).
* Simple events.
* Software Inturrupts for system calls.
* Revectoring just about everything.
* Leave the Menu Bar Argument to the uninformed, we use pop up application menus.
* No Standard File Package of any kind, instead save and load are a drag (and drop).
* File Systems of any kind, including Image File Systems.
* Modularity (though we take it further than RISC OS does).

Also an inverse argument is taken of RISC OS.  Part of the intent of YASDOE being a Preemptive Multitasking Environment is to help prove that for Desktop Computing it can be better to use Cooperative Multitasking.  And yes this does mean that YASDOE has an unanounced sister project (SiBDOE) that is Cooperative Multitasking in nature.  It is hoped that YASDOE is useful for a Preemptive multitasking system, though her sister SiBDOE is one to look at as well.



---
### Ancient Unix:

From the very early editions of Unix, though mostly the Unix Philosophy (that has been lost to most modern nix systems).

The Unix philosophy modified to a form that fits even with Graphical GUI based Multitasking applications is very much a core idealogy of YASDOE (and every other OS project that I have had control of).  That is the concept of keeping each application simple, and passing data between applications under the control of the user and/or of part of the data to perform more complex tasks by combining the function of multiple simple applications.

I truely whish modern systems would remember this philosophy.  Not to mention the creaters of standards (well they tend to be large orginizations that wish to push there products anymore, so maybe the problem is the source of the standards).  Anyone that has looked at the HTML5 standard will understand what is meant herein, it is huge without providing much actual new useful functionality (and most of what it does add is for stuff that does not belong in a web page (they want to turn web pages into applications, this is a very bad concept)).



---
### Zerro-GUI:

Zerro-GUI was the authors first ever homebrew GUI, that was more than 20 years before I started working on YASDOE.  Zerro-GUI was rewritten a few times to experiment with different methods of clipping, managing overlapping windows, cooperative Multitasking, etc.

The contribution that was made from Zerro-GUI is that what was learned from the project has had an influence on the authors thinking when working with 2D graphics on any level.



---
### PlayerKit:

Player kit is a programmers toolkit for dynamic Sprite type objects (called Player Objects in the kit) that uses inversion point line clipping to mask the sprite images.  This was for the Apple II series and initially released in 1979 as far as I can tell (may be older, though definitely the last version I can find is from late 1979, earliest I can find is from early 1979).

Player kit uses a data structure for its clipping that is fairly simple.  First are 2 bytes that define a rectangle size (up to 128 by 128), then there is an array of bytes that has for each line first the number of inversion points, then the one byte for each inversion point in number of pixels right of the left bounds of the rectangle, there is no special terminator as the number of lines is known.  The current on screen position is kept seperately from the mask and seperately from the pixel image as well.  The pixel image is kept seperately, and a single mask may be used for multiple pixel images.

The way that operations on line clipped Objects was a huge inspiration for the Region Operations of YASDOE.  This works out as Regions are a bit more advanced form of inversion point line clipping.



---
### Macintosh System Software:

From here we have a few concepts.  The most important being the concept of Regions.

The concept of resources by locality comes to us from here as well.  While there are significant differences in the details of implementation on YASDOE the concept is none the less from this great 68K OS.

Regions as used for clipping adds to the speed of the WIMP in YASDOE in ways beyond what one may expect.

Using a form of software inturrupt call that allows for each call to specify the system call intended in the instruction comes to us from this system indirectly.  As RISC OS implements this we get it directly from RISC OS, though we know that the designers of RISC OS were familiar with this concept from the Macintosh System Software, and thus it is likely that they got it from here.

Indirectly we get some language help.  It was in part Apple that evolved the Object Pascal method that has been used in Macintosh based Pascal Compilers as well as some for other platforms (like later versions of TurboPascal on Free/MS/PC/DR-DOS.
