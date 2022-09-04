[Return to Developer Doc Index](../Develop/Index.md)
[Return to User Doc Index](../user/README.md)

# YASDOE File Types

YASDOE uses filetypes stored as seperate metadata to the file in the filesystem.  Filetypes are 3-byte (24bit) unsigned little endian integers that specify the type of the file.

Filetypes that are defined in RISC OS are indicated by having the top 12-bits set to &FFF, and the low 12-bits as the normal RISC OS filetype.

If using ADFS as the filesystem the filetype in ADFS is as in RISC OS, unless it is a filetype that is not normally in RISC OS defined (one that uses the top 12 bits), in wich case it is given the file type &AF7 and the actual filetype is stored in a file in the directory named **.FileInfo**.  The **.FileInfo** file is also responsible for providing support for forked files in ADFS, and long file names in ADFS versions before long name support was added.

There is more locality available than in RISC OS.

## Local Filetypes:

By default filetypes in YASDOE are assigned to the normal global filetype and runtype variables.  Though it is possible to overide this locally to a subdirectory tree by using the **SUBTREE_SET** command to set the variable instead of the normal **SET** command.

It is also possible to open sub-directories in local only mode, thus causing changes in the tree to only  effect the sub tree made local.  This goes for filer windows as well as for star command ran scripts.  You can do a **DirLoc** command instead of **Dir** to change directories and have that SubTree be kept local for all variables set within until you leave that tree.  In the filer you can open a directory by menu clicking and selecting **Local_Open** from the menu, then any variables set by **Filer_Boot** or **Filer_Run** within those directories is local to the tree based at where you did a **Local_Open**.

## Filetype IconSprite:

IconSprites for application types are not stored gloably (as RISC OS does), though rather per directory.  This allows for applications of the same name to have different SpriteIcons in different directories.  Also if a non-default filetype IconSprite is already in effect gloably then when another application sets that IconSprite to something else it will only effect the files of that type in subdirectories of the directory where the change was made.
