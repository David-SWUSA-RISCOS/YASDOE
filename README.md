# YASDOE

![alt text](https://github.com/David-SWUSA-RISCOS/YASDOE/raw/main/docs/gifs/logo.gif "YASDOE Logo")

YASDOE (Yet Another Simple Desktop Operating Environment) a Simple  680x0 Operating System, decended from GraFaDOE.

There is some consideration being given to a future PowerPC layer, though this is unlikely to be seen in the near future.

For docs see: [YASDOE Home](https://github.com/David-SWUSA-RISCOS/YASDOE/wiki)

For news on YASDOE see: [YASDOE News:](https://github.com/David-SWUSA-RISCOS/YASDOE/blob/main/docs/md/news.md)

Imagine an Operating Environment designed from the ground up to be small, fast, responsive, and radically simple.  Not just simple in its function, also simple to program for and to use.  At its core it is a Macintosh System Software Clone written from the ground up by one person as a side project over 10 years in responce to the descusions around the Raspberry Pi SBC in 2012 / 2013.

For further information see the YASDOE Wiki HOME:
[YASDOE Home](https://github.com/David-SWUSA-RISCOS/YASDOE/wiki)

Note:  Until enough is up to have a fully documented OS, I have decided to use the Web Interface to update the github repo.  And I will continue to use the web interface as the github repo is by need documentation primarily.

This Repo will end up having archives of the source code, that can not be extracted to the github, as much of the source has resource forks.

## YFS NOTE:

YFS (the native FileSystem for Yasdoe) is much more capable than HFS+ in some ways, though much more limited in one way.  While you can have billions of files on huge drives, you can only have 65536 different types of file.  This is a known limit of YFS that does not have an easy solution without breaking the FS for programs that rely on its current structure (such as the system software of YASDOE).
