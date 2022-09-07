[Back to Programming Documentation Index](./Index.md)

# CoreDOS:

Core DOS is the component of YASDOE that provides for device access, and filesystem support.  In this case the DOS part can be looked at as meaning Device Operating System.  Though it should be noted only some devices are handled by this component, that is devices that make sense to allow this kind of access (Serial ports, Mass Storage devices, etc), devices that do not make sense are not included (no support for the display or MMU for example).



---
## Overview of CorDOS:

CoreDOS provides the services for file operations, that in combination with a filesystem provide the means to work on files (and devices in the case of the DeviceFS).

Large file operations are only blocking to the task that calls for them, other tasks will continue to get time while a large file operation is in progress.  This is done by keeping a queue (so that file operations that are requested while others are in progress do not mess things up), and performing file operations in the background of all but the calling task.  This is one thing that is surprising was not done by the other good ARM based computer OS, as it is fairly simple to implement even on a purely cooperative multitasking system.



---
## FileSystem Support:

FileSystems are separate from the core.  The primary FileSystems that are included by default with YASDOE are FFS, ADFS, YFS, and DeviceFS.  The first three of these are standard storage device FileSystems with the last being what it's name implies.

In the RISC OS hosted version of YASDOE, which is the primary version, the boot YFS file system is in a volume image (disk image if you will) file.



---
## Extending CoreDOS
