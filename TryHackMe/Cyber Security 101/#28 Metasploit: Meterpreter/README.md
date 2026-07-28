# TryHackMe - Metasploit: Meterpreter

> A learning-focused repository documenting my journey through the **Meterpreter** room on TryHackMe.

---

## Room Overview

This room introduces **Meterpreter**, one of the most powerful payloads provided by the Metasploit Framework. Instead of focusing only on obtaining access to a target machine, this room teaches how attackers and penetration testers interact with a compromised system during the **post-exploitation phase**.

Throughout the room, I learned how Meterpreter works internally, why it is different from a normal shell, how its payloads are selected, how to use common Meterpreter commands, and how these commands support post-exploitation activities.

The room concludes with a practical challenge that combines the concepts learned into a realistic workflow.

---

# Learning Objectives

After completing this room, I was able to:

- Understand what Meterpreter is.
- Differentiate between a normal shell and a Meterpreter session.
- Learn how Meterpreter operates in memory.
- Understand why Meterpreter is considered stealthy.
- Explore different Meterpreter payloads (flavors).
- Learn how payload selection depends on the target environment.
- Use common Meterpreter commands.
- Understand a basic post-exploitation workflow.
- Gather system information after exploitation.
- Search files on a compromised machine.
- Dump password hashes.
- Understand process migration.
- Learn how Meterpreter extensions expand functionality.

---

# Topics Covered

- Introduction to Meterpreter
- How Meterpreter Works
- In-Memory Execution
- Encrypted Communication
- Meterpreter Payload Flavors
- Selecting the Correct Payload
- Meterpreter Commands
- Process Management
- Post-Exploitation Workflow
- Meterpreter Extensions
- Hash Dumping
- File Searching
- System Enumeration

---

# Key Concepts Learned

## What is Meterpreter?

Meterpreter is an advanced Metasploit payload that runs on the target machine after successful exploitation. Unlike a normal command shell, Meterpreter provides a complete post-exploitation toolkit that allows an attacker or penetration tester to interact with the compromised system using many built-in capabilities.

---

## Why Meterpreter is Different

A normal shell mainly allows command execution.

Meterpreter provides:

- System enumeration
- Process management
- File management
- Network information
- Credential-related operations
- Extension loading
- Post-exploitation features

---

## How Meterpreter Works

One of the most important concepts learned in this room is that Meterpreter executes **in memory (RAM)** rather than installing itself on disk.

This provides several advantages:

- Reduced disk artifacts
- Lower chance of leaving permanent traces
- More stealth than traditional payloads
- Encrypted communication between attacker and target

Modern security products can still detect Meterpreter, but understanding why memory-based payloads are useful is an important learning objective.

---

## Meterpreter Payload Selection

Choosing the correct Meterpreter payload depends on several factors:

- Target operating system
- Available components on the target
- Network restrictions
- Compatible exploit modules

The room demonstrates that different payloads exist for multiple operating systems including Windows, Linux, Android, Java, PHP, Python, and others.

---

## Important Meterpreter Commands Learned

Some commands introduced during the room include:

- help
- sysinfo
- getuid
- ps
- migrate
- shell
- search
- hashdump
- background
- sessions

These commands support common post-exploitation tasks such as system enumeration, process inspection, privilege verification, file discovery, and session management.

---

## Post-Exploitation Workflow

A typical workflow learned during this room was:

1. Gain a Meterpreter session.
2. Identify the current user.
3. Gather system information.
4. Enumerate running processes.
5. Migrate to a stable process if necessary.
6. Search for interesting files.
7. Gather useful information.
8. Load additional extensions when required.

---

## Meterpreter Extensions

Meterpreter functionality can be expanded by loading extensions.

Examples include:

- Python extension
- Kiwi extension

These extensions provide additional capabilities beyond the default Meterpreter commands.

---

# Practical Skills Gained

During the practical challenge, I practiced:

- Connecting to a target
- Establishing a Meterpreter session
- Enumerating the system
- Viewing system information
- Identifying the current user
- Enumerating SMB shares
- Searching for files
- Reading discovered files
- Dumping password hashes
- Understanding password hash recovery workflow

The emphasis was on understanding how each action fits into a post-exploitation process rather than simply retrieving challenge answers.

---

# Challenges I Faced

During this room I experienced several learning challenges:

- Understanding why Meterpreter does not appear as its own process.
- Learning the difference between normal shells and Meterpreter sessions.
- Understanding process migration.
- Remembering the purpose of different Meterpreter commands.
- Understanding how extensions increase Meterpreter functionality.
- Understanding why payload selection depends on the target environment.

Each challenge helped reinforce how post-exploitation differs from initial exploitation.

---

# Key Takeaways

- Meterpreter is much more than a shell.
- Memory execution improves stealth.
- Payload selection is environment dependent.
- Enumeration is one of the most important post-exploitation activities.
- Extensions make Meterpreter significantly more powerful.
- Understanding commands is more valuable than memorizing them.
- Every command should have a purpose during an engagement.

---

# Beginner Practice

To reinforce the concepts learned in this room:

- Explain the difference between a shell and Meterpreter in your own words.
- Practice using common Meterpreter commands.
- Observe how process enumeration works.
- Explore system information using Meterpreter.
- Practice locating files with the search command.
- Learn when process migration is useful.
- Review why in-memory execution is important.

---

# Skills Developed

- Metasploit Framework
- Meterpreter
- Post Exploitation
- Windows Enumeration
- Process Enumeration
- File Enumeration
- Session Management
- SMB Enumeration
- Hash Dumping Concepts
- Meterpreter Extensions

---

# Final Thoughts

This room builds the foundation required for understanding post-exploitation using the Metasploit Framework. Instead of simply learning commands, it teaches why those commands exist, how they fit into a penetration testing workflow, and how Meterpreter provides capabilities that go far beyond a traditional command shell.

The concepts learned here become essential for more advanced penetration testing, privilege escalation, persistence, and post-exploitation techniques explored in later rooms.
