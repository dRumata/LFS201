[Previous Chapter](../Ch12-processmonitoring/notes_Ch12.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch14-title/notes_Ch14.md)

---

# Chapter 13 Memory: Monitoring Usage and Tuning - Notes

## 13.2 Introduction
Over time, systems more demanding of memory resources while RAM prices decreased and performance improved. Yet, bottlenecks in overall system performance often memory-related. CPUs and I/O subsystem can be waiting for data to be retrieved from/written to memory. Many tools for monitoring, debugging, tuning system's behavior with regard to its memory.


## 13.3 Learning Objectives:
- List the primary (inter-related) considerations and tasks involved in memory tuning.
- Use entries in `/proc/sys/vm` and decipher `/proc/meminfo`.
- Use **vmstat** to display information about memory, paging, I/O, processor activity, and processes' memory consumption.
- Understand how the **OOM-killer** decides when to take action and selects which processes should be exterminated to open up some memory.



##

[Back to top](#)

---

[Previous Chapter](../Ch12-processmonitoring/notes_Ch12.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch14-title/notes_Ch14.md)
