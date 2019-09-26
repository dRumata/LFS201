[Previous Chapter](../Ch43-troubleshooting/notes_Ch43.md) - [Table of Contents](../README.md#table-of-contents) - [Jump to First Chapter](../Ch01-introduction/notes_Ch01.md)

---

# Chapter 44 System Rescue - Notes

## 44.2 Introduction
Sooner or later, system likely to undergo significant failure, such as failing to boot properly, to mount filesystems, initiate a desktop display, etc. **System Rescue** media in the form of optical disks or portable USB drives can be used to fix situation. Booting into either **emergency** or **single user** mode can enable using full suite of Linux tools to repair system back to normal function.

## 44.3 Learning Objectives:
- Explain what forms system rescue media come in and how they are made available or can be prepared.
- Know how to enter **emergency mode** and what can be done there.
- Know how to enter **single user mode**, what can be done there, and how it differs from emergency mode.

## 44.4 Rescue Media and Troubleshooting
Will discuss rescue and recovery disks and other media in the next session; here, will discuss in terms of troubleshooting. These media can contain valuable tools for evaluating (and fixing) trouble systems.

Exact choices will vary from one Linux distribution to another, but when you boot from an install or live CD/DVD or USB drive, will be able to select an option with a name like **`Rescue Installed System`**.

The rescue image generally contains a limited but powerful set of utilities useful for fixing problems on a system:
- Disk Maintenance Utilities
- Networking Utilities
- Miscellaneous Utilities
- Logging files.

## 44.5 Common Utilities on Rescue/Recovery Media
Rescue disks contain many useful programs, including:
- Disk utilities for creating partitions, managing RAID devices, managing logical volume, and creating filesystems;
  
  **fdisk**, **mdadm**, **pvcreate**, **vgcreate**, **lvcreate**, **mkfs**, and many others.
- Networking utilities for network debugging and network connectivity:

  **ifconfig**, **route**, **traceroute**, **mtr**, **host**, **ftp**, **scp**, **ssh**
  
- Numerous other commands are also available:
  
  **bash**, **chroot**, **ps**, **kill**, **vi**, **dd**, **tar**, **cpio**, **gzip**, **rpm**, **mkdir**, **ls**, **cp**, **mv**, and **rm** to name a few.
  
## 44.6 Using Rescue/Recovery Media
Rescue image will ask a number of questions upon starting. One of these is whether or not to mount your filesystems (if it can).

If so, mounted at somewhere, usually at `/mnt/sysimage`. Can move to that directory to get to files, or can change into that environment with:
```shell
$ sudo chroot /mnt/sysimage
```
For a network-based rescue, may also be asked to mount `/mnt/source`.

May install software packages from inside **chroot**-ed environment. May also be able to install them from ourside the **chroot**-ed environment. Eg., on an **rpm**-based system, by using the **`--root`** option to specify the location of the root directory:
```shell
$ sudo rpm -ivh --force --root=/mnt/sysimage /mnt/sources/Packages/vsftpd-2*.rpm
```

# 44.7 Emergency Boot Media
Emergency boot media are useful when your system won't boot due to some issue such as missing, misconfigured, or corrupted files or a misconfigured service.

Rescue media may also be useful if the root password is somehow lost or scrambled and needs to be reset.

Most Linux distributions permit the install media (CD, DVD, USB) and/or Live media to serve a double purpose as a rescue disk, which is very convenient. There are also special-purpose rescue disks available.

Live media (in any format) provide a complete and bootable operating system which runs in memory, rather than loading from disk. Users can experience and evaluate an operating system and/or Linux distribution without actually installing it, or making any changes to the existing operating system on the computer.

Live removable media are unique in that they can run on a computer lacking secondary storage, such as a hard disk drive, or with a corrupted hard disk drive or file system, allowing users to rescue data.

## 44.8 Using Rescue Media
Whether using Live, install, or rescue media, procedures for entering into a special operating system for rescue and recovery are the same, and as pointed out, one medium serves all three purposes.

Rescue/recovery mode can be accessed from an option on the boot menu when the system starts from removable media. In many cases, may have to type **`rescue`** on a line like:
```shell
boot: Linux rescue
```
Can't tell all the possibilities, as each distribution has somewhat different, but easy to ascertain procedures.

Next, can expect to be asked some questions, such as which language to continue in, as well as make some distribution-dependent choices. Then, will be prompted to select where a valid rescue image is located: CD/DVD. Hard Drive, NFS, FTP, or HTTP.

Selected location must contain a valid installation tree, and the installation tree must be for the same Linux version as the rescue disk, and if using removable media, the installation tree must be the same as the one from which the media was created. If using a **`boot.iso`** image downloaded from the vendor, then will also need a network-based install tree.

Additional questions are asked about mounting your filesystems. If they can be found, they are mounted under `mnt/sysimage`. Will then be given a shell prompt and access to various utilities to make the appropriate fixes to your system.

**`chroot`** can be used to better access root (**`/`**) filesystem.

## 44.9 Rescue USB Key
Many distributions provide provide a **`boot.iso`** image file for download (name may differ). Can use **dd** to place this on a USB key drive as in:
```shell
$ dd if=boot.iso of=/dev/sdX
```
assuming system recognizes the removable drive as `/dev/sdX`. Be aware this will obliterate the previously existing contents on the drive!

Assuming system has the capability of booting from USB media and the BIOS is configured for it, can then boot from this USB drive. Will then function in the same fashion as a rescue CD or DVD. However, note that the install tree will not be present on the USB drive; therefore, this method requires a network-based install tree if one is needed.

Helpful utilities such as **livecd-tools** and **liveusb-creator** allow specification of either a local drive or the Internet as the location for obtaining an install image, and then do all the hard work of constructing a bootable image and burning it on the removable drive. Extremely convenient and works for virtually all Linux distributions.

## 44.10 Emergency Mode
In **emergency mode** you are booted into the most minimal environment possible. Root filesystem is mounted read-only, no **init** scripts are run and almost nothing is set up.

The main advantage of emergency mode over single-user mode (to be described next) is that if **init** is corrupted or not working, can still mount filesystems to recover data that might be lost during a re-installation.

To enter emergency mode, need to select an entry from the GRUB boot menu and then hit **`e`** for edit. Then add the word **`emergency`** to the kernel command line before telling the system to boot. Will be asked for the root password before getting a shell prompt.

Note: may also enter emergency mode when a boot fails for a variety of reasons, including a corrupted filesystem.

## 44.11 Single User Mode
If system boots, but does not allow you to log in when it has completed booting, try **single user mode**. In single user mode:
- **init** is started
- Services are not started
- Network is not activated
- All possible filesystems are mounted
- root access is granted without a password
- A system maintenance command line shell is launched.

In this mode, system boots to **runlevel** 1 (in SysVinit language). Because single user mode automatically tried to mount your filesystem, cannot use it when root filesystem cannot be mounted successfully, or if the **init** configuration is corrupted.

To boot into single user mode, use the same method as decribed for emergency mode with one exception, replace the keyword **`emergency`** with the keyword **`single`**.




##

[Back to top](#)

---

[Previous Chapter](../Ch43-troubleshooting/notes_Ch43.md) - [Table of Contents](../README.md#table-of-contents) - [Jump to First Chapter](../Ch01-introduction/notes_Ch01.md)
