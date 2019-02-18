[Previous Chapter](../Ch24-raid/notes_Ch24.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch26-kernelmodules/notes_Ch26.md)

---

# Chapter 25 Kernel Services and Configuration - Notes

## 25.3 Learning Objectives:
- Grasp the main responsibilities the kernel must fulfill and how it achieves them.
- Explain what parameters can be set on the kernel command line and how to make them effective either for just one system boot, or persistently.
- Know where to find detailed documentation on these parameters.
- Use **sysctl** to set kernel parameters either after the system starts, or persistently across system reboots.


## 25.4 Kernel and Operating System
Narrowly defined, Linux is *only* the **kernel** of the **operating system**, which includes many other components, eg. libraries and applications that interact with the kernel.

Kernel: essential central component that connects hardware to software, and manages system resources eg. memory, CPU time allocation among competing applications/services. Handles all connected devices using **device drivers**, makes devices available for operating system use.

System running ***only*** a kernel has rather limited functionality. Will be found only in dedicated and focused **embedded devices**.




##

[Back to top](#)

---

[Previous Chapter](../Ch24-raid/notes_Ch24.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch26-kernelmodules/notes_Ch26.md)
