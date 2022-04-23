# YASDOE Documentation.

Welcome to the markdown version of the YASDOE Documentation.

The documentation will at all times be ahead of the source and any binary releases.  This is because making sure that everything is extrememly documented is one of the main goals of YASDOE.  Any time any source is added it must first be fully documented in this section.  As such there will be information about source that is not yet present.

This will be the primary slow down in the rate at which code is added to this repo.  This is do to the fact that I wrote a large amount of documentation, and messed up most of it do to not testing viewability, so am having to redo a large portion of the documentation.  As I verify that each document is good it will be added to the repo.

The contents (Note listed items will become links as actual files added to documentation):

note: the contents is far from complete.  I had to recreate this page from scratch.  I will be improving it as I add documentation.

* [The Direct Inspiration of YASDOE.](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/inspire.md)

## User Documentation:

* Getting Started With YASDOE .
* Using the Windowing System, more power.
* Working with files in the Windowing System.
* The CLI, a powerful interface.
* More on files.
* Devices.
* Configuring your YASDOE system for your preferences.
* Power User information.
* Adding devices, libraries and other extensions.
* The startup sequence, and power user configuration.
* Getting Started With YASBasic, a powerful little programming language.

## Applicaiton Developer Documentation:

* The structure of YASDOE, a bit different, while remaining simple.
* Getting Started Writing Applications for YASDOE.
* Making use of Libraries.
* TRAP Calls.
* The main Libraries.
* The Kernel is quite Powerful (SYS.LIBRARY).
* Getting to know the Device and File Library (DOS.LIBRARY).
* Using the Graphics Library (GRAPHICS.LIBRARY)
* Working with the WindowManager (WIN.LIBRARY).
* Text Styles (FONT.LIBRARY).
* Writing CLI based programs.
* Notes on Memory Management.
* Writing Libraries.

## Driver Developer Documentation:
_the application developer documentation is a prerequesit of this section_

* Writing Device Drivers, the basics.
* When you need inturrupts.
* More advanced Driver Development.

## Detailed OS Documentation:
_each of the following leads to a topic specific contents, as each is a very large multi-page document_

_this section is the least complete_

* [ARM Hosted 680x0 Emulation Layer](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/68kemu/arm68kemu.md)
* [The 680x0 Emulation RO Hosted Version).](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/68kemu/emurohost.md)
* The 680x0 Emulation Layer for ARM Host Systems (Native boot verison).
* The Structure of YASDOE in detail.  Not as you may expect, better, simpler.
* The Kernel (SYS.LIBRARY), Very little to do a lot.
* The DOS.LIBRARY (Device Operating Systems, also handles File Systems).
* FileSystem libraries for use with DOS.LIBRARY.
* The Graphics Library (GRAPHICS.LIBRARY).
* Font Library (FONT.LIBRARY)
* The WindowManager (WIN.LIBRARY).
* The Application Library (APP.LIBRARY).
