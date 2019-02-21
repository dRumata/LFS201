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


##

[Back to top](#)

---

[Previous Chapter](../Ch26-kernelmodules/notes_Ch26.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch28-virtualization/notes_Ch28.md)
