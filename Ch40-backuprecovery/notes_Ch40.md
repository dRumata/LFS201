[Previous Chapter](../Ch39-init/notes_Ch39.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch41-securitymodules/notes_Ch41.md)

---

# Chapter 40 Backup and Recovery Methods - Notes

## 40.3 Learning Objectives:
- Identify and prioritize data that needs backup.
- Employ different kinds of backup methods, depending on the situation.
- Establish efficient backup and restore strategies.
- Use different backup utilities, such as **cpio**, **tar**, **gzip**, **bzip2**, **xz**, **dd**, **rsync**, **dump**, **restore**, and **mt**.
- Describe the two most well-known backup programs, Amanda and Bacula.

## 40.4 Why Backups?
Whether you are administering only one personal system or a network of many machines, system backups are very important. Some of the reasons are:
- **Data is valuable**

  On-disk data is an important work product, and is therefore a commodity that we wish to protect. Recreating lost data costs time and money. Some data may even be unique, and there may be no way to recreate it.

- **Hardware fails**

  While storage media reliability has increased, so has drive capacity. Even if the failure rate per byte decreases, unpredictable failures still occur. May be pessimistic to say there are only two kinds of drives: those that have failed, and those that will fail, but it is essentially true. Using **RAID** helps, but backups are still needed.

- **Software fails**

  No software is perfect. Bugs may destroy or corrupt data. Even stable programs long in use can have problems.

- **People make mistakes**

  Everyone has heard **OOPS!** (or something much worse) coming from the next cubicle (or from their own mouth) at one time or another. Sometimes, just a simple typing error can cause large scale destruction of files and data.

- **Malicious people can cause deliberate damage**

  Could be the canonical disgruntled employee or an external hacker with a point to make. Security concerns and backup capabilities are very strongly related.

- **Unexplained events happen**

  Files can just disappear without you know how, who, or even when it occured.

- **Rewinds can be useful**

  Sometimes, restoring to an earlier **snapshot** or all or part of the system may be required.

## 40.5 What Needs Backup?
Some data is critical for backup, some less critical, and some never needs saving. In priority order:
1. **Definitely**
  - Business-related date
  - System configuration files
  - User files (usually under `/home`)
2. **Maybe**
  - Spooling directories (for printing, mail, etc.)
  - Logging files (found in `/var/log`, and elsewhere)
3. **Probably not**
  - Software that can easily be re-installed; on a well-managed system, this should be almost everything
  - The `/tmp` directory, because its contents are indeed supposed to be temporary
4. **Definitely not**
  - Pseudo-filesystems such as `/proc`, `/dev`, and `/sys`
  - Any swap partitions or files

Obviously, files essential to your organization require backup. Configuration files may change frequently, and along with individual user's files, require backup as well.

Logging files can be important if you have to investigate your system's history, which can be particularly important for detecting intrusions and other security violations.

Don't have to back up anything that can easily be re-installed. Also, the **swap** partitions (or files) and `/proc` filesystems are generally not useful for necessary to backup, since the data in these areas is basically temporary (just like in the `/tmp` directory).


##

[Back to top](#)

---

[Previous Chapter](../Ch39-init/notes_Ch39.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch41-securitymodules/notes_Ch41.md)
