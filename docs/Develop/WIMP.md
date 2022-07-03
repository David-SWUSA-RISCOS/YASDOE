[Return To Programming Documentation Contents](./Index.md)

This page is still a Work In Progress (WIP).  It will take a little time to complete as this is a large component of the OS.

# The Window Manager (WIMP Library):

The YASDOE Window Manager (WIMP) is unique in many ways.  Based on familiar API's that are simple to use, and providing abilities that are beyond any of those that inspired YASDOE.

At the core the YASDOE WIMP is modeled after its namesake in the ARM OS well known (RISC OS).  This gives us a head start as it were, as many programmers are already familiar with the API despite the ABI differing a little.  The reason for this is that this is one of the two Windowing Systems with which I am most familiar, and thus it was natural to use this model.  There are some differences though, all of which are improvements and do not prevent direct ports of many programs.

Events are delivered to applications in one of two ways.  The preferred method of getting events for an application is to setup callback handlers (like signal handlers) for the Window Manager to call when an event is to be delivered.  The alternative method is to call either the Poll or PollIdle functions of the Window Manager in the way cooperative multitasking programs do, also how most programs for other preemptive systems (X11, Win32, macOS, etc) deliver events.  The two methods are provided so that no matter which a programmer is familiar with it is easy to work with, this also simplifies life when porting windowing applications from other systems.

Clipping is handled in a transparent manner using regions.  This is the most efficient means to implement clipping on most systems, and can easily be accelerated.  Yet there are calls provided for traditional rectangle list clipping, that play some tricks to make the program think it has the full window area to draw to even if partly covered, and region clipping is done behind its back.  This allows again for fast efficient operation of programs regardless of the method that the programmer is familiar with, as well as simplifying life when porting from other Windowing Systems.

Our Windowing system has more tricks up its sleeve, as it also provides some extremely simplified API's for many things, modeled largely after the GUI commands of *AmigaBASIC* and *A/C BASIC* .  This provides for a simplified API for many programs to use in implementation.

In sum the Windowing System should be easy for any programmer to work with, including when porting applications.  For most applications it is extremely unlikely that they can zombie out (so long as they are using callbacks for event handling).

In this document we will cover programming for the YASDOE WIMP in detail, with sections divided by topics covered.  User documentation is for another document.