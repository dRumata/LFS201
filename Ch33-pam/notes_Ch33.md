[Previous Chapter](../Ch32-fpo/notes_Ch32.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch34-networkaddresses/notes_Ch34.md)

---

# Chapter 33 Pluggable Authentication Modules (PAM) - Notes

## 33.2 Introduction
**Pluggable Authentication Modules** provide uniform mechanism to ensure that users and applications properly identified and authenticated. Conditional rules can be applied to limit scope of permissions and control can be established over what to do in case of either success or failure. PAM can also work with LDAP to centralize authentication throughout network.

## 33.3 Learning Objectives:
- Explain the basic concepts that motivate the user of PAM.
- List the steps involved in the authentication process.
- Use and modify PAM configuration files.
- Know how to interpret PAM rules and create new ones.
- Apply LDAP to use and administer distributed directory services over the network.


## 33.4 PAM: A Unified Approach to Authentication
Historically, authentication of users performed individually by individual applications; i.e., **su**, **login**, **ssh** would authenticate and establish user accounts independently of each other.

Most modern Linux applications have been written/rewritten to exploit PAM (<strong>P</strong>luggable <strong>A</strong>uthentication <strong>M</strong>odules) so that authentication can be done in one uniform way, using **libpam**.

This library of modules provides enormous flexibility and consistency with respect to authentication, password, session, account services.

PAM incorporates following components:
- PAM-aware applications
- Configuration files in `/etc/pam.d`
- PAM modules in the **`libpam*`** libraries, which can be found in different locations depending on the Linux distribution

Each PAM-aware application/service may be configured with respect to PAM by individual configuration file in `/etc/pam.d`.


## 33.5 Authentication Process
Several steps involved in authentication:
- User invokes PAM-aware application, such as **login**, **su**, **ssh**
- Application calls **libpam**
- Library checks for files in `/etc/pam.d`; these delineate which PAM modules to invoke, including **system-auth**
- Each referenced module executed in accordance with rules of relevant configuration file for that application





##

[Back to top](#)

---

[Previous Chapter](../Ch32-fpo/notes_Ch32.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch34-networkaddresses/notes_Ch34.md)
