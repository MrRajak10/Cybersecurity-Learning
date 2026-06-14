# What is Networking? - TryHackMe

## Overview
This repository documents my learning journey through the **What is Networking?** room on TryHackMe. The room introduces the fundamental concepts of computer networking and explains how devices communicate with each other across local and global networks.
Rather than focusing on challenge solutions, this repository focuses on understanding the core networking concepts that form the foundation for cybersecurity, system administration, cloud computing, and penetration testing.

---

## Learning Objectives
By completing this room, I learned:
  * What a network is and why networks exist
  * The difference between private and public networks
  * How the Internet is structured
  * How devices identify themselves on a network
  * The purpose of IP addresses and MAC addresses
  * The differences between IPv4 and IPv6
  * How MAC address spoofing works
  * The purpose of ICMP and Ping
  * How connectivity between devices is tested

---

## Topics Covered

### 1. What is Networking?
A network is a collection of connected devices that can communicate and share resources.
Examples include:
  * Home Wi-Fi networks
  * Corporate networks
  * Mobile phone networks
  * Public transportation systems
  * Electrical power grids
In computing, networks allow devices such as laptops, phones, servers, cameras, and IoT devices to exchange information.

---

### 2. What is the Internet?
The Internet is a massive network made up of many smaller interconnected networks.
Key concepts:
  * Private Networks connect devices within a local environment.
  * Public Networks connect private networks together through the Internet.
  * Routers help networks communicate with each other.
Historical milestones:
  * ARPANET laid the foundation for modern networking.
* Tim Berners-Lee created the World Wide Web (WWW), enabling information sharing on a global scale.

---

### 3. Device Identification
Every device on a network must be identifiable.
Devices primarily use:

#### IP Address
An IP address acts like a temporary address used to locate a device on a network.
Examples:
  * 192.168.1.10
  * 10.0.0.5

Characteristics:
  * Can change over time
  * Used for communication
  * Must be unique within a network

#### MAC Address
A MAC (Media Access Control) address is a unique hardware identifier assigned to a network interface.
Example:
* a4:c3:f0:85:ac:2d

Characteristics:
  * Assigned by the manufacturer
  * Used at the hardware level
  * Intended to be unique
  * Can be spoofed

---

### 4. Public vs Private IP Addresses

#### Private IP Addresses
Used within local networks.
Common private ranges:
  * 10.0.0.0/8
  * 172.16.0.0 – 172.31.255.255
  * 192.168.0.0/16

Examples:

* 192.168.1.74
* 192.168.1.77

#### Public IP Addresses
Used to identify networks on the Internet.
Characteristics:
  * Assigned by Internet Service Providers (ISPs)
  * Visible to external networks
  * Shared by devices behind a router through Network Address Translation (NAT)

---

### 5. IPv4 vs IPv6

#### IPv4
Example:
* 192.168.1.1

Features:
  * 32-bit addressing
  * Approximately 4.3 billion addresses
  * Most commonly used today

#### IPv6
Example:
* 2001:0db8:85a3:0000:0000:8a2e:0370:7334

Features:
  * 128-bit addressing
  * Massive address space
  * Designed to solve IPv4 exhaustion
  * Improved efficiency and scalability

---

### 6. MAC Address Spoofing
MAC spoofing occurs when a device changes its MAC address to impersonate another device.
Potential uses:
  * Bypassing poorly implemented access controls
  * Testing security configurations
  * Research and educational purposes

Important lesson:
Trusting only MAC addresses for security is not sufficient because MAC addresses can be modified.

---

### 7. ICMP and Ping
Ping is a basic networking tool used to test connectivity between devices.
Ping uses:
  * ICMP (Internet Control Message Protocol)

Process:
  1. Device sends an ICMP Echo Request.
  2. Target responds with an ICMP Echo Reply.
  3. Response times are measured.

Example:
```bash
ping 8.8.8.8
```

Common uses:
  * Testing connectivity
  * Troubleshooting network issues
  * Measuring latency
  * Verifying host availability

---

## Practical Skills Gained
During this room, I practiced:
  * Identifying IP addresses
  * Distinguishing between public and private networks
  * Recognizing MAC addresses
  * Understanding MAC spoofing concepts
  * Using Ping for connectivity testing
  * Understanding how devices communicate across networks

---

## Key Takeaways
  * Networks are simply connected devices that exchange information.
  * The Internet is a network of networks.
  * Every device requires an identifier to communicate effectively.
  * IP addresses identify devices logically.
  * MAC addresses identify devices physically.
  * IPv6 was introduced to address IPv4 limitations.
  * MAC addresses can be spoofed and should not be trusted as the sole security mechanism.
  * Ping and ICMP are essential troubleshooting tools.

---

## Challenges and Learning Moments
While studying this room, several concepts required extra attention:
  * Understanding the difference between IP addresses and MAC addresses
  * Distinguishing public and private IP addresses
  * Understanding why devices on the same network can share one public IP address
  * Learning the purpose of IPv6
  * Understanding how ICMP operates behind the Ping command

These concepts form the foundation for many advanced networking and cybersecurity topics.

---

## Why This Room Matters
Networking knowledge is essential for:
* Cybersecurity
* Penetration Testing
* SOC Analysis
* Digital Forensics
* Cloud Computing
* System Administration

Understanding how devices communicate is a prerequisite for understanding attacks, defenses, monitoring, and incident response.

---

## Final Thoughts

This room provides a beginner-friendly introduction to networking and establishes the foundational knowledge required for further cybersecurity learning. Understanding concepts such as IP addressing, MAC addressing, network communication, and ICMP creates a strong base for exploring more advanced networking and security topics in the future.
