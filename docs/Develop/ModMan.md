[Return to Programming Contents:](./Index)


---
#. The ModuleManager:

This is in part just a simple module loader, and in part a bit more.  The module manager provides easy means of dynamic (load time) SWI chunk allocation, thus providing a means to prevent conflicts without relying on any central authority of any kind.

The extended function of the module manager began as a project for RISC OS that unfortunately only caught on among a small group of RISC OS users in the United States of America.

The core of the ModuleManager is a simple Module loading, and managing system very much like the one in RISC OS.  There are some small differences, though from a programmers view writing modules the two are the same.