[Previous Chapter](../Ch22-encryptingdisks/notes_Ch22.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch24-raid/notes_Ch24.md)

---

# Chapter 23 Title - Notes

## 23.3 Learning Objectives:
- Explain the concepts behind **LVM**.
- Create logical volumes.
- Display logical volumes.
- Resize logical volumes.
- Use **LVM** snapshots.


## 23.4 LVM
**LVM** (<strong>L</strong>ogical <strong>V</strong>olume <strong>M</strong>anagement) breaks up one virtual partition into multiple chunks, each of which can be on different partitions and/or disks.

Many advantages to using LVM. Particularly, becomes really easy to change size of logical partitions and filesystems, to add more storage space, rearrange things, etc.

One or more **physical volumes** (disk partitions) grouped together into **volume group**. Then, volume group subdivided into **logical volumes**, which mimic to system nominal physical disk partitions, and can be formatted to contain mountable filesystems.

Variety of command line utilities tasked to create, delete, resize etc. physical and logical volumes. For graphical tool, some Linux distributions use **system-config-lvm**. However, RHEL 7 does not support this tool, and there is currently no graphical tool that works reliably with most recent variations in filesystem types etc. Command line utilities not hard to use, and more flexible anyway.

LVM does impact performance. Definite additional cost that comes from overhead of LVM layer. However, even on non-RAID systems, if using **striping** (splitting of data to more than one disk), can achieve some parallelization improvements.

![LVM_Components_large](/images/LVM_Components_large.png)
**LVM Components**




##

[Back to top](#)

---

[Previous Chapter](../Ch22-encryptingdisks/notes_Ch22.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch24-raid/notes_Ch24.md)
