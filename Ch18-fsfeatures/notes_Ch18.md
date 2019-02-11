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





##

[Back to top](#)

---

[Previous Chapter](../Ch17-diskpartitioning/notes_Ch17.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch19-fsfeatures2/notes_Ch19.md)
