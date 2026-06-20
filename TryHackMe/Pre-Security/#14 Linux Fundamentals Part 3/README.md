# Linux Fundamentals Part 3

## Room Overview

This repository contains my learning notes and key takeaways from the **Linux Fundamentals Part 3** room on TryHackMe.

This room is the final part of the Linux Fundamentals series and focuses on practical Linux skills that are commonly used in day-to-day system administration, cybersecurity, and penetration testing activities. Throughout the room, I learned how to work with text editors, transfer files, manage processes, automate tasks, manage packages, and analyze system logs.

Rather than focusing only on completing tasks, I used this room to strengthen my understanding of how Linux systems operate behind the scenes and how these concepts are applied in real-world environments.

---

## Learning Objectives

By completing this room, I learned:

* How to create and edit files using terminal text editors
* The differences between Nano and Vim
* How to download and transfer files using Linux utilities
* How Python can be used to quickly host files through a web server
* How Linux processes work and how to manage them
* How foreground and background processes operate
* How to automate tasks using Cron Jobs
* How Linux package management works through APT
* How repositories and packages are managed
* How to investigate system and application logs

---

## Topics Covered

### Terminal Text Editors

The room introduced terminal-based text editors, mainly:

* Nano
* Vim

I practiced creating and editing files directly from the terminal using Nano. Since I had mostly used simple commands like `echo` and output redirection before, learning a proper text editor felt much more practical.

One thing I noticed during this section was how much easier it becomes to manage multi-line content when using a dedicated text editor instead of repeatedly appending text with shell commands.

---

### File Transfers and Web Servers

This section focused on:

* `wget`
* `scp`
* Python HTTP Server

I learned how to:

* Download files from remote locations
* Transfer files securely between systems
* Host files locally using Python's built-in HTTP server

A particularly useful concept was using:

```bash
python3 -m http.server
```

to quickly create a temporary web server.

This was one of the most interesting sections because I could immediately see how these techniques are useful during penetration testing, CTFs, and lab environments where files frequently need to be moved between systems.

---

### Linux Processes

In this section, I learned about:

* Process IDs (PIDs)
* Viewing running processes
* Process monitoring
* Process termination

Commands explored:

```bash
ps
ps aux
top
kill
```

Initially, the different process management commands seemed similar, but after viewing process information and understanding PIDs, the purpose of each command became much clearer.

I also learned the differences between signals such as:

* SIGTERM
* SIGKILL
* SIGSTOP

Understanding why a process should sometimes be terminated gracefully instead of being forcefully killed was an important takeaway.

---

### Service Management

The room introduced:

```bash
systemctl
```

which is used to interact with system services.

Common actions included:

* Starting services
* Stopping services
* Checking service status
* Enabling services during boot

Examples:

```bash
systemctl start apache2
systemctl stop apache2
systemctl enable apache2
systemctl status apache2
```

This helped me understand how Linux systems automatically manage important services such as web servers and databases.

---

### Background and Foreground Processes

This section explained how commands can run:

* In the foreground
* In the background

Important concepts:

```bash
&
Ctrl + Z
fg
```

I found this section particularly useful because it explained why some commands take over the terminal and how Linux allows users to continue working while long-running processes execute in the background.

---

### Task Automation with Cron

The room introduced:

* Cron
* Crontabs
* Scheduled tasks

Commands explored:

```bash
crontab -e
```

At first, cron syntax looked confusing because of the multiple scheduling fields. After reviewing examples, I started understanding how Linux can automatically perform repetitive tasks without user interaction.

This concept is extremely useful for:

* Backups
* Maintenance scripts
* Monitoring tasks
* Automated reporting

---

### Package Management

This section explained how Linux software is installed and maintained through:

```bash
apt
```

Topics covered:

* Software repositories
* Package installation
* Package removal
* Repository management
* GPG verification

Examples:

```bash
apt update
apt install
apt remove
```

I learned that Linux package management is not simply downloading software from websites. Instead, packages are managed through trusted repositories that help keep software updated and secure.

---

### Log Analysis

The final technical section focused on Linux logs.

Directories explored:

```bash
/var/log
```

Examples included:

* Apache logs
* Authentication logs
* Firewall logs

This was one of the most security-focused sections of the room.

By reviewing Apache access logs, I was able to see how user activity is recorded and how administrators can investigate events occurring on a system.

This reinforced the importance of log analysis in both system administration and cybersecurity.

---

## Commands Practiced

```bash
nano
vim
wget
scp
python3 -m http.server
ps
ps aux
top
kill
systemctl
crontab -e
apt update
apt install
apt remove
less
cat
```

---

## Key Takeaways

* Linux provides powerful built-in tools for file management and system administration.
* Nano is beginner-friendly, while Vim offers advanced functionality.
* Python HTTP Server is a quick and effective way to share files.
* Understanding processes is essential for troubleshooting Linux systems.
* Cron allows repetitive tasks to be automated efficiently.
* Package repositories simplify software installation and updates.
* Log analysis plays a critical role in monitoring and security investigations.
* Many of the concepts introduced in this room directly relate to real-world cybersecurity workflows.

---

## Personal Reflection

Linux Fundamentals Part 3 helped connect many of the concepts introduced throughout the previous Linux Fundamentals rooms.

The most valuable lesson for me was understanding that Linux is not just a collection of commands. It provides a complete ecosystem for managing processes, automating tasks, hosting services, transferring files, and monitoring system activity.

I particularly enjoyed learning about process management, Python web servers, and log analysis because these are concepts that frequently appear in cybersecurity labs and real-world environments.

Completing this room gave me more confidence navigating Linux systems and strengthened my foundation for future penetration testing and cybersecurity learning.

---

## Skills Gained

* Linux File Management
* Linux Process Management
* Service Administration
* Task Automation
* Package Management
* Log Analysis
* File Transfer Techniques
* Web Server Fundamentals
* Cybersecurity Linux Operations

---

**Platform:** TryHackMe
**Room:** Linux Fundamentals Part 3
**Difficulty:** Beginner
**Focus Areas:** Linux Administration, Automation, Processes, Package Management, Logging, File Transfers
