# TryHackMe - Intro to LAN

## Overview

This repository contains my learning notes and key takeaways from the **Intro to LAN** room on TryHackMe.

The room introduces the fundamental concepts behind Local Area Networks (LANs), including network topologies, routers, switches, subnetting, ARP, and DHCP. These topics form the foundation of modern networking and are essential for anyone pursuing cybersecurity, penetration testing, SOC analysis, or system administration.

Rather than focusing only on completing the room, I used this opportunity to understand how devices communicate within a network and why these technologies are important in real-world environments.

---

## Learning Objectives

By completing this room, I learned:

* What a Local Area Network (LAN) is
* Different network topology designs
* Advantages and disadvantages of common topologies
* The role of switches and routers
* Basic subnetting concepts
* Network, host, and default gateway addresses
* How ARP works
* How DHCP automatically assigns IP addresses
* How these concepts relate to real-world networks

---

## Topics Covered

### LAN Topologies

The room introduced three common network topologies:

#### Star Topology

* Devices connect to a central switch or hub
* Most commonly used topology today
* Easy to expand and manage
* Failure of the central device affects the entire network

#### Bus Topology

* Uses a single backbone cable
* Cost-effective and simple
* Can become a bottleneck under heavy traffic
* Single cable failure can break communication

#### Ring Topology

* Devices form a circular connection
* Data travels around the ring
* Easier fault tracing
* Failure of one device or cable can impact the whole network

---

### Switches

Switches are responsible for connecting multiple devices within the same network.

Key concepts:

* Connect computers, printers, and other devices
* Use packet switching
* Track which device is connected to which port
* Reduce unnecessary network traffic
* More efficient than hubs

---

### Routers

Routers connect different networks together.

Key concepts:

* Forward traffic between networks
* Use routing to determine packet paths
* Allow communication beyond the local network
* Essential for Internet connectivity

---

### Subnetting

Subnetting is the process of dividing a larger network into smaller networks.

Benefits include:

* Better organization
* Improved security
* Greater efficiency
* Easier network management

Important concepts learned:

| Component       | Purpose                         |
| --------------- | ------------------------------- |
| Network Address | Identifies the network          |
| Host Address    | Identifies a device             |
| Default Gateway | Sends traffic to other networks |

---

### ARP (Address Resolution Protocol)

ARP helps devices map IP addresses to MAC addresses.

Key concepts:

* Associates logical and physical addresses
* Uses ARP Requests and ARP Replies
* Maintains an ARP Cache
* Enables communication between devices on a LAN

---

### DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP addresses to devices joining a network.

DHCP Process:

1. DHCP Discover
2. DHCP Offer
3. DHCP Request
4. DHCP Acknowledgement (ACK)

This process eliminates the need for manually assigning IP addresses to every device.

---

## Practical Learning Experience

One thing I enjoyed about this room was the interactive topology lab.

Instead of only reading theory, I was able to see how different network topologies fail under specific conditions. Breaking a ring topology by cutting a cable, overwhelming a bus topology with traffic, and taking down a star topology by disabling the switch helped me understand why network design decisions matter in real environments.

While I already had a basic understanding of networking concepts, this room helped me connect those concepts together and understand how they interact inside a real network.

Subnetting was also easier to understand after viewing it as a method of separating departments and network resources rather than just memorizing IP ranges and subnet masks.

Another useful lesson was understanding the difference between:

* IP Address = Logical Identifier
* MAC Address = Physical Identifier

This distinction made ARP much easier to understand.

---

## Challenges Faced

During this room, I found that:

* Remembering the responsibilities of routers and switches could be confusing initially.
* Network Address, Host Address, and Default Gateway concepts required careful attention.
* ARP communication flow needed multiple readings before it became intuitive.
* DHCP packet sequence was easy to mix up at first.

After reviewing the examples and practical demonstrations, these concepts became much clearer.

---

## Key Takeaways

* Star topology is the most common topology in modern networks.
* Switches improve efficiency by sending traffic only where needed.
* Routers enable communication between different networks.
* Subnetting improves organization, security, and scalability.
* ARP connects IP addresses with MAC addresses.
* DHCP automates IP address assignment.
* Understanding networking fundamentals is essential before moving into more advanced cybersecurity topics.

---

## Why This Room Matters

Many cybersecurity concepts build directly upon networking fundamentals.

Whether performing network analysis, packet inspection, vulnerability assessments, incident response, or penetration testing, understanding how devices communicate is critical.

This room provides a strong foundation for future learning and serves as an excellent starting point for beginners entering cybersecurity.

---

## Room Status

* Room: Intro to LAN
* Platform: TryHackMe
* Difficulty: Beginner
* Category: Networking Fundamentals

---

These concepts build directly upon the knowledge gained from Intro to LAN.
