[Previous Chapter](../Ch29-containers/notes_Ch29.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch31-gm/notes_Ch31.md)

---

# Chapter 30 User Account Management - Notes

## 30.3 Learning Objectives:
- Explain the purpose of individual user accounts and list their main attributes.
- Create new user accounts and modify existing account properties, as well as remove of lock accounts.
- Understand how user passwords are set, encrypted, and stored, and how to require changes in passwords over time for security purposes.
- Explain how restricted shells and restricted accounts work.
- Understand the role of the root account and when to use it.
- Use Secure Shell (**ssh**) and remove logins and commands.


## 30.4 User Accounts
Linux systems provide **multi-user** environment which permits people and processes to have separate simultaneous work environments.

Purposes of having individual user accounts include:
- Providing each user with their own individualized private space
- Creating particular user accounts for specific dedicated purposes
- Distinguishing privileges among users

One special user account is for the **root** user, who is able to do ***anything*** on the system. To avoid making costly mistakes, and for security reasons, the root account should only be used when absolutely necessary.

Normal user accounts are for people who will work on the system. Some user accounts (like the **daemon** account) exist for the purpose of allowing processes to run as a user other than root.

In next chapter, will continue with discussion of **group** management, where subsets of the users on system can share files, privileges, etc., according to common interests.


##

[Back to top](#)

---

[Previous Chapter](../Ch29-containers/notes_Ch29.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch31-gm/notes_Ch31.md)
