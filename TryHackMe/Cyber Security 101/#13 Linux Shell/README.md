# Linux Shells – TryHackMe

> A beginner-focused learning repository for understanding Linux shells, command-line basics, and introductory shell scripting.

---

# Overview

This room introduces the Linux command-line environment and explains how users interact with Linux through shells. Instead of relying only on the Graphical User Interface (GUI), learners explore the Command Line Interface (CLI), understand the purpose of a shell, practice essential Linux commands, and write simple shell scripts.

The room focuses on building foundational Linux skills that are required before moving into penetration testing, SOC analysis, automation, and general cybersecurity tasks.

---

# Learning Objectives

After completing this room, you should be able to:

* Understand the difference between GUI and CLI.
* Explain what a Linux shell is.
* Describe how a shell communicates with the Linux kernel.
* Identify common Linux shells.
* Navigate the Linux filesystem using basic commands.
* Read file contents from the terminal.
* Search for information inside files.
* Understand the basics of shell scripting.
* Create simple Bash scripts.
* Use variables, loops, conditional statements, and comments.
* Execute shell scripts safely.
* Complete beginner-level scripting exercises.

---

# Topics Covered

* Introduction to Linux Shells
* GUI vs CLI
* Shell Architecture
* Kernel and User Interaction
* Bash Shell
* Fish Shell
* Z Shell (Zsh)
* Basic Linux Commands
* Shell Scripting
* Variables
* User Input
* Loops
* Conditional Statements
* Comments
* Script Permissions
* Practical Script Analysis

---

# Key Linux Commands

| Command           | Purpose                           |
| ----------------- | --------------------------------- |
| `pwd`             | Display current working directory |
| `ls`              | List files and directories        |
| `cd`              | Change directory                  |
| `cat`             | Display file contents             |
| `grep`            | Search for text inside files      |
| `history`         | Show previously executed commands |
| `echo $SHELL`     | Display current shell             |
| `cat /etc/shells` | Show installed shells             |
| `chmod +x`        | Make a script executable          |

---

# Linux Shells Introduced

## Bash

* Most common Linux shell
* Default shell on many Linux distributions
* Supports scripting
* Supports command history
* Supports tab completion

---

## Fish

* Beginner-friendly
* Auto spell correction
* Syntax highlighting
* Command suggestions
* Tab completion

---

## Z Shell (Zsh)

* Advanced shell
* Highly customizable
* Supports plugins
* Auto correction
* Powerful interactive features

---

# Shell Scripting Concepts

The room introduces the basic building blocks of Bash scripting.

Topics include:

* Shebang (`#!/bin/bash`)
* Variables
* Reading user input
* Displaying output
* Conditional statements
* Loops
* Comments
* Executable permissions

---

# Practical Learning

The room includes practical exercises where learners:

* Create their first Bash script.
* Read user input.
* Display customized output.
* Build authentication logic using conditions.
* Search through log files using scripts.
* Analyze script behavior.
* Modify existing scripts to complete a task.

---

# Skills Gained

After completing this room, learners gain experience with:

* Linux terminal navigation
* Command-line usage
* Reading Linux files
* Basic scripting
* Automation fundamentals
* File searching
* Script execution
* Understanding existing Bash scripts

---

# Why This Room Matters

Linux is the primary operating system used in many cybersecurity environments. Security professionals regularly use the terminal for:

* Incident response
* Digital forensics
* Log analysis
* Penetration testing
* System administration
* Automation
* Threat hunting

Understanding Linux shells is an essential skill before learning more advanced cybersecurity topics.

---

# Key Takeaways

* The shell acts as an interpreter between the user and the Linux kernel.
* CLI often performs tasks faster than GUI.
* Bash is the most commonly used Linux shell.
* Shell scripts automate repetitive tasks.
* Variables, loops, and conditions are the foundation of scripting.
* Small automation scripts can significantly improve productivity.

---

# Recommended Practice

Try these exercises after completing the room:

1. Navigate through different directories using only terminal commands.
2. Create a folder structure using terminal commands.
3. Create a text file and display its contents using `cat`.
4. Search for keywords inside text files using `grep`.
5. Write a script that greets a user after asking for their name.
6. Create a script that checks whether a password matches a predefined value.
7. Write a loop that prints numbers from 1 to 20.
8. Modify an existing Bash script and observe the output.
9. Practice giving executable permissions with `chmod +x`.
10. Explore `/etc/shells` to see installed shells on your system.

---

# Prerequisites

* Basic computer knowledge
* No previous Linux experience required

---

# Difficulty

Beginner

---

# Final Thoughts

This room builds the foundation for working comfortably inside a Linux terminal. Instead of focusing only on memorizing commands, it encourages learners to understand how shells communicate with the operating system and how scripting can automate repetitive tasks. These concepts become increasingly valuable throughout a cybersecurity learning journey.
