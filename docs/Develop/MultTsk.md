[Return to Programming Contents:](./Index.md)


# Multitasking Overview:

YASDOE allows for a maximum of 256 total tasks, including 4 that are always allocated as part of the OS.  One of which is never in a queue, this being the Idle Task, as it does not obey the rules beings it is only given time if the *Active Queue* is empty.



---
## Task Scheduling:

Task scheduling is very simple in YASDOE, using the nature of cooperative multitasking in a preemptive multitasking system.  If more than one task is currently in the active queue (more rare than you likely think) then the TaskManager performs normal preemptive switching 60 times per second in round robin fashion on the active queue, otherwise the current task is kept in.

There are 4 task queues:
* **Active Queue** : Contains tasks currently active.
* **Event Wait Queue** : Contains tasks waiting for an event.
* **Time Wait Queue** : Contains tasks waiting to wake on a specific time, this queue is kept sorted by time remaining, with least time remaining at the head of the list.
* **Back Wait Queue** : Contains tasks waiting for a background system task that is blocking to that task.

A task may be moved to the **Event Wait Queue** by calling **Task:EventWait**.  If a non-zero time is specified said task is also moved to the **Time Wait Queue**.  A task is also moved to the **Event Wait Queue** when it sends a message, in order for all tasks interested to be able to see the message before it makes it back to the sending task.  There are also some Window Manager calls that can cause a task to go to the **Event Wait queue** such as **WIMP:Poll** and **WIMP:PollIdle** , in the case of the likes of **WIMP:PollIdle** the task is also put into the **Time Wait Queue**

When a task makes a blocking system call that may take some time it may end up in the **Back Wait Queue** while the call spawns a task of its own to handle the call asynchronously to other tasks.  In some cases part of the time in the **Back Wait Queue** may be to a call having to complete from other tasks before handling the request of the most recent caller (so there can be multiple levels of blocking).

A task is moved from the **Back Wait Queue** to the **Active Queue** when it is no longer blocked.

A task is moved from the **Event Wait Queue** to the **Active Queue** when it has an event to process.

A task is moved from the **Time Wait Queue** to the **Active Queue** when its time to go active has passed (or is present).



---
## Task Preemption:

The TaskManager performs a task switch 60 times per second normally (using the vertical retrace interrupt (vblank)).  Task switching is disabled in the case of being in a non-reentrant library or component.

If there is a task other than the current task in the active queue when the vblank timer calls the TaskManager a task switch is performed, allowing the other task time to run.

Some system calls are able to start a background task to perform there operation, while blocking only the task that expects the call to block.  This is done by calling the library function BackProcess of the TaskManager's library interface, with the call specifying the task handle to block until done.

In the case of the **Active Queue** being empty the TaskManager will run the task with TaskHandle 0, which is never in a queue and is the Idle task.  Where supported by the CPU the idle task uses a wait type instruction to reduce CPU usage (supported on ARMv4 and newer, also on some 68K CPU's).

A preemptive task switch still has all the overhead of a cooperative task switch.  As such there is a call to set longer timeslices than the normal one vblank, to improve performance.  The star call **TaskTimeSlice** passed single nibble parameter is used to configure the number of vblanks per time slice, from 1 through 15, a value of 0 degrades to purely cooperative multitasking.


---

## Multiple CPU Cores:

NOT TESTED AT THIS TIME (had been tested in the past, do not currently have multi Core system to test on).

-The only two differences needed with multiple CPU usage are that each task is allocated to the core that has spent the most time in the Idle queue over the last 120 vblanks. This gives a level of balance when multiple tasks are running with a lot of active time, and can speed up some workloads- .

There are also the consideration of things like callbacks setup by a task that must be catered for with multiple tasks running at the same time on separate CPU's, something that is not as much an issue in cooperative multitasking on one CPU.



---
## Starting a New Task:

............