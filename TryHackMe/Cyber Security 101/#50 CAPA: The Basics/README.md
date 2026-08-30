# TryHackMe — CAPA Basics

This repository contains learning notes and practical observations from the TryHackMe **CAPA Basics** room, part of the **Defensive Security Tooling** module in the Cyber Security 101 pathway.

The room introduces **CAPA (Common Analysis Platform for Artifacts)**, a malware-analysis tool developed by Mandiant. CAPA performs **static analysis** of executable files and identifies behaviors and capabilities that can help an analyst understand what a program is capable of doing without executing it.

The main objective of this room is not simply to learn CAPA commands, but to understand how CAPA presents its findings and how those findings can be interpreted during malware analysis and defensive investigations.

---

## Learning Objectives

By completing this room, you should be able to:

* Understand the difference between static and dynamic analysis.
* Explain the purpose of CAPA in malware analysis.
* Run CAPA against an executable.
* Use CAPA command-line options such as help and verbosity.
* Understand the general information produced by CAPA.
* Interpret CAPA's MITRE ATT&CK mappings.
* Understand the Malware Behavior Catalog (MBC).
* Distinguish between objectives, behaviors, micro-behaviors, and methods.
* Understand CAPA namespaces.
* Understand what CAPA capabilities represent.
* Trace a capability back to its corresponding rule.
* Recognize the role of YAML rules in CAPA detection.
* Use CAPA's web-based explorer to investigate analysis results.

---

## What Is CAPA?

CAPA stands for **Common Analysis Platform for Artifacts**.

It is designed to identify capabilities and behaviors present in executable files and other supported artifacts. Instead of requiring an analyst to manually reverse engineer every binary, CAPA applies a large collection of detection rules derived from reverse-engineering knowledge.

CAPA can analyze artifacts such as:

* Windows PE files
* ELF binaries
* .NET modules
* Shellcode
* Sandbox reports

The important idea is:

> CAPA tells an analyst what a file appears capable of doing without requiring the file to be executed.

For example, CAPA may identify behavior related to:

* HTTP communication
* Process creation
* File manipulation
* Virtual machine detection
* PowerShell usage
* Scheduled tasks
* Data encoding
* Anti-analysis techniques
* Persistence

A CAPA finding does not automatically mean that the file is malicious. A capability must be interpreted in context.

---

## Static Analysis vs Dynamic Analysis

One of the most important concepts in this room is the distinction between **static analysis** and **dynamic analysis**.

### Static Analysis

Static analysis examines a file without executing it.

The analyst attempts to understand the program by examining properties such as:

* Strings
* Functions
* Instructions
* Imports
* Embedded data
* Patterns
* Code structures
* Known behavioral indicators

CAPA belongs primarily to this category.

### Dynamic Analysis

Dynamic analysis involves executing the program and observing what happens.

An analyst may monitor:

* Processes
* Network connections
* Files created or modified
* Registry activity
* Memory behavior
* Child processes
* Persistence mechanisms

Dynamic analysis can provide strong behavioral evidence, but executing unknown malware directly on a normal workstation can be dangerous.

This is why malware is commonly executed inside controlled environments such as sandboxes or isolated virtual machines.

CAPA provides another option: obtain useful behavioral information **without executing the executable**.

---

## Why CAPA Is Useful

Reverse engineering malware manually can require substantial knowledge of:

* Assembly
* Operating-system internals
* Executable formats
* Debugging
* Memory analysis
* Programming
* Reverse-engineering tools

CAPA does not replace these skills, but it can reduce the amount of manual work required during an initial investigation.

CAPA effectively packages years of reverse-engineering expertise into a rule-based analysis framework.

This makes it especially useful for:

* SOC analysts
* Malware analysts
* Incident responders
* Threat hunters
* Detection engineers
* Defensive security learners

---

## Basic CAPA Workflow

A typical CAPA workflow looks like this:

```text
Suspicious File
      |
      v
   CAPA Scan
      |
      v
Behavior & Capability Detection
      |
      +------------------+
      |                  |
      v                  v
MITRE ATT&CK          MBC Mapping
      |                  |
      +---------+--------+
                |
                v
        Analyst Interpretation
```

The output gives the analyst multiple ways to understand the file.

Instead of focusing on one isolated result, it is better to correlate:

```text
Capability
   ↓
Namespace
   ↓
Rule
   ↓
Behavior
   ↓
MITRE ATT&CK / MBC context
   ↓
Investigation hypothesis
```

---

## Running CAPA

CAPA can be launched from a terminal.

A basic analysis looks conceptually like:

```powershell
capa.exe .\sample.exe
```

When CAPA is being executed from the same directory as the target file, the relative path can be used.

For example:

```powershell
capa.exe .\Cryptbot.binary
```

The `.\` notation means the file is located in the current directory.

If the executable is elsewhere, provide the appropriate path.

---

## Useful Command-Line Options

CAPA provides several command-line options.

### Help

```powershell
capa.exe -h
```

The help option displays available parameters and usage information.

### Verbose Output

```powershell
capa.exe -v
```

Verbose output provides more detailed information than the default result.

### Very Verbose Output

```powershell
capa.exe -vv
```

Very verbose output exposes substantially more analysis detail, including information useful for understanding why particular rules were matched.

---

## Reading a CAPA Report

A CAPA result can be thought of as several layers of information.

### General Information

The report can contain information such as:

* MD5
* SHA-1
* SHA-256
* Analysis type
* Operating system
* Architecture
* File format
* File path

Hashes are especially useful for identifying and tracking a particular artifact.

For example, a SHA-256 value can be used as a stable reference for a specific sample.

---

# MITRE ATT&CK

CAPA can associate discovered capabilities with the **MITRE ATT&CK** framework.

MITRE ATT&CK is a knowledge base describing adversary tactics and techniques observed in real-world attacks.

This provides valuable context.

Instead of seeing:

```text
PowerShell
```

an analyst may receive an ATT&CK mapping that explains the behavior in relation to an adversary technique.

Similarly, capabilities related to:

* Discovery
* Persistence
* Defense Evasion
* Execution
* Impact
* Command and Control

can provide clues about what an attacker or malware author may be attempting to accomplish.

---

## ATT&CK Tactics, Techniques, and Sub-techniques

The hierarchy can be understood as:

```text
Tactic
   ↓
Technique
   ↓
Sub-technique
```

For example:

```text
Defense Evasion
    ↓
Obfuscated Files or Information
    ↓
Specific Sub-technique
```

The identifiers associated with these techniques allow analysts to precisely reference the behavior.

The important lesson is that CAPA's ATT&CK output provides **context**, not a complete incident narrative.

A single capability should not be treated as proof of a specific attack chain.

---

# Malware Behavior Catalog (MBC)

Another major component discussed in the room is the **Malware Behavior Catalog (MBC)**.

MBC provides a standardized way of describing malware behavior.

It helps analysts characterize malware through:

* Objectives
* Behaviors
* Micro-behaviors
* Methods

The structure can be visualized as:

```text
Objective
   ↓
Behavior
   ↓
Micro-behavior
   ↓
Method
```

The exact relationship between these fields can vary depending on the CAPA result being examined, but the hierarchy is useful for understanding how detailed a behavioral description is.

---

## MBC Objectives

MBC objectives are high-level categories describing why a behavior may be relevant.

Examples discussed in the room include areas such as:

* Anti-behavioral analysis
* Anti-static analysis
* Communication
* Data
* Defense evasion
* Persistence
* Discovery
* Impact

These objectives provide a high-level classification of malware activity.

---

## MBC Behaviors

A behavior describes a more specific action.

Examples include:

* HTTP communication
* Virtual machine detection
* Executable code obfuscation
* Process creation
* File operations
* Data encoding

The behavior is more concrete than the objective.

---

## Micro-behaviors

Micro-behaviors represent lower-level actions.

Examples include:

* Creating a process
* Creating a TCP socket
* Reading a file
* Writing a file
* Allocating memory
* Changing memory protection
* Inspecting a string

A micro-behavior is not automatically malicious.

For example, creating a process is perfectly normal software behavior.

The security significance comes from the **combination of behaviors and context**.

This is a critical malware-analysis lesson.

---

## Methods

Methods provide additional detail about how a behavior is implemented.

For example, a behavior involving executable-code obfuscation can have a specific method such as argument obfuscation.

This provides an increasingly detailed view:

```text
Objective
    ↓
Behavior
    ↓
Method
```

or, where applicable:

```text
Objective
    ↓
Behavior
    ↓
Micro-behavior
    ↓
Method
```

The deeper the analysis goes, the more specific the explanation of the observed behavior becomes.

---

# Example: Base64 Encoding

One of the room's examples involves Base64 encoding.

Suppose CAPA detects behavior related to:

```text
Encoding Data
      ↓
Base64
```

This alone does **not** prove malicious behavior.

Base64 is widely used by legitimate applications.

However, Base64 encoding combined with other findings might become much more interesting.

For example:

```text
Base64 Encoding
       +
HTTP Communication
       +
Suspicious File Activity
       +
Persistence
```

Now the analyst has a stronger reason to investigate how those behaviors interact.

This demonstrates an important principle:

> Individual indicators can be benign while their combination can become suspicious.

---

# CAPA Namespaces

CAPA organizes rules using **namespaces**.

Namespaces help group related capabilities and rules.

Examples of top-level namespaces discussed in the room include:

* `anti-analysis`
* `collection`
* `communication`
* `compiler`
* `data-manipulation`
* `executable`
* `host-interaction`
* `impact`
* `internal`
* `library`
* `linking`
* `load-code`
* `malware-family`
* `nursery`
* `persistence`
* `runtime`
* `targeting`

Namespaces make large collections of CAPA rules easier to organize and understand.

---

## Top-Level Namespace vs Namespace

A useful mental model is:

```text
Top-Level Namespace
        ↓
Namespace
        ↓
Rule
```

For example:

```text
anti-analysis
      ↓
anti-vm
      ↓
rule related to VM detection
```

This structure helps analysts move from broad categories toward the exact detection logic.

---

# Capabilities

A **capability** represents a behavior or functionality detected by a CAPA rule.

Examples might include:

* Referencing anti-VM strings
* Creating a scheduled task
* Creating a process
* Encoding data as Base64
* Checking HTTP status codes
* Using PowerShell
* Reading or writing files

Capabilities are one of the most useful parts of a CAPA report because they describe what the analyzed artifact appears capable of doing.

---

# CAPA Rules and YAML

CAPA rules are commonly represented using YAML.

A simplified conceptual structure looks like:

```yaml
rule:
  meta:
    name: example-rule

  features:
    - string: example
```

Real CAPA rules are significantly more sophisticated.

They can contain:

* Metadata
* Namespaces
* Strings
* API references
* Regular expressions
* Logical conditions
* Feature combinations
* Cross-references

For example, a rule may use an `and` condition to require multiple features.

Conceptually:

```text
Condition A
   AND
Condition B
   AND
Condition C
```

must all be satisfied before the rule is considered matched.

An `or` condition behaves differently:

```text
Condition A
    OR
Condition B
    OR
Condition C
```

Only one matching condition may be sufficient.

Understanding these logical relationships becomes important when investigating why a capability was detected.

---

# Understanding a Rule Match

When CAPA reports a capability, the next useful question is:

> Why did CAPA identify this capability?

Verbose output and the CAPA web explorer can help answer this.

A useful investigation workflow is:

```text
Capability
   ↓
Find Namespace
   ↓
Find Rule
   ↓
Inspect YAML
   ↓
Inspect Features
   ↓
Understand Match Conditions
```

This is much more valuable than simply reading the capability name.

---

# CAPA Web Explorer

The room also introduces the **CAPA Web Explorer**.

The graphical interface makes large CAPA reports easier to navigate than raw terminal output.

It can help analysts:

* Explore capabilities
* Search results
* Filter findings
* Inspect namespaces
* Review rules
* Examine features
* Understand matched conditions

For learners, the web interface can be especially helpful because it exposes the relationships between findings in a more organized way.

---

# Why Rule Inspection Matters

Suppose CAPA reports:

```text
Scheduled Task
```

The capability name alone is useful, but the rule can provide much more information.

By inspecting the rule, an analyst can understand:

* Which strings were searched for
* Which APIs were referenced
* Which regular expressions were used
* Which logical conditions were required
* Why the rule matched

This makes the analysis more explainable.

Instead of saying:

> CAPA detected persistence.

you can reason:

> CAPA matched a scheduled-task rule because the analyzed sample contained the features associated with scheduled-task creation.

That is a stronger analytical statement.

---

# Important Analytical Principle

CAPA provides **indications of capability**, not absolute proof of execution.

For example:

```text
CAPA detects HTTP communication
```

does not automatically mean:

```text
The malware contacted a malicious server during the investigation.
```

It means the file contains characteristics associated with HTTP communication.

To determine whether the behavior actually occurred, dynamic analysis or additional telemetry may be necessary.

This distinction is essential when performing professional malware analysis.

---

# Practical Learning Exercises

## Exercise 1 — Static vs Dynamic Analysis

Take several software samples and classify the following questions:

1. Was the file executed?
2. What evidence was collected?
3. Would the activity require an isolated environment?
4. Could the same information be obtained statically?

The goal is to develop the habit of selecting the correct analysis technique.

---

## Exercise 2 — CAPA Command Practice

Practice the basic commands:

```powershell
capa.exe -h
capa.exe -v sample.exe
capa.exe -vv sample.exe
```

Compare the amount of information produced at each verbosity level.

---

## Exercise 3 — Capability Investigation

Choose one capability from a CAPA report and trace:

```text
Capability
→ Namespace
→ Rule
→ YAML
→ Feature
→ Match condition
```

Write down why the rule matched.

---

## Exercise 4 — ATT&CK Investigation

For every ATT&CK technique reported by CAPA:

1. Identify the tactic.
2. Identify the technique.
3. Identify the sub-technique, if present.
4. Read the corresponding MITRE ATT&CK documentation.
5. Determine what defensive telemetry could be useful for detecting the behavior.

This turns CAPA results into practical threat-hunting knowledge.

---

## Exercise 5 — Avoiding False Conclusions

Find a benign program that performs:

* Base64 encoding
* HTTP communication
* Process creation
* File reading

Then ask:

> Would any of these capabilities alone prove that the program is malware?

The correct analytical approach is to evaluate the complete context.

---

# Key Takeaways

* CAPA is a static-analysis tool for identifying capabilities in software.
* Static analysis does not require executing the suspicious file.
* Dynamic analysis observes behavior during execution.
* CAPA can map findings to MITRE ATT&CK.
* The Malware Behavior Catalog provides another structured way to describe malware behavior.
* Objectives, behaviors, micro-behaviors, methods, namespaces, and capabilities provide different levels of detail.
* CAPA capabilities describe what software appears capable of doing.
* A capability is not automatically proof of malicious activity.
* CAPA rules explain why a capability was detected.
* YAML is used to express CAPA detection logic.
* Verbose and very verbose output provide additional investigative detail.
* The CAPA Web Explorer can make complex results easier to understand.
* The strongest analysis comes from correlating multiple findings rather than interpreting a single indicator in isolation.

---

## Final Perspective

The most important lesson from this room is not memorizing CAPA commands.

It is learning how to move from:

```text
Tool Output
```

to:

```text
Behavior
```

and then from:

```text
Behavior
```

to:

```text
Security Interpretation
```

CAPA makes this process easier by connecting executable artifacts to known behavioral patterns, ATT&CK techniques, MBC concepts, namespaces, and detection rules.

For beginners, this is particularly valuable because it introduces the mindset used by defensive security professionals:

> Do not simply ask what a file is. Ask what the file is capable of doing, how that capability was detected, and what the behavior means in a wider security context.
