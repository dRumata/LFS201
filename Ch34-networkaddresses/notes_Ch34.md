[Previous Chapter](../Ch33-pam/notes_Ch33.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch35-networkdevices/notes_Ch35.md)

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
  - **Link-local**: auto-configured to for every interface to have one. Non-routable.
  - 
- **Network**: an address whose **host** portion is set to all binary zeroes. Ex. **`192.168.1.0`** (the host portion can be the last 1-3 octets as discussed later; here it is just the last octet)
- **Broadcast**: an address to which each member of a particular network will listen. Will have the host portion set to all 1 bits, such as in **`172.16.255.255`** or **`148.114.255.255`** or **`192.168.1.255`** (Host portion is last two octets in the first two cases, just the last one in the third case)
- **Multicast**: an address to which approximately configured nodes will listen. The address **`224.0.0.2`** is an example of a multicast address. Only nodes specifically configured to pay attention to specific multicast address will interpret packets for that multicast group



##

[Back to top](#)

---

[Previous Chapter](../Ch33-pam/notes_Ch33.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch35-networkdevices/notes_Ch35.md)
