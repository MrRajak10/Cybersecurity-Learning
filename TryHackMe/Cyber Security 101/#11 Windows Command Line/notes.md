Welcome back! Transitioning from the Graphical User Interface (GUI) to the Command Line Interface (CLI) is a major milestone in your cybersecurity journey.

While the GUI is designed for ease of use, the CLI is designed for **power, speed, and automation**. As a security professional, you will spend a massive amount of time in terminals. Attackers prefer the command line because it is stealthy and requires very little bandwidth, while defenders rely on it to pull logs, kill rogue processes, and query system states rapidly.

Let's break down your notes, organize them logically, and look at exactly how attackers and defenders use these tools in the real world.

---

## 1. The Foundation: GUI vs. CLI & Remote Access

### Why Security Professionals Use the CLI

The GUI (Graphical User Interface) is what you see when you use your mouse to click on the Start Menu or File Explorer. The CLI (Command Line Interface) is `cmd.exe` or PowerShell—pure text.

* **Low Bandwidth:** If an attacker compromises a server in another country, streaming a GUI desktop (like RDP) is noisy and slow. Sending text commands over a reverse shell is lightning fast and much harder for network defenders to spot.
* **Living off the Land (LotL):** This is a critical cybersecurity concept. Attackers try to avoid uploading custom malware because antivirus will catch it. Instead, they use the built-in command-line tools already on the system (like the ones in your notes) to do their hacking.

### Remote Access: SSH

**SSH (Secure Shell)** is a cryptographic protocol used to operate network services securely over an unsecured network.

* **Syntax:** `ssh username@IP_Address`
* **How it works:** It creates an encrypted tunnel between your computer and the target. When you type a command on your keyboard, it is encrypted, sent to the target, executed, and the text output is sent back to you.
* **Security Context:** Pentesters use SSH to log into compromised Linux servers. SOC analysts monitor network traffic for SSH connections (usually on Port 22) going to strange external IP addresses, which could indicate data exfiltration.

---

## 2. Situational Awareness: Who am I? Where am I?

When a penetration tester first gets a command-line shell on a Windows machine, they are "flying blind." They immediately run situational awareness commands to figure out what kind of system they have landed on.

### `ver` and `systeminfo`

* **`ver`:** Simply prints the Windows version.
* **`systeminfo`:** This is a goldmine of information. It outputs the OS version, whether it's a workstation or a server, the hostname, the boot time, and—crucially—**the installed hotfixes (patches)**.

> **Pentesting Context:** Attackers look at the `Hotfix(s)` section of `systeminfo`. If the system hasn't been patched in three years, the attacker immediately knows they can use a public exploit to gain Administrator privileges.

### `set` and The PATH Variable

* **`set`:** Displays all the environment variables. Think of environment variables as sticky notes the operating system leaves around to remember things (like where the temporary folder is, or the name of the logged-in user).
* **The PATH:** This is the most important environment variable. It is a list of folder locations. When you type a command like `ping`, Windows doesn't know where the `ping.exe` file actually lives. It checks the folders listed in the PATH one by one until it finds it.

---

## 3. Network Reconnaissance: Who is talking?

These commands are the absolute bread and butter for both IT troubleshooting and Incident Response (IR).

### The Basics: `ipconfig`, `ping`, and `tracert`

* **`ipconfig /all`:** Shows your network configuration. You will see your **IPv4 address** (your logical address on the network) and your **MAC Address** (the physical, permanent hardware address of your network card).
* **`ping`:** Sends an ICMP Echo Request packet to a target (like `google.com`). If the target is alive and not blocking pings, it replies. It is the easiest way to test if a machine is online.
* **`tracert` (Trace Route):** Shows every router (or "hop") your packet passes through to get to the destination. Useful for seeing exactly where a network connection is failing.

### `nslookup` (Name Server Lookup)

DNS (Domain Name System) is the phonebook of the internet, turning human-readable names (`google.com`) into computer-readable IP addresses (`142.250.190.46`).

* **What it does:** `nslookup` asks the DNS server to give you the IP address for a domain name, or vice-versa.
* **Security Context:** Attackers often use malicious domains for Command and Control (C2). SOC analysts use `nslookup` to investigate weird domain names found in firewall logs to see where they resolve.

### `netstat` (Network Statistics)

If you only remember one network command, make it this one. It shows you every active network connection your computer is making.

<img width="311" height="321" alt="image" src="https://github.com/user-attachments/assets/36c5aded-db7b-4531-b9fe-014a3d201f74" />


The golden command for Incident Responders is:
`netstat -abno`

| Flag | What it does | Why it matters |
| --- | --- | --- |
| `-a` | Displays **All** active connections and listening ports. | You want to see ports waiting for connections, not just active ones. |
| `-b` | Displays the **Binary** (executable) involved. | Shows you *which* program is making the connection (Requires Admin). |
| `-n` | Displays addresses and ports in **Numeric** form. | Stops Windows from trying to resolve names, making the command run much faster. |
| `-o` | Displays the **Owning** Process ID (PID). | Gives you the exact ID number of the program, so you can kill it. |

> **Threat Hunting Context:** If a SOC analyst runs `netstat -abno` and sees `notepad.exe` holding an established connection to a server in Russia over Port 4444, they instantly know the machine is compromised. Notepad should never connect to the internet.

---

## 4. Navigating the File System

When an attacker establishes a shell, they need to move around the system to find sensitive files, passwords, or data to steal.

* **`cd` (Change Directory):** Moves you around. `cd \` takes you to the absolute root of the drive (like `C:\`). `cd ..` moves you up one folder.
* **`dir` (Directory):** Lists the contents of the folder you are currently in.
* *Beginner Mistake:* Forgetting to use `dir /a`. Malware often hides itself by setting the "hidden" attribute on the file. Standard `dir` won't show it; `dir /a` shows everything.


* **`type`:** Prints the contents of a text file directly into the terminal window. (This is the Windows equivalent of the Linux `cat` command).
* **`more`:** If you `type` a huge file, it will scroll past the screen in half a second. Using `type notes.txt | more` pipes the output to the `more` command, which pauses the text page by page.

---

## 5. Process Hunting: Finding the Bad Guys

Every program running on a computer is called a **Process**, and the OS assigns every process a unique number called a **PID (Process Identifier)**.

### `tasklist` and `taskkill`

* **`tasklist`:** Shows a list of every running process, its PID, and how much memory it is using.
* **`taskkill`:** Forcefully terminates a process.

**How Defenders use this:**
Let's tie it all together with an Incident Response scenario:

1. You run `netstat -abno` and see a malicious connection on PID 4012.
2. You run `tasklist /FI "PID eq 4012"` to filter the list and see the name of the rogue process. (Let's say it's called `evil.exe`).
3. You run `taskkill /PID 4012 /F` to force-kill the malware and cut off the attacker's connection.

---

## Final Thoughts

You are absolutely right in your Key Learning Outcome: this room is foundational. Whether you end up doing Active Directory exploitation, digital forensics, or network defense, you will use these commands daily.
