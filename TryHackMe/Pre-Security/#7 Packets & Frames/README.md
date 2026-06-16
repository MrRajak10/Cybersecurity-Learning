# Packets & Frames

## TryHackMe Room Overview

This repository contains my notes, learning outcomes, and key takeaways from the **Packets & Frames** room on TryHackMe.

The room introduces fundamental networking concepts that explain how data travels across networks, how devices communicate with each other, and the roles played by protocols such as TCP and UDP. It also provides practical exposure to ports and network communication.

Rather than focusing only on answers, this repository documents what I learned, the concepts I reinforced, and the observations I made while working through the room.

---

## Learning Objectives

By completing this room, I learned how to:

* Understand the difference between packets and frames.
* Explain the concept of encapsulation and decapsulation.
* Identify important packet headers and their purpose.
* Understand how TCP establishes reliable communication.
* Explain the TCP Three-Way Handshake process.
* Understand how TCP connections are closed.
* Compare TCP and UDP communication methods.
* Recognize common network ports and associated services.
* Perform basic network communication using a practical port-based challenge.

---

## Room Topics Covered

### 1. Packets and Frames

One of the first concepts introduced in this room was the difference between packets and frames.

A packet operates at the Network Layer and contains information such as:

* Source IP Address
* Destination IP Address
* Time To Live (TTL)
* Checksum
* Payload Data

A frame operates at the Data Link Layer and encapsulates packets while adding information required for local network delivery.

### Key Concept: Encapsulation

As data moves through networking layers, additional information is added to it. This process is called encapsulation.

I found the envelope analogy particularly helpful:

* The packet is like a letter.
* The frame is like the envelope carrying the letter.
* The receiver removes the envelope before reading the letter.

This made it much easier to visualize how networking layers interact with one another.

---

## Important Packet Headers

| Header              | Purpose                                   |
| ------------------- | ----------------------------------------- |
| Time To Live (TTL)  | Prevents packets from circulating forever |
| Checksum            | Verifies data integrity                   |
| Source Address      | Indicates where data originated           |
| Destination Address | Indicates where data should be delivered  |

### Personal Observation

Before this room, I knew packets contained data, but I did not fully appreciate how much information exists inside packet headers. Learning about TTL and checksums helped me understand how networks prevent endless routing loops and detect corrupted data.

---

## 2. TCP/IP and the Three-Way Handshake

The room then explored TCP/IP and reliable communication.

TCP is a connection-oriented protocol, meaning both devices must establish a connection before exchanging data.

### TCP/IP Layers

* Application Layer
* Transport Layer
* Internet Layer
* Network Interface Layer

---

## TCP Packet Components

Important TCP headers include:

* Source Port
* Destination Port
* Source IP
* Destination IP
* Sequence Number
* Acknowledgement Number
* Checksum
* Data
* Flags

These fields allow TCP to provide reliable and ordered communication.

---

## The Three-Way Handshake

TCP establishes communication using three steps:

### Step 1: SYN

The client requests a connection.

### Step 2: SYN/ACK

The server acknowledges the request and responds.

### Step 3: ACK

The client confirms receipt and communication begins.

```text
Client  ---> SYN ----> Server
Client <--- SYN/ACK -- Server
Client ---> ACK ----> Server
```

### Personal Observation

This was one of the most valuable parts of the room for me.

I had previously heard the term "Three-Way Handshake" many times in networking and cybersecurity discussions, but this room finally helped me understand what actually happens during the process.

Visualizing the handshake as a conversation between two devices made the concept much easier to remember.

---

## Sequence Numbers and Acknowledgements

TCP uses sequence numbers to keep data organized.

Example:

```text
Packet 1 -> Sequence Number 0
Packet 2 -> Sequence Number 1
Packet 3 -> Sequence Number 2
```

Acknowledgement numbers confirm successful delivery.

This mechanism helps TCP:

* Maintain packet order
* Detect missing packets
* Ensure reliable transmission

---

## TCP Connection Termination

TCP closes connections using FIN and ACK packets.

Typical process:

```text
FIN
ACK
FIN
ACK
```

This ensures both devices properly release resources.

### What I Learned

Before this room, I mainly focused on how connections start. Learning how TCP connections close gave me a more complete understanding of the protocol lifecycle.

---

## 3. UDP/IP

Unlike TCP, UDP is connectionless.

UDP does not:

* Establish connections
* Use acknowledgements
* Guarantee delivery
* Verify packet ordering

Because of this, UDP is significantly faster.

---

## TCP vs UDP

| TCP                   | UDP                   |
| --------------------- | --------------------- |
| Reliable              | Faster                |
| Connection-Oriented   | Connectionless        |
| Uses Acknowledgements | No Acknowledgements   |
| Ordered Delivery      | No Ordering Guarantee |
| Higher Overhead       | Lower Overhead        |

---

## Common UDP Use Cases

* Video Streaming
* Voice Calls
* Online Gaming
* Real-Time Communication

### Personal Observation

The TCP vs UDP comparison helped me understand why different applications choose different protocols.

Initially, I assumed reliability was always better. After studying UDP, I realized that speed is often more important than perfect delivery, especially for real-time services such as voice and video communication.

---

## 4. Ports 101

Ports act as communication endpoints for network services.

Port numbers range from:

```text
0 - 65535
```

Applications use specific ports to exchange data.

---

## Common Ports

| Protocol | Port |
| -------- | ---- |
| FTP      | 21   |
| SSH      | 22   |
| HTTP     | 80   |
| HTTPS    | 443  |
| SMB      | 445  |
| RDP      | 3389 |

### Personal Observation

Memorizing ports can initially feel overwhelming. However, seeing these ports repeatedly across networking and cybersecurity rooms is helping me become more familiar with them naturally.

SSH (22), HTTP (80), HTTPS (443), and SMB (445) are ports that I expect to encounter frequently during future rooms and practical assessments.

---

## Practical Challenge

The room included a simple practical exercise where I connected to:

```text
IP Address: 8.8.8.8
Port: 1234
```

Successfully connecting returned the room flag.

### What I Learned

Although the challenge itself was straightforward, it reinforced an important networking principle:

Communication requires both:

* A destination IP address
* A destination port

Understanding this relationship helped connect the theoretical networking concepts to a practical example.

---

## Key Takeaways

* Packets and frames operate at different OSI layers.
* Encapsulation allows data to move through networking layers.
* TCP provides reliable communication through the Three-Way Handshake.
* Sequence and acknowledgement numbers keep data organized.
* TCP and UDP serve different purposes depending on reliability and speed requirements.
* Ports act as gateways for network services and applications.
* Common ports are important knowledge for networking and cybersecurity professionals.

---

## Final Thoughts

This room strengthened my understanding of how data travels across networks and how devices establish communication.

The biggest takeaway for me was understanding the logic behind TCP communication rather than simply memorizing the SYN → SYN/ACK → ACK sequence. Learning how packets, frames, ports, and protocols work together helped build a stronger networking foundation that will be useful throughout future cybersecurity learning paths.

Networking concepts can initially feel abstract, but this room breaks them into manageable pieces and provides practical examples that make them much easier to understand.
