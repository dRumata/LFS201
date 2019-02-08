[Previous Chapter](../Ch14-io/notes_Ch14.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch16-linuxfsvfs/notes_Ch16.md)

---

# Chapter 15 I/O Scheduling - Notes

## 15.2 Introduction
System performance often depends very heavily on optimizing I/O scheduling strategy. Many (often competing) factors influence behavior, including minimizing hardware access times, avoiding wear/tear on storage media, ensuring data integrity, granting timely access to applications that need to do I/O, being able to prioritize important tasks. Linux offers variety of **I/O Schedulers** to choose from, each of which has tunable parameters + number of utilities for reporting on/analyzing I/O performance.


## 15.3 Learning Objectives:
- Explain the importance of I/O scheduling and describe the conflicting requirements that need to be satisfied.
- Delineate and contrast the options available under Linux.
- Understand how the **CFQ** (<strong>C</strong>ompletely <strong>F</strong>air <strong>Q</strong>ueue) and **Deadline** algorithms work.


## 15.4 I/O Scheduling
**I/O scheduler** provides interface between generic block layer and low-level physical device drivers. Both VM (Virtual Memory) and VFS (Virtual File System) layers submit I/O requests to block devices. Job of I/O scheduling layer to prioritize + order requests before they are given to block devices.

Any I/O scheduling algorithm has to satisfy certain (sometimes conflicting) requirements:
- Hardware access times should be minimized; ie, requests should be order according to physical location on disk. Leads to **elevator** scheme where requests inserted in pending queue in physical order
- Requests should be merged to extent possible to get as big a contiguous region as possible, which also minimizes disk access time
- Requests should be satisfied with as low a latency as feasible. In some cases, determinism (in sense of deadlines) important
- Write operations usually wait to migrate from caches to disk without stalling process. Read operations almost always require process to wait for completion before proceeding further. Favoring reads over writes leads to better parallelism and system responsiveness
- Processes should share I/O bandwidth in fair, consciously prioritized fashion. Even if it means some overall performance slowdown of I/O layer, process throughput should not suffer inordinately


## 15.5 I/O Scheduler Choices
Since demands can be conflicting, different I/O schedulers may be appropriate for different workloads, eg, large database server vs. desktop system. Different hardware may mandate different strategy. To provide flexibility, Linux kernel has object oriented scheme, where pointers to various needed functions supplied in a data structure, the particular one of which can be selected at boot on kernel command line:
```shell
linux ... elevator=[cfq|deadline|noop]
```
At least one of I/O scheduling algorithms must be compiled into kernel. Current choices:
- Completely Fair Queueing (CFQ)
- Deadline Scheduling
- noop (A simple scheme)

Default choice is compile configuration option. Modern distributions choose either CFQ or Deadline.


##

[Back to top](#)

---

[Previous Chapter](../Ch14-io/notes_Ch14.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch16-linuxfsvfs/notes_Ch16.md)
