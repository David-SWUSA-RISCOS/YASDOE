[Back to Programming Documentation Index](./Index.md)

# Calling Conventions:

The two primary calling conventions used throughout YASDOE are a managed library calling convention, that allows for easy re-vectoring of calls, and a SoftWare Interrupt calling convention.

h2. Software Interrupt calling.

The SoftWare Interrupt calling is accomplished by the SWI handler on the ARM CPU's, and by the A-Line trap handler on the 68K CPU's.

On the ARM CPU the rules are very much as in the main ARM OS.

## Library Vector Calling.

The Library call interface is provided by calling through a call vector with the library handle number (as returned by an OpenLibrary() call) in the middle 16-bits of R12, the function number in the low 8-bits of R12, and up to 8 parameters in R0-R7.  The library call vector will add the calling tasks byte ID to the high byte of R12, so the library can definitely identify the calling task number.  On returning the library function may place return values in R0-R7, and must preserve R8-R12.
