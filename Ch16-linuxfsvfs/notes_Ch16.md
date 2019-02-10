[Previous Chapter](../Ch15-schedulingio/notes_Ch15.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch17-diskpartitioning/notes_Ch17.md)

---

# Chapter 16 Title - Notes

## 16.3 Learning Objectives:
- Explain the basic filesystem organization.
- Understand the role of the VFS.
- Know what filesystems are available in Linux and which ones can be used on your actual system.
- Grasp why journalling filesystems represent significant advances.
- Discuss the use of special filesystems in Linux.


## 16.4 Filesystem Basics
Application programs -> read/write files, rather than dealing with physical locations on actual hardware (where files are stored).

Files (and their names) -> abstraction camouflaging physical I/O layer. Directly writing to disk in **raw** fashion (ignoring **filesystem** layer)-> *very dangerous*, only done by low-level operating system software, never by user application.

Local filesystems generally reside within disk partition (which can be physical partition on disk, or logical partition controlled by **Logical Volume Manager** (LVM)). Filesystems can also be part of network nature, true physical embodiment completely hidden to local system across network.



##

[Back to top](#)

---

[Previous Chapter](../Ch15-schedulingio/notes_Ch15.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch17-diskpartitioning/notes_Ch17.md)
