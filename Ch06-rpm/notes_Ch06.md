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


## 6.7


## 6.8


## 6.9


## 6.10


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
