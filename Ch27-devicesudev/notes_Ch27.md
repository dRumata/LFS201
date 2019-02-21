[Previous Chapter](../Ch26-kernelmodules/notes_Ch26.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch28-virtualization/notes_Ch28.md)

---

# Chapter 27 Devices and udev - Notes

## 27.2 Introduction
Linux uses **udev**, an intelligent apparatus for discovering hardware and peripheral devices both during boot, and later when they are connected to the system. **Device nodes** are created automatically, and then used by applications/operating system subsystems to communicate with + transfer data to/from devices. System administrators can control how **udev** operates and craft special **udev** rules to assure desired behavior results.


## 27.3 Learning Objectives:
- Explain the role of **device nodes** and how they use **major** and **minor** numbers.
- Understand the need for the **udev** method and list its key components.
- Describe how the **udev** device manager functions.
- Identify **udev** rule files and learn how to create custom rules.




##

[Back to top](#)

---

[Previous Chapter](../Ch26-kernelmodules/notes_Ch26.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch28-virtualization/notes_Ch28.md)
