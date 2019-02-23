[Previous Chapter](../Ch26-kernelmodules/notes_Ch26.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch28-virtualization/notes_Ch28.md)

---

# Chapter 27 Devices and udev - Notes

## 27.2 Introduction
Linux uses **udev**, an intelligent apparatus for discovering hardware and peripheral devices both during boot, and later when they are connected to the system. **Device nodes** are created automatically, and then used by applications/operating system subsystems to communicate with + transfer data to/from devices. System administrators can control how **udev** operates and craft special **udev** rules to assure desired behavior results.


## 27.3 Learning Objectives:
- Explain the role of **device nodes** and how they use **major** and **minor** numbers.
- Understand the need for the **udev** method and list its key components.
- Describe how the **udev** device manager functions.
- Identify **udev** rule files and learn how to create custom rules.


## 27.4 Device Nodes
Character and block devices have filesystem entries associated with them. Network devices in Linux *do not*. These **device nodes** can be used by programs to communicate with devices, using normal I/O system calls such as **`open()`**, **`close()`**, **`read()`**, and **`write()`**. On other hand, network devices work by transmitting/receiving **packets**, which must be constructed by breaking up streams of data, or reassembled into streams when received.

A device driver may manage multiple device nodes, which are normally placed in `/dev` directory. Can be seen with:
```shell
$ ls -l /dev
```

Device nodes can be created with:
```shell
sudo mknod [-m mode] /dev/name <type> <major> <minor>
```
For example:
```shell
mknod -m 666 /dev/mycdrv c 254 1
```

![device_node_large](/images/device_node_large.png)
**Device nodes**


## 27.5 Major and Minor Numbers
**Major** and **minor** numbers identify driver associated with device, with driver uniquely reserving a group of numbers. In most cases (but not all), device nodes of the same type (block or character) with the same major number use the same driver.

If you list some device nodes:
```shell
$ ls -l /dev/sda*
brw-rw---- 1 root disk 8,  0 Dec 29 06:40 /dev/sda
brw-rw---- 1 root disk 8,  1 Dec 29 06:40 /dev/sda1
brw-rw---- 1 root disk 8,  2 Dec 29 06:40 /dev/sda2
.......
```
**Major** and **minor** numbers appear in same place that file size would when looking at normal file. In above example as **8**, **1**, etc. While normal users will probably never need to refer explicitly to major and minor numbers and will refer to devices by name, system administrators may have to untangle them from time to time if system gets confused about devices, or has some hardware added at runtime.

**Minor** number used only by device driver to differentiate between different devices it may control, or how they are used. These may either be different instances of same kind of device (such as first and second sound card, or hard disk partition), or different modes of operation of given device (such as different density floppy drive media).

Device numbers have meaning in user-space as well. Two system calls, **`mknod()`** and **`sta()`** return information about **major** and **minor** numbers.


## 27.6 udev
Methods of managing device nodes became clumsy and difficult as Linux evolved. Number of device nodes lying in `/dev` + its subdirectories reached numbers in 15,000 - 20,000 range in most installations during 2.4 kernel version series. Nodes for devices which would never be used on most installations were still created by default, as distributors could never be sure exactly which hardware would be present on system.

Many developers + system administrators trimmed list to what was actually needed, especially in embedded configurations, but this essentially manual and potentially error-prone task.

Note: while device nodes *not* normal files and don't take up significant space on filesystem, having huge directories slowed down access to device nodes, especially upon first usage. Exhaustion of available major and minor numbers required more modern + dynamic approach to creation/maintenance of device nodes. Ideally, one would like to register devices by name. However, major and minor numbers cannot be gotten rid of altogether, as **POSIX** standard requires them. (POSIX: acronym for **Portable Operating System Interface**, a family of standards designed to ensure compatibility between different operating systems.)

**udev** method created device nodes on the fly as needed. No need to maintain a ton of device nodes that will never be used. The **`u`** in **udev** stands for **user**, and indicates that most of the work of creating, removing, modifying nodes is done in user-space.

**udev** handles dynamical generation of device nodes, evolved to replace earlier mechanisms such as **devfs**, **hotplug**. Supports **persistent device naming**. Names need not depend on order of device connection or plugging in. Such behavior controlled by specification of **udev rules**.


##

[Back to top](#)

---

[Previous Chapter](../Ch26-kernelmodules/notes_Ch26.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch28-virtualization/notes_Ch28.md)
