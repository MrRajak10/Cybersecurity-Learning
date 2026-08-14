# TryHackMe — SOC Fundamentals

## Overview

This repository documents my learning from the **SOC Fundamentals** room on TryHackMe. The room introduces the basic structure and operation of a **Security Operations Center (SOC)** and explains how security teams continuously monitor an organization's environment to detect, investigate, and respond to security events.

The main focus of this room is understanding how a SOC works from a beginner's perspective, especially the role of a **SOC Level 1 Analyst**, the alert triage process, the **Five Ws**, the three pillars of a SOC, and the security technologies used to support monitoring and detection.

---

## Learning Objectives

By completing this room, I learned:

* What a Security Operations Center (SOC) is.
* The purpose of a SOC.
* The difference between security detection and response.
* The three pillars of a SOC: **People, Processes, and Technology**.
* The responsibilities of different SOC roles.
* What a **SOC Level 1 Analyst** does.
* What alert triage means.
* How the **Five Ws — Who, What, When, Where, and Why** — are used during alert investigation.
* What a **SIEM** is and why it is important to SOC operations.
* How security technologies such as **EDR, firewalls, and antivirus solutions** provide security telemetry.
* How a SOC analyst investigates an alert and determines whether it is a true positive or false positive.
* How authorized security scanning can generate alerts that require investigation.

---

## What Is a SOC?

A **Security Operations Center (SOC)** is a specialized security team responsible for continuously monitoring an organization's digital environment.

A SOC monitors systems, endpoints, networks, applications, accounts, and other security-relevant activity to identify suspicious or malicious behavior.

The main purpose of a SOC is:

**Detect → Investigate → Respond**

A SOC is not necessarily a physical room or facility. Modern SOC teams can operate remotely while using centralized security platforms and communication systems.

---

## Purpose of a SOC

A SOC helps an organization detect and respond to security-related activity such as:

* Unauthorized access
* Malware
* Intrusions
* Suspicious network activity
* Data exfiltration
* Vulnerabilities
* Policy violations
* Other potentially malicious activity

Detection is only one part of SOC operations. When an actual security incident is identified, appropriate personnel investigate and respond to the incident.

For a beginner SOC analyst, much of the work involves **monitoring alerts, performing alert triage, gathering evidence, documenting findings, and escalating suspicious activity when necessary**.

---

## The Three Pillars of a SOC

A SOC can be understood through three fundamental pillars:

### 1. People

People are responsible for monitoring, investigating, engineering, managing, and responding to security events.

Common SOC-related roles include:

* SOC Analyst Level 1
* SOC Analyst Level 2
* SOC Analyst Level 3
* Security Engineer
* Detection Engineer
* SOC Manager
* CISO

The exact structure can vary between organizations, but there is generally a hierarchy that allows security events to be escalated when the current analyst cannot handle them.

### 2. Processes

Processes define how the SOC handles security events.

Examples include:

* Alert monitoring
* Alert triage
* Investigation
* Documentation
* Escalation
* Incident response
* Containment
* Eradication
* Recovery

Having defined processes allows analysts to respond consistently instead of investigating every alert differently.

### 3. Technology

Technology provides the visibility and capabilities required by the SOC.

Common technologies include:

* SIEM
* EDR
* Firewalls
* Antivirus
* Intrusion Detection Systems
* Network security solutions

These technologies generate security data that can be collected and analyzed by the SOC.

---

## SOC Analyst Levels

### SOC Analyst Level 1

A Level 1 analyst is commonly responsible for the initial investigation of alerts.

Typical responsibilities include:

* Monitoring alerts
* Performing alert triage
* Investigating available logs
* Identifying suspicious activity
* Documenting findings
* Determining whether an alert requires escalation

This makes Level 1 analysts an important part of the initial detection process.

### SOC Analyst Level 2

Level 2 analysts generally handle more complex investigations and escalated alerts.

They may perform deeper analysis and support incident response activities.

### SOC Analyst Level 3

Level 3 analysts generally handle highly complex investigations and advanced security activities.

Depending on the organization, they may work with areas such as:

* Advanced incident response
* Digital forensics
* Threat hunting
* Containment
* Eradication
* Recovery

The exact responsibilities differ between organizations.

---

## Alert Triage

**Alert triage** is the process of reviewing a security alert to determine what happened, how important it is, and what should happen next.

A SOC Level 1 analyst may receive a large number of alerts. Not every alert represents an actual security incident.

The analyst therefore needs to investigate the available information and determine whether the activity is:

* Benign
* Suspicious
* Malicious
* A false positive
* A true positive

The analyst may then close the alert, continue investigating it, or escalate it to another analyst or team.

---

## The Five Ws

One of the most useful concepts introduced in the room is the **Five Ws**:

**Who — What — When — Where — Why**

These questions help an analyst structure an investigation.

### Who?

Who performed the activity?

This could be a user, process, host, application, or external source.

### What?

What happened?

For example:

* Malware was detected.
* A port scan occurred.
* Data was exfiltrated.
* An unauthorized login was attempted.

### When?

When did the activity occur?

Timestamps are important because they help establish a timeline of events.

### Where?

Where did the activity occur?

This could involve:

* An IP address
* Host
* Endpoint
* Network
* Application
* Account

### Why?

Why did the activity occur?

The analyst determines this through investigation and available evidence.

For example, a port scan could be caused by an authorized vulnerability assessment rather than an attacker.

---

## SIEM

A **SIEM (Security Information and Event Management)** platform is one of the most important technologies used by a SOC.

A SIEM collects and centralizes security-related logs and events from different sources.

Without a SIEM, an analyst might need to investigate logs separately from many systems.

With a SIEM, logs from sources such as:

* Endpoints
* Firewalls
* Servers
* Network devices
* Security tools

can be brought together into a centralized platform.

This gives analysts a single location where they can search, correlate, and investigate security events.

---

## EDR

**EDR (Endpoint Detection and Response)** is a security technology focused on endpoints such as organizational computers.

An EDR solution can collect endpoint telemetry and provide visibility into activity occurring on those systems.

The collected information can be sent to centralized security platforms such as a SIEM, allowing SOC analysts to investigate endpoint-related activity.

---

## Firewall

A **firewall** helps control network traffic between networks or systems based on defined security rules.

From a SOC perspective, firewall logs can provide useful information about network activity, including connections involving internal and external systems.

Firewall telemetry can therefore contribute to security monitoring and investigation.

---

## Practical Investigation

The practical exercise in the room simulates the work of a **SOC Level 1 analyst**.

The scenario involves a port scan being detected within the network.

The analyst receives an alert and investigates the associated SIEM logs.

The investigation requires determining:

* What activity triggered the alert
* When the activity occurred
* The destination host
* The source host
* The reason for the activity
* Whether the activity was malicious or authorized
* Whether a response was received

The investigation demonstrates an important SOC concept:

**An alert does not automatically mean that a security incident has occurred.**

An alert must be investigated using available evidence and context.

---

## True Positive vs False Positive

### True Positive

A **true positive** occurs when an alert correctly identifies activity that matches the security detection and represents a genuine security concern.

### False Positive

A **false positive** occurs when an alert is generated, but investigation determines that the activity is legitimate or not actually a security incident.

In the practical exercise, the port scan was associated with an authorized vulnerability assessment using **Nessus**.

Because the activity was expected and authorized, the alert was determined to be a **false positive** rather than a malicious incident.

This demonstrates why context is critical during alert triage.

---

## Important Learning

One of the biggest lessons from this room is that a SOC analyst should not immediately assume that suspicious-looking activity is malicious.

For example, port scanning is commonly associated with reconnaissance. However, organizations may intentionally perform port scans as part of vulnerability assessments.

The analyst must therefore investigate:

**What happened? → Who performed it? → When did it happen? → Where did it happen? → Why did it happen?**

Only after examining the available evidence should the analyst determine the appropriate action.

---

## Key Takeaways

The most important concepts from this room are:

1. A **SOC** continuously monitors an organization's environment for security-related activity.
2. The primary security objectives are **detection and response**.
3. A SOC is built around **People, Processes, and Technology**.
4. A **SOC Level 1 Analyst** commonly performs initial alert triage and investigation.
5. The **Five Ws** provide a simple framework for understanding an alert.
6. A **SIEM** centralizes security logs and events from multiple sources.
7. **EDR** provides visibility into endpoint activity.
8. Firewalls provide useful network security telemetry.
9. An alert does not automatically mean an incident has occurred.
10. Investigation and context are necessary to distinguish legitimate activity from malicious activity.
11. Proper documentation and escalation are important parts of SOC operations.

---

## Beginner Practice Activities

### Activity 1 — Five Ws Practice

Take a fictional alert such as:

> Multiple failed login attempts were detected against an employee account.

Answer:

* Who?
* What?
* When?
* Where?
* Why?

The goal is to practice thinking like an analyst rather than immediately deciding that the activity is malicious.

### Activity 2 — True Positive or False Positive

Consider the following situations:

**Scenario A:** An administrator performs an authorized vulnerability scan against company servers.

**Scenario B:** An unknown external IP repeatedly scans company systems without authorization.

Determine whether each situation should be considered potentially legitimate or suspicious and explain what additional evidence you would investigate.

### Activity 3 — Build a Simple Investigation Timeline

Choose a fictional security alert and create a timeline containing:

**Timestamp → Event → Source → Destination → Analyst Finding**

This helps develop the habit of organizing evidence chronologically.

---

## Skills Developed

After completing this room, a beginner should have a foundational understanding of:

* SOC operations
* Security monitoring
* Alert triage
* Security event investigation
* SIEM fundamentals
* EDR fundamentals
* Network security monitoring
* Five Ws investigation methodology
* Alert classification
* False positives and true positives
* Security escalation

---

## Conclusion

The SOC Fundamentals room provides a foundation for understanding how a Security Operations Center operates and what a beginner SOC analyst does.

The most important lesson is that SOC work is not simply about finding something suspicious. It is about **collecting evidence, understanding context, investigating the activity, documenting the findings, and making an appropriate decision**.

For someone beginning a SOC career, understanding these fundamentals provides a foundation for learning more advanced topics such as SIEM investigation, detection engineering, incident response, digital forensics, threat intelligence, and threat hunting.
