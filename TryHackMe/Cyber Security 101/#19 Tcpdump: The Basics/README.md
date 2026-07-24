# TryHackMe — tcpdump: The Basics

A learning-focused repository documenting my journey through the **tcpdump: The Basics** TryHackMe room. This repository is designed for beginners who want to understand how packet capture works, how to inspect network traffic from the command line, and how tcpdump is used to analyze network communications.

> **Focus:** Learning concepts, understanding packet analysis, and building practical networking skills—not simply completing the room.

---

## Room Overview

This room introduces **tcpdump**, a command-line packet analyzer used to capture, inspect, and filter network traffic.

Instead of only learning networking protocols from diagrams, this room allows you to observe how protocols communicate in real network environments.

Throughout the room, I learned how to:

- Capture packets from network interfaces
- Save captured traffic into `.pcap` files
- Read existing packet capture files
- Apply filters to reduce unnecessary traffic
- Analyze packets based on hosts, ports, and protocols
- Understand TCP flags
- Display packets in different output formats

---

# Learning Objectives

After completing this room, I was able to understand:

- What tcpdump is
- Why packet capture is important
- Difference between tcpdump and Wireshark
- Network interfaces
- Packet capture workflow
- Reading PCAP files
- Writing PCAP files
- Packet filtering
- Protocol-based filtering
- Host filtering
- Port filtering
- Logical operators
- Advanced filtering
- TCP Flags
- Different packet display options

---

# What is tcpdump?

**tcpdump** is a command-line packet analyzer.

It captures packets that travel through a network interface and displays them in the terminal or saves them into a packet capture file (`.pcap`) for later analysis.

Think of tcpdump as a network "listener" that records conversations happening on your network.

---

# Why Learn tcpdump?

Understanding packet captures helps you see what is actually happening inside a network.

Instead of imagining how protocols work, you can observe:

- ARP requests
- DNS queries
- ICMP packets
- TCP handshakes
- HTTP traffic
- HTTPS traffic
- Many other protocols

This makes networking concepts much easier to understand.

---

# Major Topics Covered

## Introduction to Packet Capture

- Packet analyzers
- libpcap
- WinPcap
- Command-line packet analysis

---

## Capturing Packets

Learned how to:

- Select interfaces
- Capture packets
- Limit packet count
- Save captures
- Read capture files

---

## Packet Filtering

Learned how to filter traffic using:

- Host
- Source Host
- Destination Host
- Port
- Source Port
- Destination Port
- Protocols
- Logical Operators

---

## Advanced Filtering

Learned filtering using:

- Packet length
- TCP flags
- Header fields
- Bit-level filtering

---

## Display Options

Learned different display formats including:

- Brief output
- Link-layer information
- ASCII output
- Hexadecimal output

---

# Practical Skills Developed

During this room I practiced:

- Reading packet captures
- Identifying DNS traffic
- Finding ARP requests
- Locating ICMP packets
- Filtering TCP traffic
- Using logical operators
- Inspecting TCP flags
- Displaying MAC addresses
- Working with PCAP files

---

# Key Concepts Learned

- Packet Capture
- Network Interface
- PCAP Files
- Packet Filters
- DNS
- ARP
- ICMP
- TCP
- UDP
- TCP Flags
- MAC Address
- Packet Headers

---

# Beginner Challenges

Some concepts may feel confusing at first:

- Choosing the correct interface
- Understanding packet flow
- Reading tcpdump output
- Difference between source and destination
- Understanding DNS resolution
- Reading ARP packets
- TCP flag filtering
- Header-based filtering

These become much easier with regular practice.

---

# Key Takeaways

- tcpdump is one of the most powerful packet analysis tools.
- Packet filtering saves significant analysis time.
- PCAP files allow traffic to be analyzed later.
- Understanding packets improves networking knowledge.
- TCP flags reveal connection states.
- Command-line packet analysis is an essential cybersecurity skill.

---

# Beginner Practice Ideas

After completing the room, try practicing the following:

### Exercise 1

Capture traffic while opening a website.

Observe:

- DNS
- TCP Handshake
- HTTP/HTTPS

---

### Exercise 2

Ping another device.

Observe:

- ARP
- ICMP

---

### Exercise 3

Capture traffic for one specific host only.

---

### Exercise 4

Capture only DNS traffic.

---

### Exercise 5

Capture only TCP traffic.

---

### Exercise 6

Compare tcpdump output with Wireshark.

Notice how both display the same packets differently.

---

### Exercise 7

Save traffic into a `.pcap` file and analyze it later.

---

# Skills Gained

- Packet Analysis
- Network Traffic Inspection
- Packet Filtering
- Network Troubleshooting
- Command-Line Networking
- TCP/IP Analysis
- PCAP Analysis

---

# Learning Reflection

This room helped transform networking concepts from theory into something visible and practical.

Instead of only reading about protocols like ARP, DNS, ICMP, and TCP, I learned how to observe their communication in real packet captures. Understanding how to filter traffic and inspect only the packets that matter made network analysis much more manageable and reinforced the importance of packet analysis in cybersecurity.

---

# Disclaimer

This repository is intended for educational purposes only.

It focuses on learning networking concepts, packet analysis, and tcpdump usage rather than providing direct challenge walkthroughs or flag solutions.
