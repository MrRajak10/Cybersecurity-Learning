# Linux Fundamentals Part 1 - Notes

## Room Goal

Learn the fundamental Linux commands required to interact with a Linux machine through the terminal. Build a strong foundation before moving to more advanced Linux and cybersecurity topics.

---

# What is Linux?

Linux is an open-source operating system based on Unix. It is one of the most widely used operating systems because it is lightweight, stable, customizable, and secure.

## Where Linux is Used

* Web servers
* Cloud infrastructure
* Android devices
* Supercomputers
* Enterprise servers
* IoT devices
* Smart TVs
* Networking devices
* Embedded systems
* Cybersecurity labs
* Penetration testing distributions

---

# Linux Distributions

Linux comes in different distributions (distros), each designed for different purposes.

Examples:

* Ubuntu
* Debian
* Kali Linux
* Fedora
* Arch Linux
* CentOS

This room uses **Ubuntu**.

---

# Why Learn Linux?

Most cybersecurity tools and environments run on Linux.

Linux skills are essential for:

* SOC Analysts
* Penetration Testers
* Incident Responders
* Digital Forensics
* System Administrators
* Cloud Security

---

# Terminal

The terminal is a text-based interface used to communicate with the operating system.

Instead of clicking icons, users type commands.

The terminal may seem difficult at first, but it becomes much faster than using a graphical interface with practice.

---

# Commands Learned

---

## echo

Displays text in the terminal.

### Syntax

```bash
echo text
```

### Example

```bash
echo Hello
```

### Output

```text
Hello
```

### Purpose

* Display text
* Test commands
* Debug scripts
* Redirect output into files

---

## whoami

Shows the currently logged-in user.

### Syntax

```bash
whoami
```

### Example Output

```text
tryhackme
```

### Purpose

Identify which user is currently using the system.

---

## ls

Lists files and folders inside the current directory.

### Syntax

```bash
ls
```

### Example

```bash
ls
```

### Purpose

View directory contents.

---

## cd

Changes the current directory.

### Syntax

```bash
cd directory_name
```

### Example

```bash
cd Documents
```

### Move Back One Directory

```bash
cd ..
```

### Purpose

Navigate through the Linux file system.

---

## pwd

Prints the current working directory.

### Syntax

```bash
pwd
```

### Example Output

```text
/home/tryhackme/Documents
```

### Purpose

Display the full path of the current directory.

---

## cat

Displays the contents of a file.

### Syntax

```bash
cat filename
```

### Example

```bash
cat notes.txt
```

### Purpose

Read text files directly from the terminal.

---

## find

Searches for files and directories.

### Search by Name

```bash
find -name passwords.txt
```

### Search All Text Files

```bash
find -name "*.txt"
```

### Purpose

Locate files quickly without manually checking folders.

---

## grep

Searches inside files for specific text.

### Syntax

```bash
grep "text" filename
```

### Example

```bash
grep "THM" access.log
```

### Purpose

Find keywords, IP addresses, usernames, flags, log entries, or other specific text inside files.

---

# Shell Operators

---

## &

Runs a command in the background.

### Example

```bash
command &
```

### Purpose

Continue using the terminal while the command executes.

---

## &&

Runs the second command only if the first command succeeds.

### Example

```bash
command1 && command2
```

### Purpose

Chain commands safely.

---

## >

Redirects output into a file.

If the file exists, its contents are overwritten.

### Example

```bash
echo Hello > notes.txt
```

---

## >>

Appends output to the end of a file.

Existing contents remain unchanged.

### Example

```bash
echo World >> notes.txt
```

---

# Important Differences

| Operator | Function                                            |
| -------- | --------------------------------------------------- |
| `>`      | Overwrites a file                                   |
| `>>`     | Appends to a file                                   |
| `&`      | Runs in the background                              |
| `&&`     | Runs the next command only if the previous succeeds |

---

# Important Concepts

* Linux is heavily used in cybersecurity.
* Most Linux servers operate without a graphical interface.
* Commands are case-sensitive.
* Every command has a specific purpose.
* Efficient navigation saves time.
* `find` searches for files.
* `grep` searches inside files.
* Practice builds command-line confidence.

---

# Real-World Usage

## ls

Checking files on a compromised server.

## cd

Moving between investigation directories.

## pwd

Confirming the current investigation location.

## cat

Reading configuration files or log files.

## find

Locating suspicious files.

## grep

Searching logs for:

* IP addresses
* Usernames
* Error messages
* Indicators of Compromise (IOCs)
* Malware names
* Flags during CTFs

---

# Key Takeaways

* Linux is a fundamental skill for cybersecurity.
* The terminal is the primary method of interacting with Linux systems.
* Learning basic commands is more important than memorizing every command.
* `find` and `grep` are powerful tools that significantly improve efficiency.
* Shell operators allow commands to be combined and output to be redirected effectively.
* Consistent practice is the fastest way to become comfortable with Linux.

---

# Skills Developed

* Basic Linux navigation
* Terminal usage
* File system exploration
* File reading
* File searching
* Text searching
* Output redirection
* Command chaining
* Linux command-line fundamentals
