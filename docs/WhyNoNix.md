## Why not a nix like system:

Many Operating systems pride themselves in being Unix like or POSIX like, or at least in having some layer that is like these.  YASDOE will never be one of these.  These are antiquated systems at best, and bloated systems at worse.

Do not get me wrong, there is a lot of positive to be learned from Unix and those systems that are modeled after Unix to verying degrees.  Some of these are great systems in there time (1970's and 1980's).  Though most have since fallen into what the real Unix tried to get away from, overly complex core systems running overly complex software, the very antithis of what Unix once was.

As such there is not today a good reason to support POSIX like calls, nor to support any software that targets Unix and/or PSOIX systems and similar today.  The software that targets these systems that one may think about porting is in general way too bloated to be worthwhile, often so complex that the maintainers allow what should be crittical errors to persist in 'Production' quality releases (such as memory leaks, bad pointers, etc).

Software that is worth porting will be simple enough to retarget by using only native system calls in place of the nix based system calls.  Remember porting **is not** bringing over a bunch of libraries to support a foriegn API, porting is bringing the application or other items to port to the native API of the OS.

The only cross platform libraries that make sense are OpenGL, and maybe one or two others that are on the same level as that.  Other API libraries are just needless additions to the levels of inderection (in programming most problems can be solved by adding more levels of indirection **except for too many levels of inderection**, in other words **do not add** unneeded levels of indirection).

Thus to provide support for anything Unix / POSIX like is counter productive and a step backwards.  Can not be too surprised, as Unix is an Antiquated system that has been pulled along against all odds into the modern clones thereof.  The clones of Unix like systems are bar none the single most antiquated and mutalated series of systems still in use today.
