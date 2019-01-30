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


## 11.5 System Log Files
System log files -> essential for monitoring/troubleshooting. In Linux, messages appear in various files under `/var/log`. Exact names vary with Linux distribution.

Ultimate control of how messages dealt with -> controlled by **syslogd** (usually **rsyslogd** on modern systems) daemon, common to many UNIX-like operating systems. Newer **systemd**-based systems can use **journalctl** instead,but usually retain **syslogd** and cooperate with it.

Important messages sent not only to logging files, but also to system console window. If not running **X**, or are at virtual terminal, will see them directly there as well. In addition, messages will be copied to `/var/log` messages (or to `/var/log/syslog` on Ubuntu), but if running **X**, have to take some steps to view them.

Can view new messages continuously as new lines appear with:
```shell
$ sudo tail -f /var/log/messages (or /var/log/syslog)
```
or
```shell
$ dmesg -w
```
which shows only kernel-related messages.


## 11.6 Important Log Files in /var/log
Besides looking at log messages in terminal window, can see them using graphical interfaces.

On GNOME desktop, can also access messages by clicking on **`System -> Administration -> System Log`** or **`Applications -> System Tools -> Log File`** Viewer in your Desktop menus, and other desktops have similar links you can locate.

Some important log files found under `/var/log`:

File | Purpose
---- | -------
**`boot.log`** | System boot messages
**`dmesg`** | Kernel messages saved after boot. To see current contents of kernel message buffer, type **dmesg**.
**`messages`** or **`syslog`** | All important system messages
**`secure`** | Security related messages

In order to keep log files from growing without bound, **logrotate** program run periodically, keeps four previous copies (by default) of log files (optionally compressed). Controlled by `/etc/logrotate.conf`.


## 11.7 The /proc and /sys Pseudo-filesystems
`/proc` and `/sys` pseudo-filesystems contain lot of information about system. Many entries in these directory trees writable, can be used to change system behavior. Most cases, requires **root** user.

Pseudo-filesystems because totally exist in memory. If look at disk partition when system not running, there will be only empty directory which is used as mount point.

Information displayed is gathered only when looked at. No constant/periodic polling to update entries.


## 11.8 /proc Basics
`/proc` pseudo-filesystem: long history. Has roots in other UNIX operating system variants. Originally developed to display information about **processes** on system, each of which has own subdirectory in `/proc` with all important process characteristics available.

Over time, grew to contain lot of information about system properties, eg. interrupts, memory, networking, etc. in somewhat anarchistic way. Still extensively used, will often refer to it.


## 11.9 A survey of /proc
What resides in `/proc` pseudo-filesystem:
![lsprocubuntu](/images/lsprocubuntu.png)

First, see there is subdirectory for each process on system, whether sleeping, running, scheduled out. Looking at random one:
![lsproc3589](/images/lsproc3589.png)

Directory full of information about status of process and resources it is using. For example:
![procstatus](/images/procstatus.png)

Other entries give system-wide information. Eg. can see **interrupt** statistics in below screenshot. For each interrupt, see what type it is, how many times it has been handled on each CPU, which devices registered to respond to it. Also get global statistics.
![procinterrupts](/images/procinterrupts.png)


## 11.10 /proc/sys
## 11.11
## 11.12
## 11.13

##

[Back to top](#)

---

[Previous Chapter](../Ch10-apt/notes_Ch10.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch12-processmonitoring/notes_Ch12.md)
