[Previous Chapter](../Ch34-networkaddresses/notes_Ch34.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch36-firewalls/notes_Ch36.md)

---

# Chapter 35 Network Devices and Configuration - Notes

## 35.2 Introduction
Network devices such as Ethernet, wireless connections require careful configuration, especially when there are multiple devices of same type. Consistent, persistent device naming can become tricky in such circumstances. Recent adoption of new schemes -> naming more predictable. Number of important utilities used to bring devices up/down, configure properties, establish routes etc. System administrators must become adept at their use.

## 35.3 Learning Objectives:
- Identify network devices and understand how the operating system names them and binds them to specific duties.
- Use the **ip** utility to display and control devices, routing, policy-based routing, and tunneling.
- Use the older **ifconfig** to configure, control, and query network interface parameters from either the command line or from system configuration scripts.
- Understand the Predictable Network Interface Device Names scheme.
- Know the main network configuration files in `/etc`.
- Use **Network Manager** (**nmtui** and **nmcli**) to configure network interfaces in a distribution-independent manner.
- Know how to set default routes and static routes.
- Configure name resolution as well as run diagnostic utilities.


## 35.4 Network Devices
Network devices *not* associated with **special device files** (also known as **device nodes**), unlike block/character devices. Know by their names rather than having associated entries in `/dev` directory.

Names consist of type identifier followed by number:
- **`eth0`**, **`eth1`**, **`eno1`**, **`eno2`**, etc. for Ethernet devices
- **`wlan0`**, **`wlan1`**, **`wlan2`**, **`wlp3s0`**, **`wlp3s2`**, etc. for wireless devices
- **`br0`**, **`br1`**, **`br2`**, etc. for bridge interfaces
- **`vmnet0`**, **`vmnet1`**, **`vmnet2`**, etc. for virtual devices for communicating with virtual clients

Historically, multiple virtual devices could be associated with single physical devices.


## 35.5 ip
**ip**: the command line utility used to configure, control, query interface parameters and control devices, routing, etc. Preferred to the venerable **ifconfig** discussed next.


##

[Back to top](#)

---

[Previous Chapter](../Ch34-networkaddresses/notes_Ch34.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch36-firewalls/notes_Ch36.md)
