# Wireshark Basics (TryHackMe)

> A beginner-focused learning repository documenting my journey through the **Wireshark Basics** room on TryHackMe. This repository focuses on understanding concepts, developing investigation skills, and learning how packet analysis is performed in real-world cybersecurity—not on providing challenge walkthroughs or flags.

---

# Overview

Wireshark is one of the most widely used **network packet analyzers** in cybersecurity. It allows analysts to capture, inspect, and analyze network traffic at a very detailed level.

During this room I learned how to:

* Navigate the Wireshark interface.
* Understand how packets are organized.
* Inspect different protocol layers.
* Search and navigate through packet captures.
* Apply display filters.
* Export useful artifacts from captures.
* Use Wireshark as an investigation tool rather than just a packet viewer.

This room serves as the foundation for more advanced packet analysis and network forensics.

---

# Learning Objectives

After completing this room, I was able to:

* Understand what Wireshark is and when it is used.
* Open and investigate PCAP files.
* Capture and inspect network traffic.
* Read packet information layer by layer.
* Navigate large packet captures efficiently.
* Search for specific data inside packets.
* Apply display filters to isolate interesting traffic.
* Export packets and objects for further investigation.
* View protocol conversations and follow network streams.
* Interpret basic protocol information during investigations.

---

# Key Concepts Learned

## What is Wireshark?

Wireshark is an **open-source packet analyzer** used to inspect network traffic.

It can analyze:

* Live network traffic
* Previously captured traffic (PCAP/PCAPNG files)

Wireshark is commonly used by:

* SOC Analysts
* Incident Responders
* Network Engineers
* Digital Forensics Investigators
* Penetration Testers

---

## What Wireshark Can Do

* Capture live packets
* Read PCAP files
* Decode hundreds of network protocols
* Inspect packet contents
* Troubleshoot network issues
* Investigate suspicious traffic
* Analyze malware communication
* Perform network forensics

---

## What Wireshark Cannot Do

Wireshark is **not**:

* An Intrusion Detection System (IDS)
* A firewall
* An antivirus
* A packet modification tool

It analyzes traffic but does not automatically determine whether activity is malicious. Accurate analysis depends on the analyst's knowledge.

---

# Wireshark Interface

Major interface components include:

* Toolbar
* Packet List Pane
* Packet Details Pane
* Packet Bytes Pane
* Display Filter Bar
* Status Bar

Understanding the purpose of each pane makes investigations faster and more efficient.

---

# Packet Structure

Each packet contains multiple protocol layers.

Common layers include:

1. Frame Information
2. Ethernet Layer
3. Internet Protocol (IPv4/IPv6)
4. Transport Layer (TCP/UDP)
5. Application Protocol
6. Application Data

Each layer reveals different information required during investigations.

---

# Important Investigation Features

During this room I learned how to:

* Jump directly to packets
* Search inside packet details
* Mark important packets
* Add packet comments
* Export packets
* Export transferred files
* View capture properties
* Follow protocol streams
* View expert information

These features significantly improve investigation efficiency.

---

# Display Filters

Display filters allow analysts to focus only on relevant traffic.

Examples include:

* HTTP traffic
* TCP traffic
* UDP traffic
* Source IP
* Destination IP
* Source Port
* Destination Port

Filtering reduces noise and helps identify suspicious activity much faster.

---

# Packet Navigation Skills

Important navigation techniques learned:

* Go to packet number
* Find specific strings
* Search packet details
* Search packet bytes
* Mark investigation points
* Follow conversations
* Follow TCP streams

These techniques are essential when working with large packet captures.

---

# Practical Skills Gained

After completing this room I became comfortable with:

* Opening PCAP files
* Reading packet details
* Understanding protocol layers
* Using packet filters
* Inspecting HTTP traffic
* Exporting transferred files
* Identifying useful investigation artifacts
* Navigating thousands of packets efficiently

---

# Beginner Challenges

Some concepts that may initially feel difficult include:

* Understanding protocol layers
* Reading packet details
* Knowing where information is stored
* Navigating large PCAP files
* Remembering display filter syntax
* Distinguishing capture filters from display filters

These become much easier with regular practice.

---

# Real-World Relevance

Wireshark is frequently used to:

* Investigate phishing incidents
* Analyze malware traffic
* Troubleshoot network problems
* Investigate suspicious connections
* Validate security alerts
* Perform incident response
* Conduct digital forensics
* Support penetration testing

Learning Wireshark is a foundational skill for both defensive and offensive cybersecurity roles.

---

# Key Takeaways

* Wireshark is one of the most important packet analysis tools.
* Effective investigations depend on analyst knowledge.
* Display filters dramatically improve analysis efficiency.
* Understanding protocol layers is critical.
* Navigation skills save significant investigation time.
* Packet analysis becomes easier with consistent practice.

---

# Practice Ideas

To reinforce this room:

1. Open a sample PCAP and identify the protocols present.
2. Practice using display filters for different protocols.
3. Locate specific packets using packet numbers.
4. Search for strings inside packet details.
5. Export HTTP objects from a capture.
6. Follow TCP conversations.
7. Inspect HTTP requests and responses.
8. Compare TCP and UDP traffic.
9. Explore Expert Information warnings.
10. Repeat the room without using hints.

---

# Skills Developed

* Packet Analysis
* Network Traffic Analysis
* Wireshark Navigation
* Protocol Analysis
* TCP/IP Fundamentals
* HTTP Analysis
* Digital Forensics Basics
* Incident Investigation
* Traffic Filtering

---

# Learning Reflection

This room was not about memorizing Wireshark features—it was about learning how analysts investigate network traffic. Every packet tells a part of the story, and Wireshark provides the tools needed to reconstruct that story. Building confidence with packet navigation, filtering, and protocol analysis creates a strong foundation for future SOC, DFIR, and penetration testing work.
