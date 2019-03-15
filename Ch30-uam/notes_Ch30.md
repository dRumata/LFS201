[Previous Chapter](../Ch29-containers/notes_Ch29.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch31-gm/notes_Ch31.md)

---

# Chapter 30 User Account Management - Notes

## 30.3 Learning Objectives:
- Explain the purpose of individual user accounts and list their main attributes.
- Create new user accounts and modify existing account properties, as well as remove of lock accounts.
- Understand how user passwords are set, encrypted, and stored, and how to require changes in passwords over time for security purposes.
- Explain how restricted shells and restricted accounts work.
- Understand the role of the root account and when to use it.
- Use Secure Shell (**ssh**) and remove logins and commands.


## 30.4 User Accounts
Linux systems provide **multi-user** environment which permits people and processes to have separate simultaneous work environments.

Purposes of having individual user accounts include:
- Providing each user with their own individualized private space
- Creating particular user accounts for specific dedicated purposes
- Distinguishing privileges among users

One special user account is for the **root** user, who is able to do ***anything*** on the system. To avoid making costly mistakes, and for security reasons, the root account should only be used when absolutely necessary.

Normal user accounts are for people who will work on the system. Some user accounts (like the **daemon** account) exist for the purpose of allowing processes to run as a user other than root.

In next chapter, will continue with discussion of **group** management, where subsets of the users on system can share files, privileges, etc., according to common interests.


## 30.5 Attributes of a User Account
Each user on the system has a corresponding line in the `etc/passwd` file that describes their basic account attributes. (Will talk about passwords, as well as this file, later). For example:
```shell
....
beav:x:1000:1000:Theodore Cleaver:/home/beav:/bin/bash
warden:x:1001:1001:Ward Cleaver:/home/warden:/bin/bash
dobie:x:1002:1002:Dobie Gillis:/home/dobie:/bin/bash
....
```

The seven elements here are:
- User name: unique name assigned to each user
- User password: password assigned to each user
- User identification number (**UID**): unique number assigned to user account. UID is used by system for variety of purposes, including determination of user privileges and activity tracking
- Group identification number (**GID**): indicates primary, principal, or default **group** of user
- Comment or GECOS information: defined method to use comment field for contact information (full name, email, office, contact number) (No need to worry about meaning of **GECOS**, very old term)
- Home directory: for most users, unique directory that offers working are for user. Normally, this directory owned by user, and except for **root** will be found on the system somewhere under **`/home`**
- Login shell: normally, shell program such as `/bin/bash` or `/bin/csh`. Sometimes, however, alternative program referenced here for special cases. In general, this field will accept any executable

## 30.6 Creating User Accounts with useradd
The command:
```shell
$ sudo useradd dexter
```
will create an account for user **`dexter`**, using default algorithms for assigning user and group id, home directory, and shell choice.


##

[Back to top](#)

---

[Previous Chapter](../Ch29-containers/notes_Ch29.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch31-gm/notes_Ch31.md)
