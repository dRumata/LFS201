[Previous Chapter](../Ch01-introduction/notes_Ch01.md) - [Main Repository](https://github.com/schatto1/LFS201) - [Next Chapter](../Ch03-processes/notes_Ch03.md)

---

# Chapter 2 Linux Filesystem Tree Layout - Notes

## 2.3 Learning Objectives:
- Explain why Linux requires the organization of one big filesystem tree, and what the major considerations are for how it is done.
- Explain the role played by the Filesystem Hierarchy Standard.
- Describe what must be available at boot in the root (/) directory, and what can be available only once the system has started.
- Explore each of the main subdirectory trees, explain their purposes, and examine their contents.

## 2.4 One Big Filesystem
Linux: consists of one big filesystem tree (similar to all UNIX-based operating systems) -> usually diagrammed as inverted tree with **root directory**, /, at top of tree.

May be more than one (or even many) distinct file systems **mounted** at various points within this one large logical filesystem -> appear as subdirectories. Distinct filesystems usually on different partitions, which can also be on any number of different devices, including on network.

Applications: do not care about what physical device files reside on, just looks like one big filesystem.

In past, different UNIX-like OS organized tree in various ways + even various Linux distributions had differences -> resulted in difficulty and frustration writing applications/accomplishing system administration tasks on more than one kind of system

Result -> Linux ecosystem worked hard establish standardized procedures to minimize pain.


## 2.5 Data Distinctions
Taxonomy for what kind of info has to be read/written when talking about how files/data organized in one big directory tree. Two kinds of distinctions:
1. **Shareable vs non-shareable**: Shareable data can be shared between different hosts, non-shareable data must be specific to particular host. Eg. home directories -> shareable, device lock files -> non-shareable.
2. **Variable vs. static**: static data -> binaries, libraries, documentation + anything that doesn't change without system administrator assistance. Variable data -> anything that may change without systems administrator's help

These logical distinctions embodied as different kinds of information residing in various directories (or partitions and filesystems).


## 2.6 FHS Linux Standard Directory Tree
**Filesystem Hierarchy Standard (FHS)**: administered by The Linux Foundation (originally by the Free Standards Group), specifies main directories that must be present and their purposes.

Specifies standard layout -> simplifies predictions of file locations.

Most Linux distributions respect FHS, but none follow exactly. Last official version -> old enough, does not take into account some new developments.

Distributions -> like to experiment, and some experiments become generally accepted.

[FHS document](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.pdf) for more information.


## 2.7 Main Directory Layout
Linux distributors -> spend lot of time making sure filesystem layout is coherent and evolves correctly over time. List of main directories normally found under **/**:

Directory | In FHS? | Purpose
--------- | ------- | --------
**/** | Yes | Primary directory of entire file system hierarchy
**/bin** | Yes | Essential executable programs that much be available in **single user mode**
**/boot** | Yes | Files needed to boot system, such as kernel, **initrd** or **initramfs** images, boot configuration files, bootloader programs
**/dev** | Yes | **Device nodes**, used to interact with hardware and software devices
**/etc** | Yes | System wide configuration files
**/home** | Yes | Use **home directories** including personal settings, files, etc
**/lib** | Yes | Libraries required by executable binaries in **/bin** and **/sbin**
**/lib64** | No | 64-bit libraries required by executable binaries in **/bin** and **/sbin**, for systems which can run both 32-bit/64-bit programs
**/media** | Yes | Mount points for removable media eg. CDs, DVDs, USB sticks etc
**/mnt** | Yes | Temporarily mounted filesystems
**/opt** | Yes | Optional application software packages
**/proc** | Yes | Virtual pseudo-filesystem giving information about the system and processes running on it. Can be used to alter system parameters
**/sys** | No | Same as **/proc**. Similar to **device tree** and is part of **Unified Device Model**
**/root** | Yes | Home directory for the **root** user
**/sbin** | Yes | Essential system binaries
**/srv** | Yes | Site-specific data served up by system. Seldom used.
**/tmp** | Yes | Temporary files; on many distributions lost by reboot and may be ramdisk in memory
**/usr** | Yes | Multi-user applications, utilities, data: theoretically read-only
**/var** | Yes | Variable data that changes during system operation

May be additional distribution-specific directories found under root directory:
- /misc, for miscellaneous data
- /tfpboot, for booting using **tftp**. If files in directory, related to diskless workstation booting

Note: does not violate FHS to have other directories, does violate to have components in directories *other* than those dictated by standard.

##

[Back to top](#)

---

[Previous Chapter](../Ch01-introduction/notes_Ch01.md) - [Main Repository](https://github.com/schatto1/LFS201) - [Next Chapter](../Ch03-processes/notes_Ch03.md)
