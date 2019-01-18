[Previous Chapter](../Ch02-filesystemtreelayout/notes_Ch02.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch04-signals/notes_Ch04.md)

---

# Chapter 3 Processes - Notes

## 3.3 Learning Objectives:
- Describe a process and the resources associated with it.
- Describe the role of the **init** process.
- Distinguish between processes, programs, and threads.
- Understand process attributes, permissions, and states, and know how to control limits.
- Explain the difference between running in user and kernel modes.
- Describe the **daemon** processes.
- Understand how new processes are forked (created).
- Use **nice** and **renice** to set and modify priorities.
- Understand how shared and static libraries are used.


## 3.4 Processes, Programs, and Threads
**Process**: executing program and associated resources, including environment, open files, signal handlers, etc. Same program may be executing more than once simultaneously -> responsible for multiple processes.

Two or more tasks (threads of execution) can share various resources (eg. entire memory spaces or particular memory areas, open files, etc.). When **everything shared** circumstance -> **multi-threaded** process.

Other OS -> distinction between full **heavy weight** and **light weight** processes. Heavy weight process may include number of light weight processes, or just one.

Linux -> different situation. Each thread of execution considered individually, difference between heavy and light -> sharing of resources, somewhat faster context switching between threads of execution.

Linux -> fast job of creating, destroying, switching between processes (unlike other OS) -> model adopted for multi-threaded application resembles multiple processes: each thread scheduled individually and normally (like stand-alone process). Done instead of involving more levels of complication (eg. having separate method of scheduling along threads of process, having scheduling method between different processes).

Linux -> also respects POSIX and other standards for multi-threaded processes, eg. each thread returns same process ID (called thread group ID internally) while returning distinct thread ID (called process ID internally). May lead to confusion for developers, invisible to administrators.


## 3.5 The init Process
First user process on system -> **init**, has **process ID = 1**. Started as soon as kernel initialized + root filesystem mounted.

Runs until system shut down -> last user process to be terminated. Serves as ancestral parent of all other user processes, both directly/indirectly.


## 3.6 Processes
Process -> instance of program in execution. Number of different states (eg. running, sleeping). Every process has **pid** (Process ID), **ppid** (Parent Process ID), **pgid** (Process Group ID); also has program code, data, variables, file descriptors, environment.

**init**: first user process run on system, becomes ancestor of all subsequent processes running on system (except for those initiated directly from kernel, show up with **[]** around name in **ps** listing).

If parent process dies before child -> **ppid** of child set to 1 (ie. process id adopted by **init**). (Note: in recent Linux systems using systemd, **ppid** set to 2, corresponding to internal kernel thread **kthreadd** that has taken over role of adopter of orphaned children from **init**).

**zombie** (or defunct) process: child process which terminated (either normally/abnormally) before parent that has not waited for it and examined its exit code. Releases almost all resources and remains only to convey exit status. Checking on adopted children + let terminated process die gracefully -> one function of **init** process -> sometimes known as **zombie killer**, or **child reaper** (yeesh).

Processes controlled by **scheduling** (completely preemptive). Only kernel has right to preempt process, processes cannot do it to each other.

Largest **PID** limited to 16-bit number, 32768, for historical reasons. Possible to alter this value by changing `/proc/sys/kernel/pid_max`, since may be inadequate for larger servers. As processes created, will eventually reach **pid_max**, and then will start again at **PID = 300**.


## 3.7


## 3.8


## 3.9


## 3.10


## 3.11


## 3.12


## 3.13


## 3.14


## 3.15


## 3.16


## 3.17


## 3.18


## 3.19


## 3.20


## 3.21


## 3.22


## 3.23

[Back to top](#)

---

[Previous Chapter](../Ch02-filesystemtreelayout/notes_Ch02.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch04-signals/notes_Ch04.md)
