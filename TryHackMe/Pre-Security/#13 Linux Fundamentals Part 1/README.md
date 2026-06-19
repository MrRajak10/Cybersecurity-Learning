# Linux Fundamentals Part 1

## Room Information

| Category         | Details                                                    |
| ---------------- | ---------------------------------------------------------- |
| Platform         | TryHackMe                                                  |
| Room Name        | Linux Fundamentals Part 1                                  |
| Difficulty       | Beginner                                                   |
| Focus Area       | Linux Basics, Terminal Navigation, File System Interaction |
| Operating System | Ubuntu Linux                                               |

---

# Overview

Linux is one of the most widely used operating systems in the world. It powers web servers, cloud infrastructure, Android devices, IoT systems, enterprise environments, and many cybersecurity platforms.

This room serves as an introduction to Linux and provides hands-on experience with the Linux terminal. The room focuses on understanding how to interact with a Linux machine, navigate the file system, search for files, and use essential shell operators.

As someone coming from a Windows environment, the terminal initially felt unfamiliar because there was no graphical interface to rely on. However, after working through the room and practicing the commands repeatedly, it became clear that the Linux terminal provides a fast and efficient way to interact with a system.

---

# Learning Objectives

By completing this room, I was able to:

* Understand where Linux is used in the real world.
* Learn the purpose of Linux distributions.
* Launch and interact with a Linux machine.
* Execute basic Linux commands.
* Navigate through directories and files.
* View file contents using terminal commands.
* Search for files efficiently.
* Search inside files for specific information.
* Understand basic shell operators.
* Build confidence using the Linux command line.

---

# Topics Covered

## 1. Introduction to Linux

The room explained that Linux is not a single operating system but a family of operating systems based on UNIX principles.

Common examples include:

* Ubuntu
* Debian
* Kali Linux
* Fedora
* CentOS

Linux is commonly used in:

* Web servers
* Cloud infrastructure
* Android devices
* Enterprise networks
* Embedded systems
* Cybersecurity environments

### Key Takeaway

Before this room, I mostly associated Linux with hacking and cybersecurity. This room helped me understand that Linux is actually everywhere and powers a huge portion of the technology we use daily.

---

## 2. Working with the Terminal

The terminal is a text-based interface used to communicate directly with the operating system.

Unlike Windows, many Linux systems are managed entirely through the command line.

### Commands Learned

#### echo

Used to display text.

Example:

```bash
echo Hello
```

Output:

```bash
Hello
```

#### whoami

Used to identify the currently logged-in user.

Example:

```bash
whoami
```

### Personal Observation

This seemed simple at first, but it helped me understand an important concept: every action performed on a Linux system happens under a specific user account. Knowing who you are logged in as becomes important later in privilege escalation and system administration.

---

## 3. Navigating the Linux File System

One of the most important skills in Linux is moving around the file system.

### Commands Learned

#### ls

Lists files and directories.

```bash
ls
```

#### cd

Changes the current directory.

```bash
cd Documents
```

#### pwd

Displays the current working directory.

```bash
pwd
```

#### cat

Displays the contents of a file.

```bash
cat file.txt
```

### What I Learned

Using these commands together creates the foundation of Linux navigation.

Typical workflow:

```bash
ls
cd Folder
ls
cat file.txt
pwd
```

### Personal Experience

The command I used most frequently during this room was `ls`.

Whenever I entered a new directory, I automatically used `ls` to see what was inside. After some practice, the combination of `cd` and `ls` started feeling natural and much faster than clicking through folders in a graphical interface.

I also found `pwd` surprisingly useful because it helped me avoid getting lost in the directory structure.

---

## 4. Searching for Files

Searching manually through directories can become difficult as systems grow larger.

Linux provides powerful tools to automate file discovery.

### Command Learned

#### find

Searches for files and directories.

Find a specific file:

```bash
find -name passwords.txt
```

Find all text files:

```bash
find -name "*.txt"
```

### Key Takeaway

The `find` command demonstrated how Linux can automate repetitive tasks that would otherwise take much longer manually.

### Personal Experience

This was one of the first commands that made Linux feel powerful.

Instead of opening multiple folders and searching manually, I could locate files instantly with a single command. I immediately understood why experienced Linux users prefer the terminal for system administration tasks.

---

## 5. Searching Inside Files

Finding a file is useful, but finding information inside files is even more valuable.

### Command Learned

#### grep

Searches for specific text inside files.

Example:

```bash
grep "THM" access.log
```

Recursive search:

```bash
grep -R "PRETTY_NAME" /etc/
```

### Real-World Relevance

Cybersecurity professionals frequently use grep to:

* Analyze log files
* Search configuration files
* Investigate incidents
* Find indicators of compromise
* Locate sensitive information

### Personal Experience

`grep` quickly became one of my favorite commands from this room.

Seeing how a single command could search hundreds of lines instantly helped me understand why log analysis becomes manageable on Linux systems.

---

## 6. Shell Operators

Shell operators allow commands to become more powerful and efficient.

### Operators Learned

| Operator | Purpose                         |
| -------- | ------------------------------- |
| &        | Run a command in the background |
| &&       | Execute multiple commands       |
| >        | Redirect output and overwrite   |
| >>       | Redirect output and append      |

### Examples

Run a command in the background:

```bash
command &
```

Run commands sequentially:

```bash
command1 && command2
```

Create a file:

```bash
echo hello > file.txt
```

Append data:

```bash
echo world >> file.txt
```

### Personal Observation

Understanding the difference between `>` and `>>` was particularly important.

Initially they looked almost identical, but learning that one overwrites data while the other appends data helped me avoid a mistake that could easily destroy existing file contents.

---

# Commands Learned Summary

| Command | Purpose                    |
| ------- | -------------------------- |
| echo    | Display text               |
| whoami  | Show current user          |
| ls      | List files and directories |
| cd      | Change directory           |
| pwd     | Print working directory    |
| cat     | Display file contents      |
| find    | Search for files           |
| grep    | Search inside files        |

---

# Challenges Faced

During this room, the biggest challenge was becoming comfortable with a terminal-only environment.

Without a graphical interface, I initially had to think carefully about where I was located and which commands to run next.

Commands such as `pwd`, `ls`, and `cd` helped solve that problem and gradually improved my confidence while navigating the system.

---

# Key Lessons Learned

* Linux powers a large portion of modern technology.
* The terminal is a powerful way to interact with systems.
* Navigation commands form the foundation of Linux usage.
* File searching becomes much easier with `find`.
* Content searching becomes efficient with `grep`.
* Shell operators increase productivity significantly.
* Practice is the fastest way to become comfortable with Linux.

---

# Conclusion

Linux Fundamentals Part 1 provided a solid introduction to Linux and terminal usage. The room focused on practical hands-on learning rather than theory alone, making it easy to understand how each command works in a real environment.

The biggest takeaway from this room was realizing that Linux is not as intimidating as it initially appears. After spending time using commands like `ls`, `cd`, `cat`, `find`, and `grep`, the command line started feeling much more approachable.

This room established the foundation required for future Linux learning and prepared me for the next room in the Linux Fundamentals series.
