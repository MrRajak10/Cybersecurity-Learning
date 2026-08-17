# Network Security Solutions

## Overview

This repository documents my learning journey through the **Network Security Solutions** room on TryHackMe, part of the **Red Teaming** path.

The room focuses on understanding how security solutions such as **Intrusion Detection Systems (IDS)** and **Intrusion Prevention Systems (IPS)** inspect network traffic and how attackers may attempt to avoid detection by manipulating network protocols, payloads, routing, and communication.

The main goal of this room was not simply to complete the tasks, but to understand **how network security controls detect suspicious activity, why signatures can be bypassed, and how attackers modify their traffic to make malicious activity harder to detect**.

---

## Learning Objectives

By completing this room, I learned:

* The basic purpose of **IDS and IPS**.
* The difference between **network-based IDS/IPS** and host-based monitoring.
* How **signature-based** and **anomaly-based** detection work.
* The basic structure of IDS/IPS rules.
* How network security solutions inspect **IP addresses, ports, protocols, packets, and payloads**.
* How attackers can perform **protocol manipulation** to make traffic appear different from its original form.
* How **payload manipulation** can change the appearance of commands and malicious data.
* How encoding, obfuscation, and encryption can affect detection.
* How attackers can manipulate **routing and proxying** to change the apparent origin of traffic.
* Why security controls must look beyond simple signatures.
* Why modern firewalls and other network security technologies may combine capabilities traditionally associated with IDS and IPS.

---

## Core Concepts Learned

### IDS and IPS

An **Intrusion Detection System (IDS)** monitors traffic and looks for suspicious or malicious activity. When it identifies something that matches a detection rule or another suspicious pattern, it can generate an alert.

An **Intrusion Prevention System (IPS)** performs detection as well, but it is placed **inline with network traffic**, allowing it to actively block or reject suspicious traffic.

A simple way to remember the difference is:

> **IDS = Detect and Alert**
> **IPS = Detect and Prevent**

The placement of these systems is also important. A network-based IDS can observe traffic without necessarily sitting directly in the traffic path, while an IPS generally needs to be positioned so that traffic passes through it before reaching the protected destination.

---

## IDS Detection Techniques

### Signature-Based Detection

A **signature-based IDS** searches for known patterns associated with malicious activity.

For example, a security rule might look for a particular command, byte sequence, protocol characteristic, or network pattern that has previously been associated with an attack.

This approach works very well when the malicious activity is already known and the signature is accurate.

The major limitation is that attackers may modify the appearance of their traffic without changing the underlying objective of the attack.

This creates an important lesson:

> A detection rule is only as effective as the behavior or pattern it is designed to recognize.

### Anomaly-Based Detection

An **anomaly-based IDS** attempts to learn what normal traffic looks like and then identifies activity that significantly differs from that expected behavior.

For example, if a system normally communicates using a predictable set of protocols and suddenly begins producing unusual traffic patterns, an anomaly-based system may consider that activity suspicious.

The important difference is:

> **Signature-based detection asks, "Does this match something known?"**
> **Anomaly-based detection asks, "Does this behave differently from normal?"**

Both approaches have strengths and weaknesses, and modern security systems can use multiple detection methods together.

---

## Understanding IDS/IPS Rules

The room introduced the idea that IDS and IPS products use a specific rule syntax to describe what traffic should be detected or blocked.

A typical rule can contain information such as:

* **Action** — what should happen when the rule matches.
* **Protocol** — TCP, UDP, ICMP, or IP.
* **Source address and port** — where the traffic originates.
* **Destination address and port** — where the traffic is going.
* **Direction** — how the traffic flows between source and destination.
* **Rule options** — additional conditions used to identify the activity.
* **Message and identifier** — information used for logging and tracking the rule.

For example, a security rule can be designed to detect or block suspicious ICMP traffic, scanning activity, or a specific pattern contained inside an HTTP request.

Learning this rule structure helped me understand that an IDS/IPS is not simply looking at a connection as "good" or "bad." It can inspect many individual characteristics of network communication.

---

## Evasion and Detection Bypass

One of the most important lessons from the room was that attackers can intentionally modify their traffic so that it does not match a security signature.

This is known as **IDS/IPS evasion**.

The room introduces several broad categories of manipulation.

### Protocol Manipulation

Attackers can change characteristics of the network communication itself.

Examples include manipulating:

* TCP or UDP source ports
* TCP flags
* IP packet structure
* Packet fragmentation
* Checksums
* Session behavior

The important idea is that a security product may expect traffic to behave in a certain way. Changing those characteristics can sometimes make malicious traffic harder to recognize.

This does **not** mean that simply changing a port automatically hides an attack. Modern security solutions can perform deeper inspection and correlate multiple characteristics.

---

## Session Manipulation

Another technique discussed in the room is **session splicing**.

Instead of sending malicious content in one obvious and easily recognizable pattern, an attacker may divide or manipulate the communication so that the detection system has more difficulty identifying the complete activity.

This demonstrates an important difference between:

**What the attacker sends**

and

**How the attacker sends it**

A detection system therefore needs to understand communication at a deeper level instead of depending on one simple packet pattern.

---

## Invalid or Unusual Packets

The room also demonstrates that attackers can deliberately generate unusual or malformed packets.

For example, traffic may contain:

* Invalid TCP or UDP checksums.
* Unusual TCP flag combinations.
* Unexpected packet structures.

The purpose is to test whether the target, security device, and other network components process the traffic differently.

This leads to an important security principle:

> Different devices may interpret the same network traffic differently.

A security control that sees something one way while the destination system processes it another way can create opportunities for evasion.

---

## Payload Manipulation

### Encoding and Obfuscation

A signature may search for an exact string or recognizable payload.

Attackers can sometimes modify that payload using techniques such as:

* Base64 encoding
* URL encoding
* Unicode escaping
* Other forms of obfuscation

The underlying command or data may remain logically similar while its visible representation changes.

For example, a security signature might expect a command in its original form. An encoded version may look completely different to a simple pattern-matching rule.

The key lesson is:

> Changing the representation of data can sometimes defeat weak signature matching.

However, stronger security solutions may decode or normalize traffic before analysis, which reduces the effectiveness of simple encoding-based evasion.

---

## Encrypted Communication

Encryption was another major concept in the room.

When network communication is encrypted, a monitoring system may no longer be able to directly read the application-layer content.

For example, a command transmitted through an encrypted communication channel may appear as encrypted data instead of readable text.

This creates a visibility problem:

**Plaintext traffic**

Security system can potentially inspect the actual content.

**Encrypted traffic**

Security system may need other methods, such as metadata analysis, endpoint telemetry, decryption mechanisms, or behavioral detection.

This shows why modern security monitoring cannot depend entirely on packet contents.

---

## Routing and Source Manipulation

The room also explores manipulation at the routing level.

Attackers may use techniques involving:

* Source routing concepts
* Proxy servers
* Intermediate systems

The purpose can include changing how traffic reaches its destination or hiding the original source of a connection.

Proxying is especially important because the target may observe the **proxy's address** rather than the original attacker's address.

This reinforces an important investigation principle:

> An IP address observed by a target does not always represent the true origin of the activity.

SOC analysts therefore need to understand network architecture, proxies, NAT, VPNs, load balancers, and other infrastructure before making attribution decisions.

---

## Tools Encountered

The room introduced or used several tools and technologies related to network traffic generation and analysis.

### Nmap

**Nmap** is a network scanning tool used to discover hosts, services, ports, and other network information.

In the context of this room, Nmap is particularly useful for understanding how changing scan parameters can alter the traffic generated by a scanner.

Concepts explored included:

* TCP scanning
* UDP scanning
* Source-port manipulation
* Fragmentation
* Custom packet behavior

### Ncat

**Ncat** is a networking utility that can create connections and listeners.

It is useful for understanding how data can be exchanged between systems and how different communication characteristics appear to network security controls.

### Wireshark

Although the room's main emphasis is not simply on packet analysis, packet captures are extremely useful for understanding what is actually happening on the network.

Wireshark can help answer questions such as:

* Which protocol was used?
* Which port was used?
* What was the source and destination?
* Was the traffic fragmented?
* Was the communication encrypted?
* What did the packet actually contain?

### CyberChef

**CyberChef** is useful for performing transformations such as encoding, decoding, and data manipulation.

It is particularly helpful when learning how an original payload changes when encoded into formats such as Base64.

### OpenSSL

**OpenSSL** can be used to create certificates and establish encrypted communication.

The room demonstrates why encrypted channels can significantly reduce the visibility of application-layer content to network monitoring systems.

---

## My Learning Journey

This room helped me move from thinking about network security as simply **"firewall blocks bad traffic"** to understanding that network detection is a much more complicated process.

At first, IDS and IPS seemed like almost identical technologies. The room helped me understand their different positions and purposes within a network.

I also learned that detection is heavily influenced by **how traffic is represented**. A command, scan, or exploit does not necessarily look exactly the same every time it travels across a network.

One of the biggest lessons was understanding the relationship between:

**Attacker → Network Traffic → Security Control → Target**

An attacker can modify the traffic between the attacker and target, while the security control attempts to interpret that traffic correctly.

This made concepts such as encoding, protocol manipulation, fragmentation, and encryption much easier to understand because they are all different ways of changing what the security system sees.

---

## Challenges Encountered

The most challenging part of the room was understanding how all the different evasion techniques relate to one another.

At first, protocol manipulation, payload manipulation, routing manipulation, and encrypted communication can feel like completely separate subjects.

After working through the room, I understood that they are all connected by one central idea:

> **Change the observable characteristics of malicious traffic so that detection becomes more difficult.**

Another challenge was understanding IDS/IPS rule syntax. A rule contains multiple fields, and each field contributes to the conditions under which traffic will be detected or blocked.

Working through practical examples made the rule structure much easier to understand than simply reading the syntax.

---

## What I Learned From My Mistakes

One important lesson from this room was that seeing a command in a walkthrough is not enough.

For example, knowing that an option exists in Nmap or another tool does not automatically mean I understand why it is being used.

A better learning process is:

**Understand the traffic → Change one characteristic → Observe the result → Compare the packet behavior → Understand why detection changed**

This approach makes security tools much easier to learn because the focus remains on the underlying networking concept rather than memorizing commands.

---

## Practical Exercises

### Exercise 1 — IDS vs IPS

Draw a simple network containing:

**Client → Firewall/IPS → Server**

Then create another version containing:

**Client → Server**

with an IDS monitoring the traffic.

Explain why the IPS must be positioned differently from the IDS.

### Exercise 2 — Signature Thinking

Create a simple hypothetical IDS rule that detects a specific command or network pattern.

Then modify the representation of that data using encoding.

Ask:

> Would a basic exact-match signature still detect it?

The objective is to understand the limitation of simple signatures.

### Exercise 3 — Packet Comparison

Use Nmap against an authorized lab machine.

Perform two scans with different options and compare the generated packets in Wireshark.

Focus on:

* Source port
* Destination port
* TCP flags
* Packet size
* Protocol
* Fragmentation

The objective is to understand how a command-line option can change actual network traffic.

### Exercise 4 — Encoding Laboratory

Take a harmless text string and encode it using:

**Base64 → URL Encoding → Unicode escaping**

Then decode each version back to the original text.

The goal is to understand the difference between **data content** and **data representation**.

### Exercise 5 — Encrypted vs Unencrypted Traffic

Create a controlled lab where one connection is plaintext and another uses encryption.

Capture both with Wireshark.

Compare what can be read directly from the packet capture.

The objective is to understand why encryption changes network visibility.

---

## Key Takeaways

The most important lessons from this room are:

1. **IDS detects suspicious activity, while IPS can actively prevent it.**
2. **Signature-based detection is powerful for known threats but can have weaknesses when traffic is modified.**
3. **Anomaly-based detection focuses on deviations from normal behavior.**
4. **Network security devices can inspect much more than IP addresses and ports.**
5. **Attackers can manipulate protocols, packets, payloads, routing, and encryption to complicate detection.**
6. **Encoding is not encryption, and neither should automatically be considered malicious.**
7. **Encryption reduces the visibility of application-layer content to network monitoring systems.**
8. **An observed source IP does not always identify the real origin of an attack.**
9. **Understanding packet behavior is more valuable than memorizing tool commands.**
10. **Effective detection requires multiple signals and deeper behavioral analysis rather than relying on a single signature.**

---

## Real-World Relevance

The concepts from this room are directly relevant to:

* SOC operations
* Network Detection and Response (NDR)
* Intrusion Detection and Prevention
* Threat Hunting
* Firewall monitoring
* Incident Response
* Network Forensics
* Red Team Operations
* Blue Team Defense
* Detection Engineering

A SOC analyst may encounter a suspicious scan, unusual port activity, fragmented packets, encoded payloads, encrypted connections, or traffic coming through a proxy.

Understanding how attackers manipulate traffic makes it easier to investigate those events and determine whether the activity is legitimate, suspicious, or malicious.

---

## Final Reflection

The most valuable lesson from this room was that **network security is not simply about blocking bad IP addresses or ports**.

Attackers continuously change how their traffic looks, while defenders continuously improve how they inspect and interpret that traffic.

Understanding this relationship between **attacker behavior, network traffic, detection logic, and defensive controls** provides a strong foundation for both offensive security and defensive security work.

This room helped strengthen my understanding of network security and showed me why learning the underlying networking concepts is essential before trying to master advanced security tools.
