# YASDOE Documentation:

**YASDOE** (**Y**et **A**nother **S**imple **D**esktop **O**perating **E**nvironment) is a simple ARM and M68K Operating system that is heavily influenced by RISC OS.

Some new features in YASDOE include the use of regions, support for resource forks instead of application dirrectories (application directories are still supported), and some other small things to improve the user experience.  YASDOE also provides an alternative library based calling mechinism toreduce the latancy of some system calls (those that can be executed in User Mode directly).

The Multitasking model is updated.  It is a hybrid between normal Preemptive Multitasking and Cooperative Multitasking.

* [Developer Documentation](./Develop/Index.md)
* [User Documentation](./user/README.md)
