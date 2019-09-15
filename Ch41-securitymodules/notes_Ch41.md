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




##

[Back to top](#)

---

[Previous Chapter](../Ch40-backuprecovery/notes_Ch40.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch42-localsecurity/notes_Ch42.md)
