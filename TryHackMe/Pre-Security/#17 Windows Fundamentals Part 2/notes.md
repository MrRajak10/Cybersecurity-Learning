# Windows Fundamentals Part 2: Comprehensive Learning Resource

**Learner Profile:** [Mr.Rajak on TryHackMe](https://tryhackme.com/p/Mr.Rajak) | [mr-rajak-10 on GitHub](https://github.com/mr-rajak-10)
**Module:** Windows Fundamentals Part 2

Welcome to this deep-dive into Windows Fundamentals. In this guide, we are not just going to read what the Windows tools are; we are going to understand *how* they breathe, *why* they were built, and *how* both attackers and defenders manipulate them. Let’s break down your notes step by step.

---

## 1. System Configuration (`msconfig`)

### What it is and Why it exists

`msconfig` (Microsoft System Configuration Utility) is a built-in troubleshooting tool designed to help administrators isolate and fix problems related to how the Windows operating system boots (starts up).

### What problem it solves

Imagine your computer takes 20 minutes to turn on, or it crashes the moment you log in. You need a way to tell Windows, "Next time you restart, only load the bare minimum so I can figure out what is breaking." `msconfig` solves this by giving you granular control over the startup process.

### Real-World Analogy

Think of booting up a computer like opening a restaurant for the day. Normally, the chefs, waiters, and cleaners all arrive at once (Normal Startup). But if someone keeps setting the kitchen on fire every morning, you might tell only the head chef to come in so you can monitor exactly what is going wrong (Diagnostic Startup).

### Technical Breakdown of the Tabs

* **General Tab:** This is your master switch.
* *Normal Startup:* Loads everything.
* *Diagnostic Startup:* Loads only basic Windows services and drivers (like Safe Mode, but slightly different).
* *Selective Startup:* Allows you to manually pick and choose whether you want system services or startup items to load.


* **Boot Tab:** Controls the actual bootloader (the program that loads Windows).
* *Safe Boot:* Forces Windows to load with the absolute minimum drivers required. If a bad graphics driver is causing your screen to go black, Safe Boot bypasses it.
* *No GUI Boot:* Turns off the Windows loading screen animation. It saves a tiny bit of time and shows you text instead.
* *Boot Log:* Tells Windows to write a text file (`ntbtlog.txt`) documenting every single driver that loaded or failed to load.


* **Services Tab:** A "Service" is simply a program that runs invisibly in the background without a user interface (like the program that manages your printing queue). This tab lets you turn them off.
* *Pro-Tip:* There is a checkbox here called "Hide all Microsoft services." If you check this, you will only see services created by third-party software (like antivirus, game launchers, or malware!).


* **Startup Tab:** Historically, this is where you managed programs that launch when you log in (like Spotify or Discord). In modern Windows, Microsoft moved this feature to the Task Manager because it is easier for average users to find.
* **Tools Tab:** A convenient shortcut menu to launch other advanced Windows tools (like the Registry Editor or Event Viewer) directly from `msconfig`.

### Cybersecurity Context

* **Incident Response (IR) & SOC:** When an analyst suspects a computer is infected, they check `msconfig`. Malware loves to establish "persistence" (making sure it survives a reboot) by adding itself as a startup service.
* **Penetration Testing / CTFs:** If you gain low-level access to a Windows machine, checking the startup services might reveal a poorly configured program that you can exploit to gain Administrator privileges.
* **Common Beginner Mistake:** Unchecking everything in the Services tab without checking "Hide all Microsoft services." If you disable vital Windows services, the computer may not boot at all!

---

## 2. Advanced System Settings (`sysdm.cpl`)

### What it is

`sysdm.cpl` is a Control Panel applet that gives you access to the deep, core behaviors of the Windows operating system, specifically regarding performance and how the system handles critical failures.

### Virtual Memory (The Page File)

**How it works internally:**
Computers have RAM (Random Access Memory), which is extremely fast but limited in size. If you open 100 Google Chrome tabs, your RAM will fill up. Instead of crashing, Windows uses a file on your hard drive called `pagefile.sys`. It takes the data from the RAM that you aren't actively using right now and moves it to the hard drive to free up space.

**Real-World Analogy:**
Imagine your RAM is your physical desk, and the hard drive is a filing cabinet. Your desk can only hold so many documents at once. When it gets full, you take the papers you aren't currently reading and put them in the filing cabinet (Virtual Memory). When you need them again, you swap them back to your desk.

**Cybersecurity Context (Forensics):**
Digital forensics experts absolutely *love* the `pagefile.sys`. Because it acts as overflow for RAM, it often contains things that were never meant to be saved to the hard drive—such as unencrypted passwords, private chat messages, or even the decrypted payload of a ransomware attack!

### Startup and Recovery (Memory Dumps)

**What it is:** When Windows experiences a fatal error (the "Blue Screen of Death" or BSOD), it panics and suddenly stops. Before it dies, it takes a "snapshot" of whatever was in the RAM at that exact moment and saves it as a file. This is called a memory dump.

* *Small Memory Dump:* Just the error code and basic details.
* *Complete Memory Dump:* A massive file containing exactly what was in the entire RAM when the crash happened.

**Cybersecurity Context (Malware Analysis):**
Some advanced malware (like rootkits) operate deep inside the Windows kernel. If they cause the system to crash, a malware analyst can take the memory dump file, open it in a debugger, and literally see the malicious code that caused the crash.

---

## 3. User Account Control (UAC)

### What it is and Why it exists

UAC is the prompt that pops up and dims your screen, asking: *"Do you want to allow this app to make changes to your device?"* It was introduced to solve a massive security flaw in older versions of Windows where any program you ran automatically had the power to destroy the operating system.

### How it works internally

Even if you are logged in as an Administrator, Windows actually treats you as a standard user during normal use. When a program needs to do something dangerous (like edit the Registry or install software), UAC forces the system to pause. It requires an explicit "Yes" from a human (or a password if you are a standard user) to temporarily grant that program an "Administrator Token."

**Real-World Analogy:**
Imagine you are the CEO of a company, but you are walking around the office in casual clothes. You can do normal things like use the coffee machine. But if you try to open the company vault, the security guard (UAC) stops you and says, "I know you are the CEO, but I still need to see your badge to prove it's really you and not someone who stole your jacket."

### Cybersecurity Context

* **Penetration Testing:** "UAC Bypass" is a major phase in offensive security. Attackers look for flaws in Windows to trick the system into granting Administrator rights without the UAC prompt ever appearing on the user's screen.
* **Common Beginner Mistake:** Users often find the UAC prompt annoying and change the setting to "Never Notify." This is incredibly dangerous. If you click a bad link, the malware will silently execute with full administrative privileges without ever warning you.

---

## 4. Computer Management (`compmgmt.msc`)

You accurately noted that this tool acts as a central dashboard. It is a unified console (Microsoft Management Console) that groups together the most important administrative tools. Let’s break down its core components.

### A. Task Scheduler

**What it is:** A utility that allows Windows to execute programs or scripts automatically at specific times or when specific conditions are met.

**Your Observation:** *"I noticed many scheduled tasks already configured by Windows and installed software."*
This is a brilliant observation. Software updaters (like Google Chrome's updater) use this to silently check for updates at 2:00 AM.

**Cybersecurity Context (Threat Hunting):**
Task Scheduler is one of the most common ways attackers maintain **Persistence**. An attacker might gain access, place malware on the computer, and then create a Scheduled Task that says: *"Every time this user logs in, run my malicious script."* In Incident Response, checking the Task Scheduler for weird, unrecognized tasks is step one.

### B. Event Viewer (`eventvwr.msc`)

**What it is:** The central logging system for Windows. Every significant thing that happens on the computer is recorded here as an "Event."

**Your Observation:** *"Seeing different log categories made it easier to understand where security analysts obtain evidence."*
Exactly! If a computer is a crime scene, the Event Viewer is the security camera footage.

* **Application Logs:** Logs from installed software (e.g., MS Word crashed).
* **System Logs:** Logs from the OS itself (e.g., A driver failed to load, or a hard drive is failing).
* **Security Logs:** The most important tab for cybersecurity. This records **Auditing** events.
* *Success Audit:* A user successfully typed their password and logged in.
* *Failure Audit:* Someone tried to log in via Remote Desktop and failed 500 times in one minute (A clear indicator of a Brute Force Attack).



**Cybersecurity Context (SOC):**
SOC analysts don't look at Event Viewer on a single computer. They use tools called SIEMs (Security Information and Event Management) like Splunk or Elastic to pull Event Viewer logs from *thousands* of computers at once. They look for specific "Event IDs" (e.g., Event ID 4624 means successful login; Event ID 4625 means failed login).

### C. Local Users and Groups

**What it is:** This is where you create local user accounts and assign them to groups (like the `Administrators` group or standard `Users` group).

**Cybersecurity Context (Privilege Escalation):**
When a penetration tester hacks a machine as a low-level user, their next goal is to add their compromised user account to the `Administrators` group. Defenders monitor this section closely. If a new user named "Admin123" suddenly appears here, the system has likely been breached.

### D. Disk Management

**What it is:** The graphical tool to format, partition, and manage hard drives.
**Terminology definition - Partition:** A hard drive is a physical piece of hardware. A partition is a logical slice of that drive. You can take a 1TB drive and slice it into a `C:` drive (500GB for Windows) and a `D:` drive (500GB for games).

**Cybersecurity Context:**
Advanced attackers sometimes shrink the user's C: drive, create a hidden partition in the empty space, format it, and hide their malware or stolen data there. It won't show up in a normal File Explorer window, but an analyst will spot it in Disk Management.

---

## 5. System Information (`msinfo32`)

**What it is:** A comprehensive summary of the system’s hardware and software environment.

**Your Observation:** *"This tool felt like a central dashboard for the entire system."*
Spot on. It’s the ultimate blueprint of the machine.

**Cybersecurity Context (Reconnaissance):**
When an attacker or a red teamer successfully gets a foothold on a machine, they need "Situational Awareness." They need to know: Is this a physical laptop or a Virtual Machine? What version of Windows is this? What antivirus drivers are running? By running `msinfo32` (or pulling its data via command line), they can gather all this intelligence to plan their next attack without crashing the system.

---

## 6. Resource Monitor (`resmon.exe`)

**What it is:** An advanced diagnostic tool that shows exactly how computer resources (CPU, RAM, Disk, Network) are being used in real-time.

**Your Observation:** *"Resource Monitor provided much deeper visibility than Task Manager."*
Task Manager tells you *that* a program is using the disk. Resource Monitor tells you *exactly which file* that program is writing to.

**Cybersecurity Context (Live Incident Response):**

* **CPU:** Is a random process named `svch0st.exe` using 99% CPU? It might be a cryptocurrency miner installed by a hacker.
* **Disk:** Is a process rapidly writing thousands of files? It might be Ransomware currently encrypting the hard drive.
* **Network:** Task Manager shows network usage. Resource Monitor shows *what IP address* the program is talking to. If a calculator app is sending gigabytes of data to an IP address in a foreign country, you have caught data exfiltration in action!

---

## 7. Command Prompt Network & Recon Commands

In cybersecurity, the Graphical User Interface (GUI) is a luxury. Often, you will only have a black terminal screen (a reverse shell). You must know these commands:

* **`hostname`**:
* *What it does:* Prints the name of the computer.
* *Cyber Context:* If you hack into a machine, you need to know where you are. If the hostname is `DESKTOP-HR-LAPTOP`, you are on a user's machine. If it is `SRV-DOMAIN-CONTROLLER`, you just hit the jackpot.


* **`whoami`**:
* *What it does:* Prints the current user account executing the terminal.
* *Cyber Context:* Determines your privilege level. Are you `nt authority\system` (God mode)? Or just a standard user?


* **`ipconfig` & `ipconfig /all**`:
* *What it does:* Shows your IP address, Subnet Mask, and Gateway. The `/all` flag shows the MAC address (Physical address) and DNS servers.
* *Cyber Context:* Essential for "pivoting." If an attacker compromises this machine, they use `ipconfig` to see what other internal networks this machine is connected to, so they can spread further into the company.


* **`netstat` (Network Statistics)**:
* *What it does:* Lists all active network connections and listening "ports." (A port is like a specific door into a computer; port 80 is for web traffic, port 445 is for file sharing).
* *States:* `LISTENING` means a program is waiting for a connection (potentially a hacker's backdoor). `ESTABLISHED` means an active conversation is happening right now.
* *Cyber Context:* Threat hunters use `netstat -ano` to find rogue backdoors communicating with hacker Command and Control (C2) servers.


* **`net help`**:
* *What it does:* The `net` command is a powerful suite for managing users, groups, and shares. `net help` teaches you how to use it. For example, `net user administrator /active:yes` enables the hidden admin account.



---

## 8. Windows Registry (`regedit`)

### What it is

The Windows Registry is a massive, hierarchical database that stores low-level settings for the operating system and for applications that opt to use the registry.

### How it works internally

Before the Registry existed, every program had to have its own `.ini` text file to remember its settings (like what color your background should be, or where a program was installed). Microsoft consolidated all these text files into one giant database: The Registry. It is broken down into "Hives" (folders) and "Keys" (values).

**Real-World Analogy:**
The Registry is the DNA of the Windows operating system. It dictates exactly how Windows looks, behaves, and functions. Just like DNA, if you randomly change a piece of it without knowing what you are doing, the organism (the computer) might suffer a fatal mutation and die (fail to boot).

### Cybersecurity Context

* **Malware Persistence:** Remember the Task Scheduler and Startup folders? Attackers also use "Autorun Keys" in the Registry. They add a line to the registry that says: *"When Windows boots, run malware.exe."*
* **Defense Evasion:** Attackers can edit the Registry to silently turn off Windows Defender, disable the firewall, or hide their files.
* **Digital Forensics:** The Registry tracks *everything*. It tracks every USB drive ever plugged into the computer, the last 20 files the user opened, and what programs were executed. Forensic investigators pull the Registry to reconstruct a timeline of a cybercrime.

---

## Conclusion & Next Steps for Your Journey

Your final thoughts on this room were incredibly accurate. Many beginners view IT Administration and Cybersecurity as two different fields. They are not. **Cybersecurity is simply the mastery of IT Administration, applied offensively and defensively.**

You cannot hack a system, nor can you defend it, if you do not understand how it works normally. By understanding Event Viewer, you now know how SOC Analysts catch hackers. By understanding Task Scheduler and the Registry, you now know where hackers hide. By understanding Resource Monitor and `netstat`, you now know how to hunt for active threats.

Keep these notes close as you progress on TryHackMe. As you start doing offensive rooms, you will find yourself using `whoami`, `netstat`, and `ipconfig` constantly. Keep up the excellent work!
