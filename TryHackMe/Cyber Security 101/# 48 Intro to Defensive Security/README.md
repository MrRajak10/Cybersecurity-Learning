# TryHackMe – Intro to Defensive Security

This repository documents my learning journey through the **Intro to Defensive Security** room on TryHackMe.

The room provides a beginner-friendly introduction to defensive cybersecurity, explains major areas of defensive security, and demonstrates how a Security Operations Center (SOC) analyst investigates and responds to a suspicious network event.

The goal of these notes is not simply to record the answers to the room. Instead, they focus on understanding the concepts, the reasoning behind defensive security activities, and how these concepts connect to real-world security operations.

---

## Learning Objectives

By completing this room, I learned:

* What defensive security means and how it differs from offensive security.
* The two fundamental goals of defensive security:

  * Preventing intrusions.
  * Detecting intrusions when they occur.
* What a Security Operations Center (SOC) does.
* The responsibilities of a SOC analyst.
* The purpose of threat intelligence.
* The role of Digital Forensics and Incident Response (DFIR).
* The basics of malware analysis.
* What a Security Information and Event Management (SIEM) system does.
* How a SOC analyst can investigate and escalate a suspicious event.
* Why incident escalation and containment are important parts of defensive security.

---

## Understanding Defensive Security

Defensive security focuses on protecting systems, networks, applications, and data from attacks and suspicious activity.

While offensive security generally focuses on identifying weaknesses by thinking like an attacker, defensive security focuses on identifying, preventing, investigating, and responding to threats.

Two broad responsibilities are central to defensive security:

### Intrusion Prevention

The objective is to prevent unauthorized or malicious activity from successfully affecting an environment.

This can involve security controls, monitoring systems, access restrictions, network defenses, and other protective measures.

### Intrusion Detection

Not every attack can be prevented.

Therefore, defenders also need to identify suspicious behavior when it occurs, investigate what happened, and determine the appropriate response.

This is one of the reasons continuous monitoring is so important in cybersecurity.

---

## Major Areas of Defensive Security

The room introduces several important areas within defensive security.

### Security Operations Center (SOC)

A Security Operations Center is responsible for monitoring systems and networks for suspicious or malicious activity.

SOC analysts commonly investigate alerts, examine relevant information, determine whether activity is legitimate or malicious, and escalate incidents when necessary.

For beginners entering defensive cybersecurity, SOC analyst roles are often an important starting point because they provide exposure to many foundational security concepts.

---

### Threat Intelligence

Threat intelligence involves collecting and analyzing information about potential or known threats.

The purpose is not simply to gather information, but to turn that information into something useful for defenders.

Threat intelligence can help organizations:

* Understand emerging threats.
* Identify potentially malicious infrastructure.
* Improve defensive controls.
* Prepare systems and networks for known or anticipated attacks.

Threat intelligence can also complement SOC operations because information about known threats can help analysts investigate alerts more effectively.

---

### Digital Forensics and Incident Response (DFIR)

Digital forensics and incident response are commonly discussed together because both are important when investigating and dealing with security incidents.

**Digital forensics** focuses on examining digital evidence to understand what happened.

**Incident response** focuses on handling and recovering from security incidents.

An incident does not necessarily have to involve a criminal act. For example, an internal mistake or user action could cause an operational or security problem that requires a response.

DFIR therefore combines investigation, evidence analysis, containment, recovery, and understanding of incidents.

---

### Malware Analysis

Malware analysis focuses on understanding malicious software.

A malware analyst investigates malware to determine:

* What the malware does.
* How it behaves.
* What systems or resources it interacts with.
* What impact it may have.
* How defenders can identify or respond to it.

Malware analysis is generally more specialized than many entry-level cybersecurity roles, but it is an excellent area for developing deeper technical skills.

---

## A Day in the Life of a Junior SOC Analyst

The practical section of the room demonstrates a simplified SOC workflow.

A SOC analyst often works with a **Security Information and Event Management (SIEM)** system.

A SIEM can be thought of as a centralized platform for collecting, organizing, and analyzing security-related logs and events.

Instead of checking every system independently, analysts can use a SIEM to bring relevant information together and generate alerts when unusual activity is detected.

A simplified workflow demonstrated by the room is:

**Alert → Investigation → Validation → Escalation → Containment**

### 1. Alert

The SIEM generates an alert because it detects unusual activity.

In the practical example, the alert represents an unauthorized connection attempt.

### 2. Investigation

The analyst examines the alert and identifies the information associated with the suspicious activity, including the source IP address.

The important point is that an alert is not automatically proof of an attack. It needs to be investigated.

### 3. Validation

The suspicious IP address is checked to determine whether it is associated with malicious activity.

This demonstrates an important SOC skill: distinguishing potentially malicious activity from legitimate activity.

### 4. Escalation

After determining that the activity is malicious, the junior analyst escalates the incident to the appropriate SOC team lead or higher-level analyst.

Escalation ensures that incidents receive the appropriate level of authority and expertise.

### 5. Containment

Once the required authorization is obtained, a defensive action can be taken to prevent further communication from the malicious source.

In the room's example, this involves implementing a rule to block the malicious IP address.

The broader lesson is that defensive security is not simply about finding suspicious activity. Analysts must investigate, validate, communicate, and take appropriate action.

---

## Important Concepts to Remember

### Alert ≠ Confirmed Attack

A security alert is an indication that something requires investigation.

An analyst should not immediately assume that every alert represents malicious activity.

The analyst must gather evidence and determine what the event actually means.

### Investigation Before Action

Blocking or changing security controls can affect legitimate users and services.

Therefore, defensive actions should normally be based on sufficient investigation and appropriate authorization.

### Escalation Matters

Junior analysts do not necessarily have authority to make every security decision.

Escalating a confirmed incident allows senior personnel to review the situation and authorize appropriate containment or response actions.

### Centralized Visibility Is Valuable

A SIEM provides defenders with centralized visibility into security events.

This can make it significantly easier to identify patterns, investigate incidents, and prioritize suspicious activity.

---

## Key Takeaways

1. Defensive security is focused on protecting environments from threats.
2. Prevention and detection are two fundamental defensive objectives.
3. SOC analysts monitor systems, investigate alerts, and escalate confirmed incidents.
4. Threat intelligence helps organizations understand and prepare for potential threats.
5. DFIR combines digital investigation with incident handling and recovery.
6. Malware analysis helps defenders understand malicious software and its behavior.
7. SIEM platforms provide centralized visibility into security events and alerts.
8. A SOC investigation should involve validation rather than blindly trusting an alert.
9. Escalation and authorization are important before implementing significant defensive actions.
10. Defensive cybersecurity is a continuous process of monitoring, investigation, response, and improvement.

---

## Suggested Beginner Practice

After completing the room, it is useful to reinforce the concepts rather than stopping at the room's exercises.

### Practice 1: Think Like a SOC Analyst

For each hypothetical alert, ask:

* What happened?
* What evidence would I need?
* Could the activity be legitimate?
* What makes the event suspicious?
* Who should I escalate it to?
* What action could contain the threat?

### Practice 2: Explore Security Logs

Use a safe lab environment and examine basic authentication, network, or application logs.

Practice identifying:

* Successful activity.
* Failed activity.
* Repeated attempts.
* Unusual source addresses.
* Unexpected times or patterns.

### Practice 3: Learn SIEM Fundamentals

Research how a SIEM collects logs from different systems and turns them into searchable security events and alerts.

The objective is to understand the workflow rather than memorizing a specific product.

---

## Room Reflection

This room provides an important foundation for understanding defensive cybersecurity.

One of the most valuable lessons is that defensive security is not simply about deploying security tools. A defender must understand what the tools are reporting, investigate suspicious behavior, communicate findings, and make informed decisions about response.

The SOC example also shows how multiple defensive concepts connect together:

**Monitoring → Detection → Investigation → Validation → Escalation → Response**

Understanding this workflow provides a strong foundation for continuing into more advanced defensive security topics.

---

## Further Learning

Useful next areas to explore include:

* SOC analyst fundamentals
* SIEM investigation
* Log analysis
* Network security monitoring
* Threat intelligence
* Incident response
* Digital forensics
* Malware analysis
* Detection engineering

The most important goal at this stage is to understand why defenders perform each step, not simply memorize tools or commands.
