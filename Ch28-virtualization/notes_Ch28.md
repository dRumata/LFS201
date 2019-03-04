[Previous Chapter](../Ch27-devicesudev/notes_Ch27.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch29-containers/notes_Ch29.md)

---

# Chapter 28 Virtualization Overview - Notes

## 28.2 Introduction
**Virtualization** entails creating (in software) an abstracted complete machine environment, under which end user software runs unaware of the physical details of the machine it is running on.

Quite a few approaches to accomplish this mission, but generally involve host operating system and filesystem which directly uses hardware. One or more guest systems run on top (or underneath, depending on how you look at it) of host system at lower level of privilege. Access to hardware such as network adapters usually done through some kind of virtual device, which may access physical device when required.

Many uses for virtual machine. Major ones: more efficient use of hardware, software isolation, security, stability, safe development options, ability to run multiple operating systems at same time without rebooting.

## 28.3 Learning Objectives:
- Understand the concepts behind **virtualization** and how it came to be widely used.
- Understand the rules of **hosts** and **guests**.
- Discuss the difference between **emulation** and **virtualization**.
- Distinguish between the different types of **hypervisors**.
- Be familiar with how Linux distributions use and depend on **libvirt**.
- Use the qemu hypervisor.
- Install, use, and manage KVM.


##

[Back to top](#)

---

[Previous Chapter](../Ch27-devicesudev/notes_Ch27.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch29-containers/notes_Ch29.md)
