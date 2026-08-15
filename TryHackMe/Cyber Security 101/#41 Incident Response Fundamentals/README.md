# TryHackMe – Incident Response Fundamentals

## Overview

This repository documents my learning from the **Incident Response Fundamentals** room in the **TryHackMe Cyber Security 101 – Defensive Security** pathway.

The room introduces the fundamentals of identifying, analyzing, containing, and recovering from cybersecurity incidents. It also explains how security teams use tools such as **SIEM, Antivirus, EDR, and SOAR**, along with **incident response plans, playbooks, and runbooks**, to respond to security incidents efficiently.

The main goal of this room is not simply to solve an incident, but to understand **how a security team thinks and responds when something suspicious happens inside an organization**.

---

## Learning Objectives

By completing this room, I learned:

* What a cybersecurity incident is.
* How events, alerts, and incidents are related.
* The difference between **false positives** and **true positives**.
* How incident severity helps security teams prioritize their work.
* Common types of cybersecurity incidents.
* The fundamentals of the **SANS Incident Response Framework**.
* The fundamentals of the **NIST Incident Response Framework**.
* What an Incident Response Plan contains.
* How SIEM helps detect suspicious activity.
* How Antivirus and EDR contribute to incident detection and response.
* The purpose of incident response playbooks.
* The difference between playbooks and runbooks.
* How containment, eradication, and recovery help reduce the impact of an incident.
* Why lessons learned are important for improving future incident response.

---

## 1. Understanding Events, Alerts, and Incidents

A digital device constantly generates **events**. Opening a file, logging in, launching a process, connecting to a network, or performing other activities can generate events that are recorded in logs.

In an organization, thousands or even millions of events can be generated across endpoints, servers, applications, and network devices.

Security tools collect and analyze these events to identify activity that may be suspicious.

The basic relationship can be understood as:

```text
Activity
   ↓
Event
   ↓
Security Tool Analysis
   ↓
Alert
   ↓
Investigation
   ↓
True Positive / False Positive
   ↓
Incident
```

An **alert** is an indication that something potentially suspicious has occurred.

An **incident** is a confirmed security event that requires a response.

This distinction is important because not every alert represents an actual security problem.

---

## 2. False Positives and True Positives

A **false positive** occurs when a security tool generates an alert for activity that appears malicious but is actually legitimate.

For example, a large transfer of data to cloud storage may look suspicious. However, investigation may show that the transfer was part of a legitimate organizational backup.

A **true positive** occurs when an alert correctly identifies genuinely suspicious or malicious activity.

For example, an alert about a phishing email may be confirmed after investigation to contain a malicious attachment intended to compromise a user's system.

A SOC analyst therefore should not automatically assume that every alert is malicious. The analyst must **investigate the available evidence and determine what actually happened**.

---

## 3. Incident Severity

Organizations can receive multiple incidents at the same time. Because security teams have limited time and resources, incidents must be prioritized.

A common severity model is:

```text
Critical
   ↓
High
   ↓
Medium
   ↓
Low
```

A **critical incident** requires immediate attention because it can cause significant damage to the organization.

A lower-severity incident may still require investigation, but it generally does not receive the same immediate priority as a critical incident.

Severity can depend on factors such as:

* The systems affected.
* The sensitivity of the data involved.
* The number of users affected.
* Whether the attacker has obtained access.
* The potential business impact.
* Whether the incident is still spreading.
* The organization's risk level.

The important lesson is that **incident response is also a prioritization problem**.

---

## 4. Common Types of Incidents

### Malware Infection

Malware is malicious software designed to perform harmful actions against a system, application, or network.

Malware can enter an environment through methods such as malicious email attachments, downloads, compromised websites, or other attack vectors.

### Security Breach

A security breach occurs when an unauthorized person gains access to protected information or systems.

The important element is **unauthorized access**.

### Data Leak

A data leak occurs when confidential information becomes exposed to unauthorized parties.

A data leak does not always require a malicious attacker. Human mistakes, insecure configurations, or accidental exposure can also cause data leaks.

### Insider Attack

An insider attack originates from someone who has legitimate access to an organization's environment.

An insider may intentionally abuse their access or may be manipulated or compromised by an external attacker.

Because insiders already have some level of legitimate access, these incidents can be particularly difficult to detect.

### Denial of Service

A **Denial-of-Service (DoS)** attack attempts to make a system, network, or application unavailable to legitimate users by overwhelming or disrupting the target.

This directly affects the **Availability** component of the CIA Triad.

---

## 5. Incident Response

Incident response is the structured process used by an organization to **prepare for, detect, investigate, contain, remove, and recover from security incidents**.

Incident response should not be improvised during an emergency.

Organizations prepare procedures beforehand so that analysts know:

* What to investigate.
* Who should be contacted.
* What actions should be taken.
* How the incident should be contained.
* When the incident should be escalated.
* How communication should be handled.
* How recovery should occur.
* What should be documented afterward.

The objective is to **minimize damage, reduce response time, and return the organization to normal operation**.

---

## 6. SANS Incident Response Framework

The SANS Incident Response Framework contains six phases:

```text
Preparation
     ↓
Identification
     ↓
Containment
     ↓
Eradication
     ↓
Recovery
     ↓
Lessons Learned
     ↓
Preparation
```

### Preparation

The organization prepares before an incident occurs.

This includes creating response procedures, establishing communication channels, preparing tools, defining responsibilities, maintaining backups, and developing playbooks.

### Identification

Security teams identify suspicious activity and determine whether an actual incident has occurred.

This commonly involves analyzing alerts, logs, endpoint activity, network activity, and other evidence.

### Containment

The goal is to stop the incident from spreading or causing additional damage.

For example, a compromised endpoint may be isolated from the network.

Containment can be performed at different levels depending on the incident.

### Eradication

The malicious activity or underlying threat is removed from the environment.

Depending on the situation, this can involve removing malware, eliminating persistence, deleting malicious accounts, or rebuilding compromised systems.

### Recovery

Systems are returned to normal operation.

Organizations may use backups, redundant systems, or clean recovery points to restore affected services.

### Lessons Learned

After the incident, the organization reviews what happened.

The team asks questions such as:

* What happened?
* Why did it happen?
* What worked well?
* What failed?
* How quickly did we respond?
* How could detection be improved?
* What should be changed in the playbook?

The lessons learned are then used to improve the **Preparation** phase.

This makes incident response a continuous improvement cycle rather than a one-time process.

---

## 7. NIST Incident Response Framework

The NIST approach presented in the room organizes incident response into four major areas:

```text
Preparation
     ↓
Detection & Analysis
     ↓
Containment, Eradication & Recovery
     ↓
Post-Incident Activity
```

The concepts are very similar to the SANS framework.

The main difference is how the activities are grouped.

For example, SANS separates **Containment**, **Eradication**, and **Recovery**, while the NIST model groups these activities together.

The final **Post-Incident Activity** stage covers activities such as reviewing the incident and applying lessons learned.

The important point is not simply memorizing the names. The important concept is understanding the **logical flow of incident response**.

---

## 8. Incident Response Plan

An **Incident Response Plan (IRP)** is a formal document that defines how an organization responds to cybersecurity incidents.

It establishes the organization's overall approach before, during, and after an incident.

An incident response plan can define:

* Roles and responsibilities.
* Incident response procedures.
* Communication procedures.
* Escalation paths.
* Stakeholders who must be contacted.
* Legal and regulatory requirements.
* Law-enforcement communication.
* Recovery procedures.
* Documentation requirements.

A well-designed plan reduces confusion during a high-pressure incident.

Instead of asking:

> "What should we do now?"

the response team can follow an established process.

---

## 9. Security Tools Used in Incident Response

### SIEM

**SIEM** stands for **Security Information and Event Management**.

A SIEM collects logs and security events from different sources and brings them into a centralized platform.

It can correlate events and generate alerts when activity appears suspicious.

A simplified model is:

```text
Endpoints
Servers
Network Devices
Applications
      ↓
     Logs
      ↓
     SIEM
      ↓
Correlation & Analysis
      ↓
    Alerts
      ↓
Security Team
```

The SIEM helps analysts deal with the enormous number of events generated in an organization's environment.

---

### Antivirus

Antivirus software detects and blocks known malicious software.

Traditional antivirus solutions commonly rely heavily on known malware characteristics or signatures, although modern solutions can use additional detection techniques.

Antivirus is one layer of endpoint protection.

---

### EDR

**EDR** stands for **Endpoint Detection and Response**.

EDR provides visibility into endpoint activity and helps security teams investigate and respond to suspicious behavior.

An EDR solution can provide information about processes, files, connections, and other endpoint activity.

Depending on the solution and organizational configuration, EDR can also help analysts isolate compromised endpoints and perform response actions.

---

### SOAR

**SOAR** stands for **Security Orchestration, Automation and Response**.

SOAR platforms can automate repetitive security response actions.

For example:

```text
Alert
  ↓
SOAR
  ↓
Automated Action
  ↓
Block / Isolate / Enrich / Notify
```

Automation can reduce the time required to respond to repetitive and well-understood incidents.

---

## 10. Playbooks and Runbooks

### Playbooks

A **playbook** provides guidance for responding to a particular type of security incident.

For example, a phishing playbook can define a general response process:

```text
Phishing Alert
      ↓
Analyze Email
      ↓
Inspect Sender
      ↓
Inspect Headers
      ↓
Check Attachment/URL
      ↓
Determine User Interaction
      ↓
Contain Affected Endpoint
      ↓
Block Malicious Indicators
      ↓
Investigate Further
      ↓
Document Incident
```

The purpose of a playbook is to provide analysts with a consistent response methodology.

### Runbooks

A **runbook** provides more detailed, step-by-step execution instructions for specific actions.

The distinction can be simplified as:

```text
Playbook = What should we do?

Runbook = How exactly do we perform a specific action?
```

Both help organizations standardize and improve incident response.

---

## 11. Practical Investigation

The practical exercise in this room demonstrated an incident involving a **phishing email with a malicious attachment**.

The investigation required examining the environment to determine which systems were affected and what happened after the attachment was downloaded.

The investigation demonstrated an important real-world concept:

**One phishing campaign can affect multiple users or endpoints.**

Not every affected endpoint necessarily has the same level of compromise.

For example:

```text
Endpoint A → Attachment downloaded
Endpoint B → Attachment downloaded
Endpoint C → Attachment downloaded + Executed
```

This means an analyst must investigate each affected system rather than assuming that every endpoint experienced exactly the same activity.

The exercise also demonstrated the importance of looking at a **process timeline**.

A timeline can help connect events together and answer questions such as:

```text
What happened first?
        ↓
Which process was involved?
        ↓
What file was downloaded?
        ↓
Was the file executed?
        ↓
What happened afterward?
        ↓
Did suspicious activity occur?
```

This type of reasoning is fundamental to incident investigation.

---

## 12. Key Lessons Learned

The biggest lesson from this room is that **incident response is a structured process, not random troubleshooting**.

A security analyst must first understand what happened, determine whether the alert represents a real threat, assess the severity, and then take appropriate response actions.

Another important lesson is that **speed matters, but incorrect actions can also cause damage**. An analyst should follow established procedures and collect enough evidence to understand the situation before taking actions that could destroy useful evidence or interfere with an investigation.

I also learned that **containment is extremely important**. If one endpoint is compromised, the objective is not only to clean that machine. The security team must consider whether the threat could have spread to other systems.

The room also showed why organizations need **playbooks, runbooks, backups, communication procedures, and clearly defined responsibilities before an incident occurs**.

Finally, incident response does not end when the malware is removed or the system is restored. The organization must review the incident and use what it learned to improve its defenses and future response process.

---

## 13. Beginner Practice Activities

### Activity 1 – Alert Classification

Create five imaginary security alerts.

For each alert, decide:

```text
Alert
↓
False Positive or True Positive?
↓
Why?
↓
Severity?
```

The goal is to practice thinking like a SOC analyst instead of automatically treating every alert as malicious.

### Activity 2 – Incident Classification

Create examples of:

* Malware infection.
* Security breach.
* Data leak.
* Insider attack.
* Denial-of-Service attack.

For each example, explain what happened and what part of the CIA Triad could be affected.

### Activity 3 – Incident Response Mapping

Take a fictional malware incident and map the response to the SANS framework:

```text
Preparation
Identification
Containment
Eradication
Recovery
Lessons Learned
```

Write one or two actions that could occur during each phase.

### Activity 4 – Timeline Analysis

Create a small timeline containing:

```text
Email received
↓
Attachment downloaded
↓
Attachment executed
↓
Process created
↓
Network connection
↓
Security alert
```

Then explain what evidence an analyst would want to investigate at each stage.

---

## 14. Important Concepts to Remember

```text
Event
    ↓
Alert
    ↓
Investigation
    ↓
True Positive / False Positive
    ↓
Incident
    ↓
Severity
    ↓
Response
```

```text
SANS

Preparation
Identification
Containment
Eradication
Recovery
Lessons Learned
```

```text
Security Tools

SIEM → Collects, correlates and analyzes security events
AV   → Detects and blocks malicious software
EDR  → Provides endpoint visibility and response
SOAR → Automates security response actions
```

```text
Playbook → General response guidance
Runbook  → Detailed execution instructions
IRP      → Organization-wide incident response plan
```

---

## 15. Final Takeaway

Incident response is one of the fundamental responsibilities of defensive cybersecurity.

The objective is not simply to detect an attacker. A security team must understand **what happened, determine the impact, contain the threat, remove it, recover affected systems, and learn from the incident**.

For a beginner entering a SOC environment, understanding this process provides a strong foundation for working with SIEM and EDR alerts.

The most important mindset is:

**Do not just ask, "What alert did I receive?"**

Ask:

**"What happened, what evidence supports it, how serious is it, what is affected, what should I do next, and how can we prevent or respond to this better in the future?"**
