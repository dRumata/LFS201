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

## 40.6 Backup vs. Archive
All backup media have finite lifetime before becoming unreadable. Conventional estimates are listed below:
- Magnetic tapes: 10-30 years
- CDs and DVDs: 3-10 years
- Hard Disks: 2-5 years

Lifetime is very sensitive to:
- Environmental conditions (temperature, humidity, etc.)
- Quality of media
- Haivng working software that can read data on current operating systems and hardware.

Lifetime is sufficient for backup, but nor for permanent digital archiving.

For lifetimes longer than the usual backup timescales, data can be preserved using multiple copies, plus copying over to newer media from time to time.

FOr very long times (i.e., many decades, centuries, etc.), standard methods do not work easily, as everything can go obsolete, hardware, software, and document format, media.

None of the inexpensive digital formats can actually compete with paper and film for long periods of time (if they are properly stored and continuously cared for - like wine).

This is a problem serious people think about and there should be good solutions available before all is lost.

## 40.7 Tape Drives
Tape drives not as common as they used to be. Relatively slow and permit only sequential access. On any modern setup, rarely used for primary backup. Sometimes used for off-site storage for archival purposes for long time reference. However, magnetic tape drives always have only finite lifetime without physical degradation and loss of data.

Modern tape drives usually of the LTO (Linear Tape Open) variety, whose first versions appeared in the late 1990s as an open standards alternative; early formats were mostly proprietary. Early versions held up to 100 GB; newer versions can hold 2.5 TB or more in a cartridge of the same size.

Day to day backups are usually done with some form of NAS (Network Attached Storage) or with cloud-based solutions, making new tape-based installations less and less attractive. However, they can still be found and system administrators may be required to deal with them.

In what follows, will try not to focus on particular physical forms for the backup media, and will speak more abstractly.

## 40.8 Backup Methods
Should never have all backups residing in same physical location as systems being protected. Otherwise, fire or other physical damage could lead to a total loss. In the past, this usually meant physically transporting magnetic tapes to a secure location. Today, this is more likely to mean transferring backups files over the Internet to alternative physical locations. Obviously, has to be done in secure way, using encryption and other security precautions as appropriate.

Several different kinds of backup methods can be used, often in concert with each other:
- **Full**

  Back up all files on the system.

- **Incremental**

  Backup all files that have changed since the last incremental or full backup.

- **Differential**

  Backup all files that have changed since the last full backup.

- **Multiple level incremental**

  Backup all files that have changed since the previous backup at the same or a previous level.

- **User**

  Backup only files in a specific user's directory.


## 40.9 Backup Strategies
Should note that backup methods useless without associated **restore** methods. Have to take into account the robustness, clarity, ease of both directions when selecting strategies.

Simplest backup scheme: do a full backup of everything once, and then perform incremental backups of everything that subsequently changes. While full backups can take a lot of time, restoring from incremental backups can be more difficult and time consuming. Thus, can use a mix of both to optimize time and effort.

Example of one useful strategy involving tapes (can easily substitute other media in description):
1. Use tape 1 for a full backup on Friday.
2. Use tapes 2-5 for incremental backups on Monday-Thursday.
3. Use tape 6 for full backup on second Friday.
4. Use tapes 2-5 for incremental backups on second Monday-Thursday.
5. Do not overwrite tape 1 until completion of full backup on tape 6.
6. After full backup to tape 6, move tape 1 to external location for disaster recovery.
7. For next full backup (next Friday) get tape 1 and exchange for tape 6.

A good rule of thumb is to have at least two weeks of backups available.

## 40.10 Backup utilities
A number of programs are used for backup purposes:
- **cpio**
- **tar**
- **gzip**, **bzip2**, **xz**

  **cpio** and **tar** create and extract **archives** of files. The archives are often compressed with **gzip**, **bzip2**, or **xz**. The archive file may be written to disk, magnetic tape, or any other device which can hold files. Archives are very useful for transferring files from one filesystem or machine to another.

- **dd**

  This powerful utility is often used to transfer raw data between media. It can copy entire partitions or entire disks.

- **rsync**

  This powerful utility can synchronize directory subtrees or entire filesystems across a network, or between different filesystem locations on a local machine.

- **dump and restore**

  These ancient utilities are designed specifically for backups. They read from the filesystem directly (which is more efficient). However, they must be restored only on the same filesystem type that they came from. There are newer alternatives.

- **mt**

  Useful for querying and positioning tapes before performing backups and restores.

## 40.11 Using tar for Backups
**tar** is easy to use:
- When creating **tar** archive, for each directory given as argument, all files and subdirectories will be included in archive
- When restoring, reconstitutes directories as necessary
- Even has **`--newer`** option that allows incremental backups
- Version of **tar** used in Linux can also handle backups that do not fit on one tape or whatever device being used.

Few examples of how to use **tar** for backups:
- Create an archive using **`-c`** or **`--create`**:
  ```shell
  $ tar --create --file /dev/st0 /root
  $ tar -cvf /dev/st0 /root
  ```
  Can specify a device or file with **`-f`** or **`--file`** option.

- Create with multi-volume option, using **`-M`** or **`--multi-volume`** if backup won't fit on one device:
  ```shell
  $ tar -cMf /dev/st0 /root
  ```
  Will be prompted to put next tape when needed.

- Verify files with compare option, using **`-d`** or **`--compare`**:
  ```shell
  $ tar --compare --verbose --file /dev/st0
  $ tar -dvf /dev/st0
  ```
  After making backup, can make sure that it is complete and correct using above verification option.

By default, **tar** will recursively include all subdirectories in archive.

When creating archive, **tar** prints message about removing leading slashes from absolute path name. While this allows for restoring files anywhere, default behavior can be modified.

Most **tar** options can be given in short form with one dash, or long form with two: **`-c`** is completely equivalent to **`--create`**.

Note: can combine options (when using short notation) so no need to type every dash.

Furthermore, single-dashed **tar** options can be used with or without dashes; i.e., **`tar cvf file.tar dir1`** has same result as **`tar -cvf file.tar dir1`**.

## 40.12 Using tar for Restoring Files
**`-x`** or **`--extract`** option extracts files from archive, all by default. Can narrow the file extraction list by specifying ony particular files. If directory specified, all included files and subdirectories are also extracted.

**`-p`** or **`--same-permissions`** options ensures files are restored with their original permissions.

**`-t`** or **`--list`** option lists, but does not extract, the files in the archive.

**Examples**:
- Extract from an archive:
  ```shell
  $ tar --extract --same-permissions --verbose --file /dev/st0
  $ tar -xpvf /dev/st0
  $ tar xpvf /dev/st0
  ```

- Specify only specific files to restore:
  ```shell
  $ tar xvf /dev/st0 somefile
  ```

- List the contents of a **tar** backup:
  ```shell
  $ tar --list --file /dev/st0
  $ tar -tf /dev/st0
  ```

## 40.13 Incremental Backups with tar
Can do incremental backup with **tar** using the **`-N`** (or the equivalent **`--newer`**), or the **`--after-date`** options. Either option requires specifying either a date or a qualified (reference) file name:
```shell
$ tar --create --newer '2011-12-1' -vf backup1.tar /var/tmp
$ tar --create --after-date '2011-12-1' -vzf backup1.tar /var/tmp
```
Either form creates backup archive of all files in `/var/tmp` which were modified after December 1, 2011.

Because **tar** only looks at file's date, does not consider any other changes to the file, such as permissions or file name. To include files with these changes in incremental backup, use **find** and create a list of files to be backed up.

**Note**: when followed by an option like **`--newer`**, must use the dash in options like **`-vzf`**, or **tar** will get confused. This kind of option specification confusion sometimes occurs with old UNIX utilities like **ps** and **tar** with complicated histories involving different families of UNIX.

## 40.14 Archive Compression Methods
Often desired to compress files to save disk space and/or network transmission time, especially since modern machines will often find the compress -> transmit -> decompress cycle faster than just transmitting (or copying) an uncompressed file.

Number of commonly used compression schemes available in Linux. In order of increasing compression efficiency (which comes at the cost of longer compression times):
- **gzip**

  Uses Lempel-Zip Coding (LZ277) and produces **`.gz`** files.

- **bzip2**

  Uses Burrow-Wheeler block sorting text compression algorithm and Huffman coding, and produces **`.bz2`** files.

- **xz**

  Produces **`.xz`** files and also support legacy **`.lzma`** format.

Decompression times do not vary as much as compression times do. For day-to-day use on smaller files, one usually just uses **gzip**, as it is extremely fast, but, for larger files and for archiving purposes, the other two methods are often used. E.g., [The Linux Kernel Archives](https://www.kernel.org/) now offers kernels only in the **xz** format.

The **`.zip`** format is rarely used in Linux, except to extract legacy archives from other operating systems.

Compression utilities very easily (and often) used in combination with **tar**:
```shell
$ tar zcvf source.tar.gz source
$ tar jcvf source.tar.bz2 source
$ tar Jcvf source.tar.xz source
```
for producing a compressed archive. Note: first command has the exact same effect as doing:
```shell
$ tar cvf source.tar source; gzip -v source.tar
```
but is more efficient because:
1. There is no intermediate file storage.
2. Archiving and compression happen simultaneously in the pipeline.

For decompression:
```shell
$ tar xzvf source.tar.gz
$ tar xjvf source.tar.bz2
$ tar xJvf source.tar.xz
```
or even simpler:
```shell
$ tar xvf source.tar.gz
```
as modern versions of **tar** can sense the method of compression and take care of it automatically.

Obviously, not worth using these methods on archives whose component files are already compressed, such as **`.jpg`** images, or **`.pdf`** files.

##

[Back to top](#)

---

[Previous Chapter](../Ch39-init/notes_Ch39.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch41-securitymodules/notes_Ch41.md)
