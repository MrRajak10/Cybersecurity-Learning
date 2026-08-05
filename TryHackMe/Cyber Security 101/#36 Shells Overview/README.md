# Shells Overview

A learning-focused repository documenting my journey through the **TryHackMe – Shells Overview** room.

This repository is intended for educational purposes and serves as a reference for understanding the concepts behind shell access in cybersecurity. The goal is to build a strong foundation by learning **how shells work**, **why they are important**, and **where they are used** during penetration testing and post-exploitation activities, rather than simply collecting flags or following walkthroughs.

---

# About This Room

The **Shells Overview** room introduces one of the most fundamental concepts in offensive security: **Shell Access**.

After exploiting a vulnerability, attackers often aim to gain remote command execution on the target machine. This remote access is commonly referred to as obtaining a **shell**.

This room explains:

* What a shell is
* Reverse Shells
* Bind Shells
* Shell Listeners
* Shell Payloads
* Web Shells
* Basic practical usage of shell access

The room also includes hands-on exercises to reinforce the concepts through practical application.

---

# Learning Objectives

After completing this room, I was able to:

* Understand the purpose of a shell.
* Explain the difference between a normal operating system shell and a shell in cybersecurity.
* Understand how Reverse Shells work.
* Understand how Bind Shells work.
* Learn why Reverse Shells are commonly used during penetration testing.
* Understand how shell listeners receive incoming connections.
* Recognize different shell payloads.
* Understand the purpose of Bash, PHP, and Python reverse shell payloads.
* Learn how Web Shells operate.
* Perform practical shell-based exercises in a controlled environment.

---

# Topics Covered

* Shell Fundamentals
* Shell Access in Cybersecurity
* Remote Command Execution
* Privilege Escalation
* Persistence
* Pivoting
* Reverse Shell
* Bind Shell
* Netcat Listener
* rlwrap
* Ncat
* Socat
* Named Pipes (FIFO)
* Linux File Descriptors
* Input / Output Redirection
* Bash Reverse Shell
* PHP Reverse Shell
* Python Reverse Shell
* Web Shell
* Unrestricted File Upload
* Practical Shell Exploitation

---

# Key Concepts Learned

## What is a Shell?

A shell is a program that allows users to interact with an operating system by executing commands.

In cybersecurity, obtaining a shell means gaining remote command execution on a target machine.

---

## Reverse Shell

A Reverse Shell is a connection where the **target machine initiates the connection back to the attacker**.

General workflow:

1. Attacker starts a listener.
2. Target executes a payload.
3. Target connects back.
4. Attacker receives shell access.

---

## Bind Shell

A Bind Shell works in the opposite direction.

General workflow:

1. Target opens a listening port.
2. Attacker connects to that port.
3. Attacker gains shell access.

---

## Shell Listeners

This room introduced common tools used for receiving shell connections.

Examples include:

* Netcat
* rlwrap
* Ncat
* Socat

---

## Shell Payloads

A shell payload is responsible for establishing communication between the attacker and the target while exposing a command shell.

The room introduced payloads written in:

* Bash
* PHP
* Python
* Telnet
* AWK
* BusyBox

Instead of memorizing payload syntax, the room emphasizes understanding their common structure.

---

## Web Shell

A Web Shell is a malicious script uploaded to a vulnerable web server.

Instead of providing an interactive terminal immediately, it executes commands through HTTP requests.

---

# Practical Skills Gained

During the practical exercises, I learned how to:

* Start a shell listener.
* Receive a Reverse Shell.
* Navigate a compromised Linux system.
* Read files from the target.
* Upload a PHP Web Shell.
* Execute commands through a browser.
* Retrieve flags from the vulnerable machine.

---

# Challenges Faced

While completing this room, some concepts required additional attention, including:

* Understanding the difference between Reverse Shells and Bind Shells.
* Understanding how shell payloads actually work internally.
* Learning Linux input/output redirection.
* Understanding file descriptors (`0`, `1`, and `2`).
* Following the communication flow between attacker and target.
* Understanding how Web Shells differ from traditional shells.

These topics became much easier after studying the workflow step by step rather than memorizing payloads.

---

# Key Takeaways

* A shell provides command-line interaction with an operating system.
* In cybersecurity, shell access usually means remote command execution.
* Reverse Shells are more common than Bind Shells because they work better with modern firewalls.
* Shell listeners wait for incoming shell connections.
* Every reverse shell payload follows the same fundamental workflow even if the programming language changes.
* Understanding Linux file descriptors and redirection is essential for understanding shell payloads.
* Web Shells provide command execution through web applications instead of traditional shell sessions.
* Learning the concepts behind shell payloads is far more valuable than memorizing payload syntax.

---

# Repository Structure

```text
.
├── README.md
└── notes.md
```

---

# Prerequisites

Before attempting this room, it is helpful to understand:

* Basic Linux commands
* Basic networking concepts
* Command Line Interface (CLI)
* Basic web application fundamentals

---

# Learning Resources

* TryHackMe — Shells Overview
* Linux Command Line documentation
* Bash documentation
* PHP documentation
* Python documentation
* Netcat documentation

---

# Disclaimer

This repository is created solely for educational purposes to document my learning journey through the TryHackMe **Shells Overview** room.

It intentionally focuses on understanding concepts, workflows, and practical learning rather than providing a direct flag walkthrough or offensive instructions against real-world systems.
