[Previous Chapter](../Ch10-apt/notes_Ch10.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch12-processmonitoring/notes_Ch12.md)

---

# Chapter 11 System Monitoring - Notes

## 11.3 Learning Objectives:
- Understand the concept of inventory and gain familiarity with available system monitoring tools.
- Understand where the system stores log files and examine the most important ones.
- Use the `/proc` and `/sys` pseudo-filesystems.
- Use **sar** to father system activity and performance data and create reports that are readable by humans.


## 11.4 Available Monitoring Tools
Linux distributions comes with many standard performance/profiling tools already installed. Many familiar from other UNIX-like operating systems, while some developed specifically for Linux.

Most tools make use of mounted **pseudo-filesystems**, especially `/proc` and `/sys`, both which have already been discussed while examining filesystems/kernel configuration. Will look at both.

Also a number of graphical system monitors that hide many details, but will only consider command line tools in course.

Before considering main utilities in detail, can see summary on next few sections, broken down by type: note: some utilities have overlapping domains of coverage. Will revisit tables in following chapters that focus on specific topics.

Summary of main process monitoring utility tools:

**Process and Load Monitoring Utilities**
Utility | Purpose | Package
------- | ------- | -------
**top** | Process activity, dynamically updated | **procps**
**uptime** | How long system is running and average load | **procps**
**ps** | Detailed information about processes | **procps**
**pstree** | Tree of processes and their connections | **psmisc** (or **pstree**)
**mpstat** | Multiple processor usage | **sysstat**
**iostat** | CPU utilization and I/O statistics | **sysstat**
**sar** | Display and collect information about system activity | **sysstat**
**numstat** | Information about **NUMA** (Non-Uniform Memory Architecture) | **numactl**
**strace** | Information about all system calls a process makes | **strace**

**Memory Monitoring Utilities**
Utility | Purpose | Package
------- | ------- | -------
**free** | Brief summary of memory usage | **procps**
**vmstat** | Detailed virtual memory statistics and block I/O, dynamically updated | **procps**
**pmap** | Process memory map | **procps**

**I/O Monitoring Utilities**
Utility | Purpose | Package
------- | ------- | -------
**iostat** | CPU utilization and I/O statistics | **sysstat**
**sar** | Display and collect information about system activity | **sysstat**
**vmstat** | Detailed virtual memory statistics and block I/O, dynamically updated | **procps**

**Network Monitoring Utilities**
Utility | Purpose | Package
------- | ------- | -------
**netstat** | Detailed networking statistics | **netstat**
**iptraf** | Gather information on network interfaces | **iptraf**
**tcpdump** | Detailed analysis of network packets and traffic | **tcpdump**
**wireshark** | Detailed network traffic analysis | **wireshark**


## 11.5



## 11.6
## 11.7
## 11.8
## 11.9
## 11.10
## 11.11
## 11.12
## 11.13

##

[Back to top](#)

---

[Previous Chapter](../Ch10-apt/notes_Ch10.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch12-processmonitoring/notes_Ch12.md)
