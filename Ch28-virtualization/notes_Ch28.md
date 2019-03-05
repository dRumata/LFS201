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

![virt-emu](/images/virt-emu.jpg)
**Emulator**


## 28.8 Emulation vs. Virtualization
An Emulator runs completely in software. Hardware constructs replaced by software. Useful for running virtual machines on different architectures, eg. running pretend ARM guest machine on X86 host. Emulation often used for developing operating system for new CPU, even before hardware is available. Performance relatively slow.


## 28.9 Types of Virtualization Hypervisors
Host system (besides functioning normally with respect to software that it runs) also acts as hypervisor that initiates, terminates, manages guests. Also called **Virtual Machine Monitor** (**VMM**).

Two basic methods of virtualization:
- **Hardware virtualization** (also known as **Full Virtualization**)

  Guest system runs without being aware it is running as virtualized guest, does not require modifications to be run in this fashion.

- **Para-virtualization**

  Guest system is aware it is running in virtualized environment, has been modified specifically to work with it.

Recent CPUs from Intel and AMD incorporate virtualization extensions to the x86 architecture that allow the hypervisor to run fully virtualized (ie. unmodified) guest operating systems with only minor performance penalties.

The Intel extension (Intel Virtualization Technology), usually abbreviated as VT, IVT, VT-32, or VT-64, also known under the development code name of Vanderpool. Has been available since the spring of 2005.

The AMD extension usually called AMD-V, still sometimes referred to by the development code name of Pacifica.

For detailed explanation and comparison of how these two extensions work, see [the Xen and the new processors article](https://lwn.net/Articles/182080/).

Can check directly if your CPU supports hardware virtualization extensions by looking at `/proc/cpuinfo`. If you have an IVT-capable chip, will see **`vmx`** in **`flags`** field. If you have an AMD-V capable chip, will see **`svm`** in same field. May also have to ensure virtualization capability is turned on in your CMOS.

While choice of operating systems tends to be more limited for para-virtualized guests, originally they tended to run more efficiently than fully virtualized guests. Recent advances in virtualization techniques have narrowed or eliminated such advantages, and the wider availability of the hardware support needed for full virtualization has made para-virtualization less advantageous and less popular.

Most modern hardware has hardware virtualization abilities (must be turned on in BIOS).


## 28.10 External and in-Kernel Hypervisors
Hypervisor can be:
- External to the host operating system kernel: VMware
- Internal to the host operating system kernel: KVM

In this course, will concentrate on KVM, as it is all open source, and requires no external third party hypervisor program.


## 28.11 Dedicated Hypervisor
Going past emulation, merging of hypervisor program into specially-designed lightweight kernel was next step in Virtualization deployment.

VMware ESX (and related friends): an example of hypervisor embedded into operating system.

![virt-hyper](/images/virt-hyper.jpg)
**Dedicated Hypervisor**


## 28.12 Hypervisor in the Kernel
The KVM project added hypervisor capabilities into the Linux kernel.

As discussed, specific CPU chip functions and facilities were required and deployed for this type of virtualization.

![virt-kvm](/images/virt-kvm.jpg)
**Hypervisor in the Kernel**


## 28.13 libvirt
The libvirt project: toolkit to interact with virtualization technologies


##

[Back to top](#)

---

[Previous Chapter](../Ch27-devicesudev/notes_Ch27.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch29-containers/notes_Ch29.md)
