[Previous Chapter](../42-localsecurity/notes_Ch42.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch44-systemrescue/notes_Ch44.md)

---

# Chapter 43 Basic Troubleshooting - Notes

## 43.3 Learning Objectives:
- Troubleshoot your system, following a number of steps iteratively until solutions are found.
- Check your network and file integrity for possible issues.
- Resolve problems when there is system boot failure.
- Repair and recover corrupted filesystems.
- Understand how **rescue and recovery** media can be used for troubleshooting.

## 43.4 Troubleshooting Levels
There are three levels of troubleshooting:
1. **Beginner**: Can be taught very quickly.
2. **Experienced**: Comes after a few years of practice.
3. **Wizard**: Some people think you have to be born this way, but that is nonsense; all skills can be learned. Every organization should have at least one person at this level of expertise to use as the go-to person.

Even the best administered systems will develop problems. Troubleshooting can isolate whether the problems arise from software or hardware, as well as whether they are local to the system, or come from within the local network or the Internet.

Troubleshooting properly requires judgment and experience, and while it will always be somewhat of an art form, following good methodical procedures can really help isolate the sources of problems in reproducible fashion.

## 43.5 Basic Techniques
Troubleshooting involves taking number of steps which need to be repeated iteratively until solutions are found. Basic recipe:
1. Characterize the problem
2. Reproduce the problem
3. Always try the easy things first
4. Eliminate possible causes one at a time
5. Change only one thing at a time; if that doesn't fix the problem, change it back
6. Check the system logs (`/var/log/messages`, `/car/log/secure`, etc.) for further information.

## 43.6 Intuition and Experience
Sometimes, ruling philosophy and methodology requires following very established procedure; making leaps based on intuition discouraged. Motivation for using a checklist and uniform procedure is to avoid reliance on a wizard, to ensure any system administrator will be able to eventually solve a problem if they adhere to well known procedures. Otherwise, if the wizard leaves the organization, there is no one skilled enough to solve tough problems.

If, on the other hand, you elect to respect your intuition and check hunches, should make sure you can get sufficient data quickly enough to decide whether or not to continue or abandon an intuitive path, based on whether it looks like it will be productive.

While ignoring intuition can sometimes make solving a problem take longer, troubleshooter's previous track record is critical benchmark for evaluating whether to invest resources this way. In other word's, useful intuition is not magic, it is distilled experience.

## 43.7 Things to Check: Networking


##

[Back to top](#)

---

[Previous Chapter](../42-localsecurity/notes_Ch42.md) - [Table of Contents](../README.md#table-of-contents) - [Next Chapter](../Ch44-systemrescue/notes_Ch44.md)i
