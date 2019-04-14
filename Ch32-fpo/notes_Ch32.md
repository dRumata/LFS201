[Previous Chapter](../Ch31-gm/notes_Ch31.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch33-pam/notes_Ch33.md)

---

# Chapter 32 File Permissions and Ownership - Notes

## 32.3 Learning Objectives:
- Explain the concepts of **owner**, **group**, and **world**.
- Set file access rights (read, write, and execute) for each category.
- **Authenticate** requests for file access, respecting proper permissions.
- Use **chmod** to change file permissions, **chown** to change user ownership, and **chgrp** to change group ownership.
- Understand the role of **umask** in establishing desired permissions on newly created files.
- Use ACLs to extend the simpler user, group, world and read, write, execute model.


## 32.4 Owner, Group, and World
When you do an **`ls -l`** as in:
```shell
$ ls -l a_file
-rw-rw-r-- 1 coop aproject 1601 Mar 9 15:03  a_file
```
after the first character (which indicates the type of the file object), there are nine more which indicate the access rights granted to potential file users. There are arranged in three groups of three:
- **owner**: the user who owns the file (also called **user**)
- **group**: the group of users who have access
- **world**: the rest of the world (also called **other**)

In above listing, user is **`coop`** and group is **`aproject`**.


## 32.5 File Access Rights
If you do a long listing of a file, as in:
```shell
$ ls -l /usr/bin/vi
-rwxr-xr-x. 1 root root 910200 Jan 30 2014 /usr/bin/vi
```
each of the triplets can have each of the following sets:
- **r**: read access is allowed
- **w**: write access is allowed
- **x**: execute access is allowed

If permission not allowed, a **`-`** appears instead of one of these characters.

In addition, other specialized permissions exist for each category, such as the **setuid/setgid** permissions.

This, in preceding example, user **`coop`** and members of the group **`aproject`** have read and write access, while anyone else has only read access.


## 32.6 File Permissions and Security and Authentication
**File access permissions** are critical part of Linux security system. Any request to access file requires comparison of credentials and identity of requesting user to those of the owner of the file.

This **authentication** is granted depending on one of these three sets of permissions, in following order:
1. If the requester is the file owner, the file owner permissions are used
2. Otherwise, is the requester is in the group that owns the files, the group permissions are examined
3. If that doesn't succeed, the world permissions are examined


## 32.7 Changing Permissions: chmod
Changing file permissions is done with **chmod**. You can only change permissions on files you own, unless you are the superuser.

There are a number of different ways to use **chmod**. For instance, to give owner and world execute permission, and remove group write permission:
```shell
$ ls -l a_file
-rw-rw-r-- 1 coop coop 1601 Mar 9 15:04  a_file
$ chmod uo+x,g-w a_file
$ ls -l a_file
-rwxr--r-x 1 coop coop 1601 Mar 9 15:04  a_file
```
where **`u`** stands for user (owner), **`o`** stands for other (world), and **`g`** stands for group.

Permissions can be represented either as a bitmap, usually written in octal, or in a symbolic form. Octal bitmaps usually look like **`0755`**, which symbolic representations look like **`u+rwx,g+rwx,o+rx`**.



##

[Back to top](#)

---

[Previous Chapter](../Ch31-gm/notes_Ch31.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch33-pam/notes_Ch33.md)
