[Previous Chapter](../Ch40-backuprecovery/notes_Ch40.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch42-localsecurity/notes_Ch42.md)

---

# Chapter 41 Linux Security Modules - Notes

## 41.3 Learning Objectives:
- Understand how the Linux Security Module framework works and how it is deployed.
- List the various LSM implementations available.
- Delineate the main features of SELinux.
- Explain the different modes and policies available.
- Grasp the importance of contexts and how to get and set them.
- Know how to use the important SELinux utility programs.
- Gain some familiarity with AppArmor.

## 41.4 What Are Linux Security Modules?
A modern computer system must be made secure, but needs vary according to sensitivity of data, number of users with accounts, exposure to outside networks, legal requirements, and other factors. Resposibility for enabling good security controls falls both on application designers and the Linux kernel developers and maintainers. Users should have to follow good procedures as well, but on a well run system, non-privileged users should have very limited ability to expose system to security violations. In this section, concerned with how Linux kernel enhances security through use of Linux Security Modules framework, particularly with deployment of SELinux. Idea is to implement **mandatory access controls** over variety of requests made to kernel, but to do so in a way that:
1. Minimizes changes to the kernel
2. Minimizes overhead on the kernel
3. Permits flexibility and choice between different implementations, each of which is presented as a self-contained **LSM** (<strong>L</strong>inux <strong>S</strong>ecurity <strong>M</strong>odule).

Basic idea to **hook system calls**; insert code wherever an application requests transition to kernel (system) mode in order to accomplish work that requires enhanced abilities; this code makes sure permissions are valid, malicious intent is protected against, etc. Does this by invoking security-related functional steps before and/or after a system call is fulfilled by kernel.

## 41.5 LSM Choices
For a long time, only enhanced security model implemented was **SELinux**. When project was first floated upstream in 2001 to be included directly in kernel, there were objections about using only one approach to enhanced security.

As a result, LSM approach was adopted, where alternative modules to SELinux could be used as they were developed and was incorporated into Linux kernel in 2003.

Current LSM implementations:
- [SELinux](https://selinuxproject.org/page/Main_Page)
- [AppArmor](https://gitlab.com/apparmor)
- [Smack](http://schaufler-ca.com/)
- [Tomoyo](https://tomoyo.osdn.jp)

Only one LSM can be used at a time, as they potentially modify the same parts of the Linux kernel.

Will concentrate primarily on SELinux and secondarily on AppArmor in order of usage volume.

## 41.6 SELinux Overview
SELinux originally developed by United States NSA (<strong>N</strong>ational <strong>S</strong>ecurity <strong>A</strong>dministration)
 and has been integral in RHEL for a very long time, which has brought it a large usage base.

 Operationally, SELinux is a set of security rules that are used to determine which processes can access which files, directories, ports, and other items on the system.

 Works with three conceptual quantities:
 1. **Contexts**: Are labels to files, processes, and ports. Examples of contexts are SELinux user, role, and type.
 2. **Rules**: Describe access control in terms of contexts, processes, files, ports, users, etc.
 3. **Policies**: Are a set of **rules** that describe what system-wide access control decisions should be made by SELinux.

 A SELinux context is a name used by a rule to define how users, processes, files, and ports interact with each other. As the default policy is to deny any access, rules are used to describe allowed actions on the system.

## 41.7 SELinux Modes
SELinux can be run under one of the three following modes:
- **Enforcing**: All SELinux code is operative and access is denied according to policy. All violations are audited and logged.
- **Permissive**: Enables SELinux code, but only audits and warns about operations that would be denied in enforcing mode.
- **Disabled**: Completely disables SELinux kernel and application code, leaving the system without any of its protections.

These modes are selected (and explained) in a file (usually `/etc/selinux/config`) whose location varies by distribution (it is often either at `/etc/sysconfig/selinux` or linked from there). The file is well self-documented. The **sestatus** utility can display the current mode and policy.

![SELinus_Mode_Enforcing_large](/images/SELinus_Mode_Enforcing_large.png) **SELinux Enforcing Mode**

![SELinus_Mode_Permissive_large](/images/SELinus_Mode_Permissive_large.png) **SELinux Permissive Mode**

To examine or set current mode, one can use **getenforce** and **setenforce**:
```shell
$ getenforce
Disabled
$ sudo setenforce Permissive
$ getenforce
Permissive
```

**setenforce** can be used to switch between **enforcing** and **permissive** modes on the fly while system is in operation. However, changing in or out of the **disabled** mode cannot be done this way. While **setenforce** allows you to switch between **permissive** and **enforcing** modes, it does not allow you to disable SELinux completely. There are at least two different ways to disable SELinux:
- **Configuration file**

  Edit the SELinux configuration file (usually `/etc/selinux/config`) and set **`SELINUX=disabled`**. This is the default method and should be used to permanently disable SELinux.

- **Kernel parameter**

  Add **`selinux=0`** to the kernel parameter list when rebooting.

However, important to note that disabling SELinux on systems in which SELinux will be re-enabled is not recommended. Preferable to use the **permissive** mode instead of disabling SELinux, so as to avoid relabeling the entire filesystem, which can be time-consuming.

## 41.8 SELinux Policies
The same configuration file, usually `/etc/sysconfig/selinux`, also sets the **SELinux policy**. Multiple policies are allowed, but only one can be active at a time. Changing the policy may require a reboot of the system and a time-consuming re-labeling of filesystem contents. Each policy has files which must be installed under `/etc/selinux/[SELINUXTYPE]`.

Most common policies:
- **targeted**

  The **default** policy in which SELinux is more restricted to targeted processes. User processes and **init** processes are not targeted. SELinux enforces memory restrictions for **all** processes, which reduces the vulnerability to buffer overflow attacks.
- **minimum**

  A modification of the targeted policy where only selected processes are protected.
- **MLS**

  The Multi-Level Security policy is much more restrictive; all processes are placed in fine-grained security domains with particular policies.

##



##

[Back to top](#)

---

[Previous Chapter](../Ch40-backuprecovery/notes_Ch40.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch42-localsecurity/notes_Ch42.md)
