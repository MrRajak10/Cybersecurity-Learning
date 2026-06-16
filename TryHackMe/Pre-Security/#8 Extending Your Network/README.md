# Extending Your Network

## Overview

This repository documents my learning journey through the **Extending Your Network** room on TryHackMe. The room introduces several fundamental networking concepts that explain how networks communicate beyond local environments and securely connect to external networks.

Throughout this room, I learned how technologies such as port forwarding, firewalls, VPNs, routers, switches, and VLANs work together to enable secure and efficient communication across networks. Rather than focusing only on answering room questions, I used this room as an opportunity to strengthen my understanding of how modern networks operate in real-world environments.

---

## Learning Objectives

By completing this room, I learned:

* The purpose and functionality of port forwarding
* How firewalls control incoming and outgoing network traffic
* The differences between stateful and stateless firewalls
* How VPNs create secure communication tunnels
* Common VPN technologies and their characteristics
* The role of routers in network communication
* The differences between Layer 2 and Layer 3 switches
* How VLANs improve network segmentation and security
* Basic packet flow and TCP handshake behavior

---

## Topics Covered

### Port Forwarding

Port forwarding allows services hosted inside a private network to become accessible from external networks through a public IP address.

Key concepts learned:

* Internal services are normally only accessible within the local network.
* Port forwarding maps traffic arriving on a public IP and specific port to a private internal device.
* Routers are responsible for configuring port forwarding rules.
* Port forwarding and firewalls serve different purposes:

  * Port forwarding directs traffic.
  * Firewalls decide whether traffic should be allowed or blocked.

#### Personal Learning Reflection

One concept I initially mixed up was the difference between port forwarding and firewalls. Both seemed related to controlling network access, but this room helped me understand that port forwarding simply creates a path to an internal service, while the firewall determines whether traffic is permitted to use that path.

---

### Firewalls

Firewalls act as security checkpoints that inspect network traffic and determine whether it should be allowed or denied.

A firewall can make decisions based on:

* Source IP address
* Destination IP address
* Port number
* Network protocol

#### Stateful Firewalls

Stateful firewalls analyze entire connections rather than individual packets.

Characteristics:

* Track connection history
* Make dynamic decisions
* More resource intensive
* Can block entire malicious connections

#### Stateless Firewalls

Stateless firewalls evaluate packets individually against predefined rules.

Characteristics:

* Faster and less resource intensive
* Rule-based filtering
* Effective for handling large volumes of traffic
* Less context-aware than stateful firewalls

#### Practical Firewall Exercise

The firewall simulator demonstrated how firewall rules are created using:

* Source address
* Destination address
* Port
* Action (Allow or Deny)

#### Personal Learning Reflection

The firewall exercise helped me understand how security rules are actually implemented. Instead of viewing a firewall as a mysterious security device, I began seeing it as a collection of logical rules that inspect traffic and decide what should happen next.

---

### VPN Basics

A Virtual Private Network (VPN) creates a secure tunnel across the Internet that allows devices on separate networks to communicate privately.

Benefits of VPNs include:

* Connecting remote locations
* Protecting data through encryption
* Improving privacy
* Supporting secure remote access

TryHackMe uses VPN technology to securely connect learners to vulnerable machines without exposing them directly to the Internet.

#### VPN Technologies

##### PPP (Point-to-Point Protocol)

* Provides authentication
* Provides encryption support
* Uses certificates and keys
* Non-routable by itself

##### PPTP (Point-to-Point Tunneling Protocol)

* Allows PPP traffic to travel across networks
* Easy to configure
* Widely supported
* Weaker encryption compared to modern alternatives

##### IPSec

* Encrypts traffic using the IP framework
* Strong security
* Industry-standard technology
* More complex to configure

#### Personal Learning Reflection

Before this room, I mostly associated VPNs with privacy and hiding IP addresses. This room helped me understand their broader role in enterprise networking, particularly how organizations securely connect offices and remote users through encrypted tunnels.

---

### Routers

Routers connect multiple networks and determine the best path for data to travel between them.

Key responsibilities:

* Route packets between networks
* Determine optimal communication paths
* Support features such as:

  * Port forwarding
  * Firewall configuration
  * Network management

Routers operate primarily at Layer 3 of the OSI model.

Routing decisions can be influenced by:

* Distance
* Reliability
* Link speed
* Network conditions

#### Personal Learning Reflection

The routing examples reinforced the idea that networking is not simply about sending data from one point to another. Routers actively make decisions about which path provides the most efficient and reliable route for packet delivery.

---

### Switches

Switches connect devices within a network and facilitate communication between them.

#### Layer 2 Switches

Layer 2 switches:

* Operate using MAC addresses
* Forward Ethernet frames
* Connect devices within the same network segment

#### Layer 3 Switches

Layer 3 switches:

* Forward frames like Layer 2 switches
* Perform routing functions
* Use IP addresses for packet forwarding

#### VLANs (Virtual Local Area Networks)

VLANs logically separate devices into different network segments.

Benefits include:

* Improved security
* Better traffic management
* Departmental isolation
* Reduced broadcast traffic

Example:

* Sales Department VLAN
* Accounting Department VLAN

Both can access the Internet while remaining isolated from each other.

#### Personal Learning Reflection

The VLAN concept was particularly interesting because it demonstrated how organizations can separate departments without requiring completely separate physical networks. This showed me how security and organization can be achieved through logical network design.

---

### Network Simulator Exercise

The final practical task visualized packet movement between devices across a network.

Concepts reinforced:

* Packet transmission
* TCP communication
* Network paths
* Connection establishment

The simulator also provided a visual representation of the TCP three-way handshake.

#### Personal Learning Reflection

Seeing the TCP handshake broken down step by step made the process much easier to understand than simply reading about SYN, SYN-ACK, and ACK packets in theory. Watching the packet flow helped connect networking concepts with real communication processes.

---

## Key Takeaways

* Port forwarding exposes internal services to external networks.
* Firewalls control traffic based on configurable security rules.
* Stateful and stateless firewalls use different inspection methods.
* VPNs provide secure communication across untrusted networks.
* Routers determine the best path for data transmission.
* Switches connect devices within networks using Layer 2 or Layer 3 functionality.
* VLANs improve network organization and security.
* TCP communication relies on a structured handshake process.

---

## Skills Developed

* Network fundamentals
* Firewall rule analysis
* VPN concepts
* Routing fundamentals
* Switching concepts
* VLAN understanding
* Packet flow analysis
* TCP communication basics

---

## Conclusion

The Extending Your Network room provided an excellent introduction to the technologies that allow modern networks to communicate securely and efficiently. Beyond learning definitions, the practical exercises helped reinforce how networking components interact in real environments.

One of the biggest lessons I took away from this room was that networking technologies rarely operate independently. Routers, firewalls, VPNs, switches, and VLANs all work together to create secure, scalable, and reliable communication systems. Understanding how these technologies interact has strengthened my networking foundation and prepared me for more advanced cybersecurity and networking topics.
