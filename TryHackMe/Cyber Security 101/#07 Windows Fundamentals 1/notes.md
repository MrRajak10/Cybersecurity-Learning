Welcome to **Windows Fundamentals**. You have hit on a crucial truth in your notes: before you can secure a system, hunt for threats, or execute an attack, you must understand how the environment operates under normal conditions.

Many beginners want to skip straight to the hacking tools, but the best penetration testers and SOC analysts are often just experts in how the operating system is *supposed* to work. If you don't know what normal looks like, you will never spot the abnormal.

Let’s expand on your notes, break down the technical internals, and connect these concepts directly to real-world cybersecurity operations.

---

## 1. The Operating System and GUI

### What it is

The Operating System (OS) is the bridge between the physical hardware (CPU, RAM, Hard Drive) and the software applications you want to run.

* **Analogy:** Think of a computer like a massive restaurant. The hardware is the kitchen and ingredients. The applications are the customers placing orders. The OS is the restaurant manager—it takes the orders, tells the kitchen what to do, ensures no one customer takes all the food (memory management), and delivers the results.

The **Graphical User Interface (GUI)** is the visual dashboard (Desktop, Taskbar, Start Menu) that makes interacting with the manager easy.

### Cybersecurity Context

* **Red Team (Attackers):** Attackers rarely use the GUI. When they compromise a system, they usually get a "shell" (command-line access). However, they need to know how the GUI works because they often steal data from GUI-centric locations, like the user's Desktop or recent files.
* **Blue Team (Defenders):** Digital Forensics and Incident Response (DFIR) professionals hunt for evidence in GUI artifacts. For example, Windows tracks every program a user clicks in the Start Menu or pins to the Taskbar. Defenders analyze these logs to prove a malicious file was executed by a specific user.

---

## 2. File Systems: FAT vs. NTFS

### What is a File System?

If a hard drive is an empty warehouse, the file system is the shelving unit and inventory catalog that dictates exactly how and where data is stored.

| File System | Characteristics | Security Perspective |
| --- | --- | --- |
| **FAT16 / FAT32** | Older, highly compatible (used on USB drives). Max file size 4GB (FAT32). | **No built-in security.** If you can plug in the drive, you can read and modify all the files. |
| **NTFS** | New Technology File System. The Windows default. Handles massive files. | **Highly secure.** Supports file-level permissions, encryption (EFS), and activity journaling. |

### Cybersecurity Context

NTFS is foundational to Windows security because it introduced **Access Control Lists (ACLs)**. Before NTFS, if multiple people shared a computer, anyone could read anyone else's files. NTFS ensures that User A cannot read User B's tax documents unless explicitly granted permission.

> **Important Concept:** NTFS also supports **Alternate Data Streams (ADS)**. This allows data to be hidden "behind" a normal file. Attackers sometimes use ADS to hide malicious scripts inside an innocent-looking text file without changing the file's visible size!

---

## 3. Critical Windows Folders

Understanding where things live is critical for both attacking and defending.

### `C:\Windows\System32`

This is the heart of the operating system. It contains the core executables (like `cmd.exe` or `calc.exe`) and **DLLs** (Dynamic Link Libraries — shared code that programs use to function).

* **Defender View:** This folder is highly restricted. If a SOC analyst sees a random, unsigned file named `svchost.exe` trying to run from a temporary folder instead of `System32`, alarm bells go off.

### `C:\Users\<Username>`

This holds the user profile. Inside is a hidden folder called `AppData`.

* **Attacker View:** Because a standard user does not have permission to install programs into `Program Files`, attackers (and sometimes legitimate apps like Google Chrome) will install their software directly into `AppData` to bypass security restrictions.

---

## 4. Environment Variables

### What they are

Environment Variables are dynamic shortcuts the operating system uses to find things.

* Instead of hardcoding the path `C:\Users\MrRajak\AppData\Local\Temp`, Windows just uses `%TEMP%`. No matter who logs in, `%TEMP%` always routes to the correct user's temporary folder.

### The `%PATH%` Variable

The most important variable is `%PATH%`. It tells Windows where to look for commands. If you type `ping` into a command prompt, Windows checks every folder listed in the `%PATH%` variable until it finds `ping.exe`.

### Cybersecurity Context

* **Path Interception:** If an attacker can modify the `%PATH%` variable, they can add their own malicious folder to the very beginning of the list. Then, when an administrator types a common command, Windows runs the attacker's malicious version first.

---

## 5. User Account Control (UAC)

### What it is and How it Works

UAC is the security prompt that darkens your screen and asks, *"Do you want to allow this app to make changes to your device?"*.

Here is the brilliant internal mechanic behind UAC:
When you log into Windows as an Administrator, Windows actually gives you **two separate ID badges (Access Tokens)**:

1. A Standard User token.
2. A Full Administrator token.

By default, every program you open (browsers, games, Word) runs using the **Standard User token**. You are technically an admin, but you are operating with stripped-down privileges.

When you try to do something dangerous (like install software), Windows pauses everything, switches to a "Secure Desktop" (which prevents malware from auto-clicking the button), and asks for your consent. If you click "Yes," Windows temporarily applies your Full Administrator token to that specific task.

### Cybersecurity Context

* **UAC Bypass:** UAC is designed to prevent accidental damage, but Microsoft does not consider it a strict "security boundary". Penetration testers and malware frequently use techniques to trick Windows into auto-elevating their malicious scripts without prompting the user, a process known as a UAC Bypass.

---

## 6. File Permissions (NTFS Permissions)

Permissions dictate exactly what an authenticated user is allowed to do with a specific file.

| Permission | What it allows |
| --- | --- |
| **Read** | Open the file and view its contents. |
| **Write** | Create new files or modify the contents of an existing file. |
| **Execute** | Run the file as a program or script. |
| **Modify** | Read, write, execute, and delete the file. |
| **Full Control** | Do everything above, plus change the permissions for other users. |

### Cybersecurity Context

* **Privilege Escalation:** A classic penetration testing technique involves hunting for poorly configured file permissions. If a system administrator installs a high-level background service but accidentally grants the "Users" group **Write** permissions to the folder, an attacker can delete the legitimate service file, replace it with a malicious one, and wait for the system to restart. The OS will then execute the malware with system-level privileges.

---

## 7. Task Manager

### What it is

Task Manager is your live diagnostic dashboard. It shows running processes, memory consumption, disk usage, and network activity.

### Cybersecurity Context

* **Threat Hunting:** Malware tries to hide. It will rarely name itself `virus.exe`. Instead, it will name itself something that looks normal, like `svch0st.exe` (using a zero instead of an 'o'). A sharp defender uses Task Manager to spot these anomalies by checking the spelling, observing unusually high CPU usage, or right-clicking a suspicious process and selecting "Open file location" to see if it is running from the correct system folder.

---

## Summary of Your Growth

By understanding these fundamentals, you are building the foundation required to understand attacks. You can't grasp a "UAC Bypass" without understanding what UAC is, and you can't understand "DLL Hijacking" without knowing how Environment Variables work.

You are doing excellent work taking these detailed notes.
