# TryHackMe - Blue

## Overview

This repository documents my learning journey through the **Blue** room on TryHackMe. The room introduces one of the most well-known Windows vulnerabilities, **MS17-010 (EternalBlue)**, and demonstrates how attackers can discover, exploit, escalate privileges, extract password hashes, crack credentials, and locate sensitive information on a compromised Windows system.

The goal of this repository is **education**, not simply solving the room. It focuses on understanding the concepts, developing a logical methodology, and building practical cybersecurity knowledge that can be applied in future assessments.

---

## Learning Objectives

By completing this room, I learned how to:

* Perform reconnaissance using Nmap.
* Identify vulnerable services through version enumeration.
* Research publicly known vulnerabilities.
* Understand the EternalBlue vulnerability (MS17-010).
* Use Metasploit to exploit a vulnerable Windows machine.
* Configure exploit modules and payloads.
* Upgrade a command shell to a Meterpreter session.
* Perform privilege verification.
* Migrate Meterpreter into another process.
* Dump Windows password hashes.
* Crack NTLM password hashes.
* Navigate the Windows filesystem after compromise.
* Locate important files and capture flags.

---

## Topics Covered

* Nmap Enumeration
* SMB Enumeration
* Windows Service Version Detection
* MS17-010 (EternalBlue)
* Metasploit Framework
* Payload Configuration
* Meterpreter
* Privilege Escalation
* Process Migration
* Windows Password Hashes
* Hash Dumping
* Password Cracking
* Windows File System Navigation

---

## Learning Workflow

### 1. Reconnaissance

The room begins by identifying open ports using Nmap. Rather than guessing vulnerabilities, the process teaches how service versions provide valuable clues for further investigation.

Key concept learned:

* Enumeration always comes before exploitation.

---

### 2. Vulnerability Research

Instead of immediately launching exploits, the room encourages researching discovered services.

Skills practiced:

* Reading service banners
* Searching Exploit-DB
* Matching Windows versions
* Identifying MS17-010

---

### 3. Exploitation

Using Metasploit, the vulnerable SMB service is exploited through the EternalBlue module.

Important concepts:

* Selecting the correct exploit
* Configuring required options
* Understanding payloads
* Establishing a remote shell

---

### 4. Shell Management

After obtaining a shell, it is upgraded into a Meterpreter session.

This demonstrates:

* Why Meterpreter provides additional capabilities
* How post-exploitation modules work
* Session management inside Metasploit

---

### 5. Privilege Verification

The room verifies that the compromised session is running with **NT AUTHORITY\SYSTEM**, demonstrating complete system compromise.

---

### 6. Process Migration

Meterpreter is migrated into another Windows process to create a more stable session.

This introduces:

* Windows processes
* Process IDs (PID)
* Session stability

---

### 7. Password Hash Extraction

Windows password hashes are extracted from the compromised machine.

Concepts learned:

* Password hashes
* NTLM authentication
* Offline password attacks

---

### 8. Password Cracking

The extracted NTLM hash is cracked to recover the user's password.

Important lesson:

Hashes are not encrypted passwords. They represent passwords mathematically and may be cracked if weak.

---

### 9. Windows File Exploration

The final section reinforces Windows directory structure by locating important files and discovering hidden flags.

---

## Challenges I Encountered

During the room, several technical challenges occurred:

* Meterpreter sessions occasionally died unexpectedly.
* Exploits did not always succeed on the first attempt.
* Process migration sometimes failed.
* Target machine occasionally required restarting.
* Exploitation proved to be unreliable at times.

These experiences reinforced an important lesson:

**Real-world exploitation is rarely perfect. Troubleshooting is an essential cybersecurity skill.**

---

## Key Takeaways

* Enumeration determines the success of exploitation.
* Service versions often reveal known vulnerabilities.
* Research should always precede exploitation.
* Meterpreter provides significantly more functionality than a basic shell.
* SYSTEM privileges provide complete control over a Windows host.
* Weak passwords remain vulnerable even when stored as hashes.
* Patience and troubleshooting are part of penetration testing.

---

## Beginner Practice

After completing this room, try practicing the following:

* Perform Nmap scans against multiple vulnerable machines.
* Research service versions using Exploit-DB.
* Practice identifying vulnerable SMB services.
* Learn common Metasploit commands.
* Study Windows directory structure.
* Learn the difference between LM and NTLM hashes.
* Practice hash cracking in a safe lab environment.

---

## Skills Developed

* Enumeration
* Vulnerability Identification
* Exploit Research
* Metasploit Usage
* Windows Post-Exploitation
* Meterpreter Operations
* Privilege Verification
* Password Hash Analysis
* Windows Navigation
* Troubleshooting

---

## Disclaimer

This repository is intended solely for educational purposes. All activities were performed within the TryHackMe training environment. Do not attempt these techniques against systems without explicit authorization.
