# IDS Fundamentals — TryHackMe Learning Notes

## Overview

**TryHackMe Room:** IDS Fundamentals

This room introduces the fundamentals of **Intrusion Detection Systems (IDS)** and explains how security teams can identify suspicious activity that has already entered a network.

The room builds on firewall concepts. A firewall primarily controls traffic based on security rules, but an attacker may sometimes bypass those controls or enter through a seemingly legitimate connection. An IDS adds another layer of visibility by monitoring activity and generating alerts when suspicious behavior is detected.

The practical portion of the room uses **Snort**, an open-source network intrusion detection tool, to understand detection modes, Snort rules, custom rule creation, and investigation of previously captured network traffic stored in a PCAP file.

The main goal of this room is not simply to learn how to use Snort commands, but to understand **how intrusion detection works and how defenders investigate suspicious network activity**.

---

## Learning Objectives

By completing this room, you should understand:

* What an Intrusion Detection System (IDS) is
* The difference between IDS and IPS
* Host-based and network-based IDS deployment
* Signature-based, anomaly-based, and hybrid detection
* The purpose and operating modes of Snort
* How Snort rules are structured
* How custom detection rules can be created
* How network traffic can be analyzed using PCAP files
* How IDS alerts can help during network investigations
* How individual alerts can provide useful evidence about suspicious activity

---

## 1. What Is an IDS?

An **Intrusion Detection System (IDS)** is a security mechanism that monitors activity and attempts to identify suspicious or malicious behavior.

When an IDS detects activity that matches its detection logic, it generates an **alert**.

A key point to remember is:

> **IDS detects and alerts; it does not normally prevent the detected activity.**

This makes IDS different from a firewall or an Intrusion Prevention System.

### IDS vs Firewall vs IPS

| Technology | Primary Purpose                                            |
| ---------- | ---------------------------------------------------------- |
| Firewall   | Controls network traffic according to security rules       |
| IDS        | Detects suspicious activity and generates alerts           |
| IPS        | Detects suspicious activity and can take preventive action |

A useful way to visualize this is:

**Firewall → controls access**
**IDS → watches for suspicious activity**
**IPS → detects and can respond automatically**

### Simple Analogy

Imagine an apartment building:

* The **firewall** is the security guard at the entrance.
* An attacker bypasses the guard and enters the building.
* The **IDS** is similar to the CCTV system inside the building.
* Even though the attacker passed the entrance, their activity can still be observed and detected.

This illustrates why IDS is valuable as a **defense-in-depth** mechanism.

---

# 2. Types of IDS

IDS can be categorized in two major ways:

1. **Deployment type**
2. **Detection method**

---

## 2.1 Deployment Types

### HIDS — Host-Based Intrusion Detection System

A **HIDS** is deployed directly on an individual host, such as:

* A workstation
* A server
* Another monitored endpoint

It focuses primarily on activity occurring on that specific system.

### Advantages

* Detailed visibility into the monitored host
* Can inspect host-specific activity
* Useful for monitoring important endpoints or servers

### Disadvantages

* Requires deployment and management on individual systems
* Can become difficult to manage across a large environment
* Consumes resources on monitored hosts

### Key Idea

**HIDS = monitoring an individual host**

---

## 2.2 NIDS — Network-Based Intrusion Detection System

A **NIDS** monitors network traffic and can provide visibility across a larger portion of the network.

Instead of installing detection software on every host, network traffic can be inspected centrally.

### Advantages

* Broader network visibility
* Centralized monitoring
* Useful for observing communication between multiple systems

### Disadvantages

* Visibility depends on where the monitoring sensor is positioned
* Encrypted traffic may limit what can be inspected
* High traffic volumes can increase processing requirements

### Key Idea

**NIDS = monitoring network traffic**

---

## HIDS vs NIDS

| Feature          | HIDS                            | NIDS                                  |
| ---------------- | ------------------------------- | ------------------------------------- |
| Monitoring Scope | Individual host                 | Network traffic                       |
| Deployment       | Installed on host               | Positioned to inspect network traffic |
| Visibility       | Detailed host-level information | Broader network visibility            |
| Management       | More difficult at scale         | More centralized                      |
| Example Use      | Server monitoring               | Network intrusion detection           |

---

# 3. IDS Detection Methods

The second major classification is based on **how an IDS identifies suspicious behavior**.

The three major approaches introduced in the room are:

* Signature-based detection
* Anomaly-based detection
* Hybrid detection

---

## 3.1 Signature-Based IDS

A **signature** represents a recognizable pattern associated with known malicious activity.

A signature-based IDS compares observed traffic or activity against a database of known signatures.

For example, if a known attack generates a specific network pattern, the IDS can identify that pattern and generate an alert.

### Advantages

* Effective against known threats
* Generally fast when matching known patterns
* Easier to understand and tune for known attack types

### Limitation

Signature-based detection depends heavily on having a signature for the threat.

A completely new or previously unknown attack may not match an existing signature.

### Key Idea

**Signature-based = "Have I seen this known attack pattern before?"**

---

## 3.2 Anomaly-Based IDS

An **anomaly-based IDS** attempts to establish what normal behavior looks like and then identifies activity that significantly deviates from that baseline.

For example:

```text
Normal behavior
      ↓
Baseline established
      ↓
Unexpected behavior observed
      ↓
Potential anomaly
      ↓
Alert
```

This approach can be useful for identifying previously unknown or unusual attacks.

### Advantage

It may detect activity that does not have a known signature.

### Limitation

Not every unusual event is malicious.

Therefore, anomaly-based systems can generate **false positives** when legitimate activity differs from the expected baseline.

### Key Idea

**Anomaly-based = "Is this behavior unusual compared with the normal baseline?"**

---

## 3.3 Hybrid IDS

A **hybrid IDS** combines multiple detection approaches, particularly:

* Signature-based detection
* Anomaly-based detection

This provides a broader detection capability than relying on only one method.

A hybrid approach can use known attack signatures while also looking for unusual behavior.

### Key Idea

**Hybrid IDS = known attack detection + abnormal behavior detection**

---

## Detection Method Comparison

| Detection Method | Strength                               | Main Limitation                 |
| ---------------- | -------------------------------------- | ------------------------------- |
| Signature-Based  | Strong for known threats               | Can miss unknown attacks        |
| Anomaly-Based    | Can identify unusual/unknown behavior  | Can produce false positives     |
| Hybrid           | Combines multiple detection approaches | More complex to manage and tune |

---

# 4. Introduction to Snort

**Snort** is an open-source network intrusion detection tool used to inspect network traffic and identify suspicious activity.

A major concept in the room is that Snort can analyze traffic according to **rules**.

A rule defines what traffic or behavior should be considered interesting and what action should be taken when it matches.

This makes Snort highly customizable.

---

# 5. Snort Operating Modes

The room introduces three important Snort modes.

## 5.1 Packet Sniffer Mode

In packet sniffer mode, Snort reads and displays packets.

The focus is on **observing traffic**, rather than performing a complete intrusion-detection workflow.

Think of it as:

> "Show me the packets."

---

## 5.2 Packet Logging Mode

In packet logging mode, network traffic is written to files for later analysis.

A common format for captured network packets is **PCAP (Packet Capture)**.

This is useful when traffic needs to be preserved and investigated at a later time.

Think of it as:

> "Record the traffic so it can be investigated later."

---

## 5.3 NIDS Mode

NIDS mode is used for intrusion detection.

Snort analyzes traffic against its configured rules and can generate alerts when a rule matches.

Think of it as:

> "Monitor the traffic and tell me when something suspicious happens."

---

## Snort Modes at a Glance

| Mode           | Main Purpose                                   |
| -------------- | ---------------------------------------------- |
| Packet Sniffer | Read/display packets                           |
| Packet Logging | Save packet traffic for later analysis         |
| NIDS           | Detect suspicious activity and generate alerts |

---

# 6. Understanding Snort Rules

One of the most important lessons from the room is that **Snort rules describe what should be detected**.

A simplified rule concept looks like:

```text
Action + Protocol + Traffic Direction + Conditions + Metadata
```

A rule can tell Snort:

* What action to take
* Which protocol to inspect
* Where the traffic is coming from
* Where the traffic is going
* What conditions must match
* What message should appear in the alert
* Which signature identifier is associated with the rule
* Which revision of the rule is being used

---

## Example Detection Concept

The room demonstrates a rule designed to detect an **ICMP ping request**.

Conceptually, the rule says:

```text
When ICMP traffic matching the specified conditions
is observed,
generate an alert with a descriptive message.
```

This is useful because ICMP is commonly used for network connectivity testing, but repeated or unexpected ICMP activity can also provide valuable information during reconnaissance investigations.

The important lesson is not the exact syntax alone, but understanding how each component contributes to detection.

---

# 7. Important Snort Rule Components

A Snort rule can contain several important elements.

### Action

Defines what Snort should do when the rule matches.

For example:

```text
alert
```

This tells Snort to generate an alert.

---

### Protocol

Specifies the network protocol being inspected.

Examples include:

```text
ICMP
TCP
UDP
```

---

### Source and Destination

Rules can define:

* Source IP
* Source port
* Destination IP
* Destination port

Special values can be used to represent broad matches, depending on the rule syntax.

This allows a rule to be highly specific or more general.

---

### Message

A rule can include a descriptive message that appears when the rule triggers.

A meaningful alert message makes investigations easier because the analyst can immediately understand what the rule was intended to identify.

For example:

```text
Ping detected
```

---

### SID — Signature ID

The **SID** identifies the rule.

It provides a way to distinguish one signature from another.

When analyzing alerts, identifying the SID can help determine **which rule generated the detection**.

---

### Rev — Revision

The **revision number** indicates the revision of a rule.

When the rule is modified, its revision can be incremented.

Conceptually:

```text
Revision 1
   ↓
Rule modified
   ↓
Revision 2
   ↓
Rule modified again
   ↓
Revision 3
```

This helps track changes made to detection rules.

---

# 8. Snort Configuration and Custom Rules

The room introduces the Snort configuration structure and the location used for custom rules.

The main configuration area discussed is:

```text
/etc/snort
```

The rules are maintained within the Snort rules structure, including:

```text
/etc/snort/rules
```

A particularly important file for custom rules is:

```text
local.rules
```

The purpose of this file is to provide a place for locally defined/custom detection rules.

### Why Custom Rules Matter

Real environments cannot rely only on pre-existing signatures.

Organizations may want to detect:

* Internal reconnaissance
* Organization-specific attack patterns
* Suspicious administrative activity
* Custom malware behavior
* Policy violations
* Environment-specific network anomalies

Custom rules allow defenders to adapt Snort to the environment they are protecting.

---

# 9. Testing a Detection Rule

The room demonstrates an important security practice:

> **A rule should be tested after it is created.**

Creating a detection rule is not enough.

An analyst should verify:

1. The rule loads correctly.
2. The intended traffic actually triggers the rule.
3. The alert message is understandable.
4. The rule does not generate unexpected behavior.
5. The detection logic matches the intended scenario.

The room demonstrates this by creating an ICMP detection rule and generating ping traffic to verify that Snort produces the expected alert.

This is an important real-world lesson because poorly designed detection rules can lead to:

* Missed detections
* Excessive alerts
* False positives
* Analyst fatigue

---

# 10. PCAP Analysis

The room also introduces the idea of running Snort against a **PCAP file**.

A PCAP file contains previously captured network traffic.

Instead of monitoring live traffic, an analyst can inspect historical traffic.

This is especially useful for:

* Incident response
* Forensic investigation
* Malware analysis
* Threat hunting
* Detection testing
* Training
* Security research

The general workflow is:

```text
PCAP file
   ↓
Snort analyzes captured traffic
   ↓
Rules are evaluated
   ↓
Matching events generate alerts
   ↓
Analyst investigates the results
```

This demonstrates that IDS technologies are useful not only for **real-time detection**, but also for **retrospective investigation**.

---

# 11. Practical Investigation Skills

The final practical exercise demonstrates how IDS alerts can be used as investigative evidence.

Instead of simply asking whether an attack occurred, analysts can extract information such as:

* Source IP address
* Destination IP address
* Protocol
* Destination port
* Alert message
* Signature ID
* Type of detected activity

For example, an SSH-related alert can indicate that one machine attempted to communicate with another machine over the SSH service.

Similarly, an ICMP-related alert can indicate ping activity.

The important mindset is:

> **An alert is evidence that needs to be interpreted in context.**

An alert does not automatically prove that a successful compromise occurred.

---

# 12. Important Security Concepts Learned

## Detection vs Prevention

One of the most important distinctions in this room is:

```text
IDS → Detect
IPS → Prevent
```

Understanding this distinction is fundamental when learning defensive security.

---

## Visibility Is Critical

A firewall may control traffic at the network boundary, but defenders still need visibility into what happens after traffic enters the environment.

IDS provides an additional visibility layer.

---

## Known vs Unknown Threats

Different detection methods have different strengths.

```text
Known attack pattern
        ↓
Signature-based detection
```

```text
Unexpected behavior
        ↓
Anomaly-based detection
```

```text
Both requirements
        ↓
Hybrid detection
```

No single detection method is perfect.

---

## Detection Engineering

The room also introduces an early concept of **detection engineering**.

Security teams must create, test, maintain, and improve detection rules.

A detection rule should answer:

> What behavior are we trying to identify, and what evidence should trigger an alert?

This is an important transition from simply using cybersecurity tools to understanding how defensive detections are designed.

---

# 13. Common Beginner Mistakes

Several mistakes are common when learning IDS technologies.

### Mistake 1: Thinking IDS Blocks Attacks

IDS primarily detects and alerts.

Blocking is associated with prevention mechanisms such as IPS or other security controls.

---

### Mistake 2: Confusing HIDS and NIDS

Remember:

```text
HIDS → Host
NIDS → Network
```

---

### Mistake 3: Memorizing Rule Syntax Without Understanding It

It is more useful to understand what each rule field controls than to memorize a complete rule blindly.

---

### Mistake 4: Assuming Every Alert Means a Successful Attack

An alert means the detection logic matched.

The analyst still needs to investigate:

* What generated the alert?
* Was the activity expected?
* Was the connection successful?
* What happened before and after the event?
* Is there supporting evidence?

---

### Mistake 5: Ignoring False Positives

A detection that generates too many irrelevant alerts can become operationally ineffective.

Good detection requires a balance between:

* Detection coverage
* Accuracy
* Alert volume
* Investigation effort

---

# 14. Practical Exercises

After completing the room, the following exercises can reinforce the concepts.

## Exercise 1 — IDS Classification

For each scenario, decide whether HIDS or NIDS would be more appropriate.

1. Monitoring file changes on a Linux server
2. Monitoring traffic crossing a network segment
3. Monitoring authentication activity on a workstation
4. Monitoring communication between multiple internal systems

Explain why you selected each deployment type.

---

## Exercise 2 — Detection Method Selection

For each scenario, decide whether signature-based or anomaly-based detection would be more appropriate:

1. Detecting a known network exploit
2. Detecting unusual outbound communication
3. Detecting a previously identified malicious pattern
4. Detecting behavior that significantly deviates from an established baseline

Then identify situations where combining both approaches would be useful.

---

## Exercise 3 — Create a Simple Detection Idea

Design a conceptual Snort rule for detecting one of the following:

* Unexpected ICMP activity
* Suspicious SSH connection attempts
* Traffic to an unusual destination port

Before writing the rule, define:

```text
What behavior?
Which protocol?
Source?
Destination?
What should happen when matched?
What alert message should appear?
```

---

## Exercise 4 — PCAP Investigation

Use a sample PCAP file and investigate it with a network analysis tool.

Try to identify:

* Top communicating hosts
* Common protocols
* Unusual ports
* Repeated connection attempts
* ICMP activity
* SSH activity
* Suspicious communication patterns

Then compare what you discover manually with what an IDS rule would detect.

---

## Exercise 5 — Detection Validation

Create a simple test environment in which you intentionally generate traffic that should trigger a detection rule.

Then verify:

```text
Traffic generated
      ↓
Rule matches
      ↓
Alert generated
      ↓
Alert interpreted
```

Afterward, modify the traffic so that it should **not** trigger the rule.

This teaches an important detection-engineering principle:

> A good rule should detect what it is designed to detect without producing unnecessary alerts.

---

# 15. Suggested Learning Path

The concepts from this room fit naturally into a defensive security learning path:

```text
Networking Fundamentals
        ↓
Firewalls
        ↓
IDS / IPS
        ↓
Packet Analysis
        ↓
PCAP Investigation
        ↓
Detection Rules
        ↓
Threat Detection
        ↓
Incident Response
        ↓
Threat Hunting
```

Understanding IDS becomes much easier when networking fundamentals are already familiar.

---

# 16. Key Takeaways

* **IDS detects suspicious activity and generates alerts.**
* **IDS is different from IPS because IDS does not primarily prevent the detected activity.**
* **HIDS monitors an individual host.**
* **NIDS monitors network traffic.**
* **Signature-based detection identifies known patterns.**
* **Anomaly-based detection identifies deviations from normal behavior.**
* **Hybrid IDS combines multiple detection approaches.**
* **Snort is an open-source tool used for network intrusion detection.**
* **Snort has packet sniffing, packet logging, and NIDS capabilities.**
* **Snort relies heavily on rules for detection.**
* **SID identifies a rule, while Rev tracks its revision.**
* **Custom rules can be stored in the local rules configuration.**
* **PCAP files allow historical network traffic to be analyzed.**
* **IDS alerts are evidence that requires investigation and context.**
* **Detection engineering involves creating, testing, tuning, and maintaining reliable detections.**

---

## Personal Learning Reflection

This room provides an important transition from understanding **how security controls protect a network** to understanding **how defenders identify suspicious activity inside that network**.

The biggest conceptual lesson is that security is not based on one control. A firewall may stop many unwanted connections, but security teams still need visibility into activity that gets through.

Learning Snort also introduces a more practical side of defensive security: **writing detection logic, testing it, reading alerts, and investigating captured traffic**.

The ability to understand why an alert was generated is more valuable than simply knowing which command produced it. This mindset is essential for progressing toward areas such as SOC analysis, incident response, threat hunting, and detection engineering.

---

## Final Perspective

The IDS Fundamentals room demonstrates a simple but powerful defensive-security idea:

> **Prevention is important, but visibility and detection are equally important.**

An effective security program assumes that some suspicious activity may reach the internal environment and therefore needs mechanisms capable of detecting it.

By understanding IDS architecture, detection methodologies, Snort rules, PCAP analysis, and alert interpretation, beginners can start developing the mindset required for real-world security monitoring and investigation.
