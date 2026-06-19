# Linux Fundamentals Part 2

## Room Information

| Platform  | Room                      |
| --------- | ------------------------- |
| TryHackMe | Linux Fundamentals Part 2 |

---

## Overview

This room continues the Linux Fundamentals learning path by introducing remote system access, command-line enhancements, filesystem management, file permissions, and common Linux directories.

Unlike the first room, where interactions were performed directly through the browser, this room focuses on connecting to a remote Linux machine using SSH and performing real-world Linux administration tasks.

The room builds foundational skills that are essential for cybersecurity, system administration, penetration testing, SOC operations, and general Linux usage.

---

## Learning Objectives

By completing this room, I learned how to:

* Connect to remote Linux machines using SSH.
* Understand how encrypted remote communication works.
* Use command flags and switches to extend command functionality.
* Read Linux documentation using help menus and man pages.
* Create, copy, move, rename, and delete files and directories.
* Identify file types using Linux utilities.
* Understand Linux file permissions.
* Switch between user accounts.
* Explore important Linux system directories.
* Develop confidence navigating Linux from the command line.

---

## Topics Covered

### SSH (Secure Shell)

* What SSH is.
* Why SSH is used for remote administration.
* Encrypted communication between systems.
* Logging into remote Linux machines.
* Using credentials and IP addresses for remote access.

### Flags and Switches

* Understanding command arguments.
* Using flags such as:

```bash
ls -a
ls -lh
ls --help
```

* Learning how command behavior changes when options are added.

### Linux Documentation

* Using:

```bash
man command
```

* Reading manual pages.
* Finding command syntax and available options.
* Learning how Linux documentation helps solve problems independently.

### Filesystem Management

Working with:

```bash
touch
mkdir
cp
mv
rm
file
```

Operations performed:

* Creating files.
* Creating directories.
* Copying files.
* Moving files.
* Renaming files.
* Removing files and directories.
* Identifying file types.

### Linux Permissions

Understanding:

* Read (r)
* Write (w)
* Execute (x)

Permission groups:

* Owner
* Group
* Others

Examples:

```text
rwxr-xr-x = 755
rw-r--r-- = 644
rwx------ = 700
```

### User Management

* Switching users with:

```bash
su
su -l
```

* Understanding user ownership.
* Understanding group ownership.
* Learning why permissions matter for security.

### Common Linux Directories

| Directory | Purpose                            |
| --------- | ---------------------------------- |
| /etc      | System configuration files         |
| /var      | Logs and variable application data |
| /root     | Home directory of the root user    |
| /tmp      | Temporary storage location         |

---

## My Learning Experience

This room felt much more practical than the first Linux Fundamentals room because it introduced SSH and remote machine access. Before this room, I mostly interacted with Linux through the browser-based terminal provided by TryHackMe. Using SSH to connect to a remote machine made the experience feel much closer to how Linux systems are accessed in real-world environments.

One of the concepts I found most useful was learning about command flags and switches. Initially, I used commands only in their default form, but after experimenting with options like `-a`, `-l`, and `--help`, I realized how much additional information commands can provide. The `man` pages also became a valuable resource whenever I needed clarification about a command.

While practicing filesystem commands, I occasionally mixed up the behavior of `cp` and `mv`. Creating test files and directories helped me understand the difference between copying data and moving or renaming it. Repeating these commands several times made them much easier to remember.

The permissions section was particularly interesting because it connected Linux administration with cybersecurity concepts. Understanding who can read, write, or execute a file helped me see how Linux protects sensitive resources and why permission misconfigurations can become security risks.

Another important lesson was becoming familiar with common Linux directories. Knowing where configuration files, logs, temporary files, and root user data are stored gives valuable context when troubleshooting systems or performing security investigations.

Overall, this room significantly improved my confidence working in Linux and helped me understand many concepts that are commonly used in cybersecurity environments.

---

## Key Takeaways

* SSH is the standard method for remotely managing Linux systems.
* Command flags greatly extend the functionality of Linux commands.
* Man pages are one of the most valuable learning resources available directly on Linux systems.
* Files and directories can be efficiently managed using a small set of core commands.
* Linux permissions form an important layer of system security.
* Understanding ownership and access rights is critical for cybersecurity.
* Common Linux directories store important configuration files, logs, and temporary data.
* Practical repetition is the best way to become comfortable with Linux commands.

---

## Commands Practiced

```bash
ssh
ls
man
touch
mkdir
cp
mv
rm
file
su
pwd
cat
```

---

## Skills Gained

* Linux Navigation
* Remote System Access
* SSH Usage
* File Management
* Directory Management
* User Management
* Permission Analysis
* Linux Documentation Usage
* Basic System Administration
* Cybersecurity Linux Fundamentals

---

## Conclusion

Linux Fundamentals Part 2 expanded my understanding of Linux by introducing remote access, file management, permissions, and important system directories. The room provided hands-on experience with commands that are frequently used by cybersecurity professionals, system administrators, and Linux users. Completing this room strengthened my Linux foundation and prepared me for more advanced Linux and cybersecurity topics in future learning paths.
