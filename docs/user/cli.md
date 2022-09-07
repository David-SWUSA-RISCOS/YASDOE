The default CLI of yasdoe is provided by COMMAND.PRG, and uses the backslash as the directory seperator.  If you are familiar with Atari TOS and the Atari distributed version of COMMAND.PRG then you are off to a good start.   If not you may be familiar with DR-DOS, or PC-DOS, which use a very similar CLI.

At the CLI volumes are usually refered to by there volume letter assignment, though may be accessed by there volume name, in either case the volume name or letter is folowed by a colon character.  Thus the drive having drive letter **C** is refered to as '**C:**' without the quotes.  The default boot volume is assigned to volume **C:** unless it is a floppy type device in which case it is assigned to drive **A:**, this is regardless of the name of the volume.

Each drive has a **CWD** (Current Working Directory) which is the working directory for commands in that drive.

File and directory names may be up to 32-characters long, and can not contain any of the characters inside the following braces { " : \ / , * ? | > < ! } though may contain spaces.  Any valid typable PETSCII character is allowed in filenames, and language may be selected on a per file bases for extended character interpretation (though extended graphics characters are lost for some languages).

Any command line entered must be less than 511 characters in length.

Supported Commands builtin to the CLI include:
* ASSIGN
* BREAK
* CALL
* CD
* CHDIR
* CLS
* COPY
* DEL
* DIR
* ECHO
* ERASE
* EXEC
* EXIT
* FOR
* GOTO
* IF
* MD
* MKDIR
* PATH
* PAUSE
* PROMPT
* RD
* REM
* RENAME
* RMDIR
* RUN
* SET
* SHIFT
* STATP
* TIME
* TRUENAME
* TYPE
* VER
* VOL
