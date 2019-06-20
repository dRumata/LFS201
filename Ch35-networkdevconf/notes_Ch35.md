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
- Set IP address to `192.168.1.50` on interface `eth0`:
  ```shell
  $ sudo ifconfig eth0 192.168.1.50
  ```
- Set the *netmask* to 24-bit:
  ```shell
  $ sudo ifconfig eth0 netmask 255.255.255.0
  ```
- Bring interface `eth0` up:
  ```shell
  $ sudo ifconfig eth0 up
  ```
- Bring interface `eth0` down:
  ```shell
  $ sudo ifconfig eth0 down
  ```

Set the **MTU** (<strong>M</strong>aximum <strong>T</strong>ransfer <strong>U</strong>nit)
```shell
$ sudo ifconfig eth0 mtu 1480
```

![ifconfigrhel7](/images/ifconfigrhel7.png)


## 35.8 Problems with Network Device Names
Classic device naming conventions described earlier encountered difficulties, especially when multiple interfaces of same type present. Eg., if two network cards, one named `eth0` and other `eth1`, but which physical device should be associated with each name?

Simplest method: have first device found be `eth0`, second `eth1` etc. Unfortunately, probing for devices not deterministic for modern systems, and devices may be located/plugged in unpredictable order. Thus, one might wind up with Internet interface swapped with local interface. Even if no change in hardware, order in which interfaces located known to vary with kernel version and configuration.

Many system administrators solved this problem in a simple manner: by hardcoding associations between hardware (MAC) addresses and device names in system configuration files and startup scripts. While this method worked for years, required manual tuning + had other problems, eg., when MAC addresses not fixed. Can happen in both embedded and virtualized systems.


## 35.9 Predictable Network Interface Device Names
**Predictable Network Interface Device Names** (**PNIDN**): strongly correlated with use of **udev** and integration with **systemd**. 5 types of names that devices can be given:
1. Incorporating Firmware or BIOS provided index numbers for on-board devices:
   
   Example: `eno1`
2. Incorporating **Firmware** or **BIOS** provided **PCI Express** hotplug slow index numbers:
   
   Example: `ens1`
3. Incorporating physical and/or geographical location of the hardware connection:
   
   Example: `enp2s0`
4. Incorporating the `MAC` address:
   
   Example: `enx7837d1ea46da`
5. Using the old classic method:
   
   Example: `eth0`

## 35.10 Examples of the New Naming Scheme
For example, on machine with two onboard PCI network interfaces that would have been `eth0` and `eth1`:
```shell
$ ip link show | grep enp
2: enp4s2: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo-fast state DOWN mode DEFAULT qlen 1000
3: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo-fast state UP mode DEFAULT qlen 1000
```

These names are correlated with physical locations of the hardware on the PCI system.

Likewise, for wireless device that previously would have been simply named `wlan0`:
```shell
17:/home/coop>ip link show | grep w1
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
```
See same pattern. Easy to turn off new scheme, go back to classic names. Left as research project. In following, will mostly use classic names for definiteness + simplicity.

## 35.11 NIC Configuration Files
While network interfaces can be configured on the fly using either **ip** or **ifconfig** utilities, settings not persistent. Thus, number of Linux distribution-dependent files store persistent network interface and device configuration information.

Each distribution has own set of files and/or directories. Depending on version, might be:

**Red Hat**
```shell
/etc/sysconfig/network
/etc/sysconfig/network-scripts/ifcfg-ethX
/etc/sysconfig/network-scripts/ifcfg-ethX:Y
/etc/sysconfig/network-scripts/route-ethX
```
**Debian**
```shell
/etc/network/interfaces
```
**SUSE**
```shell
/etc/sysconfig/network
```

When using **systemd**, preferable to use Network Manager, rather than try to configure underlying text files. In fact, in new Linux distributions, many of these files non-existent, empty, or much smaller, there only for backward compatibility reasons.

## 35.12 Network Manager
Once upon a time, network connections almost all wired (Ethernet), did not change unless there was significant change to either the hardware, software, or network configuration. During system boot, files in `/etc` consulted to establish all device configurations.

However, modern systems often have dynamic configurations:
- Networks may change as a device is moved from place to place
- Wireless devices may have a large choice of networks to hook into
- Devices may change as hardware such as wireless devices are plugged in or turned on and off

Previously discussed configuration files created to deal with more static situations, very distribution dependent.

**Network Manager** still uses configuration files, but administrator can avoid directly manipulating them. Its use hopefully almost the same on different systems.

##

[Back to top](#)

---

[Previous Chapter](../Ch34-networkaddresses/notes_Ch34.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch36-firewalls/notes_Ch36.md)
