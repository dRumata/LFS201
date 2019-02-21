[Previous Chapter](../Ch25-kernelservices/notes_Ch25.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch27-devicesudev/notes_Ch27.md)

---

# Chapter 26 Kernel Modules - Notes

## 26.2 Introduction
Linux kernel makes extensive use of **modules**, which contains important software that can be loaded/unloaded as needed after system starts. Many modules incorporate **device drivers** to control hardware either inside system, or attached peripherally. Other modules can control network protocols, support different filesystem types, and many other purposes. Parameters can be specified when loading modules to control their behavior. End result: great flexibility and agility in responding to changing conditions and needs.

## 26.3 Learning Objectives:
- List the advantages of utilizing kernel modules.
- Use **insmod**, **rmmod**, and **modprobe** to load and unload kernel modules.
- Use **modinfo** to find out information about kernel modules.




##

[Back to top](#)

---

[Previous Chapter](../Ch25-kernelservices/notes_Ch25.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch27-devicesudev/notes_Ch27.md)
