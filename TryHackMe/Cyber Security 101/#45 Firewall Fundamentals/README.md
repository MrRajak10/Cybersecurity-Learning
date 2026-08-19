# TryHackMe — Firewall Fundamentals

## Overview

This repository documents my learning journey through the **Firewall Fundamentals** room on TryHackMe. The room introduces the purpose of firewalls, major firewall types, firewall rules, Windows Defender Firewall, and Linux firewall management.

The main goal of this room is not simply to memorize firewall commands, but to understand **how firewalls control network traffic, how firewall rules are evaluated, and how firewall configuration differs between Windows and Linux systems**.

This room also reinforces basic networking knowledge, especially the **OSI model, IP addresses, ports, protocols, inbound traffic, and outbound traffic**.

---

## Learning Objectives

By completing this room, I learned how to:

* Understand the purpose of a firewall.
* Explain how a firewall filters network traffic.
* Distinguish between stateless and stateful firewalls.
* Understand proxy firewalls and their role as intermediaries.
* Understand the purpose of Next-Generation Firewalls (NGFWs).
* Identify common components of a firewall rule.
* Understand inbound and outbound traffic.
* Create and inspect firewall rules in Windows Defender Firewall.
* Understand the role of Netfilter in Linux.
* Understand common Linux firewall tools such as `iptables`, `nftables`, `firewalld`, and `UFW`.
* Create, view, and remove basic UFW firewall rules.
* Understand the security importance of correctly configured firewall policies.

---

## 1. What Is a Firewall?

A firewall can be understood as a **filter between systems or networks**.

When network traffic enters or leaves a device or network, the firewall evaluates that traffic against configured rules. Depending on the rules, the firewall can **allow, deny, block, or forward** the traffic.

For example, a firewall can be configured to:

```text
Allow TCP port 80
Allow TCP port 443
Block TCP port 22
```

This means web traffic may be allowed while SSH traffic is blocked.

Firewalls can exist at multiple points in an environment. A computer may have its own host-based firewall, while the router or network infrastructure may also enforce firewall policies.

This creates multiple layers of traffic control between a user and an external service.

---

## 2. Types of Firewalls

### Stateless Firewall

A stateless firewall evaluates traffic using predefined rules.

It does not maintain information about previous connections or traffic history.

A rule may be based on:

```text
Source IP
Destination IP
Port
Protocol
```

For example:

```text
Allow TCP traffic to port 80
```

Each packet is evaluated against the rules independently.

### Key Characteristic

**Stateless = no connection state is remembered.**

This makes stateless firewalls relatively simple and fast, but they have less context when making traffic decisions.

---

## 3. Stateful Firewall

A stateful firewall can track the **state of network connections**.

Instead of evaluating every packet completely independently, it can remember information about established connections and previous traffic.

For example, if a legitimate connection has already been established, the firewall can recognize packets that belong to that connection.

### Key Characteristic

**Stateful = remembers connection state.**

This gives the firewall more context than a stateless firewall.

### Simple Comparison

```text
Stateless Firewall
        |
        v
Checks packet against rules
        |
        v
Does not remember connection state


Stateful Firewall
        |
        v
Checks packet against rules
        |
        v
Tracks connection state
```

---

## 4. Proxy Firewall

A proxy firewall acts as an **intermediary** between the client and the destination.

Instead of communicating directly with the external service, the client communicates with the proxy, and the proxy communicates with the destination.

```text
Client
   |
   v
Proxy Firewall
   |
   v
Internet
```

Because the proxy sits in the middle of the communication, it can inspect traffic at a higher level and examine application-layer information.

A proxy can also prevent the destination from directly seeing the client's original connection details because the proxy is the system communicating on the client's behalf.

### Key Characteristic

**Proxy Firewall = intermediary that can inspect application-level traffic.**

---

## 5. Next-Generation Firewall (NGFW)

A **Next-Generation Firewall (NGFW)** provides more advanced traffic inspection and security capabilities than traditional basic filtering.

An NGFW can provide functionality across multiple layers and may include capabilities such as:

* Deep packet inspection
* Application awareness
* Traffic analysis
* Heuristic analysis
* Threat intelligence integration
* Advanced security policies

### Heuristic Analysis

Heuristic analysis means making security decisions by identifying **patterns or suspicious behavior**, instead of relying only on a simple fixed rule.

For example, instead of checking only:

```text
Is this IP address blocked?
```

advanced analysis may consider:

```text
What is this traffic doing?
Does the behavior look suspicious?
Does it match a known attack pattern?
Is the destination associated with malicious activity?
```

This provides more context for security decisions.

---

## 6. Firewall Type Comparison

| Firewall Type | Main Characteristic                                                      |
| ------------- | ------------------------------------------------------------------------ |
| Stateless     | Filters traffic using predefined rules without tracking connection state |
| Stateful      | Tracks connection state and traffic history                              |
| Proxy         | Acts as an intermediary and can inspect application-layer traffic        |
| NGFW          | Provides advanced inspection and security capabilities                   |

The important distinction is that these firewalls provide **different levels of context and inspection**.

---

## 7. Firewall Rules

A firewall rule defines **what traffic should be handled and what should happen to it**.

Common components of a firewall rule include:

```text
Source Address
Destination Address
Protocol
Port
Direction
Action
```

### Source Address

The source identifies **where the traffic is coming from**.

Example:

```text
192.168.1.10
```

### Destination Address

The destination identifies **where the traffic is going**.

Example:

```text
192.168.1.20
```

### Port

The port identifies the service or communication endpoint.

Examples:

```text
80  = HTTP
443 = HTTPS
22  = SSH
```

### Protocol

The protocol defines how the communication is performed.

Examples:

```text
TCP
UDP
```

### Direction

Traffic can generally be classified as:

```text
Inbound
Outbound
```

**Inbound traffic** enters the system or network.

**Outbound traffic** leaves the system or network.

### Action

The firewall must decide what to do when traffic matches the rule.

Common actions include:

```text
Allow
Deny
Forward
```

---

## 8. Example Firewall Rules

### Allow Rule

```text
Source: Any
Destination: Any
Protocol: TCP
Port: 80
Direction: Outbound
Action: Allow
```

This permits outbound HTTP traffic.

### Deny Rule

```text
Source: Any
Destination: Any
Protocol: TCP
Port: 22
Direction: Inbound
Action: Deny
```

This blocks inbound SSH traffic.

### Forward Rule

A firewall can also forward matching traffic to another destination.

For example:

```text
Incoming TCP port 80
        |
        v
Firewall
        |
        v
192.168.1.8
```

This can be used to direct incoming web traffic toward a specific web server.

---

# Windows Defender Firewall

Windows includes a built-in firewall called **Windows Defender Firewall**.

It allows administrators to control network traffic using firewall rules.

One important concept introduced in the room is the use of **network profiles**.

Windows can apply different firewall policies depending on the type of network, such as:

```text
Domain
Private
Public
```

This is useful because the security requirements of a trusted private network can be different from those of an untrusted public network.

For example, a computer connected to a public Wi-Fi network may require stricter rules than when it is connected to a trusted home network.

---

## Creating a Custom Windows Firewall Rule

The room demonstrates how to create a custom outbound rule.

A simplified process is:

```text
Windows Defender Firewall
        |
        v
Advanced Settings
        |
        v
Outbound Rules
        |
        v
New Rule
        |
        v
Custom
```

The rule can then specify:

```text
Program
Protocol
Ports
Source/Destination IP
Action
Network Profiles
Rule Name
```

The example used in the room created a rule to block outbound traffic associated with:

```text
TCP port 80
TCP port 443
```

This demonstrates how a firewall administrator can control traffic based on ports and protocols.

---

## Important Windows Firewall Lesson

One important troubleshooting lesson from the room was the need to distinguish between:

```text
Inbound Rules
```

and:

```text
Outbound Rules
```

When investigating or creating a rule, it is essential to identify the correct direction.

A rule designed to control incoming traffic must be looked for under **Inbound Rules**, while a rule controlling traffic leaving the system belongs under **Outbound Rules**.

Incorrectly checking the wrong rule collection can lead to confusion during an investigation.

---

# Linux Firewall Fundamentals

Linux provides firewall functionality through the **Netfilter framework**.

Netfilter provides the underlying packet-filtering functionality, while different tools provide ways for administrators to interact with it.

Common tools include:

```text
iptables
nftables
firewalld
UFW
```

---

## iptables

`iptables` is a widely known Linux firewall management tool.

It provides a command-line interface for configuring packet-filtering rules using Netfilter.

The syntax can become difficult to remember, but understanding the underlying firewall concepts makes the commands easier to understand.

---

## nftables

`nftables` is the modern successor to `iptables`.

It provides a more modern framework and syntax for configuring packet filtering.

A key point from the room is:

```text
nftables → successor to iptables
```

---

## firewalld

`firewalld` is another Linux firewall management solution built around Netfilter.

It provides a different management approach and includes predefined **network zones**.

These zones allow administrators to apply different levels of trust and firewall behavior depending on the network environment.

---

# UFW — Uncomplicated Firewall

**UFW** stands for **Uncomplicated Firewall**.

It is designed to make firewall configuration easier, especially for users who do not want to work directly with more complex firewall syntax.

For example:

```bash
ufw status
```

displays the current firewall status.

To enable UFW:

```bash
ufw enable
```

A default outgoing policy can be configured with:

```bash
ufw default allow outgoing
```

This allows outgoing traffic unless another rule restricts it.

A specific port can also be denied.

For example:

```bash
ufw deny 22/tcp
```

This blocks TCP traffic on port 22, which is commonly used for SSH.

---

## Viewing UFW Rules

To display numbered rules:

```bash
ufw status numbered
```

Numbered rules are useful because a specific rule can then be deleted by its number.

For example:

```bash
ufw delete 2
```

The important lesson is that UFW simplifies common firewall administration tasks by providing easier-to-understand commands.

---

# Important Commands Learned

## Linux

```bash
ufw status
```

Check firewall status.

```bash
ufw enable
```

Enable the firewall.

```bash
ufw default allow outgoing
```

Allow outgoing traffic by default.

```bash
ufw deny 22/tcp
```

Deny TCP port 22.

```bash
ufw status numbered
```

Display numbered firewall rules.

```bash
ufw delete 2
```

Delete rule number 2.

---

# Key Concepts to Remember

The most important concepts from this room are:

```text
Firewall
    ↓
Filters network traffic

Stateless
    ↓
No connection state

Stateful
    ↓
Tracks connection state

Proxy Firewall
    ↓
Acts as an intermediary

NGFW
    ↓
Advanced inspection and security capabilities

Firewall Rule
    ↓
Defines what traffic is allowed, blocked, or forwarded

Inbound
    ↓
Traffic entering the system/network

Outbound
    ↓
Traffic leaving the system/network

Netfilter
    ↓
Linux packet-filtering framework

iptables / nftables / firewalld / UFW
    ↓
Tools used to manage Linux firewall functionality
```

---

# Challenges and Learning Lessons

One of the important lessons from this room was that firewall security is not just about knowing commands. It requires understanding **what the traffic represents and why a rule should exist**.

Another important lesson was identifying whether traffic is **inbound or outbound**. This becomes particularly important when working with Windows Firewall because similar-looking rules can exist in separate inbound and outbound rule collections.

The Linux section also demonstrated the difference between understanding the concept and remembering syntax. Tools such as UFW make firewall configuration easier by providing simpler commands, while tools such as `iptables` require more detailed knowledge of their syntax.

The room also reinforced the importance of networking fundamentals. Understanding ports, protocols, IP addresses, and traffic direction makes firewall rules much easier to understand.

---

# Beginner Practice Exercises

## Exercise 1 — Identify the Traffic

For each example, determine whether the traffic is inbound or outbound.

```text
Your computer connects to google.com
A remote SSH server connects to your machine
Your browser downloads a web page
A remote system attempts to connect to port 22 on your machine
```

Focus on the question:

```text
Is the traffic entering my system or leaving my system?
```

---

## Exercise 2 — Analyze a Firewall Rule

Consider:

```text
Source: Any
Destination: Any
Protocol: TCP
Port: 443
Direction: Outbound
Action: Allow
```

Explain in your own words what this rule allows.

Then modify it so that HTTPS traffic is blocked instead.

---

## Exercise 3 — UFW Practice

In a safe Linux lab environment:

```bash
ufw status
ufw enable
ufw default allow outgoing
ufw deny 22/tcp
ufw status numbered
```

Then remove the rule you created.

```bash
ufw delete <rule-number>
```

The goal is to understand the **effect of each command**, not simply copy the commands.

---

# Practical Security Relevance

Firewalls are an important part of defensive security because they can reduce unwanted network communication and limit the attack surface of a system.

In a real security environment, firewall rules can be used to:

* Restrict unnecessary services.
* Limit communication between network segments.
* Block known malicious IP addresses or ports.
* Control application communication.
* Reduce exposure of sensitive systems.
* Enforce network security policies.
* Support incident response investigations.

However, a firewall should not be considered a complete security solution by itself.

A firewall is one security control within a larger defensive architecture that may also include:

```text
Firewall
+
EDR
+
IDS/IPS
+
SIEM
+
Network Monitoring
+
Threat Intelligence
+
Endpoint Security
```

---

# What I Learned

The biggest takeaway from this room is that a firewall is fundamentally a **traffic-control mechanism**.

Understanding firewall security starts with simple questions:

```text
Where is the traffic coming from?
Where is it going?
Which protocol is being used?
Which port is involved?
Is the traffic inbound or outbound?
What should happen to it?
```

Once these questions become familiar, firewall configuration becomes much easier to understand.

This room also provided a foundation for moving into more advanced areas such as **network security monitoring, intrusion detection, SIEM analysis, endpoint security, segmentation, and incident response**.

---

# Conclusion

The **Firewall Fundamentals** room provided a practical introduction to one of the most important defensive security technologies.

The room covered firewall purposes, firewall types, rule structures, traffic direction, Windows Defender Firewall, Linux firewall technologies, and UFW.

The most valuable lesson is to understand the **logic behind firewall rules**, rather than memorizing commands without understanding what they do.

A strong understanding of firewalls provides an important foundation for anyone pursuing cybersecurity, especially in areas such as **SOC operations, network security, penetration testing, incident response, and defensive security engineering**.
