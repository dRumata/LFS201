[Previous Chapter](../Ch14-io/notes_Ch14.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch16-linuxfsvfs/notes_Ch16.md)

---

# Chapter 15 I/O Scheduling - Notes

## 15.2 Introduction
System performance often depends very heavily on optimizing I/O scheduling strategy. Many (often competing) factors influence behavior, including minimizing hardware access times, avoiding wear/tear on storage media, ensuring data integrity, granting timely access to applications that need to do I/O, being able to prioritize important tasks. Linux offers variety of **I/O Schedulers** to choose from, each of which has tunable parameters + number of utilities for reporting on/analyzing I/O performance.


## 15.3 Learning Objectives:
- Explain the importance of I/O scheduling and describe the conflicting requirements that need to be satisfied.
- Delineate and contrast the options available under Linux.
- Understand how the **CFQ** (<strong>C</strong>ompletely <strong>F</strong>air <strong>Q</strong>ueue) and **Deadline** algorithms work.




##

[Back to top](#)

---

[Previous Chapter](../Ch14-io/notes_Ch14.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch16-linuxfsvfs/notes_Ch16.md)
