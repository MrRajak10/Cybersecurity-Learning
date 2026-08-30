# Flare VM — TryHackMe Learning Repository

## Overview

This repository documents my learning from the **Flare VM** room on TryHackMe, a practical introduction to a Windows-based environment designed for **digital forensics, malware analysis, incident response, reverse engineering, and investigation**.

Flare VM is a curated collection of security tools developed to support analysts when investigating suspicious files, processes, memory, network activity, and other artifacts. Rather than learning every tool in the environment, this room focuses on understanding several commonly used tools and how they can be combined during an investigation.

The most important lesson from the room is that effective investigation is not about knowing one tool or looking for one obvious indicator. It is about collecting evidence from multiple sources, understanding what that evidence means, and validating findings through different analytical techniques.

---

## Learning Objectives

By completing this room, I learned how to:

* Understand the purpose of Flare VM and the types of security professionals who use it.
* Distinguish between **static analysis** and **dynamic analysis**.
* Understand how Windows processes and parent-child process relationships can reveal suspicious behavior.
* Use process-monitoring tools to investigate system activity.
* Examine executable files without executing them.
* Inspect binary data and hexadecimal representations.
* Generate and compare file hashes for integrity verification.
* Understand the importance of **MD5, SHA-1, and SHA-256** hashes during investigations.
* Analyze network traffic and identify suspicious connections.
* Extract potentially useful strings from suspicious binaries.
* Recognize indicators associated with malware, encryption, remote execution, and command-and-control activity.
* Understand why investigators should correlate evidence from multiple tools rather than relying on a single source.

---

## What Is Flare VM?

**Flare VM** is a Windows-based security distribution containing a large collection of tools used for malware analysis, reverse engineering, digital forensics, incident response, and penetration testing.

The name **FLARE** refers to **Forensics, Logic Analysis, and Reverse Engineering**.

Instead of manually installing individual utilities, analysts can work from an environment where many commonly required tools are already available.

Typical users include:

* Malware analysts
* Reverse engineers
* Digital forensic investigators
* Incident responders
* Security researchers
* Penetration testers

The room demonstrates why having a specialized analysis environment can be useful when investigating potentially malicious Windows files and processes.

---

## Important Safety Consideration

The room contains **malicious example files** for practical investigation.

These samples should only be handled inside an isolated and controlled environment.

Malware samples must not be:

* Executed on a normal workstation.
* Copied onto production systems.
* Distributed unnecessarily.
* Connected to an unprotected network.
* Tested outside an appropriate laboratory or virtual machine.

The purpose of the exercise is to study malicious behavior safely, not to execute malware on a personal or production system.

A strong malware-analysis workflow therefore begins with **containment and isolation**.

---

# Static Analysis vs Dynamic Analysis

One of the most important concepts from the room is the distinction between static and dynamic analysis.

## Static Analysis

Static analysis examines a file **without executing it**.

An analyst can inspect things such as:

* File hashes
* File metadata
* PE headers
* Imported functions
* Strings
* Entropy
* Manifest information
* Embedded resources
* Binary structure

The advantage is that the analyst can learn about a suspicious file while reducing the risk associated with executing it.

## Dynamic Analysis

Dynamic analysis examines a file or process **while it is executing**.

An analyst can observe:

* Processes being created
* Files being accessed
* Registry activity
* Network connections
* DLL activity
* Process relationships
* Runtime behavior

Dynamic analysis can reveal behavior that is difficult or impossible to determine from static inspection alone.

### Simple mental model

**Static analysis:**
"What is inside this file?"

**Dynamic analysis:**
"What does this file do when it runs?"

Both approaches complement each other.

---

# Tool Arsenal

Flare VM contains many tools. The room introduces several major categories.

## Reverse Engineering and Debugging

Examples include:

* Ghidra
* x64dbg
* OllyDbg
* R2 / radare2
* Binary Ninja
* PEiD

These tools can assist with disassembly, debugging, reverse engineering, and understanding compiled binaries.

## Disassemblers and Decompilers

Examples include:

* CFF Explorer
* Hopper
* RetDec

These tools help analysts inspect executable structures and translate compiled code into forms that are easier to understand.

## Static and Dynamic Analysis

Examples include:

* Process Hacker
* Process Explorer
* PE-bear / PE analysis utilities
* Dependency Walker
* Detect It Easy
* PE Studio
* FLOSS

These tools provide different perspectives on executable files and running processes.

## Forensics and Incident Response

Examples include:

* Volatility
* Rekall
* FTK Imager

These tools are useful for memory analysis, forensic acquisition, and incident-response investigations.

## Network Analysis

Examples include:

* Wireshark
* Nmap
* Ncat

These tools help investigate network traffic, connections, services, and protocols.

## File and Binary Analysis

Examples include:

* HxD
* Hex editors
* File-analysis utilities

These tools allow analysts to inspect raw binary data and identify file structures or anomalies.

## Scripting and Automation

Examples include:

* Python
* PowerShell

Automation becomes particularly valuable when analysts need to process large numbers of files, logs, indicators, or forensic artifacts.

## Sysinternals

The room also highlights Microsoft's Sysinternals utilities, including:

* Process Explorer
* Process Monitor
* Autoruns

These are especially useful for understanding Windows processes, system activity, startup behavior, and other operating-system internals.

---

# Core Investigation Tools

## Process Monitor — Procmon

**Process Monitor (Procmon)** records system activity in real time.

It can provide visibility into:

* File-system operations
* Registry operations
* Process activity
* Thread activity

A Procmon event can contain information such as:

* Timestamp
* Process name
* Process ID
* Operation
* Path
* Result
* Additional details

This makes Procmon useful for malware analysis, troubleshooting, and forensic investigation.

### Investigative value

A suspicious process may appear normal when viewed only by name. Procmon can reveal what the process is actually attempting to access or modify.

For example, unusual activity involving sensitive system resources may deserve further investigation.

---

# Process Explorer

**Process Explorer** provides detailed visibility into currently running processes.

It helps analysts understand:

* Running processes
* Parent-child process relationships
* Process IDs
* Loaded DLLs
* Process properties
* Associated users
* Network-related information

### Parent-child relationships

The process tree is especially useful during investigation.

For example:

```text
explorer.exe
└── suspicious.exe
```

This relationship tells us which process launched the suspicious process.

That information becomes valuable when investigating suspicious documents, shortcuts, scripts, or other files that may launch secondary processes.

### Why process lineage matters

Malware often creates or launches additional processes.

Understanding the process tree can therefore help answer:

> "How did this process get here?"

rather than merely:

> "Is this process running?"

---

# HxD and Hexadecimal Analysis

HxD is a hexadecimal editor that allows investigators to inspect the raw bytes of files and memory.

A typical hexadecimal view contains:

```text
Hexadecimal bytes | ASCII representation
```

For example, executable files commonly begin with the bytes:

```text
4D 5A
```

These correspond to the `MZ` signature commonly associated with Windows PE files.

A hex editor can help investigators:

* Inspect raw file contents.
* Identify file signatures.
* Search for byte sequences.
* Modify binary data.
* Compare binary content.
* Investigate corruption or anomalies.

The important lesson is that a file's extension does not necessarily tell us what the file really is. Examining the underlying bytes can provide stronger evidence.

---

# CFF Explorer

**CFF Explorer** is useful for inspecting Portable Executable files.

It can expose information such as:

* PE structure
* DOS header
* File information
* Hash values
* Metadata
* Binary characteristics

It can also help investigators verify file integrity.

---

# File Hashes and Integrity

Cryptographic hashes are extremely important in forensic investigations.

Examples include:

* MD5
* SHA-1
* SHA-256

A hash can be treated as a fingerprint of a file.

If the file contents change, the resulting hash will normally change as well.

For example:

```text
File A
   ↓
SHA-256
   ↓
Hash value
```

After modification:

```text
Modified File A
   ↓
SHA-256
   ↓
Different hash value
```

### Why this matters in forensics

Hash values help investigators determine whether evidence has remained unchanged.

This becomes especially important during **chain of custody**, where evidence may move between investigators, analysts, evidence storage, or legal proceedings.

The hash provides a way to verify that the artifact received is the same artifact that was originally acquired.

---

# Wireshark

**Wireshark** is a packet-analysis tool used to inspect network traffic.

It can provide detailed information about:

* Source addresses
* Destination addresses
* Source ports
* Destination ports
* Protocols
* Packet contents
* TCP behavior
* TLS traffic
* Other packet-level metadata

Wireshark is particularly useful when investigating:

* Suspicious network connections
* Command-and-control activity
* Data exfiltration
* Unexpected remote communication
* Protocol behavior

### Important lesson

Encrypted traffic does not automatically mean malicious traffic.

For example, TLS is widely used by legitimate applications.

The analyst must therefore combine network evidence with:

* Process information
* Destination addresses
* Timing
* Application behavior
* Other indicators

This is why **context matters**.

---

# PE Studio

**PE Studio** supports static analysis of Windows executable files without executing them.

It can provide information such as:

* File hashes
* File size
* Entropy
* PE characteristics
* Architecture
* Imported functions
* Manifest information
* Metadata
* Potentially suspicious API calls

This is particularly useful as an initial triage tool.

---

## Entropy

Entropy can help an analyst identify files or sections that may contain:

* Compression
* Encryption
* Packing
* Obfuscation

A higher entropy value may indicate that data has been compressed, encrypted, or packed.

However:

> High entropy alone does not prove that a file is malicious.

It is an indicator that should be considered alongside other evidence.

---

# Suspicious API Functions

Imported API functions can reveal hints about what a Windows executable may attempt to do.

For example, the room highlights:

### `ShellExecute`

A function such as `ShellExecute` can be used to invoke programs through the Windows shell.

If a suspicious application imports functionality capable of launching additional processes, this can become relevant to the investigation.

### Cryptographic APIs

Functions associated with encryption or cryptographic operations may indicate that the executable performs cryptographic tasks.

This could be legitimate, but in malware investigations it may also be associated with:

* Encrypted communication
* Encrypted files
* Protected configuration
* Ransomware-like behavior
* Obfuscation

Again, an API import is an **indicator**, not definitive proof of malicious intent.

---

# FLOSS

**FLOSS** stands for **FireEye Labs Obfuscated String Solver** and is designed to extract strings from binaries, including strings that are difficult to recover using basic string extraction techniques.

This is valuable because malware may hide useful information inside a binary.

Extracted strings can contain things such as:

* URLs
* IP addresses
* File paths
* Registry paths
* API names
* Error messages
* Configuration information
* Command-and-control indicators

A basic string view may miss dynamically generated or obfuscated strings, which is why tools such as FLOSS are useful during malware analysis.

---

# Windows Process Investigation

The room demonstrates how several tools can be used together to investigate processes.

A simplified workflow looks like this:

```text
Suspicious file
      ↓
Static analysis
      ↓
PE Studio / CFF Explorer / FLOSS
      ↓
Identify indicators
      ↓
Controlled execution
      ↓
Process Explorer / Procmon
      ↓
Observe behavior
      ↓
Wireshark
      ↓
Investigate network communication
      ↓
Correlate evidence
```

This is much stronger than relying on a single tool.

---

# Investigating Suspicious Malware

The practical portion of the room demonstrates a typical investigative mindset.

A suspicious executable is initially analyzed using static techniques.

The analyst examines:

* Hashes
* Metadata
* PE properties
* Entropy
* Manifest configuration
* Imported functions
* Strings

Potentially suspicious characteristics can include:

* Unexpected metadata
* Unusual execution requirements
* Suspicious cryptographic functions
* Remote execution capabilities
* Unexpected file locations
* Obfuscated or packed content

The next stage is to investigate behavior in a controlled environment.

---

# Network Connectivity and C2 Investigation

The room uses a Cobalt Strike sample to demonstrate process and network investigation.

The important concept is not simply recognizing the name of a known tool.

Instead, investigators should ask:

* Which process is running?
* What is its parent process?
* What process ID does it have?
* Is it communicating with another host?
* What destination address is being contacted?
* Which destination port is used?
* Can packet captures confirm the connection?
* Does process telemetry agree with network telemetry?

This is an example of **evidence correlation**.

---

# Parent Process Analysis

One of the practical exercises involved identifying the parent process of a suspicious executable.

Understanding parent-child relationships helps analysts reconstruct execution chains.

For example:

```text
explorer.exe
      ↓
malicious.exe
      ↓
child_process.exe
```

This can reveal how a malicious program entered the execution chain and whether another application was responsible for launching it.

---

# Process Monitor + Process Explorer

These tools provide complementary information.

### Process Explorer

Best for understanding:

* Process hierarchy
* Process properties
* Process relationships
* Loaded components

### Process Monitor

Best for observing:

* Real-time system activity
* File operations
* Registry operations
* Process events
* Thread events

Using both provides a broader view of what a process is doing.

---

# Why Multiple Tools Matter

One of the strongest lessons from the room is:

> Never depend on a single piece of evidence when investigating suspicious activity.

Suppose a process appears suspicious.

PE Studio may show suspicious imports.

FLOSS may reveal suspicious strings.

Process Explorer may show the process lineage.

Procmon may reveal unusual file or registry activity.

Wireshark may show unexpected network communication.

When several independent sources point toward the same conclusion, confidence in the finding increases significantly.

---

# Research and Problem-Solving Skills

The room also reinforced an important cybersecurity skill that is easy to overlook:

## Effective Searching

Security professionals frequently work with large amounts of information.

Learning how to efficiently search documentation is therefore extremely valuable.

Examples include:

* `Ctrl + F`
* Searching exact technical terms
* Searching tool documentation
* Reviewing API names
* Looking up unfamiliar file structures
* Consulting trusted security references

Knowing **how to research** is often more important than memorizing every tool or command.

---

# Practical Skills Learned

By the end of the room, I had practiced using:

* Process Explorer
* Process Monitor
* PE Studio
* CFF Explorer
* HxD
* FLOSS
* Wireshark

I also reinforced concepts involving:

* Windows processes
* Parent-child process relationships
* PE files
* Hashes
* Binary analysis
* Static analysis
* Dynamic analysis
* Network connections
* C2 communication
* Cryptographic APIs
* Process monitoring
* File integrity

---

# Beginner Practice Activities

## Activity 1 — Static Triage

Take a harmless Windows executable inside an isolated lab environment.

Record:

```text
Filename:
File size:
MD5:
SHA-1:
SHA-256:
Architecture:
Entropy:
Imported functions:
```

Then write a short assessment explaining which indicators appear normal and which deserve additional investigation.

---

## Activity 2 — Process Tree Investigation

Open Process Explorer and select several normal Windows processes.

For each process, identify:

```text
Process name
PID
Parent process
User
Executable path
```

Then explain why the parent process is useful during incident investigation.

---

## Activity 3 — Procmon Observation

Use a harmless program inside a lab environment and observe its activity through Procmon.

Focus on:

* File creation
* File reads
* File writes
* Registry operations
* Process creation

Try to answer:

> What changed on the system when the application executed?

---

## Activity 4 — Hex Inspection

Open a known Windows executable with HxD.

Look at the first few bytes.

Identify:

```text
File signature
ASCII representation
PE-related information
```

Then compare the result with a non-executable file.

---

## Activity 5 — Network Analysis

Open a known-safe packet capture in Wireshark.

Identify:

* Source IP
* Destination IP
* Source port
* Destination port
* Protocol
* Transport-layer information

Create a simple explanation of how the packet moved from source to destination.

---

## Activity 6 — String Extraction

Run FLOSS against a harmless sample.

Look for:

* URLs
* Domains
* File paths
* Registry paths
* API names
* Error messages

Then classify the discovered strings as:

```text
Normal
Interesting
Suspicious
Unknown
```

The goal is not to label everything malicious. The goal is to develop the habit of **evidence-based analysis**.

---

# Key Takeaways

1. **Flare VM is an investigation environment, not simply a collection of random tools.**

2. **Static analysis allows analysts to inspect files without executing them.**

3. **Dynamic analysis reveals what a program actually does at runtime.**

4. **Process trees can reveal how suspicious programs were launched.**

5. **Procmon provides detailed visibility into Windows activity.**

6. **Process Explorer provides valuable process relationships and properties.**

7. **PE Studio helps perform rapid static triage of executable files.**

8. **CFF Explorer can expose PE information and help with integrity verification.**

9. **HxD allows analysts to inspect raw hexadecimal file contents.**

10. **FLOSS can uncover strings that ordinary string extraction may miss.**

11. **Wireshark provides detailed visibility into network communication.**

12. **Hash values are important for identifying files and verifying integrity.**

13. **High entropy can be an indicator of packing or encryption, but it is not proof of malware.**

14. **Suspicious API imports should be treated as indicators that require context.**

15. **Encrypted traffic is not automatically malicious.**

16. **Multiple tools should be used to correlate evidence.**

17. **Cybersecurity investigation requires strong research and documentation skills.**

18. **Malware must always be handled in an isolated, controlled environment.**

---

# Final Reflection

This room provided a practical introduction to a workflow that is much closer to real security investigation than simply identifying whether a file is "good" or "bad."

The biggest lesson was that investigation is a process of building evidence.

A suspicious executable can be examined statically. Its process behavior can then be monitored. Its network communication can be analyzed. Its hashes can be verified. Its strings can be extracted. Its process relationships can be reconstructed.

Each tool contributes a different piece of the puzzle.

For a beginner, the goal should not be to memorize every Flare VM tool. The more valuable skill is learning **which question needs to be answered and which tool can provide the evidence needed to answer it**.

That mindset becomes increasingly important as investigations become larger and more complex.

---

# Repository Structure

```text
Flare-VM/
├── README.md
└── notes.md
```

This repository intentionally focuses on learning, investigation methodology, and technical understanding rather than simply recording challenge answers.
