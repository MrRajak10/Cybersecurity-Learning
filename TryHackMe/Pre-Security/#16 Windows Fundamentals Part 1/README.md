# Windows Fundamentals Part 1

## Overview

Windows Fundamentals Part 1 is an introductory room that provides a foundational understanding of the Windows operating system. The room covers essential Windows concepts including Windows editions, the graphical user interface (GUI), file systems, user accounts, permissions, User Account Control (UAC), Control Panel, Settings, and Task Manager.

As a cybersecurity beginner, understanding how Windows works is extremely important because Windows is one of the most widely used operating systems in both personal and enterprise environments. Many security incidents, investigations, and administrative tasks involve Windows systems, making these fundamentals valuable for anyone pursuing a career in cybersecurity.

---

## Learning Objectives

By completing this room, I learned:

* The evolution of Windows operating systems and their editions.
* The purpose of Windows Home, Pro, and Server editions.
* How to navigate the Windows Desktop and GUI components.
* The role of NTFS and its security-related features.
* The importance of the Windows and System32 folders.
* How Windows user accounts and groups work.
* The difference between Administrator and Standard User accounts.
* The purpose of User Account Control (UAC).
* The difference between Settings and Control Panel.
* Basic use of Windows Task Manager.

---

## Topics Covered

### Windows Editions

The room introduced different versions of Windows and explained how Microsoft has evolved the operating system over time.

Key concepts:

* Windows XP
* Windows Vista
* Windows 7
* Windows 8 / 8.1
* Windows 10
* Windows 11
* Windows Server 2019

Important takeaway:

* Windows Pro supports BitLocker Device Encryption, while Windows Home does not.

---

### Windows Desktop and GUI

The graphical user interface (GUI) is the environment users interact with after logging in.

Components explored:

* Desktop
* Start Menu
* Search Box
* Task View
* Taskbar
* Toolbars
* Notification Area

I learned how users can customize the desktop, manage icons, access applications, and configure display settings.

---

### Windows File System (NTFS)

The room introduced NTFS (New Technology File System), the primary file system used by modern Windows operating systems.

Key NTFS features:

* File permissions
* Encryption
* Compression
* Support for large files
* Journaling capabilities

I also learned about:

* Full Control
* Modify
* Read & Execute
* Read
* Write

Understanding permissions helped me see how Windows controls access to files and folders.

---

### Alternate Data Streams (ADS)

A particularly interesting concept introduced in the room was Alternate Data Streams (ADS).

Key learning points:

* ADS allows files to contain hidden streams of data.
* Windows Explorer does not display ADS by default.
* ADS has legitimate uses but has also been abused by attackers to hide malicious data.

This was my first introduction to ADS, and it showed me how attackers may take advantage of lesser-known Windows features.

---

### Windows Folder and System32

The room explained the purpose of the Windows directory and the System32 folder.

Important concepts:

* Windows environment variables
* %windir%
* Critical operating system files
* System32 folder importance

Key lesson:

Deleting or modifying files inside System32 can severely damage the operating system and make it unusable.

---

### User Accounts and Groups

The room covered Windows user management and permissions.

Topics included:

* Administrator accounts
* Standard User accounts
* User profiles
* Local Users and Groups Management
* Security groups

Useful tool learned:

```text
lusrmgr.msc
```

This tool allows administrators to manage users and groups on a local Windows system.

---

### User Account Control (UAC)

User Account Control (UAC) was introduced as a security feature designed to reduce the risk of unauthorized system changes.

Key concepts:

* Privilege separation
* Elevation prompts
* Administrator approval
* Malware protection

I learned that even administrator accounts do not automatically run every process with elevated privileges.

---

### Settings and Control Panel

The room compared two major Windows management interfaces:

* Settings
* Control Panel

I learned that modern Windows versions are gradually moving configuration options toward the Settings application, although many advanced options still exist within Control Panel.

---

### Task Manager

The room concluded with Task Manager.

Key uses:

* View running processes
* Monitor CPU usage
* Monitor memory usage
* Analyze system performance
* Manage applications

Useful shortcut:

```text
Ctrl + Shift + Esc
```

---

## My Learning Experience

Before starting this room, I used Windows daily but never paid much attention to how many components worked behind the scenes. I knew how to use the operating system as a regular user, but I had very little understanding of the security and administrative features built into Windows.

One area I found particularly useful was learning about user accounts, groups, and permissions. Before this room, I often saw Administrator and Standard User accounts but never fully understood why they existed or how they affected system security.

The introduction to UAC helped me understand why Windows displays permission prompts before making important system changes. Previously, I viewed these prompts as annoying pop-ups, but now I understand their role in reducing security risks.

Learning about NTFS permissions also changed the way I think about file security. I realized that access control is one of the fundamental security mechanisms used to protect systems and data.

The concept that surprised me the most was Alternate Data Streams (ADS). It was interesting to learn that Windows files can contain hidden streams of information and that attackers have historically abused this feature.

Another valuable lesson was understanding the importance of the System32 directory. Many people joke about deleting System32, but this room helped me understand why that folder is so critical to Windows operations.

Overall, the room strengthened my understanding of Windows from both a user and security perspective.

---

## Key Takeaways

* Windows is the most widely used desktop operating system.
* BitLocker encryption is available in Windows Pro editions.
* NTFS provides advanced security and file management features.
* Alternate Data Streams can hide additional file data.
* System32 contains critical operating system components.
* User groups simplify permission management.
* UAC helps prevent unauthorized system modifications.
* Settings and Control Panel both play important roles in system administration.
* Task Manager is an essential troubleshooting and monitoring tool.

---

## Skills Gained

* Windows Navigation
* Windows Administration Basics
* User Management
* Permission Management
* NTFS Fundamentals
* UAC Understanding
* System Configuration
* Windows Security Fundamentals
* Basic Troubleshooting

---

## Conclusion

Windows Fundamentals Part 1 provided a solid introduction to the Windows operating system and its core components. The room helped bridge the gap between being a regular Windows user and beginning to understand how Windows functions from an administrative and cybersecurity perspective. The concepts learned here provide a strong foundation for future Windows security, system administration, and SOC-related learning paths.
