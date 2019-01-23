[Previous Chapter](../Ch04-signals/notes_Ch04.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch06-rpm/notes_Ch06.md)

---

# Chapter 5 Package Management Systems - Notes

## 5.3 Learning Objectives:
- Explain why software package management systems are necessary.
- Understand the function of both binary and source packages.
- Enumerate the main available package management systems.
- Understand why two levels of utilities are needed: one that deals with just bare packages, and one that deals with dependencies among packages.
- Explain how creating your own package enhances the control you have over exactly what goes in software and how it is installed.
- Understand the role of source control systems, and git in particular.


## 5.4 Software Packaging Concepts
**Package management systems** supply tools that allow system administrators to automate installing, upgrading, configuring and removing software packages in known, predictable, consistent manner. These systems:
- Gather and compress associated software files into single package (archive), which may require one or more other packages to be installed first.
- Allow for easy software installation or removal
- Can verify file integrity via internal database
- Can authenticate origin of packages
- Facilitate upgrades
- Group packages by logical features
- Manage dependencies between packages

Given package may contain executable files, data files, documentation, installation scripts, configuration files. Also included -> **metadata** attributes such as version numbers, checksums, vendor information, dependencies, descriptions, etc.

Upon installation, all information stored locally into internal database, which can be queried for version status and update information.


## 5.5 Why Use Packages?
Software package management systems widely seen as one of biggest advancements Linux brought to enterprise IT environments. By keeping track of files, metadata in automated, predictable, reliable way, system administrators can use package management systems to make installation processes scale to thousands of systems without requiring manual work on each individual system. Included features:
- Automation: No need for manual installs and upgrades
- Scalability: Install packages on one system, or 10,000 systems
- Repeatability and predictability
- Security and auditing


## 5.6 Package Types
Several different types of packages:
- **Binary** packages contain files ready for deployment, including executable files and libraries. Architecture-dependent, must be compiled for each type of machine
- **Source** packages used to generate binary packages. Should always be able to rebuild binary package (eg. by using **`rpmbuild --rebuild`** on **RPM**-based systems) from source package. One source package can be used to multiple architectures
- **Architecture-independent** packages contain files, scripts that run under script interpreters, + documentation, configuration files
- **Meta-packages**: essentially groups of associated packages that collect everything needed to install relatively large subsystem, eg. desktop environement, office suite, etc.

Binary packages -> ones that system administrators have to deal with most of the time.

On 64-bit systems that can run 32-bit programs, may have two binary packages installed for  given program, one with **x86-64** or **amd64** in name, and other with **i386** or **i686** in name.

Source packages helpful in keeping track of changes and source code used to come up with binary packages. Usually not installed on system by default, but can always be retrieved from vendor.


## 5.7 Available Package Management Systems
Two very common package management systems:
1. **RPM** (**Red Hat Package Manager**): system used by all Red Hat-derived distributions (eg. Red Hat Enterprise Linux, CentOS, Scientific Linux, SUSE and its related community openSUSE distribution)
2. **dpkg** (**Debian Package**): system used by all Debian-derived distributions, including Debian, Ubuntu, Linux Mint.

Other package management systems: **portage/emerge** used by Gentoo, **pacman** used by Arch, specialized ones used by Embedded Linux systems and Android.

Another ancient system: supply packages as **tarballs** without any real management or clean removal strategies. Approach still marks Slackware, one of oldest Linux distributions.

Most of time, either **RPM** or **dpkg**, only ones considered in course.
![RPM_logo](/images/RPM_Logo.png)
![apt](/images/apt.png)

## 5.8 Packaging Tool Levels and Varieties
Two levels to packaging systems:
1. **Low Level Utility**: simply installs/removes single package, or list of packages, each one individually/specifically named. Dependencies not fully handled, only warned about:
    - If another package needs to be installed, first installation will fail
    - If package needed by another package, removal will fail

    **rpm** and **dpkg** utilities play this role for packaging systems that use them.

2. **High Level Utility**: solves dependency problems:
    - If another package/group of packages needs to be installed before software can be installed, such needs will be satisfied
    - If removing package interferes with another installed package, administrator given choice of aborting or removing all affected software

    **yum**, **dnf**, **zypper** and Package Kit utilities take care of dependency resolution for rpm systems, **apt**, **apt-cache** and other utilities take care of it for dpkg systems.

In course, only discuss command line interface to each packaging systems. Graphical frontends used by each Linux distribution *can* be useful, would like to be less tied to any one interface, have more flexibility.


## 5.9


## 5.10


## 5.11


## 5.12


## 5.13


## 5.14


## 5.15


[Back to top](#)

---

[Previous Chapter](../Ch04-signals/notes_Ch04.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch06-rpm/notes_Ch06.md)
