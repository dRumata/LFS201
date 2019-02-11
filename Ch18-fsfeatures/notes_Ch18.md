[Previous Chapter](../Ch17-diskpartitioning/notes_Ch17.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch19-fsfeatures2/notes_Ch19.md)

---

# Chapter 18 Filesystem Features: Attributes, Creating, Checking, Mounting - Notes

## 18.3 Learning Objectives:
- Explain concepts such as inodes, directory files, and extended attributes.
- Create and format filesystems.
- Check and fix errors on filesystems.
- Mount and unmount filesystems.
- Use network file systems.
- Understand how to automount filesystems and make sure they mount at boot.


## 18.4 Extended Attributes and lsattr/chattr
**Extended Attributes** associate metadata not interpreted directly by filesystem with files. Four namespaces exist:
- user
- trusted
- security
- system

System namespace used for **Access Control Lists** (<strong>ACL</strong>s) and security namespace used by SELinux.

Flag values stored in file inode, maybe modified and set only by root user. Viewed with **lsattr** and set with **chattr**. Flags may be set for files:
- **`i`**: Immutable. File with immutable attribute cannot be modified (not even my root). Cannot be deleted or renamed. No hard link can be created to it, and no data can be written to file. Only superuser can set or clear this attribute.
- **`a`**: Append-only. FIle with append-only attribute set can only be opened in append mode for writing. Only superuser can set ot clear this attribute.
- **`d`**: No-dump. File with no-dump attribute set is ignored when the **dump** program is run. Useful for swap and cache files that you don't want to waste time backing up.
- **`A`**: No **atime** update. File with no-atime-update attribute set will not modify its **atime** (access time) record when file accessed but not otherwise modified. Can increase performance on some systems because it reduces amount of disk I/O on system.

Note: there are other flags that can be set; typing **`man chattr`** will show whole list. Format for **chattr**:
```shell
$ chattr [+|-|=mode] filename
```
**lsattr** used to display attributes for file:
```shell
$ lsattr filename
```

## 18.5 Creating and Formatting Filesystems
Every filesystem type has utility for **formatting** (making) filesystem on partition. Generic name for these utilities: **mkfs**. However, this is just frontend for filesystem-specific programs, each of which may have particular options.

![mkfs](/images/mkfs.png)

Thus, following two commands entirely equivalent:
```shell
$ sudo mkfs -t ext4 /dev/sda10
$ sudo mkfs.ext4 /dev/sda10
```
General format for **mkfs**:
```shell
mkfs [-t fstype] [options] [device-file]
```
where **`[device-file]`** is usually device name like `/dev/sda3` of `/dev/vg/lvm1`.

Each filesystem has own particular options that can be set when formatting. Eg. when creating **ext4** filesystem, journalling settings = one thing to keep in mind. Include defining journal file size, whether or not to use external journal file.

Should look at **man** page for each of **mkfs.\*** programs to see details.


## 18.6 Checking an Repairing Filesystems
Every filesystem type has utility designed to check for errors (and hopefully fix any that are found). Generic name for these utilities: **fsck**. However, just frontend for filesystem-specific programs.

![fsck](/images/fsck.png)

Thus, following two commands entirely equivalent:
```shell
$ sudo fsck -t ext4 /dev/sda10
$ sudo fsck.ext4 /dev/sda10
```
If filesystem is of type understood by operating system, can almost always just do:
```shell
$ sudo fsck /dev/sda10
```
and system will figure out type by examining first few bytes on partition.

**fsck** run automatically after set number of mounts, or set interval since last time it was run, or after abnormal shutdown. Should only be run on unmounted filesystems. Can force a check of all ounted filesystems at boot by doing:
```shell
$ sudo touch /forcefsck
$ sudo reboot
```
The file `/forcefsck` will disappear after successful check. One reason this is valuable trick: can do **fsck** on root filesystem, which is hard to do on running system.

General format for **fsck**:
```shell
fsck [-t fstype] [options] [device-file]
```
where **`[device-file]`** is usually device name like `/dev/sda3` or `/dev/vg/lvm1`. Usually, do not need to specify filesystem type, as **fsck** can figure it out by examining superblocks at start of partition.

Can control whether any errors found should be fixed one by one manually with **`-r`** option, or automatically, as best possible, by using **`-a`** option, etc. In addition, each filesystem type may have own particular options that can be set when checking.

Note: **journalling** filesystems much faster to check than older generation filesystems for two reasons:
- Rarely need to scan entire partition for errors, as everything but very last transaction logged and confirmed, so takes almost no time to check
- Even if whole filesystem checked, newer filesystems designed with **fast fsck** in mind. Older filesystems did not think much about this when designed as sizes were much smaller

Should look at **man** page for each of **fsck.\*** programs to see details.


##

[Back to top](#)

---

[Previous Chapter](../Ch17-diskpartitioning/notes_Ch17.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch19-fsfeatures2/notes_Ch19.md)
