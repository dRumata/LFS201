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


## 5.7


## 5.8


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
