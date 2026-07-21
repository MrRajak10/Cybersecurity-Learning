# TryHackMe - Networking Concepts

## Overview

This repository contains my learning notes from the **Networking Concepts** room on TryHackMe.

The goal of this room is not simply to memorize networking terms, but to build a strong understanding of how devices communicate across networks. The room introduces the OSI Model, TCP/IP Model, IP Addressing, TCP vs UDP, Encapsulation, and basic Telnet usage.

Rather than focusing on obtaining flags, this repository documents the concepts learned, important observations, and practical understanding gained throughout the room.

---

## Learning Objectives

After completing this room, I was able to understand:

- Why networking is important in cybersecurity.
- The purpose of the OSI Model.
- The TCP/IP networking model.
- IPv4 addressing fundamentals.
- Public and Private IP addresses.
- Basic routing concepts.
- The differences between TCP and UDP.
- The TCP Three-Way Handshake.
- Network encapsulation and decapsulation.
- Basic Telnet communication.
- Reading simple HTTP responses using Telnet.

---

## Topics Covered

### OSI Model

Understanding the seven layers of the OSI Model and the responsibility of each layer.

- Physical Layer
- Data Link Layer
- Network Layer
- Transport Layer
- Session Layer
- Presentation Layer
- Application Layer

---

### TCP/IP Model

Understanding the practical networking model used on the Internet.

- Link Layer
- Internet Layer
- Transport Layer
- Application Layer

Relationship between the TCP/IP model and the OSI Model.

---

### IP Addressing

Learning how devices are uniquely identified on a network.

Topics included:

- IPv4 format
- Octets
- Network Address
- Broadcast Address
- Private IP addresses
- Public IP addresses

---

### Routing

Understanding how routers forward packets between different networks.

Concepts learned:

- Routers
- Network paths
- IP-based forwarding
- Packet delivery

---

### TCP and UDP

Understanding how data is transported across networks.

TCP:

- Reliable communication
- Three-Way Handshake
- Error checking
- Ordered delivery

UDP:

- Fast communication
- No connection establishment
- No delivery guarantee
- Commonly used for streaming and real-time communication

---

### Encapsulation

Learning how data moves through networking layers.

Process covered:

Application Data

↓

Transport Header

↓

IP Header

↓

Ethernet/Wi-Fi Header

↓

Transmission

Then reversing the process during reception (Decapsulation).

---

### Telnet

Using Telnet to communicate directly with TCP services.

Practical activities included:

- Connecting to TCP services
- Echo server
- Daytime server
- HTTP server
- Sending manual HTTP requests
- Reading HTTP response headers

---

## Key Concepts Learned

- Layered networking architecture
- Logical vs Physical communication
- MAC Address vs IP Address
- Network-to-Network communication
- Host-to-Host communication
- Reliable vs unreliable protocols
- Packet encapsulation
- Manual client-server communication

---

## Beginner Challenges

Some concepts that may initially seem difficult include:

- Understanding the purpose of every OSI layer
- Distinguishing between MAC and IP addresses
- Understanding routing
- Remembering private IP address ranges
- Learning encapsulation
- Understanding TCP vs UDP
- Writing manual HTTP requests in Telnet

These concepts become much easier after repeated practice.

---

## Practical Skills Gained

After completing this room, I can:

- Explain the OSI Model.
- Explain the TCP/IP Model.
- Identify private and public IP addresses.
- Describe packet routing.
- Differentiate TCP and UDP.
- Explain encapsulation and decapsulation.
- Use Telnet to communicate with a TCP server.
- Read basic HTTP responses.

---

## Suggested Practice

To strengthen these concepts:

- Draw the OSI Model from memory.
- Compare the OSI and TCP/IP models.
- Identify private and public IP addresses.
- Practice identifying TCP and UDP protocols.
- Observe packet encapsulation using Wireshark.
- Use Telnet to communicate with different TCP services.
- Inspect HTTP responses manually.

---

## Key Takeaways

This room builds the networking foundation required for future cybersecurity learning.

Understanding networking concepts makes it much easier to study:

- Network Security
- Web Security
- Packet Analysis
- Wireshark
- Nmap
- SOC Analysis
- Threat Detection
- Penetration Testing

A strong networking foundation is essential before moving into more advanced cybersecurity topics.
