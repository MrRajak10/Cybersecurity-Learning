# TryHackMe – Defensive Security Intro

## Overview

**Defensive Security Intro** is an introductory TryHackMe room focused on the fundamentals of defensive cybersecurity. The room introduces the defensive side of cybersecurity and explains how security teams prevent attacks, detect suspicious activity, investigate incidents, and respond to threats.

Unlike offensive security, where the goal is to identify and exploit weaknesses, defensive security focuses on protecting systems, detecting malicious activity, investigating security events, and reducing the impact of attacks.

The room provides an introduction to several important areas of defensive security, including:

* Security Operations Center (SOC)
* Threat Intelligence
* Digital Forensics
* Incident Response
* Malware Analysis
* Security Information and Event Management (SIEM)

The room also introduces a basic SOC investigation scenario where an analyst investigates a suspicious authentication event, identifies a malicious IP address, escalates the incident, and blocks the malicious source.

---

## Learning Objectives

By completing this room, the learner should understand:

* What defensive security means
* The role of a Blue Team
* What a Security Operations Center (SOC) does
* How SOC analysts investigate security alerts
* What threat intelligence is and why it is useful
* The purpose of digital forensics
* The basic incident response process
* The difference between static and dynamic malware analysis
* What a SIEM is used for
* How analysts investigate suspicious IP addresses
* Why successful authentication from a malicious IP can be more serious than a failed login attempt
* How security events are escalated and contained

---

## 1. Defensive Security

Defensive security is the practice of protecting systems, networks, applications, users, and data from cyber threats.

A defensive security team works to prevent attacks where possible, detect attacks when they occur, investigate suspicious activity, and respond appropriately.

A simple way to understand the difference is:

**Offensive Security → Find and exploit weaknesses**

**Defensive Security → Find, detect, investigate, and stop threats**

The Blue Team is commonly associated with defensive security.

Defensive security activities can include security awareness training, asset management, security policies, system updates and patching, firewall configuration, intrusion prevention, monitoring, threat intelligence, incident response, and forensic investigation.

---

## 2. Security Operations Center (SOC)

A **Security Operations Center (SOC)** is a team responsible for monitoring an organization's systems and network for suspicious or malicious security activity.

SOC analysts continuously investigate security alerts and determine whether an event represents a genuine threat or a legitimate activity.

Common areas investigated by a SOC include:

### Vulnerabilities

A vulnerability is a weakness in a system that could potentially be exploited by an attacker.

Organizations need to identify and remediate vulnerabilities before attackers can take advantage of them.

### Policy Violations

Organizations establish security policies that define how systems and data should be used.

For example, uploading confidential company information to an unauthorized service could violate an organization's security policy.

### Unauthorized Activity

SOC analysts investigate activity that appears unusual or unauthorized.

Examples include unexpected account activity, suspicious logins, or unusual system behavior.

### Network Intrusions

A network intrusion occurs when an attacker gains unauthorized access to a network or system.

An intrusion could occur through methods such as exploiting a vulnerable public-facing server or convincing a user to interact with a malicious link.

---

## 3. Threat Intelligence

**Threat Intelligence** is information collected and analyzed about current or potential cyber threats and adversaries.

Threat intelligence helps organizations understand:

* Who may target them
* What techniques attackers use
* What infrastructure attackers use
* What indicators may be associated with malicious activity
* How the organization can better prepare for threats

A useful concept introduced in the room is **Tactics, Techniques, and Procedures (TTPs)**.

TTPs describe how adversaries operate.

Threat intelligence generally follows a process where data is collected, processed, analyzed, and turned into useful intelligence that defenders can use for security decisions.

One practical example is checking a suspicious IP address against threat-intelligence or reputation databases.

---

## 4. Digital Forensics

**Digital forensics** is the use of scientific investigation techniques to examine digital systems and establish facts about an incident.

Digital forensic investigations can involve:

* Computers
* Smartphones
* System memory
* Disk images
* System logs
* Application logs
* Network logs

Forensic investigators may create forensic images of systems so that evidence can be examined without unnecessarily modifying the original data.

### Memory Forensics

System memory can contain valuable evidence.

For example, an attacker may execute malicious code directly in memory without saving the program to disk. In such situations, capturing and analyzing system memory can provide evidence that may not be available from disk artifacts alone.

This is why memory forensics is an important area of digital investigation.

---

## 5. Incident Response

An **incident** can involve a confirmed cyberattack or data breach, but it can also involve less severe security events such as an intrusion attempt or security misconfiguration.

Incident response provides a structured approach for handling these events.

The room introduces the following major phases:

**Preparation → Detection & Analysis → Containment → Eradication & Recovery → Post-Incident Activity**

### Preparation

The organization prepares people, processes, and technology to respond to security incidents.

### Detection and Analysis

Security teams detect suspicious activity and investigate it to determine what happened and whether it represents a real incident.

### Containment

The objective is to prevent the incident from spreading or causing additional damage.

### Eradication and Recovery

The underlying threat is removed and affected systems are restored to a secure operating state.

### Post-Incident Activity

After recovery, the organization documents and reviews the incident to understand what happened and improve future security operations.

---

## 6. Malware Analysis

**Malware** means malicious software.

Malware can include malicious programs, documents, or files designed to perform harmful or unauthorized actions.

The room introduces several common malware concepts.

### Virus

A virus is malicious code that can attach itself to another program or file and reproduce when the infected program is executed.

### Trojan Horse

A Trojan is a malicious program that appears to provide a legitimate or desirable function while hiding malicious behavior.

### Ransomware

Ransomware is malware that commonly encrypts a victim's files and demands payment from the victim.

The important concept is that encryption can make files unreadable without the required decryption key.

---

## 7. Static and Dynamic Malware Analysis

Malware can be investigated using different analysis approaches.

### Static Analysis

Static analysis examines a malicious file **without executing it**.

An analyst may inspect characteristics of the file, its structure, strings, metadata, hashes, or other properties.

The main advantage is that the malware does not need to be executed during the initial investigation.

### Dynamic Analysis

Dynamic analysis involves executing the malware in a controlled environment, commonly an isolated virtual machine or sandbox, and observing its behavior.

An analyst may investigate:

* Network connections
* Processes
* File modifications
* Registry changes
* System behavior

Malware should never be casually executed on a normal personal or production system. Controlled and isolated environments are important when performing dynamic analysis.

---

# 8. SIEM and SOC Alert Investigation

The practical scenario in the room places the learner in the role of a SOC analyst protecting a bank.

The organization uses a **Security Information and Event Management (SIEM)** platform.

A SIEM collects security-related information and events from different sources and presents them to security analysts for monitoring and investigation.

A SOC analyst may receive many alerts, but **not every alert is necessarily malicious**.

For example, multiple failed login attempts could happen because a legitimate user forgot their password.

Therefore, the analyst needs to examine additional information and context before deciding whether an alert represents a real threat.

---

## 9. Investigating a Suspicious Login

The scenario contains authentication-related events.

One important lesson is that a failed authentication attempt is not automatically evidence of a successful compromise.

However, a **successful authentication from a known malicious IP address** is much more concerning.

The investigation can therefore follow a basic reasoning process:

**Alert → Examine events → Identify suspicious IP → Check reputation → Determine maliciousness → Escalate → Contain**

This demonstrates an important SOC principle:

> An alert is only the starting point of an investigation.

The analyst needs to correlate information and determine what the evidence means.

---

## 10. IP Address Reputation

An **IP address** identifies a network endpoint and allows systems to communicate with it.

During an investigation, a SOC analyst may check a suspicious IP address against threat-intelligence and reputation databases.

Services such as **AbuseIPDB** and **Cisco Talos Intelligence** can provide information that helps analysts investigate the reputation of an IP address.

A reputation check can provide information such as:

* Whether an IP has been reported as malicious
* Confidence or reputation information
* Geographic information
* Associated network or organization information

However, an IP reputation result should be treated as **investigative evidence**, not automatically as the complete explanation for an incident.

---

## 11. Escalation

After investigating the alert, the analyst must determine whether it needs to be escalated.

In the scenario, a successful authentication from a malicious IP is more serious than a simple failed authentication attempt.

The analyst therefore escalates the event to the appropriate security team.

This demonstrates another important SOC concept:

**The analyst must understand not only what happened, but also who should handle the next stage of the incident.**

Different security roles have different responsibilities, so escalation should be directed to the appropriate team rather than indiscriminately notifying unrelated personnel.

---

## 12. Containment

After identifying the malicious IP address, the scenario demonstrates blocking the source.

Blocking a malicious IP is an example of **containment**.

The purpose of containment is to prevent the identified threat from continuing to affect the organization.

In a real environment, the exact containment action would depend on the organization's architecture, security controls, incident severity, and established procedures.

---

# 13. Key SOC Investigation Mindset

One of the most important lessons from this room is that security analysts should not immediately assume that every alert is malicious.

Instead, an analyst should investigate the available evidence.

For example:

**Failed login**

A user may simply have entered the wrong password.

**Multiple failed logins**

This could still be a legitimate user, but it may require additional investigation.

**Successful login from a known malicious IP**

This provides significantly stronger evidence that the account may have been compromised and should be investigated and potentially escalated.

The analyst's job is therefore not simply to react to alerts. The analyst must **interpret evidence and determine the appropriate response**.

---

# 14. Important Concepts Learned

| Concept             | What It Means                                                  |
| ------------------- | -------------------------------------------------------------- |
| Defensive Security  | Protecting systems and detecting/responding to threats         |
| Blue Team           | Team responsible for defensive security activities             |
| SOC                 | Team that monitors and investigates security events            |
| Threat Intelligence | Information about threats and adversaries                      |
| TTPs                | Tactics, Techniques, and Procedures used by adversaries        |
| Digital Forensics   | Investigation of digital evidence                              |
| Incident Response   | Structured process for handling security incidents             |
| Malware Analysis    | Investigation of malicious software                            |
| Static Analysis     | Examining malware without executing it                         |
| Dynamic Analysis    | Executing malware in a controlled environment                  |
| SIEM                | Platform that collects and analyzes security events            |
| IP Reputation       | Information about the historical or reported behavior of an IP |
| Containment         | Action taken to limit the impact or spread of a threat         |
| Escalation          | Passing an investigated event to the appropriate security team |

---

# 15. Practical Learning Exercises

After completing the room, beginners can strengthen their understanding by practicing the following exercises.

### Exercise 1 – Alert Reasoning

Consider these events:

1. One failed login from an employee's normal location.
2. Ten failed logins against the same account.
3. A successful login from an unfamiliar location.
4. A successful login from an IP reported as malicious.

For each event, determine:

* Is it automatically malicious?
* What additional information would you investigate?
* Would you escalate it?
* What evidence would support your decision?

### Exercise 2 – IP Investigation

Take a publicly available suspicious IP from a security-training environment and research it using an IP reputation service.

Record:

* IP address
* Reputation
* Number of reports
* Reported categories
* Associated organization
* Geographic information
* Your conclusion

Do not treat reputation alone as proof of compromise.

### Exercise 3 – Incident Response

Take a simple scenario such as:

> An employee successfully authenticated from a suspicious external IP.

Practice describing what you would do during:

**Detection → Analysis → Containment → Eradication → Recovery → Post-Incident Activity**

### Exercise 4 – Malware Analysis Concepts

Choose a known malware sample from a safe cybersecurity training environment and research:

* What type of malware it is
* What static analysis means
* What dynamic analysis means
* What artifacts analysts may observe
* Why malware should be analyzed in an isolated environment

---

# 16. Beginner Takeaways

The most important lesson from this room is that **defensive security is much more than simply installing security software**.

A real defensive security operation combines people, processes, technology, monitoring, investigation, intelligence, forensics, and incident response.

The SOC is particularly important because it acts as a central point for monitoring and investigating security events.

Another important lesson is to avoid making conclusions from a single piece of evidence. A login failure, IP address, or alert may look suspicious, but the analyst must investigate the surrounding context.

The practical scenario demonstrates the basic SOC workflow:

**Detect → Investigate → Validate → Escalate → Contain**

This workflow forms a foundation for more advanced SOC and defensive-security learning.

---

# 17. Next Steps

After completing this introductory room, useful areas to study further include:

* SOC Analyst fundamentals
* SIEM fundamentals
* Windows Event Logs
* Linux logs
* Network traffic analysis
* Threat intelligence
* MITRE ATT&CK
* Digital forensics
* Incident response
* Malware analysis
* Detection engineering
* EDR fundamentals

The goal should not be to memorize the steps from one TryHackMe scenario. The goal is to develop the ability to **look at security evidence, understand what it means, investigate further, and make a defensible security decision**.
