[Previous Chapter](../Ch05-packagemanagementsystems/notes_Ch05.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch07-dpkg/notes_Ch07.md)

---

# Chapter 6 RPM - Notes

## 6.2 Introduction
**Red Hat Package Manager** (**RPM**) used by number of major distributions (and close relatives) to control installation, verification, upgrade, removal of software on Linux systems. Low-level **rpm** program performs all these operations, either on just one package or on list of packages. Operations that would cause problems (eg. removing package that another package depends on, or installing package when system needs other software to be installed first) blocked from completion.


## 6.3 Learning Objectives:
- Understand how the **RPM** system is organized and what major operations the **rpm** program can accomplish.
- Explain the naming conventions used for both binary and source **rpm** files.
- Query, verify, install, uninstall, upgrade, and freshen packages.
- Grasp why new kernels should be installed, rather than upgraded.
- Use **rpm2cpio** to copy packaged files into a **cpio** archive, as well as to extract the files without installing them.


## 6.4 RPM
**RPM** (<strong>R</strong>ed Hat <strong>P</strong>ackage <strong>M</strong>anager) developed by Red Hat (unsurprisingly). All files related to specific task packaged into single **rpm** file, which also contains information about how/where to install/uninstall files. New versions of software lead to new **rpm** files, which then used for updating.

**rpm** files also contain dependency information. Note: unless given specific **URL** to draw from, **rpm** does not retrieve packages over network, installs only from local machine using absolute/relative paths.

**rpm** files usually distribution-dependent; installing package on different distribution than it was created for -> difficult, if not impossible.


## 6.5 Advantages of Using RPM
For system administrators, RPM makes it easy to:
- Determine what package (if any) any file on system is part of
- Determine what version installed
- Install/uninstall (erase) packages without leaving debris behind
- Verify that package was installed correctly. Useful for both troubleshooting/system auditing
- Distinguish documentation files from rest of package, optionally decide not to install them to save space
- Use **ftp** or **HTTP** to install packages over internet

For developers, RPM also offers advantages:
- Software often made available on more than one operating system. With RPM, original full + unmodified source used as basis, but developer can separate out changes needed to build on Linux
- More than one architecture can be built using only one **source package**


## 6.6 Package File Names
RPM package file names based on fields representing specific information, as documented in [RPM standard](http://rpm.org/):
- Standard naming format for binary package:

  `<name>-<version>-<release>.<distro>.<architecture>.rpm`

  `sed-4.2.2-5.el7.x86_64.rpm`

- Standard naming format for source package:

  `<name>-<version>-<release>.<distro>.src.rpm`

  `sed-4.2.2-5.el7.src.rpm`

Note: **distro** field often actually specifies repository that package came from, as given installation may use number of different package repositories, as discussed for **yum**/**zypper** which work above RPM.


## 6.7 Database Directory
`/var/lib/rpm` -> default system directory that holds RPM database files in form of Berkeley DB hash files. Database files should not be manually modified, updated should be done only through use of **rpm** program.

Alternative database directory can be specified with **`--dbpath`** option to **rpm** program. Might do this, for example, to examine RPM database copied from another system.

Can use **`--rebuilddb`** option to rebuild database indices from installed package headers. More of repair, not rebuild from scratch.


## 6.8 Helper Programs and Modifying Settings
Helper programs and scripts used by RPM reside in `/usr/lib/rpm`. Quite a few, eg. on RHEL 7 system:
```shell
$ ls /usr/lib/rpm | wc -l
73
```
where **wc** repoting number of lines of output.

Can create **`rpmrc`** file to specify default settings for **rpm**. By default, **rpm** looks for:
1. `/usr/lib/rpm/rpmrc`
2. `/etc/rpmrc`
3. `~/.rpmrc`

in above order. Note: all these files read; **rpm** does not stop as soon as it finds that one exists. Alternative **`rpmrc`** file can be specified usinr **`--rcfile`** option.


## 6.9 Queries
All **rpm** inquiries include **`-q`** option, which can be combined with numerous sub-options:
- Which version of a package is installed?

  `$ rpm -q bash`
- Which package did this file come from?

  `$ rpm -qf /bin/bash`
- What files were installed by this package?

  `$ rpm -ql bash`
- Show information about this package.

  `$ rpm -qi bash`
- Show information about this package from the package file, not the package database.

  `$ rpm -qip foo-1.0.0-1.noarch.rpm`
- List all installed packages on this system.

  `$ rpm -qa`

Couple of other useful options: `--require`, `--whatprovides`:
- Return a list of prerequisites for a package:

  `$ rpm -qp --requires foo-1.0.0-1.noarch.rpm`
- Show what installed package provides a particular requisite package:

  `$ rpm -q --whatprovides libc.so.6`


## 6.10 Verifying Packages
**`-V`** option to **rpm** allows you to verify whether files from particular package consistent with system's RPM database. To verify all packages installed on system:
```shell
$ rpm -Va
missing /var/run/pluto
....
S.5....T. c /etc/hba.conf
S.5....T. /usr/share/applications/defaults.list
....L.... c /etc/pam.d/fingerprint-auth
....L.... c /etc/pam.d/password-auth
....
.M....... /var/lib/nfs/rpv-pipefs
....
.....UG.. /usr/local/bin
.....UG.. /usr/local/etc
```
showing just few items. (Note: command can take long time, as it examines all files owned by all packages.)

Output generated only when there is problem.

Each characters displayed denotes result of comparison of attribute(s) of file to value of those attribute(s) recorded in database. Single . (period) means test passed, while single ? (question mark) indicates test could not be performed (eg. file permissions prevent reading). Otherwise, character denotes failure of corresponding verification test:
- **S**: file size differs
- **M**: file permissions and/or type differs
- **5**: MD5 checksum differs
- **D**: device major/minor number mismatch
- **L**: symbolic link path mismatch
- **U**: user ownership differs
- **G**: group ownership differs
- **T**: modification time differs
- **P**: capabilities differ

Note: many verification tests do not indicate problem. Eg. many configuration files modified as system evolves.

If specifying one or more package names as argument, examine only that package:
- No output when everything is OK:

  `$ rpm -V bash`
- Output indicating that a file's size, checksum, and modification time have changed:
  ```shell
  $ rpm -V talk
  S.5....T in.ntalkd.8
  ```
- Output indicating that a file is missing:
  ```shell
  $ rpm -V talk
  missing /usr/bin/talk
  ```


## 6.11


## 6.12


## 6.13


## 6.14


## 6.15


## 6.16


## 6.17


[Back to top](#)

---

[Previous Chapter](../Ch05-packagemanagementsystems/notes_Ch05.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch07-dpkg/notes_Ch07.md)
