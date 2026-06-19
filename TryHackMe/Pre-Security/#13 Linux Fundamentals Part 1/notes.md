# Linux Fundamentals Part 1 - Notes

## Room Objective

This room introduces the fundamentals of Linux and provides hands-on experience with the Linux terminal. The goal is to become comfortable interacting with a Linux machine using commands instead of a graphical user interface (GUI).

---

# Task 1 - Introduction

Linux is one of the most widely used operating systems in the world.

It powers:

* Websites
* Android devices
* Cloud servers
* Smart devices
* Supercomputers
* Enterprise infrastructure

### Learning Goals

* Run basic Linux commands
* Navigate the file system
* Read file contents
* Search for files
* Understand shell operators

### My Observation

Before starting this room, I mostly knew Linux as an operating system used by hackers and cybersecurity professionals. This task helped me realize that Linux is actually used almost everywhere in modern technology.

---

# Task 2 - A Bit of Background on Linux

## Why Linux?

Linux is:

* Lightweight
* Fast
* Open-source
* Highly customizable
* Widely used in cybersecurity

## Common Linux Distributions

### Ubuntu

* Beginner friendly
* Popular server operating system
* Used throughout this room

### Debian

* Stable
* Commonly used for servers

### Kali Linux

* Designed for penetration testing
* Includes many security tools

### Important Fact

Linux was first released in:

```text
1991
```

### My Observation

One thing that surprised me was how little hardware Linux needs compared to Windows. Learning that Ubuntu Server can run on only 512MB RAM helped me understand why Linux is used on servers and embedded devices.

---

# Task 3 - Starting the Linux Machine

Before interacting with Linux, the virtual machine must be started.

Important machine information:

* Machine IP Address
* Expiration Timer
* Start Button
* Terminate Button

### My Observation

This was my first time working with a Linux machine directly inside the browser. It felt much easier than setting up a virtual machine manually.

---

# Task 4 - First Linux Commands

## Command: echo

Used to display text.

### Syntax

```bash
echo Hello
```

### Example

```bash
echo "Hello Friend"
```

### Output

```text
Hello Friend
```

### Use Cases

* Display messages
* Testing scripts
* Debugging

---

## Command: whoami

Displays the current logged-in user.

### Syntax

```bash
whoami
```

### Example Output

```text
tryhackme
```

### Why It Matters

Knowing which user account is currently active becomes important when:

* Managing permissions
* Privilege escalation
* System administration

### My Observation

At first, `whoami` looked too simple to be useful. Later I realized that knowing which user account is executing commands is a very important concept in cybersecurity.

---

# Task 5 - Interacting With the File System

Linux file navigation is one of the most important skills to learn.

---

## Command: ls

### Full Form

```text
Listing
```

### Purpose

Shows files and folders inside the current directory.

### Syntax

```bash
ls
```

### Example Output

```text
Documents
Pictures
Notes
Downloads
```

### Pro Tip

List contents without entering a directory:

```bash
ls Pictures
```

### My Observation

I found myself using `ls` almost every few seconds while solving the room. It quickly became my most-used command.

---

## Command: cd

### Full Form

```text
Change Directory
```

### Purpose

Move between directories.

### Syntax

```bash
cd Documents
```

### Example

```bash
cd Pictures
```

### Move Back One Directory

```bash
cd ..
```

### My Observation

Initially, I occasionally forgot where I was in the filesystem. Repeated use of `cd` helped me understand how Linux directories are organized.

---

## Command: cat

### Full Form

```text
Concatenate
```

### Purpose

Display file contents.

### Syntax

```bash
cat filename.txt
```

### Example

```bash
cat todo.txt
```

### Output

```text
Complete Linux room
```

### Common Use Cases

* Read text files
* View configuration files
* Read logs
* Capture flags

### Cybersecurity Relevance

Many sensitive files contain:

* Usernames
* Passwords
* API Keys
* Configuration Data

### My Observation

This was the first command that made me feel like I was actually interacting with a system rather than just navigating folders.

---

## Command: pwd

### Full Form

```text
Print Working Directory
```

### Purpose

Displays the full path of the current location.

### Syntax

```bash
pwd
```

### Example Output

```text
/home/tryhackme/Documents
```

### Why Useful?

Helps identify:

* Current location
* Full path
* Navigation mistakes

### My Observation

Whenever I became confused about where I was, `pwd` immediately solved the problem.

---

# Task 6 - Searching For Files

Searching manually becomes difficult on large systems.

Linux provides powerful search tools.

---

## Command: find

### Purpose

Search for files and directories.

---

### Find a Specific File

```bash
find -name passwords.txt
```

### Example Output

```text
./folder1/passwords.txt
```

---

### Find All Text Files

```bash
find -name "*.txt"
```

### Example Output

```text
./folder1/passwords.txt
./Documents/todo.txt
```

### Why Important?

Instead of manually opening every folder, Linux can search automatically.

### My Observation

This was one of the first commands that showed me how efficient Linux can be. A task that would take several clicks in Windows could be completed with a single command.

---

## Command: grep

### Purpose

Search for specific text inside files.

### Syntax

```bash
grep "search_term" filename
```

### Example

```bash
grep "THM" access.log
```

### Example Output

```text
THM{ACCESS}
```

### Common Use Cases

* Log analysis
* Threat hunting
* Searching configurations
* Finding indicators of compromise

---

## Recursive Search

### Syntax

```bash
grep -R "PRETTY_NAME" /etc/
```

### Meaning

* Search all files
* Search subdirectories
* Return matching results

### My Observation

`grep` immediately felt like a cybersecurity tool. I could already imagine using it to search through large log files during investigations.

---

# Task 7 - Shell Operators

Operators make commands more powerful.

---

## Operator: &

### Purpose

Run commands in the background.

### Example

```bash
command &
```

### Use Case

Long-running processes.

### Example

```bash
cp largefile.iso backup.iso &
```

---

## Operator: &&

### Purpose

Run multiple commands.

Second command runs only if the first succeeds.

### Example

```bash
mkdir Test && cd Test
```

### Why Useful?

Automates multiple steps.

### My Observation

This operator showed me how Linux users save time by combining commands instead of running them individually.

---

## Operator: >

### Purpose

Redirect output and overwrite content.

### Example

```bash
echo hello > file.txt
```

### Result

Creates file:

```text
hello
```

### Warning

If the file exists, previous content is deleted.

---

## Operator: >>

### Purpose

Append output to a file.

### Example

```bash
echo world >> file.txt
```

### Result

```text
hello
world
```

### Difference

| Operator | Action    |
| -------- | --------- |
| >        | Overwrite |
| >>       | Append    |

### My Observation

Understanding the difference between `>` and `>>` was important because accidentally overwriting a file can result in data loss.

---

# Commands Summary

| Command | Purpose               |
| ------- | --------------------- |
| echo    | Display text          |
| whoami  | Show current user     |
| ls      | List files            |
| cd      | Change directory      |
| cat     | Display file contents |
| pwd     | Show current location |
| find    | Search for files      |
| grep    | Search inside files   |

---

# Key Cybersecurity Relevance

These commands are used constantly during:

* Penetration Testing
* Digital Forensics
* Incident Response
* Threat Hunting
* Log Analysis
* System Administration
* Capture The Flag (CTF) Challenges

---

# Biggest Lessons Learned

1. Linux is used almost everywhere.
2. The terminal is not as scary as it first appears.
3. Navigation commands form the foundation of Linux.
4. `find` saves significant time when locating files.
5. `grep` is extremely useful for searching data.
6. Shell operators make workflows more efficient.
7. Consistent practice is the fastest way to become comfortable with Linux.

---

# Personal Reflection

This room was my first serious hands-on interaction with Linux. At the beginning, using only the terminal felt unfamiliar because I was used to graphical interfaces. However, after repeatedly using commands like `ls`, `cd`, `pwd`, `cat`, `find`, and `grep`, I started becoming more comfortable navigating the system.

The biggest takeaway for me was realizing that Linux commands are not difficult when learned one step at a time. By the end of the room, I felt much more confident using the terminal and understood why Linux skills are considered essential in cybersecurity.
