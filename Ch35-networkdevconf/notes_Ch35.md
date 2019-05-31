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
**ip**: the command line utility used to configure, control, query interface parameters and control devices, routing, etc. Preferred to the venerable **ifconfig** discussed next, since more versatile + more efficient because it uses **netlink** sockets rather than **ioctl** system calls.

**ip** can be used for wide variety of tasks. Can be used to configure, control, query devices and interface parameters. Also manipulate routing, policy-based routing, tunneling.

Basic syntax:
```shell
ip [ OPTIONS ] OBJECT { COMMAND | help }
ip [ -force ] -batch filename 
```
where second form can read commands from designated file.

**ip** a multiplex utility. `OBJECT` argument describes what kind of action going to be performed. Possible `COMMANDS` depend on which `OBJECT` selected.

Some of the main values of `OBJECT`:

**Main ip `object`s**

`OBJECT` | Function
-------- | --------
`address` | **IPv4** or **IPv6** protocol device address
`link` | Network Devices
`maddress` | Multicast Address
`monitor` | Watch for netlink messages
`route` | Routing table entry
`rule` | Rule in the routing policy database
`tunnel` | Tunnel over IP


## 36.6 Examples of Using ip
**ip** utility can be used in many ways:
- Show information for all network interfaces:
  ```shell
  $ ip link show
  ```
- Show information for `eth0` network interface, including statistics:
  ```shell
  $ ip -s link show eth0
  ```
- Set IP address for `eth0`:
  ```shell
  $ sudo ip addr add 192.168.1.7 dev eth0
  ```
- Bring `eth0` down:
  ```shell
  $ sudo ip link set eth0 down
  ```
- Set **MTU** to 1480 bytes for `eth0`:
  ```shell
  $ sudo ip link set eth0 mtu 1480
  ```
- Set networking route:
  ```shell
  $ sudo ip route add 172.16.1.0/24 via 192.168.1.5
  ```
  
![ipubuntu](/images/ipubuntu.png)


## 35.7 ifconfig
**ifconfig**: system administration utility long found in UNIX-like operating systems, used to configure, control, query network interface parameters from either command line or from system configuration scripts. Superseded by **ip**, some Linux distributions no longer install by default. Some usage examples:
- Display some information about all interfaces:
  ```shell
  $ ifconfig
  ```
- Display information about only `eth0`:
  ```shell
  $ ifconfig eth0
  ```
- Set IP address to `192.168.1.50`
  ```shell

  ```
- 
  ```shell

  ```
- 
  ```shell

  ```
- 
  ```shell

  ```


##

[Back to top](#)

---

[Previous Chapter](../Ch34-networkaddresses/notes_Ch34.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch36-firewalls/notes_Ch36.md)
