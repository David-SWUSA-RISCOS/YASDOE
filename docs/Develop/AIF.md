[Back to Programming Documentation Index](./Index.md)

**KISS :** For simplicity it is unlikely to support hunks, as this adds to the codebase and increases the opportunity for a bug to sneak in.  Sp it is realized that to KISS it is better to stick to AIF and module like formats.

With AIF format it is possible to support multiple CPU's by cheating a little, though only one CPU per executable code file.


---
## AIF Support:

An AIF is a flat binary with an executable header.  We take advantage of the flags field of the header (after the final defined branch) to define not only if it is 26-bit ARM or 32-bit ARM, though also if it is little endian or big endian (easy, just look at the byte with the value) as well as if it is 24-bit 68K or 32-bit 68K.  To distinguish a YASDOE executable from a RISC OS equivalent we set bit 8 of the flags word to one (always 0 in RISC OS AIFs).  The 65816 code places the value &0000010F in the flag word, is always little endian, and usually reuses the 64bytes of space taken by the header for runtime data storage space.

In an AIF the flags word is at offset &30 and is used to determine the addressing mode in RISC OS AIF files.  We also use it to determine the addressing mode, as well as the target platform.

For ARM based YASDOE AIFs we have the flag word equal to &000000120 for 32-bit PC clean and &00000011A if only runs with a 26 bit effective PC (actually 24 bits though word aligned so effectively a 26 bit byte address range) with combined Status Word.  It should be noted that on CPU's that support such access to 32-bit address space for data is possible with the PC range stuck to the 26-bit (64MB) address range.

For the 68K values we simply have the high bit of the low byte set, and OR that with either 24 or 32 (thus the value is either &98 or &A0).  Thus the word value for 68K is big endian &00000198 for 24-bit address space only, or &000001A0 for 320bit address space compatible (should run in 24-bit still, or check at start in case it can not).

RISC OS AIF programs are supported so long as they do not need anything RISC OS Specific (except for what matches in YASDOE).  RISC OS AIFs follow the same rule as they do in RISC OS, which is to say there flag word is set to &00000020 if they are 32-bit clean and to either &00000000 or &0000001A if they require a 26-bit PC with combined status word.  AIF formats that do not have a status word, or non-AIF flat binaries are not yet supported, though may be supported in a future version of YASDOE.

The header of an AIF takes the form:

| OFFSET  |  WHAT  |
|:-------:|-------------------------------------
| &00     | Branch to decompress code, NOP if not compressed. |
| &04     | branch to Self relocation code, NOP if not self relocating. |
| &08     | Branch to zero init code, NOP if none. |
| &0C     | Branch to entry point, required. |
| &10     | Fallback Exit Instruction in case of return (usually SWI &11 (SWI OS_Exit)). |
| &14     | Code section size, must be a multiple of 4. |
| &18     | Data section size, zero if no separate data section in file. |
| &1C     | Size of debug area. |
| &20     | Size of Zero Initialization. |
| &24     | Debug type. |
| &28     | Base address of AIF as a flat binary (usually &8000). |
| &2C     | Size of relocation workspace. |
| &30     | Address mode flags. |
| &34     | Base address for Data, or zero if no separate data section. |
| &38     | Reserved, not defined.  Should be 0. |
| &3C     | Reserved, not defined.  Should be 0. |
| &40     | Begin of debug init, outside of header. |
| &xx     | Zero Init code normally follows header if present. |

It goes without saying that we can determine byte order very easily in the flag word at offset &30 to determine if it is little endian data or big endian data.



---
## Normal Modules:

Modules must have the flag word.  For the most part they are the same as there equivalent on RISC OS with only small differences in the rules of usage.


---
## Library Modules:

Library modules are normal Modules that in there initialization code call the library module with a pointer to there library call table.  This makes it possible to mix a Library Module with a normal module in the same module.



---
## NOTES:

