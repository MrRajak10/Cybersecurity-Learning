# Metasploit: Introduction (TryHackMe)

> **Learning Repository**
> This repository documents my learning journey through the **Metasploit: Introduction** room on TryHackMe. The purpose of this repository is to understand the concepts behind the Metasploit Framework rather than simply learning how to execute attacks. The focus is on building a strong foundation in penetration testing concepts, Metasploit architecture, modules, payloads, and the MSF Console.

---

# Learning Objectives

After completing this room, I was able to understand:

* What the Metasploit Framework is.
* Why Metasploit is used in penetration testing.
* The different phases of penetration testing where Metasploit can help.
* The difference between Metasploit Framework and Metasploit Pro.
* The purpose of the MSF Console.
* The concepts of Vulnerability, Exploit, and Payload.
* Different Metasploit module categories.
* Different payload types.
* Common MSF Console commands.
* How modules are selected and configured.
* How options are set before running a module.
* Basic session management.

---

# What is Metasploit?

Metasploit Framework is an **open-source penetration testing framework** that helps security professionals perform multiple stages of a penetration test.

Although many beginners think Metasploit is only used for exploitation, it actually supports several phases of penetration testing.

These include:

* Information Gathering
* Scanning
* Exploitation
* Post-Exploitation

Metasploit provides a large collection of modules and tools that simplify these activities.

---

# Metasploit Versions

## Metasploit Framework

* Free
* Open Source
* Command-line based
* Pre-installed in Kali Linux
* Available in the TryHackMe AttackBox

This is the version used throughout this room.

## Metasploit Pro

* Commercial version
* Paid software
* Graphical User Interface (GUI)
* Includes automation and reporting features

---

# Penetration Testing Workflow

The room explains how Metasploit supports multiple penetration testing phases.

1. Information Gathering
2. Scanning
3. Exploitation
4. Post-Exploitation

Rather than replacing these phases, Metasploit provides tools that assist throughout the workflow.

---

# Core Components of Metasploit

## MSF Console

The primary command-line interface used to interact with the framework.

It is used to:

* Search modules
* Select modules
* Configure options
* Launch modules
* Manage sessions

---

## Modules

Modules are individual components designed to perform specific security tasks.

Examples include:

* Scanning
* Exploitation
* Enumeration
* Brute-force testing
* Post-exploitation activities

---

## Tools

Metasploit also includes several standalone tools that assist during penetration testing and exploit development.

Examples include:

* msfvenom
* pattern_create
* pattern_offset

---

# Understanding Three Important Concepts

Before using Metasploit, three concepts must be understood.

## Vulnerability

A vulnerability is a weakness inside a system.

Examples include:

* Programming mistakes
* Design flaws
* Logic errors
* Misconfigurations

Attackers attempt to exploit these weaknesses.

---

## Exploit

An exploit is the code that takes advantage of a vulnerability.

Without a vulnerability, an exploit cannot succeed.

---

## Payload

A payload is the code executed **after** successful exploitation.

Examples include:

* Opening a shell
* Executing commands
* Running additional programs
* Creating a reverse connection

The exploit gains access.

The payload performs the attacker's intended action.

---

# Metasploit Module Categories

The room introduces several important module categories.

## Auxiliary

Used for activities that do not exploit vulnerabilities directly.

Examples include:

* Scanners
* Crawlers
* Fuzzers

---

## Encoders

Used to encode payloads.

Historically useful for avoiding signature-based antivirus detection.

Modern antivirus solutions are generally much more effective at detecting encoded payloads.

---

## Evasion

Designed to help bypass security products such as antivirus software.

These modules are generally more advanced than encoders.

---

## Exploits

The core modules of Metasploit.

These modules leverage vulnerabilities to gain access to a target.

---

## NOPs

NOP modules help maintain payload consistency and reliability during exploit execution.

---

## Payloads

Payloads define what happens after successful exploitation.

---

## Post Modules

Used after initial access has been obtained.

Common activities include:

* Privilege escalation
* Enumeration
* Credential collection
* Persistence
* Additional system discovery

---

# Payload Types

The room introduces several payload categories.

## Singles

* Self-contained payloads
* Perform one action
* No additional download required

---

## Stagers

* Small initial payload
* Establishes communication
* Downloads the larger payload

---

## Stages

* Larger payload
* Delivered after the stager
* Performs the main functionality

---

## Adapters

Used to wrap payloads so they can operate under different situations.

---

# Single vs Staged Payload Identification

A useful naming convention:

Single payload

```
shell_reverse_tcp
```

Staged payload

```
shell/reverse_tcp
```

Underscore (`_`) generally indicates a single payload.

Forward slash (`/`) generally indicates a staged payload.

---

# MSF Console Basics

The MSF Console is launched using:

```
msfconsole
```

Inside the console, many Linux commands continue to work.

Examples include:

* ls
* cd
* pwd
* clear
* history

The console also supports tab completion for faster command entry.

---

# Important MSF Commands Learned

| Command       | Purpose                    |
| ------------- | -------------------------- |
| msfconsole    | Launch Metasploit          |
| search        | Search modules             |
| use           | Select a module            |
| info          | Display module information |
| show options  | View required options      |
| show payloads | View compatible payloads   |
| set           | Set an option              |
| unset         | Remove an option           |
| setg          | Set a global option        |
| unsetg        | Remove a global option     |
| exploit       | Launch exploitation        |
| run           | Alternative to exploit     |
| back          | Exit current module        |
| sessions      | List active sessions       |
| sessions -i   | Interact with a session    |
| background    | Background a session       |
| history       | Display command history    |

---

# Understanding Module Options

Common options include:

| Option | Description          |
| ------ | -------------------- |
| RHOSTS | Target IP address    |
| RPORT  | Target service port  |
| LHOST  | Local attacker's IP  |
| LPORT  | Local listening port |

These options must often be configured before running a module.

---

# Global Variables

Normally, module settings remain inside the currently selected module.

Using global variables allows settings such as **RHOSTS** to remain available when switching between modules.

This reduces repetitive configuration.

---

# Session Management

After successful exploitation, Metasploit creates a session between the attacker and the target.

Useful commands include:

* sessions
* sessions -i <ID>
* background

Managing sessions efficiently is an important part of post-exploitation.

---

# Key Takeaways

* Metasploit is much more than an exploitation tool.
* Understanding vulnerabilities is more important than memorizing exploits.
* Payloads determine what happens after successful exploitation.
* Modules are organized by purpose.
* MSF Console is the central interface for operating the framework.
* Correct configuration of module options is essential.
* Session management becomes important after gaining access.
* Building conceptual understanding first makes learning advanced exploitation much easier.

---

# Personal Learning Reflection

This room helped me understand the overall architecture of the Metasploit Framework instead of treating it as a collection of commands. The concepts of **Vulnerability**, **Exploit**, and **Payload** became much clearer after studying how they relate to each other. Learning the different module categories and practicing MSF Console commands also made the framework feel much less intimidating. Rather than memorizing commands, I now have a better understanding of why each command is used and where it fits into the penetration testing process.

---

# Skills Practiced

* Penetration Testing Fundamentals
* Metasploit Framework Basics
* MSF Console Navigation
* Module Selection
* Payload Concepts
* Exploit Concepts
* Session Management
* Command-Line Usage

---

# Next Topics to Learn

* Metasploit Searching Techniques
* Payload Generation with msfvenom
* Meterpreter Fundamentals
* Auxiliary Modules
* Post-Exploitation
* Windows Exploitation
* Linux Exploitation
* Exploit Development Basics
