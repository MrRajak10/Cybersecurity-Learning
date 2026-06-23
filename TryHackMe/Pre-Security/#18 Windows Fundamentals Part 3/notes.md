# Windows Fundamentals 3 - Notes

## Room Overview

This room focuses on the built-in security features of Windows. Unlike the previous Windows Fundamentals rooms that introduced the operating system and administrative utilities, this room explores how Windows protects users, devices, files, and data from various security threats.

Throughout this room, I learned that Windows includes many security mechanisms by default, and most users rely on them daily without realizing how important they are. Understanding these features helped me gain a better appreciation of Windows security from both a user and cybersecurity perspective.

---

# Windows Update

## What is Windows Update?

Windows Update is a Microsoft service that delivers:

* Security updates
* Bug fixes
* Feature improvements
* Microsoft Defender updates

Microsoft usually releases updates on the second Tuesday of every month, commonly known as **Patch Tuesday**.

Critical security patches can also be released outside the normal schedule if immediate action is required.

## Accessing Windows Update

Windows Update can be accessed through:

* Settings → Update & Security
* Run Dialog Box

Command:

```text
control /name Microsoft.WindowsUpdate
```

## Why Windows Updates Matter

Regular updates help:

* Fix security vulnerabilities
* Protect against newly discovered threats
* Improve system stability
* Keep Microsoft Defender definitions current

## Personal Learning Note

Before this room, I mostly thought of Windows Updates as feature upgrades that sometimes forced system restarts. After learning about Patch Tuesday and security patches, I realized updates are one of the most important defenses against newly discovered vulnerabilities.

---

# Windows Security

## What is Windows Security?

Windows Security is the central dashboard used to manage and monitor Windows protection features.

Main Protection Areas:

* Virus & Threat Protection
* Firewall & Network Protection
* App & Browser Control
* Device Security

## Security Status Indicators

### Green

Device is protected.

### Yellow

Recommended action is available.

### Red

Immediate attention is required.

## Personal Learning Note

The color-based alert system makes it easy to quickly identify security issues. This reminded me of how SOC analysts prioritize alerts based on severity levels.

---

# Virus and Threat Protection

## Purpose

Protects the system from:

* Malware
* Viruses
* Trojans
* Ransomware
* Other malicious software

---

## Scan Types

### Quick Scan

Checks common locations where malware is typically found.

### Full Scan

Scans all files and running processes.

### Custom Scan

Allows scanning of selected files or folders.

---

## Threat History

### Last Scan

Shows previous scan activity.

### Quarantined Threats

Dangerous files isolated from the system.

### Allowed Threats

Threats manually permitted to run.

**Warning:** Only allow files if you fully trust them.

---

## Protection Settings

### Real-Time Protection

Continuously monitors for malware activity.

### Cloud-Delivered Protection

Uses Microsoft's cloud intelligence for faster threat detection.

### Automatic Sample Submission

Sends suspicious files to Microsoft for analysis.

### Controlled Folder Access

Protects important folders from unauthorized changes.

### Exclusions

Files or folders excluded from scans.

### Notifications

Displays security alerts and updates.

---

## Ransomware Protection

Uses Controlled Folder Access to help prevent ransomware from encrypting important files.

---

## Personal Learning Note

One interesting observation was that Real-Time Protection was intentionally disabled in the lab environment. This helped me understand how important this feature is in real-world systems. I would never disable it on a personal machine unless another trusted security product was providing protection.

---

# Firewall and Network Protection

## What is a Firewall?

A firewall controls network traffic entering and leaving a device.

It acts like a security guard by deciding what traffic is allowed and what traffic should be blocked.

---

## Firewall Profiles

### Domain Profile

Used when connected to an Active Directory domain.

### Private Profile

Used for trusted home or private networks.

### Public Profile

Used for untrusted public networks.

Examples:

* Airports
* Hotels
* Cafes
* Public Wi-Fi

---

## Why Firewalls Matter

Firewalls help:

* Block unauthorized access
* Restrict malicious traffic
* Protect network services
* Reduce attack surface

---

## Personal Learning Note

I had previously seen Public and Private network options in Windows but never understood their purpose. This room helped me understand that each profile applies different security rules depending on the environment.

---

# App and Browser Control

## Microsoft Defender SmartScreen

SmartScreen helps protect users from:

* Phishing websites
* Malicious downloads
* Unrecognized applications

---

## Features

### Check Apps and Files

Evaluates downloaded files before execution.

### Exploit Protection

Provides built-in protection against software exploitation techniques.

---

## Security Importance

SmartScreen provides an additional layer of defense before malicious files can execute on the system.

---

# Device Security

## Core Isolation

Protects critical operating system processes from malicious code injection.

---

## Memory Integrity

Uses virtualization-based security to prevent malicious code from accessing protected processes.

---

## Trusted Platform Module (TPM)

### What is TPM?

TPM stands for:

**Trusted Platform Module**

A hardware-based security chip that:

* Stores cryptographic keys
* Supports secure boot processes
* Assists encryption technologies
* Provides hardware-level protection

---

## Personal Learning Note

Before this room, I had heard TPM mentioned frequently when discussing Windows 11 requirements, but I never fully understood its purpose. Learning how TPM supports encryption and device security gave me a much clearer understanding of its importance.

---

# BitLocker

## What is BitLocker?

BitLocker is Microsoft's disk encryption technology.

It protects data from:

* Theft
* Unauthorized access
* Lost devices
* Stolen computers

---

## How BitLocker Works

BitLocker encrypts data stored on a drive.

Even if an attacker physically removes the hard drive, the data remains inaccessible without proper authentication.

---

## TPM and BitLocker

BitLocker works best when combined with TPM.

If TPM is unavailable, a:

**USB Startup Key**

can be used for authentication.

---

## Personal Learning Note

This section helped me understand how hardware security and encryption work together. Previously, I viewed encryption and TPM as separate concepts, but now I see how they complement each other to secure data.

---

# Volume Shadow Copy Service (VSS)

## What is VSS?

VSS stands for:

**Volume Shadow Copy Service**

It creates snapshots of files and system data.

These snapshots can be used for:

* Backups
* Recovery
* System Restore

---

## Benefits

### Restore Points

Allow recovery after system issues.

### File Recovery

Recover previous file versions.

### Backup Consistency

Ensures reliable backups while files remain in use.

---

## Security Perspective

Many ransomware families attempt to delete shadow copies before encrypting files.

Why?

Because shadow copies can help victims restore data without paying the ransom.

---

## Personal Learning Note

This was one of the most interesting sections for me. I learned that ransomware often targets backups first. It showed me why security professionals always recommend maintaining offline or off-site backups.

---

# Key Takeaways

* Windows Update is critical for patching vulnerabilities.
* Windows Security serves as the central security dashboard.
* Real-Time Protection continuously monitors threats.
* Firewalls regulate inbound and outbound network traffic.
* SmartScreen helps prevent phishing and malicious downloads.
* TPM provides hardware-based security.
* BitLocker protects data through encryption.
* Volume Shadow Copy Service assists with backup and recovery.
* Ransomware often attempts to remove recovery mechanisms before encryption.
* Built-in Windows security features provide multiple layers of defense.

---

# Final Reflection

This room helped me understand that Windows security is much more than antivirus software. Multiple security layers work together to protect a system, including updates, firewalls, encryption, hardware security, and recovery mechanisms.

As someone learning cybersecurity, this room helped me connect everyday Windows features with real-world defensive security concepts. Many of these technologies are commonly encountered by SOC analysts, system administrators, and security professionals, making this foundational knowledge valuable for future learning.
