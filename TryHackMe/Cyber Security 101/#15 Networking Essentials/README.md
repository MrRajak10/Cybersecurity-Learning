# Networking Essentials - TryHackMe

## Overview

**Networking Essentials** builds on fundamental networking concepts by introducing the core protocols that allow devices to communicate across a network. Instead of focusing only on theory, this room explains how devices automatically obtain network configurations, discover other devices, test connectivity, communicate across multiple networks, and access the Internet using a limited number of public IP addresses.

The room focuses on understanding how these protocols work together rather than simply memorizing definitions. By completing this room, learners gain a stronger understanding of what happens behind the scenes every time a device connects to a network.

---

## Learning Objectives

After completing this room, you should be able to:

* Understand the purpose of DHCP.
* Explain the DHCP DORA process.
* Understand how ARP maps IP addresses to MAC addresses.
* Explain why broadcast addresses are used.
* Understand how ICMP helps troubleshoot network connectivity.
* Use Ping and understand its purpose.
* Understand how Traceroute works using the TTL field.
* Understand the purpose of routing protocols.
* Explain why NAT is required.
* Understand the difference between private and public IP addresses.

---

## Topics Covered

### Dynamic Host Configuration Protocol (DHCP)

Learn how devices automatically receive:

* IP Address
* Default Gateway
* DNS Server

Understand the four DHCP stages:

* Discover
* Offer
* Request
* Acknowledge (DORA)

---

### Address Resolution Protocol (ARP)

Learn how computers discover the MAC address that belongs to an IP address.

Topics include:

* MAC addresses
* Broadcast MAC address
* ARP Requests
* ARP Replies
* ARP Cache

---

### Internet Control Message Protocol (ICMP)

Learn how ICMP assists with troubleshooting network communication.

Concepts covered include:

* Ping
* Echo Request
* Echo Reply
* Packet loss
* Round-trip time

---

### Traceroute

Understand how Traceroute uses the IP packet's Time To Live (TTL) value to identify each router between a source and destination.

Topics include:

* TTL
* Time Exceeded messages
* Network path discovery

---

### Routing

Introduction to how routers determine the best path for network traffic.

Routing protocols discussed:

* OSPF
* EIGRP
* BGP
* RIP

---

### Network Address Translation (NAT)

Understand why IPv4 addresses are limited and how NAT allows many private devices to share one public IP address.

Topics include:

* Private IP addresses
* Public IP addresses
* Port translation
* NAT tables

---

## Skills Developed

* Understanding packet flow
* Reading networking diagrams
* Understanding protocol responsibilities
* Identifying network communication stages
* Understanding how hosts communicate inside and outside a network
* Building stronger networking fundamentals for cybersecurity

---

## Key Takeaways

* DHCP automatically configures devices on a network.
* ARP connects IP addresses with MAC addresses.
* ICMP helps verify connectivity and diagnose network issues.
* Traceroute reveals the path packets take across routers.
* Routing protocols determine efficient paths across networks.
* NAT conserves public IPv4 addresses by translating private addresses.

---

## Beginner Practice

After completing this room, try the following exercises:

1. Run `ipconfig` (Windows) or `ip addr` (Linux) to identify your IP configuration.
2. Use `ping` to test connectivity to another host.
3. Run `tracert` (Windows) or `traceroute` (Linux) to observe packet paths.
4. Display your ARP cache using:

   * Windows: `arp -a`
   * Linux: `ip neigh`
5. Identify whether your device is using a private or public IP address.

---

## Real-World Importance

The protocols covered in this room appear constantly throughout cybersecurity.

SOC analysts investigate packet captures containing DHCP, ARP, and ICMP traffic.

Penetration testers verify connectivity using Ping, identify network paths with Traceroute, and analyze ARP behavior during internal assessments.

Network administrators troubleshoot connectivity problems using these same protocols every day.

Understanding these protocols forms an essential foundation before learning packet analysis, Wireshark, Active Directory, network attacks, and defensive monitoring.

---

## Room Summary

Networking Essentials explains how computers communicate on modern networks by introducing the core protocols responsible for automatic configuration, address resolution, connectivity testing, routing, and Internet access. Rather than treating these protocols as isolated concepts, the room demonstrates how they work together whenever a device joins a network and communicates with other systems.

Strong knowledge of these networking fundamentals makes future cybersecurity topics significantly easier to understand.
