[Previous Chapter](../Ch07-dpkg/notes_Ch07.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch09-zypper/notes_Ch09.md)

---

# Chapter 8 YUM - Notes

## 8.2 Introduction
**yum** program provides higher level of intelligent services for using underlying **rpm** program. Can automatically resolve dependencies when installing, updating, removing packages. Accesses external software **repositories**, synchronizing with them, retrieving/installing software as needed.

## 8.3 Learning Objectives:
- Discuss package installers and their characteristics.
- Explain how **yum** works as a high level package management system.
- Configure **yum** to use repositories.
- Discuss the queries **yum** can be used for.
- Verify, install, remove, and upgrade packages using **yum**.
- Learn about additional commands and how to install new repositories.
- Understand how to use **dnf**, which has replaced **yum** on Fedora.


## 8.4 Package Installers
Lower-level package utilities (eg. **rpm**, **dpkg**) deal with details of installing specific software package files. managing already installed software.

Higher-level package **management systems** (eg. **yum**, **dnf**, **apt**, **zypper**) work with databases of available software, incorporate tools needed to find, install, update, uninstall software in highly intelligent fashion.
- Can use both local/remote repositories as source to install/update binary as well as source software packages
- Used to automate install, upgrade, removal of software packages
- Resolve dependencies automatically
- Save time because no need to either download packages manually/search out dependency information separately

Software repositories provided by distributions/other independent software providers. Package installers maintain databases of available software derived from catalogs kept by repositories. Unlike low-level package tools, have ability to find/install dependencies automatically -> critical feature.

In this section, discuss **yum** and **dnf**. **zypper** and **apt** discussed in later chapters.


## 8.5 What is yum?
**yum** provides frontend to **rpm**. Primary task: fetch packages from multiple remote repositories, resolve dependencies among packages. Used by majority (but not all) of distributions using **rpm**, including RHEL, CentOS, Scientific Linux, Fedora.

**yum** caches information + databases to speed up performance. To remove some or all cached information, can run command:
```shell
$ yum clean [ packages | metadata | expire-cache | rpmdb | plugins | all ]
```
**yum** has number of modular expressions (plugins) + companion programs that can be found under `/usr/bin/yum*` and `/usr/sbin/yum*`.

Will concentrate on command line use of **yum**, not consider graphical interfaces distributions provide.


## 8.6 Configuring yum to Use Repositories
Repository configuration files kept in `/etc/yum.repos.d`, have **`.repo`** extension. Eg. on one RHEL 7 system:
![yumrepos](/images/yumrepos.png)

Note: on RHEL 6 there is no **`redhat.repo`** file. RHEL 6 + earlier versions handled distribution-supplied repos in somewhat different manner, although RHEL clones like CentOS used conventional repos for main distribution packages.


## 8.7 Repository Files
Very simple repository file may look like:
<strong>
```shell
[repo-name]
    name=Description of the repository
    baseurl=http://somesystem.com/path/to/repo
    enabled=1
```
</strong>
More complicated examples found in `/etc/yum.repos.d`, would be good idea to examine them.

Can toggle the use of particular repository on/off by changing value of enabled to 1/0, or using **`--disablerepo=somerepo`** and **`--enablerepo=somerepo`** options when using **yum**.

Can (but should not) also turn off integrity checking with **`gpgcheck`** variable.

## 8.8 Queries
Like **rpm**, **yum** can be used for queries such as searches. However, can search not just what is present on local system, but also inquire about remote repositories. Examples:
- Search for packages with **`keyword`** in name:
  ```shell
  $ sudo yum search keyword
  $ sudo yum list "*keyword*"
  ```
  These two commands give somewhat different information. First one tells more about packages, second one makes it clearer what is installed, what else is available.

- Display information about a package:
  ```shell
  $ sudo yum info package
  ```
  Information includes size, version, what repository it came from, source URL, longer description. Wildcards can be given, eg. **`yum info "libc*"`** for this + most **yum** commands. Note: package need not be installed, unlike queries make with **`rpm -q`**.


## 8.9
## 8.10
## 8.11
## 8.12

##

[Back to top](#)

---

[Previous Chapter](../Ch07-dpkg/notes_Ch07.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch09-zypper/notes_Ch09.md)
