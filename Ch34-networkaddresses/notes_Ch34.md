[Previous Chapter](../Ch33-pam/notes_Ch33.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch35-networkdevconf/notes_Ch35.md)

---

# Chapter 34 Network Addresses - Notes

## 34.3 Learning Objectives:
- Differentiate between different types of IPv4 and IPv6 addresses.
- Understand the role of netmasks.
- Get, set, and change the hostname, based on the system you are using.


## 34.4 IP Addresses
**IP addresses** used globally to uniquely identify nodes across internet. Registered through <strong>ISP</strong>s (<strong>I</strong>nternet <strong>S</strong>ervice <strong>P</strong>roviders).

IP address is the number that identifies your system on the network. Comes in two varieties:
- **IPv4**: A 32-bit address, composed of 4 **octets** (an octet is just 8 bits, or a byte)

  Example: **`148.114.252.10`**
- **IPv6**: A 128-bit address, composed of 8 16-bit octet pairs.

  Example: **`2003:0db5:6123:0000:1f4f:0000:5529:fe23`**

In either case, set of **reserved** addresses also included. Will focus somewhat more on IPv4, as it is still what is most commonly used.


## 34.5 IPv4 Address Types
IPv4 address types include:
- **Unicast**: an address associated with specific host. Might be something like **`140.211.169.4`** or **`64.254.248.193`**
- **Network**: an address whose **host** portion is set to all binary zeroes. Ex. **`192.168.1.0`** (the host portion can be the last 1-3 octets as discussed later; here it is just the last octet)
- **Broadcast**: an address to which each member of a particular network will listen. Will have the host portion set to all 1 bits, such as in **`172.16.255.255`** or **`148.114.255.255`** or **`192.168.1.255`** (Host portion is last two octets in the first two cases, just the last one in the third case)
- **Multicast**: an address to which approximately configured nodes will listen. The address **`224.0.0.2`** is an example of a multicast address. Only nodes specifically configured to pay attention to specific multicast address will interpret packets for that multicast group


## 34.6 Reserved Addresses
Certain addresses and address ranges are reserved for special purposes:
- **`127.x.x.x`**: reserved for loopback (local system) interface, where **`0 <= x <= 254`**. Generally, **`127.0.0.1`**
- **`0.0.0.0`**: used by systems that do not yet known their own address. Protocols like DHCP and BOOTP use this address when attempting to communicate with a server
- **`255.255.255.255`**: generic broadcast private address, reserve for internal use. These addresses are never assigned or registered to anyone. Generally not routable
- Other examples of reserved address ranges include:

  **`10.0.0.0`** - - **`10.255.255.255`**

  **`172.16.0.0`** - - **`172.31.255.255`**

  **`192.168.0.0`** - - **`192.168.255.255`**

  etc.

  Each of these has purpose. For example, the familiar address range **`192.168.x.x`** is used only for local communications within a private network.

Can see long list of reserved addresses for both IPv4 and IPv6 on the [Reserved IP addresses Wikipedia page](https://en.wikipedia.org/wiki/Reserved_IP_addresses).

![ID_addresses_large](/images/ID_addresses_large.png)
**Private vs. Public IP addresses**


## 34.7 IPv6 Address Types
IPv6 address types include:
- **Unicast**: packet delivered to one interface
  - **Link-local**: auto-configured to for every interface to have one. Non-routable
  - **Global**: dynamically or manualle assigned. routable
  - Reserved for documentation
- **Multicast**: a packet is delivered to multiple interfaces
- **Anycast**: a packet is delivered to the nearest of multiple interfaces (in terms of routing distance)
- **IPv4-mapped**: an IPv4 address mapped to IPv4. For example, **`::FFFF:a.b.c.d/96`**

In addition, IPv6 has some special types of addresses such as loopback, which is assigned to the **`lo`** interface, as **`::1/128`**.


## 34.8 IPv4 Address Classes
Historically, IP addresses based on defined **classes**. Classes A, B, C used to distinguish network portion of address from host portion of address. This is used for routing purposes.

**Address Classes**

Network Class | Highest order octet range | Notes
------------- | ------------------------- | -----
A | 1-127 | 128 networks, 16,772,214 hosts per network, 127.x.x.x reserved for loopback
B | 128-191 | 16,384 networks, 65,534 hosts per network
C | 192-223 | 2,097,152 networks, 254 hosts per network
D | 224-239 | Multicast addresses
E | 240-254 | Reserved address range


## 34.9 Netmasks
**Netmask** used to determine how much of address used for network portion and how much for host portion, as seen. Also used to determine network/broadcast addresses.

**Address Classes and Netmasks**

Network Class | Decimal | Hex | Binary
------------- | ------- | --- | ------
A | **`255.0.0.0`** | **`ff:00:00:00`** | **`11111111 00000000 00000000 00000000`**
B | **`255.255.0.0`** | **`ff:ff:00:00`** | **`11111111 11111111 00000000 00000000`**
C | **`255.255.255.0`** | **`ff:ff:ff:00`** | **`11111111 11111111 11111111 00000000`**

Class A addresses use 8 bits for network portion of address and 24 bits for host portion of address.

Class B addresses use 16 for network, 16 for host.

Class C addresses use 24 for network, 8 for host.

Class D addresses used for multicasting.

Class E addresses currently not used.

Network address obtained by **anding** (logical and - &) IP address with netmask. Interested in network addresses because they define local network which consists of collection of nodes connected via same media and sharing same network address. All nodes on same network can directly see each other.

**Example:**
```shell
172.16.2.17  ip address
&255.255.0.0  netmask
-----------------
172.16.0.0  network address
```


## 34.10 Hostname
**Hostname**: simply a label used to identify networked device to distinguish from other elements on network. Historically, also been called nodename.

For DNS purposes, hostnames appended with period (dot) and domain name, so that machine with hostname of **`antje`** could have **fully qualified domain name (FQDN)** of **`antje.linuxfoundation.org`**.

Hostname generally specified at installation time, can be modified at any time later.


## 34.11 Getting and Setting a Hostname
At any given time, ascertaining hostname as simple as:
```shell
$ hostname
wally
```
Changing hostname involved giving parameter, requires root privilege:
```shell
$ sudo hostname lumpy
lumpy
```
Current value always stored in `/etc/hostname` on most Linux distributions.

Changing hostname in this fashion -> not persistent; when system rebooted, reverts to value before modification. As usual, making persistent changes involves changing configuration files in `/etc` directory tree. Best done by using **hostnamectl** facility, which arises from **systemd** infrastructure.

![hostnamectl](/images/hostnamectl.png)

Changing hostname persistently (surviving reboot):
```shell
$ sudo hostnamectl set-hostname MYPC
```
Most distributions do not use "pretty" hostname for anything.

On almost all Linux systems, one can simply edit (as root) the file `/etc/hostname` and put in new name.





##

[Back to top](#)

---

[Previous Chapter](../Ch33-pam/notes_Ch33.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch35-networkdevconf/notes_Ch35.md)
