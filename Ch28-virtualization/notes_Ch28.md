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


## 28.4 What Is Virtualization?
In this chapter, will be concerned with creation, deployment, and maintenance of Virtual Machines (VMs).

Virtual Machines: virtualized instance of an entire operating system, may fulfill the role of a **server** or a **desktop/workstation**.

Outside world sees the VM as if it were actual physical machine, present somewhere on network. Applications running in VM generally unaware of their non-physical environment.

Other kinds of virtualizations include:
- **Network**

  Details of actual physical entwork, such as type of hardware, routers, etc. abstracted and need not be known by software running on it and configuring it: Software Defined Networking or SDN.

- **Storage**

  Multiple network storage devices configured to look like one big storage unit, such as disk: Network Attached Storage or NAS.

- **Application**

  Application isolated into standalone format, such as **container**, which will be discussed later.

There are differences between physical and virtual machines that are not always easy to ignore. Eg. performance tuning at low level needs to be done (separately) on both VM and physical machine residing underneath it.


## 28.5 Virtualization History
**Virtualization** has long proud history. Implemented originally on mainframes decades ago:
- Enables better hardware utilization
- Operating systems often progress more quickly than hardware
- It is microcode driven
- Not particularly user-friendly

Later on, virtualization technology migrated to PCs and workstations:
- Initially, it was done using **Emulation**
- CPUs enhanced to support virtualization led to boost in performance, easier configuration, more flexibility in VM installation and migration

From early **mainframes** to **mini-computers**, virtualization has been used for expanding limit, debugging and administration enhancements.

Today, virtualization found everywhere in many forms. Each of the different forms and implementations that are available provide particular advantages.


## 28.6 Hosts and Guests
**Host**: underlying physical operating system managing one or more virtual machines.

**Guest**: the VM which is an instance of a complete operating system, running one or more applications. Sometimes, guest also called **client**. In most cases, guest should not care what host it is running on, can be **migrated** from one host to another, sometimes while actually running.

In fact, possible to convert physical machines to virtual ones, by copying the entire contents into a VM. Specialized software utilities can make this easier.

Low-level performance tuning on areas such as CPU utilization, networking throughput, memory utilization, often best done on host, as guest may have only simulated quantities not directly useful.

Application tuning done most on guest.


## 28.7 Emulators
First implementations of virtualization on PC architecture -> through the use of **emulators**. Application running on current operating system would appear to another OS as specific hardware environment. Emulators generally do not require special hardware to operate.

Qemu -> one such emulator.

![virt-emu](/images/virt-emu.png)
**Emulator**


## 28.8 Emulation vs. Virtualization
An Emulator runs completely in software. Hardware constructs replaced by software. Useful for running virtual machines on different architectures, eg. running pretend ARM guest machine on X86 host. Emulation often used for developing operating system for new CPU, even before hardware is available. Performance relatively slow.


## 28.9 Types of Virtualization Hypervisors



##

[Back to top](#)

---

[Previous Chapter](../Ch27-devicesudev/notes_Ch27.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch29-containers/notes_Ch29.md)
