[Previous Chapter](../Ch35-networkdevconf/notes_Ch35.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch37-systemsusd/notes_Ch37.md)

---

# Chapter 36 Firewalls - Notes

## 36.2 Introduction
**Firewalls** are used to control both incoming and outgoing access to your systems and local network, and are an essential security facility in modern networks, where intrusions and other kinds of attacks are a fact of life on any computer connected to the internet. You can control the level of trust afforded on traffic across particular interfaces, and/or with particular network addresses.

## 36.3 Learning Objectives:
- Understand what firewalls are and why they are necessary.
- Know what tools are available both at the command line and using graphical interfaces.
- Discuss about **firewalld** and the **firewall-cmd** programs.
- Know how to work with **zones**, **sources**, **services**, and **ports**.

## 36.4 What Is a Firewall?
**Firewall**: network security system that monitors and controls all network traffic. Applies **rules** on both incoming and outgoing network connections and packets and builds flexible barrier (i.e., firewalls) depending on the level of trust of a given connection.

Firewalls can be hardware or software based. They are found both in network routers, as well as in individual computers, or network nodes. Many firewalls also have routing capabilities.

## 36.5 Packet Filtering
Almost all firewalls based on **Packet Filtering**.

Information transmitted across networks in form of packets, and each one of these packets has:
- Header
- Payload
- Footer.

Header and footer contain information about destination and source addresses, what kind of packet it is, which protocol it obeys, various flags, which packet number this is in a stream, all sorts of other metadata about transmissions. Actual data in payload.

Packet filtering intercepts packets at one or more stages in network transmission, including application, transport, network, datalink.

Firewall establishes set of rules by which each packet may be:
- Accepted or rejected based on content, address, etc.
- Mangled in some way
- Redirected to another address
- Inspected for security reasons
- Etc.

Various utilities exist for establishing rules and actions to be taken as the result of packet filtering.

## 36.6 Firewall Generations
Early firewalls (dating back to the late 1980's) based on **packet filtering**: content of each network packet inspected and either dropped, rejected, or sent on. No consideration given about **connection state**: what stream of traffic the packet was part of.

Next generation of firewalls based on **stateful filters**, which also examine **connection state** of packet, to see if it is a new connection, part of an already existing one, or part of none. Denial of service attacks can bombard this kind of firewall to try and overwhelm it.

Third generation of firewalls called **Application Layer Firewalls**, aware of the kind of application and protocol the connection is using. Can block anything which should not be part of the normal flow.

## 36.7 Firewall Interfaces and Tools
Configuring your system's firewall can be done by:
- Using relatively low-level tools from the command line, combined with editing various configuration files in the `/etc` subdirectory tree:

    **'iptables'**

    **'firewall-cmd'**

    **'ufw'**

- Using robust graphical interfaces:

    **'system-config-firewall'**

    **'firewall-config'**

    **'gufw'**

    **'yast'**

Will work with lower-level tools for following reasons:
- Change less often than graphical ones
- Tend to have larger set of capabilities
- Tend to be quite different and each confined to GUI. Vary little from distribution to distribution, while only one family of distributions

Disadvantage: can seem more difficult to learn at first. In following, will concentrate on use of modern **firewalld** package, includes both **firewall-cmd** and **firewall-config**. FOr distributions which don't have it by default, can be installed from source rather easily, as will do if necessary in exercise.




##

[Back to top](#)

---

[Previous Chapter](../Ch35-networkdevconf/notes_Ch35.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch37-systemsusd/notes_Ch37.md)
