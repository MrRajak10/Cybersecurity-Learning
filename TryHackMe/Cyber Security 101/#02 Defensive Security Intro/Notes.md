
# Introduction

Defensive Security, commonly known as **Blue Teaming**, is one of the most fundamental disciplines in cybersecurity. While Offensive Security focuses on discovering and exploiting vulnerabilities, Defensive Security is responsible for protecting systems, detecting malicious activities, responding to incidents, and ensuring business continuity.

Unlike attackers, defenders cannot afford repeated mistakes. An attacker only needs to succeed once to compromise an organization, whereas defenders must consistently prevent, detect, and respond to every attack.

The primary objective of Defensive Security is to build multiple layers of protection that reduce risk and minimize the impact of cyber threats.

---

# 1. Defense in Depth

## Overview

Modern organizations do not rely on a single security control. Instead, they implement **Defense in Depth**, a layered security strategy where multiple defensive mechanisms work together.

If one security layer fails, another layer continues protecting the organization.

This significantly reduces the likelihood of a successful compromise.

---

## Castle Analogy

Imagine protecting a medieval castle.

Instead of relying on one wall, the castle has:

* A moat
* An outer wall
* Guard towers
* Inner walls
* Locked treasure rooms

Even if an attacker crosses one layer, additional security barriers remain.

Corporate networks follow the same principle.

---

## Security Layers

| Layer               | Security Controls                                              | Purpose                                       |
| ------------------- | -------------------------------------------------------------- | --------------------------------------------- |
| **Perimeter**       | Firewalls, Intrusion Prevention Systems (IPS)                  | Filter malicious inbound and outbound traffic |
| **Network**         | Network Segmentation, Internal Firewalls                       | Limit attacker movement inside the network    |
| **Host (Endpoint)** | EDR, Antivirus                                                 | Detect and stop threats on individual systems |
| **Application**     | Web Application Firewall (WAF), Secure Configuration, Patching | Protect applications from exploitation        |
| **Data**            | Encryption, Access Control, Data Loss Prevention (DLP)         | Protect sensitive information                 |

---

# 2. Security Operations Center (SOC)

## What is a SOC?

A **Security Operations Center (SOC)** is a centralized team of cybersecurity professionals responsible for continuously monitoring, detecting, investigating, and responding to security incidents across an organization's infrastructure.

SOC analysts work around the clock to identify suspicious activity before it becomes a major security breach.

---

## Primary Responsibilities

* Monitor security events
* Investigate alerts
* Validate potential threats
* Respond to incidents
* Escalate serious cases
* Improve detection capabilities

---

# 3. Security Information and Event Management (SIEM)

## What is a SIEM?

Large organizations generate millions of security logs every day from:

* Servers
* Firewalls
* Workstations
* Applications
* Active Directory
* Cloud services
* Network devices

Manually reviewing these logs is impossible.

A **Security Information and Event Management (SIEM)** platform collects, normalizes, stores, correlates, and analyzes logs from multiple sources within a single centralized platform.

---

## Why SIEM is Important

A SIEM enables analysts to:

* Detect attacks faster
* Correlate events from different systems
* Reduce investigation time
* Generate automated alerts
* Support incident response

---

## Correlation Rules

One of the most important capabilities of a SIEM is **event correlation**.

Instead of examining individual logs independently, the SIEM combines multiple related events to identify suspicious patterns.

### Example

**Event 1**

* Five failed login attempts from New York

**Event 2**

* Successful login from London two minutes later

Individually, these events may appear harmless.

Together, they indicate an **Impossible Travel** scenario and may suggest compromised credentials.

The SIEM correlates both events and generates a security alert for investigation.

---

# 4. SIEM vs EDR vs XDR

## SIEM

Focuses on:

* Log collection
* Event correlation
* Security monitoring
* Centralized visibility

---

## EDR (Endpoint Detection and Response)

Focuses directly on endpoint devices.

Capabilities include:

* Process monitoring
* Memory inspection
* Registry monitoring
* File activity monitoring
* One-click host isolation

Examples:

* Microsoft Defender for Endpoint
* CrowdStrike Falcon
* SentinelOne

---

## XDR (Extended Detection and Response)

XDR expands endpoint visibility by combining data from:

* Endpoints
* Email
* Identity systems
* Cloud workloads
* Network devices

This provides broader attack visibility across the enterprise.

---

# 5. Threat Intelligence

## Definition

Threat Intelligence is the process of collecting, analyzing, and applying information about current and emerging cyber threats.

Its purpose is to help organizations move from **reactive defense** to **proactive defense**.

---

## Why Threat Intelligence Matters

Instead of waiting for attacks to happen, organizations learn:

* Who is targeting them
* Why they are being targeted
* How attackers operate
* Which techniques attackers commonly use

This knowledge allows defenders to prepare in advance.

---

## Threat Intelligence Lifecycle

1. Collect Data
2. Process Information
3. Analyze Intelligence
4. Produce Actionable Recommendations

---

# Indicators of Compromise (IoCs)

Threat Intelligence commonly uses **Indicators of Compromise (IoCs)**.

IoCs are technical artifacts that indicate malicious activity.

Examples include:

| Indicator                | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| File Hashes (MD5/SHA256) | Unique fingerprint of malware                           |
| IP Addresses             | Malicious servers or command-and-control infrastructure |
| Domain Names             | Known phishing or malware domains                       |
| URLs                     | Malicious download locations                            |

---

# Tactics, Techniques and Procedures (TTPs)

Unlike IoCs, **TTPs** describe **how attackers behave**.

TTPs remain valuable even when attackers change their infrastructure.

Because attacker behavior changes less frequently than IP addresses or file hashes, TTPs provide more durable intelligence.

---

# Practical Example

During the TryHackMe lab:

1. A suspicious IP address appeared in the SIEM.
2. The IP was copied.
3. The IP reputation was checked using public Threat Intelligence platforms.
4. The analyst confirmed that the IP had previously been associated with malicious activity.
5. The incident was escalated for response.

This demonstrates how Threat Intelligence supports real-world investigations.

---

# 6. Digital Forensics and Incident Response (DFIR)

## Overview

When preventive controls fail and a security incident occurs, **Digital Forensics and Incident Response (DFIR)** becomes responsible for investigating and containing the attack.

DFIR combines two complementary disciplines:

* Digital Forensics
* Incident Response

---

# Digital Forensics

Digital Forensics involves collecting, preserving, analyzing, and presenting digital evidence.

The goal is to determine:

* What happened
* When it happened
* How it happened
* Who was involved
* What systems were affected

---

## Common Sources of Evidence

* File systems
* Memory dumps
* System logs
* Network captures
* Browser history
* Registry entries

---

# Order of Volatility

Some evidence disappears quickly.

Analysts must collect the most volatile evidence first.

## Volatile Evidence

Examples:

* RAM contents
* Running processes
* Active network connections
* Encryption keys

Memory evidence disappears when a computer is powered off.

---

## Non-Volatile Evidence

Examples:

* Hard drive contents
* Event logs
* Deleted files
* Master File Table (MFT)

These remain available after shutdown.

---

# 7. Incident Response Lifecycle

The **NIST Incident Response Framework** consists of four phases.

---

## Phase 1 — Preparation

Objectives:

* Train responders
* Develop playbooks
* Deploy security tools
* Define response procedures

---

## Phase 2 — Detection and Analysis

Objectives:

* Detect suspicious activity
* Validate alerts
* Determine attack severity
* Identify affected systems

---

## Phase 3 — Containment, Eradication and Recovery

Objectives:

* Isolate infected systems
* Remove malicious software
* Eliminate persistence mechanisms
* Restore systems from trusted backups

Example workflow:

```
Alert Generated
        │
        ▼
Isolate Host
        │
        ▼
Remove Malware
        │
        ▼
Restore Clean System
```

---

## Phase 4 — Post-Incident Activity

Objectives:

* Document findings
* Conduct lessons learned
* Improve detection rules
* Patch vulnerabilities
* Update security procedures

---

# 8. Malware Analysis

## Purpose

Malware Analysis seeks to understand:

* What malware does
* How it spreads
* How it persists
* How it communicates
* How to detect it

---

## Static Analysis

The malware is **not executed**.

Analysts inspect:

* File hashes
* Strings
* PE headers
* Imported libraries

Advantages:

* Safe
* Fast

Limitations:

* Obfuscated malware may hide important behavior.

---

## Dynamic Analysis

The malware is executed inside an isolated **sandbox** or virtual machine.

Analysts observe:

* Process creation
* File modifications
* Registry changes
* Network communication
* Persistence mechanisms

Advantages:

* Reveals actual runtime behavior.

Risk:

Never execute malware on a production or personal system.

---

# 9. Real-World SOC Investigation Workflow

The practical lab closely resembles the workflow of a Tier 1 SOC Analyst.

## Step 1 — Alert Triage

Review incoming alerts and identify suspicious activity.

---

## Step 2 — Context Enrichment

Gather additional information:

* Source IP
* Destination IP
* File hash
* Username
* Hostname

Validate indicators using Threat Intelligence platforms.

---

## Step 3 — Containment

Prevent the threat from spreading.

Examples:

* Isolate endpoint
* Disable compromised account
* Block malicious IP

---

## Step 4 — Escalation and Remediation

Escalate confirmed incidents to the Incident Response team.

Typical remediation includes:

* Blocking attacker infrastructure
* Removing malware
* Restoring systems
* Closing the incident after validation

---

# Common Beginner Mistakes

## Assuming a Quiet SIEM Means Everything is Secure

A lack of alerts may indicate:

* Broken logging
* Disabled sensors
* Misconfigured detection rules

Always verify that monitoring systems are functioning correctly.

---

## Executing Malware Outside a Sandbox

Never analyze malware on your personal computer.

Always use:

* Virtual Machines
* Sandboxes
* Isolated lab environments

---

## Ignoring Post-Incident Reviews

Failing to conduct a post-incident review means the same attack may succeed again.

Every incident should improve the organization's future defenses.

---

# Key Takeaways

* Defensive Security relies on multiple layers of protection rather than a single security control.
* SIEM platforms centralize and correlate logs to identify suspicious activity.
* SOC analysts investigate, validate, and respond to security alerts.
* Threat Intelligence enables organizations to proactively defend against known threats.
* DFIR provides structured procedures for investigating and recovering from security incidents.
* Malware Analysis reveals attacker techniques and supports detection engineering.
* Successful defenders continuously improve security through monitoring, investigation, response, and lessons learned.
