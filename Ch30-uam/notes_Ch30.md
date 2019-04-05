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

Specifically, the **useradd** command above causes following steps to execute:
- Next available UID greater than **`UID_MIN`** (specified in `/etc/login.defs`) by default assigned as **`dexter`**'s **`UID`**
- A group called **`dexter`** with a **`GID=UID`** also created and assigned as **`dexter`**'s primary group
- A home directory `/home/dexter` created and owned by **`dexter`**
- **`dexter`**'s login shell will be `/bin/bash`
- Contents of `/etc/skel` copied to `/home/dexter`. By default, `/etc/skel` includes startup files for **bash** and for the X Window system
- Entry of either **`!!`** placed in password field of `/etc/shadow` file for **`dexter`**'s entry, thus requiring administrator to assign a password for the account to be usable

Defaults can be easily overruled by using options to **useradd**:
```shell
$ sudo useradd -s /bin/csh -m -k /etc/skel -c "Bullwinkle J Moose" bmoose
```
where explicit non-default values have been given for some of the user attributes.

## 30.7 Modifying and Deleting User Accounts
Root user can remove user accounts using **userdel**:
```shell
$ sudo userdel morgan
```
All references to user **`morgan`** will be erased from `/etc/passwd`, `/etc/shadow`, and `/etc/group`.

While this removes account, does not delete the home directory (usually `/home/morgan`) in case the account may be re-established later. If **`-r`** option given to **userdel**, home directory will also be obliterated. However, all other files on system owned by removed user will remain.

**usermod** can be used to change characteristics of a user account, such as group memberships, home directory, login name, password, default shell, user id, etc. For example, the command
```shell
$ sudo usermod -L dexter
```
locks the account for **`dexter`**, so he cannot login.

Usage pretty straightforward. Note: **usermod** will take care of any modifications to files in `/etc` directory as necessary.

![usermod](/image/usermod.png)


## 30.8 Locked Accounts
Linus ships with some system accounts that are **locked** (such as **`bin`**, **`daemon`**, **`sys`**), which means they can run programs, but can never login tot he system and have no valid passoword associated with them. For example, `etc/passwd` has entries like:
```shell
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
```

The **`nologin`** shell returns the following if a locked user tries to login to the system:
```shell
This account is currently not available.
```
or whatever message may be stored in `/et/nologin.txt`.

Such locked accounts are created for special purposes, either by system services or applications; if you scan `/etc/passwd` for users with the **`nologin`** shell, you can see who they are on your system.

Also possible to lock account of particular user:
```shell
$ sudo usermod -L dexter
```
which means the accounts stays on the system but logging in is impossible. Unlocking can be done with **`-U`** option.

Customary practice: lock user's acocunts whenever they leave the organization or is on an extended leave of absence.

Another way to lock an account: use **chage** to change expiration date of account to date in the past:
```shell
$ sudo chage -E 2014-09-11 morgan
```
Actual date irrelevant as long as it is in the past. Will discuss **chage** shortly.

Another approach is to edit `etc/shadow` file and replace user's hashed password with **`!!`** or some other invalid string.


## 30.9 User IDs and /etc/passwd
Have already seen how `etc/passwd` contaisn one record (one line) for each user on system:
```shell
beav:x:1000:1000:Theodore Cleaver:/home/beav:/bin/bash
rsquirrel:x:1001:1001:Rocket J Squirrel:/home/rsquirrel:/bin/bash
```
and have already discussed the fields in here. Each record consists of number of fields separated by colons:
- **`username`** - the user's unique name
- **`password`** - either the hashed password (if `/etc/shadow` is not used) or a placeholder ("x" when `/etc/shadow` is used)
- **`UID`** - user identification number
- **`GID`** - primary group identification number for the user
- **`comment`** - comment area, usually the user's real name
- **`home`** - directory pathname for the user's home directory
- **`shell`** - absolutely qualified name of the shell to invoke at login

If `/etc/shadow` is not used, password field contains hashed password. If used, contains a placeholder ("**x**").

The convention most Linux distributions have used is that any account with a user ID less than **`1000`** is considered special and belongs to the system; normal user accounts start at **`1000`**. Actual value defined as **`UID-MIN`** and is defined in `/etc/login.defs`.

If User ID if not specified when using **useradd**, system will incrementally assign UIDS starting at **`UID_MIN`**

Additionally, each user gets a **Primary Group ID** whick, by default, is the same number as the UID. These are sometimes called **User Private Groups (UPG)**.

Bad practice to edit `/etc/passwd`, `/etc/group`, `/etc/shadow` directly. Either user appropriate utilities such as **usermod**, or use **vipw** special editor to do so as it is careful about file locking, data corruption, etc.


## 30.10 Why Use /etc/shadow?
Use of `/etc/shadow` enables password aging on a per user basis. At same time, also allows for maintaining greater security of hashed passwords.

Default permissions of `/etc/passwd` are **644** (**`-rw-r--r--`**); anyone can read the file. Unfortunately necessary because system programs and user applications need to read information contained in file. These system programs do not run as user root; in any event, only root may change the file.

Of particular concern: hashed passwords themselves. If appear in `/etc/passwd`, anyone may make copy of hashed passwords and then make use of utilities such as **Crack** and **John the Ripper** to guess original cleartext passwords given hashed password. Huge security risk!

`etc/shadow` has permission settings of **`400`** (**`-r--------`**), means that only root can access this file. Makes it more difficult for someone to collect hashed passwords.

Unless compelling good reason not to, should use `/etc/shadow` file.







##

[Back to top](#)

---

[Previous Chapter](../Ch29-containers/notes_Ch29.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch31-gm/notes_Ch31.md)
