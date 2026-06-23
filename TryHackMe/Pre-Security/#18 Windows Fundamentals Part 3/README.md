# Windows Fundamentals Part 3

## Room Information

| Room       | Windows Fundamentals Part 3 |
| ---------- | --------------------------- |
| Platform   | TryHackMe                   |
| Category   | Windows Fundamentals        |
| Difficulty | Beginner                    |
| Focus Area | Windows Security Features   |

---

# Overview

Windows Fundamentals Part 3 focuses on the built-in security features available within the Windows operating system. Throughout this room, I explored how Windows protects users, devices, applications, and data using various security mechanisms such as Windows Update, Windows Security, Microsoft Defender, Firewall, BitLocker, TPM, and Volume Shadow Copy Service.

This room helped me understand that Windows security is not just a single antivirus program. Instead, multiple security layers work together to protect the operating system from threats, malware, unauthorized access, and data loss.

---

# Learning Objectives

By completing this room, I learned:

* The purpose of Windows Update and Patch Tuesday.
* How Windows Security helps protect a system.
* The role of Microsoft Defender Antivirus.
* How Firewall profiles protect network communications.
* The importance of SmartScreen and Browser Protection.
* How Device Security uses TPM for hardware-based protection.
* How BitLocker protects sensitive data through encryption.
* The purpose of Volume Shadow Copy Service (VSS).
* Why attackers and ransomware frequently target backup mechanisms.

---

# Topics Covered

## Windows Update

Windows Update is Microsoft's service for delivering:

* Security patches
* Feature updates
* Bug fixes
* Defender definition updates

One important concept introduced in this room was Patch Tuesday, which refers to Microsoft's regular monthly security update release schedule.

### What I Learned

Before completing this room, I mainly viewed Windows Updates as feature upgrades that often required a reboot. This room helped me understand that updates are actually one of the most important security controls because they patch vulnerabilities that attackers may actively exploit.

---

## Windows Security

Windows Security serves as a central dashboard for managing the protection of a Windows system.

Major protection areas include:

* Virus & Threat Protection
* Firewall & Network Protection
* App & Browser Control
* Device Security

### Security Status Indicators

| Status | Meaning                       |
| ------ | ----------------------------- |
| Green  | Device is protected           |
| Yellow | Recommended actions available |
| Red    | Immediate attention required  |

### What I Learned

While exploring Windows Security, I realized how useful the status indicators are for quickly identifying security issues. It provides a centralized location where users can monitor multiple security components at once.

---

## Virus & Threat Protection

Microsoft Defender Antivirus provides protection against malware and malicious software.

Available scan types include:

* Quick Scan
* Full Scan
* Custom Scan

Additional protection features include:

* Real-Time Protection
* Cloud-Delivered Protection
* Automatic Sample Submission
* Controlled Folder Access
* Exclusions Management

### What I Learned

One observation I found interesting was that Real-Time Protection was disabled in the lab environment. Initially, I wondered why a security feature would be turned off. After reading further, I learned it was disabled to improve performance because the virtual machine had no internet access and was isolated from external threats.

This helped me understand that security configurations often depend on the environment being used.

---

## Firewall and Network Protection

Windows Defender Firewall controls incoming and outgoing network traffic.

The room introduced three firewall profiles:

### Domain Profile

Used when a system is connected to a domain environment.

### Private Profile

Used for trusted home or private networks.

### Public Profile

Used for untrusted networks such as:

* Airports
* Hotels
* Coffee shops
* Public Wi-Fi hotspots

### What I Learned

This section made me think differently about public Wi-Fi. I had previously connected to public networks without considering how Windows changes security settings based on network type. Understanding firewall profiles showed me how Windows automatically adapts security depending on the environment.

---

## App and Browser Control

This section introduced Microsoft Defender SmartScreen.

SmartScreen helps protect users from:

* Malicious websites
* Phishing attacks
* Suspicious downloads
* Untrusted applications

### What I Learned

I learned that many attacks begin through simple user actions such as downloading files or visiting malicious websites. SmartScreen acts as an additional layer of defense before threats can execute.

---

## Device Security

Device Security focuses on hardware-based protections.

Key concepts include:

* Core Isolation
* Memory Integrity
* Security Processor
* Trusted Platform Module (TPM)

### Trusted Platform Module (TPM)

TPM is a dedicated hardware component designed to securely perform cryptographic operations.

Benefits include:

* Secure key storage
* Hardware-based security
* Protection against tampering
* Support for encryption technologies

### What I Learned

Before this room, I had heard TPM mentioned in discussions about Windows 11 requirements but never fully understood its purpose. Learning about TPM helped me see how modern security relies on both software and hardware protections working together.

---

## BitLocker

BitLocker is Microsoft's full-disk encryption solution.

It helps protect data if a device is:

* Lost
* Stolen
* Improperly decommissioned

BitLocker works best when combined with TPM.

### What I Learned

This section highlighted the importance of encryption. I realized that even if someone physically steals a device, encrypted data remains protected if proper security controls are in place.

---

## Volume Shadow Copy Service (VSS)

Volume Shadow Copy Service creates snapshots of files and system states that can later be used for recovery purposes.

Common uses include:

* Restore Points
* System Recovery
* Backup Operations

### Security Relevance

Many ransomware families attempt to delete shadow copies before encrypting files because they know recovery becomes much harder without backups.

### What I Learned

This was one of the most interesting sections of the room. I had previously heard about ransomware deleting backups but never understood the exact Windows feature being targeted. Learning about VSS connected the concepts of backups, recovery, and ransomware defense together.

---

# Key Takeaways

* Security updates are critical for vulnerability management.
* Microsoft Defender provides multiple layers of protection beyond antivirus scanning.
* Firewall profiles help secure systems in different network environments.
* SmartScreen protects users from web-based threats.
* TPM provides hardware-level security functions.
* BitLocker helps prevent unauthorized access to sensitive data.
* Volume Shadow Copy Service plays an important role in recovery and ransomware resilience.
* Windows security relies on layered defenses rather than a single protection mechanism.

---

# Personal Reflection

Windows Fundamentals Part 3 helped me better understand the security side of the Windows operating system. While previous Windows Fundamentals rooms focused more on navigation, system utilities, and operating system components, this room explained how Windows actively protects users and data.

The biggest lesson I took away from this room is that many security features operate silently in the background. Most users rarely interact with TPM, BitLocker, SmartScreen, or VSS directly, yet these technologies play a major role in keeping systems secure.

As someone interested in cybersecurity, understanding these built-in Windows security mechanisms is important because defenders rely on them for protection, while attackers often look for ways to bypass, disable, or abuse them.

---

# Skills Gained

* Windows Security Navigation
* Microsoft Defender Basics
* Windows Firewall Fundamentals
* Endpoint Protection Concepts
* TPM Fundamentals
* BitLocker Basics
* Backup and Recovery Concepts
* Windows Security Awareness
* Defensive Security Foundations

---

# Conclusion

Windows Fundamentals Part 3 provided a practical introduction to the security features built into Windows. The room demonstrated how Microsoft uses multiple defensive layers to protect devices, users, applications, and data.

For beginners entering cybersecurity, this room serves as a strong foundation for understanding Windows security concepts that are commonly encountered in system administration, SOC operations, incident response, malware analysis, and defensive security roles.
