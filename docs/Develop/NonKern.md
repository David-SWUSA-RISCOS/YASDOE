RETURN TO: [Programming Contents](./Index.md)


**No more MicroKernel**.  I managed to get a clean compile of a working system that breaks up the functionality of the microkernel into smaller Libraries, that are able to simultaneously host some of the normal OS  calls with the same code thus simplifying the system, and improving the system by simplifying it.  There is no longer any single component that you could point at and say that is the kernel.

Originally the core system was based on a MicroKernel in the true sense, now this has been simplified greatly to instead be a series of even more simple modules that provide functionality of the lowest level operations.  This page persists as it is already referenced by too many other pages to remove the page.  As such this page quickly goes over the modules that make up the low level functionality that would be expected from a MicroKernel.

**BACK TO ORIGINAL** : The API has been reverted to that of the originally planned release, so the divisions of this page are to change.  No more worrying about secondary API's having a low level influence.



## The OS Level Modules:

The Modules that provide extended low level function, at an OS level include:

| Module             | Description                 |
|:-------------------|-----------------------------|
| **MemoryManager**  |Provides the Memory Management calls, including mapping, allocation management, Dynamic Areas, etc. |
| **ModuleManager** | The core of controlling loading and setting up modules, an alternative to libraries. |
| **LibManager**    | This OS module provides support for all other libraries.
| **ListManager**   | The System wide extensible list type is managed by this module. |
| **TaskManager**   | Preemptive Multitasking, Task Queue management, and such things. |
| **CallBack**      | Call to task type signal callbacks.
| **VectorManager** | Manages all Vectors of all types. |
| **ServiceMan**    | Manages allocation and dispatching of services. |
| **Clock**         | Manages clock/timer interrupts.  |


---
## ModuleManager:

The ModuleManager is responsible for initializing modules, allocating there memory requests, and other tasks directly related to modules.  This includes allocating the SWI chunks if present.  As both are possible with the current YASDOE codebase I am debating if the core should be built from libraries or from modules, and if SWI calling should be the primary  means of system calling (the decision comes down to which version of three source files for SWI and Module core, or replacing those three with twelve source files for the library call core setup).

Do to simplicity and maintainability I am very likely to release the Module based version, potentially with a module to add library support as needed.


---
## LibManager:

The library provides manages getting libraries usable as well as accessing libraries.  This is a component of the OS that could in some ways be viewed as among the lowest level, as it starts all but one of the other libraries (the exception being the ListManager, as the Library Manager uses it so it has to be in a usable state without the services of the library manager).

**ALL LIBRARIES** :

The following assumes that we keep with the library direct call method of making system calls.  It is likely that the following will always apply to some extensions though there is a strong pull to release the simpler low level component of using SWI calls for most system calls.  Otherwise this component will be higher level, and the low level will be a module manager.

All libraries have certain functions needed for housekeeping and keeping everything clean and separate in runtime.  These are the first 8 functions of the library:

| FUNCTION      |       DESCRIPTION                                                           |
|:-------------:|-----------------------------------------------------------------------------|
| **BootInit**  | Called at system boot, or when the library is first loaded.                 |
| **StartUp**   | Called by a program to initialize the library for the task before using it. |
| **ShutDown**  | Called to close the library when a program is done using it.                |
| **Version**   | Returns the current version of the library.                                 |
| **Reset**     | Called on system reset if library stays persistant.                         |
| **Status**    | Get the current status of the library.                                      |
| **GetBase**   | Get the base address of the libraries call table.                           |
| **Reserved**  | This function reserved for future use.                                      |

---
## ListManager:

Many parts of the OS rely on lists, a consistent way of managing lists is provided by the ListManager.


---
## TaskManager:

The TaskManager deals with all levels of Multitasking in YASDOE.


---
## CallBack:

CallBack Library provides support for easing implementing of callback type work, such as events passed as part of the WM thread to applications, and similar.

---
## VectorManager:

The VectorManager provides all the calls related to managing the OS vectors, CPU vectors,  etc.


---
## FakeKernel:

This library exists to allow kernel related calls through a single library.  That said all it does is to call out to the correct libraries to handle the actual work.