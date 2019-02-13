[Previous Chapter](../Ch20-extfs/notes_Ch20.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch22-encryptingdisks/notes_Ch22.md)

---

# Chapter 21 The XFS and btrfs Filesystems - Notes

## 21.2 Introduction
**XFS** and **btrfs** filesystems have risen as important challengers to dominance of **ext4** in Enterprise Linux distributions. These next generation filesystems have robust capabilities with respect to handling large sizes, spanning multiple physical + logical volumes, and performance metrics.

## 21.3 Learning Objectives:
- Describe the **XFS** filesystem.
- Maintain the **XFS** filesystem.
- Describe the **btrfs** filesystem.


## 21.4 XFS Features
XFS filesystem designed + created by Silicon Graphics Inc. (SGI), used in IRIX operating system, subsequently ported to Linux. Engineered to deal with large data sets for SGI systems + handle parallel I/O tasks very effectively.

Can handle:
- Up to 16 EB (exabytes) for total filesystem
- UP to 8 EB for an individual file.

High performance -> one of the key design elements of **XFS**, which implements methods for:
- Employing **DMA** (<strong>D</strong>irect <strong>M</strong>emory <strong>A</strong>ccess) I/O
- Guaranteeing an I/O rate
- Adjusting stripe size to match underlying **RAID** or **LVM** storage devices

Unline other Linux filesystems, **XFS** can also journal quota information. Leads to decreased recovery time when quota-enabled filesystem uncleanly mounted. Furthermore, journal can be on external device.

As with other UNIX and Linux filesystems, **XFS** supports extended attributes.


## 21.5 XFS Details
Maintaining **XFS** filesystem made easier by the fact that most of the maintenance tasks can done on-line (ie. while filesystem fully mounted). Include:
- Defragmenting
- Resizing (enlarge only)
- Dumping/Restoring

Backup and restore can be done with native **XFS** utilities:
- **xfsdump**
- **xfsrestore**

which can be conveniently paused and then resumed at later time. Because these utility programs also multi-threaded, **XFS** dumps and restores can be accomplished very quickly.

Traditional quota commands can be used to manipulate per-filesystem quotas on XFS volume. However, if you use **xfs_quota** command, can use the per-directory quotas that XFS supports.

**XFS** filesystem does not directly support hardware or software **snapshots**. However, **xfs_freeze** utility can be used to quiesce filesystem for snapshots.


## 21.6 The btrfs Filesystem
Both Linux developers and Linux users with high performance and high capacity or specialized needs -> following the development and gradual deployment of **btrfs** filesystem, created by Chris Mason. Name stands for **B**-<strong>t</strong>ree <strong>f</strong>ile <strong>s</strong>ystem. Full documentation can be found on [btrfs wiki page](https://btrfs.wiki.kernel.org/index.php/Main_Page).

**btrfs** intended to address lack of pooling, snapshots, checksums, integral multi-device spanning in other Linus filesystems such as **ext4**. Such features can be crucial for Linus to scale into larger enterprise storage configurations.

While **btrfs** has been in mainline kernel since 2.6.29, has generally been viewed as experimental. However, some vendors using it in new products, default root filesystem on SLES and OpenSUSE.

One of the main features -> ability to take frequent snapshots of entire filesystems, or sub-volumes of entire file-systems in virtually no time. Because **btrfs** makes extense use of COW techniques (Copy on Write), such snapshot does not involve any more initial space for data blocks or any I/O activity except for some metadata updating.

One can easily revert to state described by earlier snapshots, even induce kernel to reboot off earlier root filesystem snapshot.

**btrfs** maintains it own internal framework for adding or removing new partitions and/or physical media to existing filesystems, such as LVM (Logical Volume Management) does.

Before **btrfs** suitable for day-to-day use in critical filesystems, some tasks require finishing. For review of development history of **btrfs** and expected evolution, see https://lwn.net/Articles/575841/.





##

[Back to top](#)

---

[Previous Chapter](../Ch20-extfs/notes_Ch20.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch22-encryptingdisks/notes_Ch22.md)
