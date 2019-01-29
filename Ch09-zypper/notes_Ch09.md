[Previous Chapter](../Ch08-yum/notes_Ch08.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch10-apt/notes_Ch10.md)

---

# Chapter 8 zypper - Notes

## 9.2 Introduction
For use on SUSE-based systems, **zypper** program provides higher level of intelligent services for using underlying **rpm** program, plays same role as **yum** on Red Hat-based systems. Can automatically resolve dependencies when installing, updating, removing packages. Accesses external software repositories, synchronizing with them, retrieving/installing software as needed.


## 9.3 Learning Objectives:
- Explain what **zypper** is.
- Discuss the queries **zypper** can be used for.
- Install, remove, and upgrade packages using **zypper**.
- Learn additional and more advanced **zypper** commands.


## 9.4 What is zypper?
**zypper**: command line tool for installing/managing packages in SUSE Linux and openSUSE. Very similar to **yum** in functionality, even in basic command syntax, also works with **rpm** packages.

Retrieves packages from repositories, installs, removes, updates while resolving any dependencies encountered. Equivalent in practice to **yum** and **apt-get** in that it can retrieve packages from repository and also resolve dependencies.


## 9.5 zypper Queries
Some examples of commonly performed operations involving querying:
- Show a list of available updates:
  ```shell
  $ zypper list-updates
  ```

- List available repositories:
  ```shell
  $ zypper repos
  ```

- Search repositories for **`string`**:
  ```shell
  $ zypper search <string>
  ```

- List information about package:
  ```shell
  $ zypper info <package>
  ```

- Search repositories to ascertain what packages provide a file:
  ```shell
  $ zypper search --provides <file>
  ```

## 9.6 Installing/Removing/Upgrading
Some examples of commonly performed operations:
- Install or update package(s):
  ```shell
  $ sudo zypper install package
  ```

- Do not ask for confirmation when installing or upgrading:
  ```shell
  $ sudo zypper --non-interactive install <package>
  ```
  This is useful for scripts and is equivalent to running **`yum -y`**.

- Update all installed packages:
  ```shell
  $ sudo zypper update
  ```
  Giving package names as an argument will update only those packages and any required dependencies. Do this without asking for confirmation:
  ```shell
  $ sudo zypper --non-interactive update
  ```

- Remove a package from the system:
  ```shell
  $ sudo zypper remove <package>
  ```
  Like with **yum**, have to be careful with removal command, as any package that needs the package being removed would be removed as well.


## 9.7 Additional zypper Commands
Sometimes, number of **zypper** commands must be run in sequence. To avoid re-reading all databases for each command, can run **zypper** in **shell mode**:
```shell
$ sudo zupper shell
> install bash
...
> exit
```
Because **zypper** supports **readline** library, can use all the same command line editing function available in bash shell in zypper shell.

To add new repository:
```shell
$ sudo zypper addrepo URI alias
```
which is located at the supplied **`URI`** and will use supplied **`alias`**.

To remove repository from list:
```shell
$ sudo zypper removerepo alias
```
using **`alias`** of repo you want to delete.

To clean up and save space in `/var/cache/zypp`:
```shell
$ sudo zypper clean [--all]
```


##

[Back to top](#)

---

[Previous Chapter](../Ch08-yum/notes_Ch08.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch10-apt/notes_Ch10.md)
