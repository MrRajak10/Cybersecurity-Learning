# README.md

# Windows Command Line (TryHackMe)

## Overview

This repository contains my learning notes from the **Windows Command Line** room on TryHackMe. The purpose of this repository is to document what I learned while exploring the Windows Command Line Interface (CLI), understanding how common Windows commands work, and practicing basic system administration tasks from the terminal.

This repository is focused on **learning**, **understanding concepts**, and **building practical Windows command-line skills** rather than simply solving the room.

---

## Learning Objectives

Throughout this room I learned how to:

* Understand the difference between GUI and CLI.
* Connect to a Windows machine remotely using SSH.
* Gather basic system information.
* Perform basic network troubleshooting.
* Navigate the Windows file system from the command line.
* Create, remove, and manage directories.
* View and manipulate files.
* Monitor running processes.
* Understand how command-line tools help system administrators and security professionals.

---

## Topics Covered

### Windows Interfaces

* Graphical User Interface (GUI)
* Command Line Interface (CLI)

### Remote Access

* SSH

### System Information

* Windows Version
* Hostname
* Environment Variables
* System Information

### Network Troubleshooting

* IP Configuration
* Connectivity Testing
* Route Tracing
* DNS Resolution
* Active Network Connections

### File and Directory Management

* Navigating directories
* Listing files
* Creating folders
* Removing folders
* Viewing file contents
* Copying files
* Moving files
* Deleting files

### Process Management

* Viewing running processes
* Filtering processes
* Terminating processes

---

## Commands Practiced

### Basic System Information

* `set`
* `ver`
* `systeminfo`
* `help`

### Network Commands

* `ipconfig`
* `ipconfig /all`
* `ping`
* `tracert`
* `nslookup`
* `netstat`

### File & Directory Commands

* `cd`
* `dir`
* `tree`
* `mkdir`
* `rmdir`
* `type`
* `copy`
* `move`
* `del`
* `erase`

### Process Commands

* `tasklist`
* `taskkill`

### Useful Commands

* `cls`
* `more`
* `driverquery`
* `shutdown`

---

## Key Concepts Learned

### GUI vs CLI

GUI allows users to interact using windows, icons, buttons, and a mouse.

CLI is a text-based interface where commands are typed using the keyboard.

---

### Why Command Line Matters

The command line provides:

* Faster administration
* Lower resource usage
* Automation through scripts
* Remote administration
* Better control over Windows systems

These capabilities make the command line an important skill for cybersecurity professionals.

---

### Remote Administration

The room demonstrated connecting to a Windows machine using SSH.

This introduced the concept of remotely managing systems without physical access, which is commonly used by administrators and security teams.

---

### System Enumeration

Before troubleshooting or investigating a machine, it is important to understand:

* Windows version
* Hostname
* Hardware information
* Memory
* Network adapters
* Installed drivers

The room introduced several commands used for gathering this information.

---

### Network Troubleshooting

Several essential networking commands were introduced.

These commands help determine:

* Current IP configuration
* Whether another machine is reachable
* How packets travel across the network
* DNS name resolution
* Current TCP connections

These skills form the foundation for future networking and SOC investigations.

---

### File Management

Instead of using File Explorer, the room demonstrates how to perform file operations directly from the terminal.

Examples include:

* Navigating folders
* Creating directories
* Removing directories
* Viewing text files
* Copying files
* Moving files
* Deleting files

---

### Process Monitoring

Processes can be viewed and filtered directly from the command line.

Learning to identify running processes is an important skill for:

* Windows administration
* Malware analysis
* Incident response
* SOC investigations

---

## Biggest Takeaways

This room helped me understand that Windows Command Prompt is much more than a simple terminal.

Many tasks that normally require multiple mouse clicks can be completed with a single command. Learning these commands improves speed, efficiency, and troubleshooting skills.

The room also introduced several commands that are commonly used in cybersecurity, making it an excellent foundation before learning Windows internals, Active Directory, incident response, and SOC analysis.

---

## Skills Gained

* Windows Command Prompt
* Basic Windows Administration
* Remote Access
* Windows Networking Basics
* System Enumeration
* File System Navigation
* Process Enumeration
* Basic Troubleshooting

---

## Recommended Practice

To reinforce the concepts from this room, practice the following:

1. Find your computer's hostname.
2. Display your Windows version.
3. View complete IP configuration.
4. Ping another device on your network.
5. Run `tracert` on a website.
6. Resolve a domain using `nslookup`.
7. List all active network connections.
8. Create and remove practice folders.
9. Copy and move text files.
10. View running processes and identify common Windows services.

---

## What This Room Prepared Me For

Completing this room builds the foundation needed for:

* Windows Fundamentals
* Active Directory
* Windows Event Logs
* SOC Level 1
* Digital Forensics
* Incident Response
* Malware Analysis
* Windows Privilege Escalation
* Defensive Security
