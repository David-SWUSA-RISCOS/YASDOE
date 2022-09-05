# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

PLEASE SEE: [The YASDOE Documents](./docs/README.md) For more information.

**NOTE:**
The author has been rewriting small parts of YASDOE in a compiled subset of BASIC V as appropriate while documenting the function.

YASDOE is going to be primarily hosted on another site.  The author may end up uploading the archives here as well, though that is to be seen, there are difficulties with using git for files that are typed in nature, and some of which have multiple forks.  Most of the documentation takes advantage of forked files, using the resource fork for formatting information (in a format that is viewable in the **ED** program in YASDOE as well as in **Teach** on GS/OS (after a simple conversion)).

The Author will continue to convert some parts of the documentation to markdown for viewing here, though this will only be small parts of the documentation.

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple [ARM](./docs/WhatIsARM.md), and 680x0 Operating System.

As the athour works on YASDOE it makes the author like RISC OS even more.  The reason there is an RISC OS hosted version of YASDOE.

The author will continue to document, debug and upload (binaries and sources) YASDOE material.   It already does exist so it is sensible to so do.

To note there is one major bug in the current version that is being looked into.  That bug is that the core OS image is 135KB in size, and the mapping expects less than 128KB, so the image needs cut back a little bit in size.  This has not yet caused an issue as the os usage heap grows downwards, and so far has yet to reach close enough to its limits to cause an issue, though it easily could under some conditiions.
