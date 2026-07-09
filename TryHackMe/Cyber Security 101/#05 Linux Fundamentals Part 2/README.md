# Linux Fundamentals Part 2

## Overview

This repository documents my learning journey through the **Linux Fundamentals Part 2** TryHackMe room. The room builds upon the basics introduced in Part 1 and focuses on essential Linux commands, shell operators, remote access, environment variables, file permissions, and advanced file operations.

The objective of this repository is to help beginners understand the concepts taught in the room, explain why they are important, and document the knowledge gained during the learning process. This repository is intended for educational purposes and focuses on understanding Linux rather than simply completing the room.

---

## Learning Objectives

By completing this room, I learned how to:

* Connect to remote Linux systems using SSH.
* Understand the purpose of PuTTY for Windows users.
* Use common Linux shell operators.
* Work with environment variables.
* Redirect command output to files.
* Combine commands using pipes.
* Understand Linux file permissions.
* Change file ownership and permissions.
* Perform advanced file operations.
* Manage files and directories safely.

---

## Topics Covered

### Remote Access

* SSH (Secure Shell)
* SSH syntax
* Remote login
* PuTTY overview

### Linux Operators

* `&&` (AND Operator)
* `&` (Background Operator)
* `$` (Environment Variables)
* `|` (Pipe Operator)
* `;` (Semicolon Operator)
* `>` (Overwrite Output Redirection)
* `>>` (Append Output Redirection)

### Environment Variables

* Viewing variables
* Creating variables
* Exporting variables
* Using variables inside commands

### File Permissions

* Read (r)
* Write (w)
* Execute (x)
* Owner
* Group
* Others

### Permission Management

* `chmod`
* Numeric permission values
* Understanding 4, 2, and 1 permission model

### File Ownership

* `chown`
* User ownership
* Group ownership

### File Operations

* Creating files
* Moving files
* Renaming files
* Removing files
* Removing directories recursively

---

## Key Commands Practiced

* `ssh`
* `pwd`
* `ls`
* `cat`
* `echo`
* `grep`
* `export`
* `chmod`
* `chown`
* `rm`
* `mv`
* `mkdir`
* `cd`

---

## Important Concepts Learned

### SSH

SSH allows secure remote access to another Linux machine through the command line. It is one of the most commonly used tools by Linux administrators, system engineers, and cybersecurity professionals.

### Shell Operators

The room introduced several operators that make Linux commands more powerful by allowing commands to work together, execute conditionally, or redirect their output.

### Environment Variables

Environment variables store information that programs and users can access during a session. They simplify configuration and make scripts more flexible.

### File Permissions

Linux protects files using read, write, and execute permissions for three different groups:

* Owner
* Group
* Others

Understanding permissions is essential for both Linux administration and cybersecurity.

### File Ownership

Ownership determines which users and groups control files. Managing ownership correctly is an important administrative task.

### Advanced File Operations

The room demonstrated how to safely move, rename, delete, and manage files and directories using Linux commands.

---

## Skills Gained

* Linux command-line navigation
* Remote Linux access
* Basic system administration
* Understanding Linux permissions
* Working with shell operators
* File and directory management
* Environment variable management

---

## Challenges Faced

Some concepts required additional practice before becoming comfortable, including:

* Understanding the difference between `&&`, `;`, and `&`.
* Remembering numeric permission values used with `chmod`.
* Understanding how pipes transfer output between commands.
* Learning when to overwrite files versus append to them.
* Distinguishing between file ownership and file permissions.

Practicing each command multiple times helped reinforce these concepts.

---

## Key Takeaways

* Small Linux commands become powerful when combined.
* Understanding shell operators improves efficiency.
* File permissions are fundamental to Linux security.
* SSH is an essential skill for cybersecurity professionals.
* Environment variables simplify system configuration and scripting.
* Practicing commands regularly is the best way to build confidence.

---

## Practical Learning Outcome

After completing this room, I gained a stronger understanding of Linux command-line operations and became more comfortable working with remote systems, managing files, controlling permissions, and using shell operators. These are foundational skills that support future learning in penetration testing, system administration, digital forensics, and SOC operations.

---

## Disclaimer

This repository is intended for educational purposes only. It documents personal learning from the TryHackMe Linux Fundamentals Part 2 room and is designed to help beginners understand Linux concepts through study and practice. It is not intended as a walkthrough for obtaining challenge answers or flags.
