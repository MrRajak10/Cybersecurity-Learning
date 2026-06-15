# TryHackMe — OSI Model

## Overview

The OSI (Open Systems Interconnection) Model is one of the most important concepts in networking. It provides a standardized framework that explains how data travels between devices across a network. Understanding the OSI Model helps build a strong foundation for networking, cybersecurity, troubleshooting, and communication protocols.

This room introduces the seven layers of the OSI Model, explains the role of each layer, and demonstrates how data moves from one device to another through a process known as encapsulation.

---

## Learning Objectives

By completing this room, I learned:

* What the OSI Model is and why it exists.
* The purpose of each of the seven OSI layers.
* How data is encapsulated and transmitted across networks.
* The difference between physical and logical addressing.
* The roles of TCP and UDP in data transmission.
* How routing works at the Network Layer.
* Where encryption, sessions, and user applications fit into network communication.
* How the OSI Model can be used as a troubleshooting framework.

---

## Room Summary

The OSI Model consists of seven layers that work together to ensure successful communication between devices.

| Layer | Name         | Primary Responsibility                   |
| ----- | ------------ | ---------------------------------------- |
| 7     | Application  | User interaction and network services    |
| 6     | Presentation | Translation, formatting, encryption      |
| 5     | Session      | Establishing and maintaining connections |
| 4     | Transport    | Reliable or fast data transmission       |
| 3     | Network      | Routing and IP addressing                |
| 2     | Data Link    | MAC addressing and frame creation        |
| 1     | Physical     | Physical transmission of bits            |

Each layer performs specific tasks before passing data to the next layer.

---

## Key Concepts Learned

### Layer 1 — Physical

The Physical Layer is responsible for the actual transmission of data through hardware components.

Examples include:

* Ethernet cables
* Network connectors
* Electrical signals
* Fibre optic connections

At this layer, data is represented as binary values (1s and 0s).

**Key takeaway:** Without the Physical Layer, no data could physically travel between devices.

---

### Layer 2 — Data Link

The Data Link Layer handles physical addressing through MAC addresses.

Important concepts:

* MAC (Media Access Control) Address
* Network Interface Card (NIC)
* Frame creation
* Local network communication

Every network-enabled device contains a NIC with a unique MAC address used for identification on a local network.

**Key takeaway:** IP addresses identify devices logically, while MAC addresses identify them physically.

---

### Layer 3 — Network

The Network Layer is responsible for routing data between networks.

Important concepts:

* IP Addresses
* Routing
* Routers
* OSPF (Open Shortest Path First)
* RIP (Routing Information Protocol)

This layer determines the best path for packets to reach their destination.

Factors affecting routing:

* Shortest path
* Reliability
* Connection speed

**Key takeaway:** Routers operate at Layer 3 and use IP addresses to move data across networks.

---

### Layer 4 — Transport

The Transport Layer controls how data is delivered between devices.

Two major protocols operate here:

#### TCP (Transmission Control Protocol)

TCP focuses on reliability.

Features:

* Error checking
* Packet ordering
* Guaranteed delivery
* Connection-oriented communication

Common uses:

* Web browsing
* Email
* File transfers

#### UDP (User Datagram Protocol)

UDP focuses on speed.

Features:

* No delivery guarantees
* No packet ordering
* Faster transmission

Common uses:

* Video streaming
* Voice calls
* Real-time communication

**Key takeaway:** TCP prioritizes accuracy, while UDP prioritizes speed.

---

### Layer 5 — Session

The Session Layer establishes, maintains, and terminates communication sessions between devices.

Responsibilities:

* Session creation
* Session management
* Synchronization
* Checkpoint recovery

If a connection drops, checkpoints help avoid retransmitting all data again.

**Key takeaway:** Sessions allow devices to maintain organized communication channels.

---

### Layer 6 — Presentation

The Presentation Layer acts as a translator between applications.

Responsibilities:

* Data formatting
* Data translation
* Character encoding
* Encryption and decryption

Examples:

* HTTPS encryption
* File format conversions
* Data standardization

**Key takeaway:** Different applications can understand each other's data because of this layer.

---

### Layer 7 — Application

The Application Layer is the closest layer to the end user.

Examples:

* Web browsers
* Email clients
* File transfer applications
* DNS services

This layer provides the interface users interact with every day.

**Key takeaway:** Most users directly interact with Layer 7 applications without realizing the lower layers are working underneath.

---

## Practical Exercise

The room included the OSI Dungeon challenge.

The challenge required arranging the OSI layers in the correct order:

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

This exercise helped reinforce the layer order and improved recall of the OSI structure.

---

## My Learning Experience

Before starting this room, I had heard about the OSI Model many times, but it always felt like something people memorized rather than understood.

While working through the room, I realized that each layer solves a specific problem in network communication. Instead of trying to memorize all seven layers immediately, I focused on understanding the purpose of each layer and how they work together.

One concept that initially confused me was the difference between MAC addresses and IP addresses. After studying the Data Link and Network layers, it became much clearer that MAC addresses are used for physical identification on a local network, while IP addresses help devices communicate across networks.

Another important lesson came from understanding TCP and UDP. Previously, I only knew that TCP was "reliable" and UDP was "fast." This room helped me understand why those differences exist and where each protocol is useful in real-world situations.

The OSI Dungeon challenge was surprisingly helpful because it forced me to recall the layer order without looking at notes. By the end of the room, remembering the seven layers became much easier.

Overall, this room strengthened my networking fundamentals and provided a clearer understanding of how data travels across networks.

---

## Skills Developed

* Networking Fundamentals
* OSI Model Understanding
* TCP vs UDP Comparison
* Routing Concepts
* MAC and IP Addressing
* Network Troubleshooting Foundations
* Protocol Awareness

---

## Key Takeaways

* The OSI Model consists of seven layers.
* Each layer performs a specific networking function.
* Encapsulation occurs as data moves through the layers.
* TCP provides reliability and accuracy.
* UDP provides speed and efficiency.
* MAC addresses operate at Layer 2.
* IP addresses operate at Layer 3.
* Encryption occurs at Layer 6.
* User-facing applications operate at Layer 7.
* Understanding the OSI Model is essential for cybersecurity and networking careers.

---

## Conclusion

The OSI Model is a foundational networking framework that helps explain how devices communicate across networks. Although the seven layers may seem overwhelming at first, understanding the purpose of each layer makes the model much easier to learn and apply.

This room provided a strong introduction to networking concepts that will continue to appear throughout cybersecurity, penetration testing, system administration, and network troubleshooting. Building a solid understanding of the OSI Model is an important step toward becoming more effective in any cybersecurity role.
