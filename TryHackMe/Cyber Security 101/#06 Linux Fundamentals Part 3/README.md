# Linux Fundamentals Part 3

> A beginner-friendly learning repository for the **TryHackMe – Linux Fundamentals Part 3** room.

> **Note:** This repository is intended for educational purposes. It focuses on understanding Linux concepts rather than providing a walkthrough or flag solutions.

---

# Overview

Linux Fundamentals Part 3 is the final room in the Linux Fundamentals series. Instead of introducing basic Linux commands, this room focuses on topics that are commonly used in real-world Linux system administration, penetration testing, and defensive security.

The room teaches how to edit files efficiently, transfer files between systems, manage running processes, automate repetitive tasks, install software using package managers, and investigate system logs. These concepts form the foundation for working with Linux in cybersecurity environments.

---

# Learning Objectives

After completing this room, I was able to understand:

* Using terminal-based text editors.
* Downloading and transferring files securely.
* Running a simple web server.
* Understanding Linux processes.
* Managing processes and services.
* Working with foreground and background jobs.
* Understanding automation with Cron.
* Installing and managing software packages.
* Reading Linux log files.
* Understanding why these topics matter in cybersecurity.

---

# Topics Covered

## Terminal Text Editors

The room introduced terminal-based text editors and explained why they are preferred over using simple commands like `echo` when creating or editing files.

### Nano

Nano is a beginner-friendly text editor that allows editing multiple lines of text inside the terminal.

Important concepts learned:

* Creating files
* Editing existing files
* Saving changes
* Exiting Nano
* Basic keyboard shortcuts

The room also briefly introduced **Vim**, explaining that it is a more advanced editor that can be learned later.

---

## File Download and Transfer

The room explained different methods for transferring files in Linux.

### Downloading Files

Files can be downloaded directly from a URL using terminal commands.

Concept learned:

* Downloading files from remote servers.

### Secure File Transfer

The room introduced secure file copying between systems through SSH.

Concepts learned:

* Copying files from local to remote systems.
* Copying files from remote to local systems.
* Understanding secure encrypted file transfer.

---

## Hosting Files

One of the most useful practical exercises in this room was creating a temporary web server.

Topics learned:

* Hosting files from the current directory.
* Sharing files with another machine.
* Downloading hosted files from another system.

This demonstrates how simple it is to share files between Linux systems.

---

## Linux Processes

Processes are simply programs that are currently running on a Linux system.

The room covered:

* Viewing running processes.
* Understanding Process IDs (PID).
* Monitoring processes.
* Managing system resources.

Important concepts:

* Current user processes
* System-wide processes
* Process monitoring
* Process hierarchy

---

## Managing Processes

The room explained how Linux controls processes.

Topics learned:

* Process termination
* Clean process shutdown
* Forcefully killing processes
* Process signals

The room also introduced the idea that every running program receives its own Process ID.

---

## systemd and Services

One of the most important concepts introduced was **systemd**.

Topics learned:

* Services
* Starting services
* Stopping services
* Enabling services during boot
* Disabling services

This is an essential concept for Linux administration.

---

## Foreground and Background Processes

Linux allows programs to run in either:

* Foreground
* Background

The room demonstrated how to:

* Move processes into the background.
* Resume them later.
* Bring them back into the foreground.

This is especially useful when running long-running tasks.

---

## Automation

Automation is an important Linux feature.

Instead of manually performing repetitive work, Linux can schedule tasks automatically.

The room introduced:

* Cron
* Crontab
* Scheduled jobs

Examples include:

* Automatic backups
* Scheduled scripts
* Routine maintenance

---

## Package Management

The room explained how Linux installs software.

Topics covered:

* Software repositories
* Package managers
* Installing software
* Updating software
* Removing software

The room also introduced the idea of repository trust and package authenticity.

---

## Linux Logs

Logs record what happens inside a Linux system.

Topics learned:

* System logs
* Service logs
* Web server logs
* Authentication logs

The room demonstrated how logs help administrators and security analysts investigate system activity.

Examples include:

* User logins
* Service activity
* Errors
* Web requests
* Security events

---

# Why This Room Matters

Although the commands introduced in this room appear simple, they are used every day by:

* SOC Analysts
* Penetration Testers
* Linux Administrators
* Cloud Engineers
* DevOps Engineers
* Incident Responders

Understanding these topics builds a strong Linux foundation before moving into more advanced cybersecurity concepts.

---

# Skills Gained

After completing this room, I gained practical experience with:

* Terminal text editing
* Secure file transfer
* Temporary web servers
* Linux process management
* Service management
* Background jobs
* Task automation
* Package management
* Linux logging
* Basic Linux administration

---

# Beginner Practice

To reinforce the concepts learned in this room, try completing the following exercises on your own Linux virtual machine.

### Practice 1

Create a text file using Nano and edit it multiple times.

---

### Practice 2

Host a directory using Python's HTTP server and download a file from another terminal.

---

### Practice 3

Start a process, identify its PID, monitor it, and terminate it safely.

---

### Practice 4

Create a simple Cron job that runs automatically at a scheduled time.

---

### Practice 5

Install and remove a software package using your Linux package manager.

---

### Practice 6

Explore the system log directory and identify different log files generated by services.

---

# Key Takeaways

* Nano is an excellent editor for beginners.
* Secure file transfer is an essential Linux skill.
* Temporary web servers are useful for sharing files.
* Every running program is a process with its own PID.
* Services can be managed through the Linux service manager.
* Cron automates repetitive tasks.
* Package managers simplify software installation.
* Log files provide valuable information for troubleshooting and security investigations.

---

# What's Next?

After completing Linux Fundamentals Part 3, the next step is to continue building operating system knowledge before moving deeper into cybersecurity topics such as networking, Windows fundamentals, web technologies, privilege escalation, and security monitoring.

---

**Room:** Linux Fundamentals Part 3
**Platform:** TryHackMe
**Repository Purpose:** Personal learning notes and educational reference.
