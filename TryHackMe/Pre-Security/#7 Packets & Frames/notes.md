# Packets & Frames - Notes

## Room Summary

This room focuses on how data travels across networks using packets, frames, TCP, UDP, and ports. It helped me understand the journey data takes from one device to another and how networking protocols ensure communication happens correctly.

---

# Task 1: What Are Packets and Frames?

## Packet

A packet is a unit of data that operates at the **Network Layer (Layer 3)** of the OSI model.

Packets contain:

* Source IP Address
* Destination IP Address
* TTL (Time To Live)
* Checksum
* Payload Data

## Frame

A frame operates at the **Data Link Layer (Layer 2)**.

Frames encapsulate packets and add information required for local network communication such as MAC addresses.

## Encapsulation

Encapsulation is the process of adding information as data moves through networking layers.

Example:

```text
Data
 ↓
Packet
 ↓
Frame
```

The receiving device performs the reverse process called **Decapsulation**.

---

## Packet Headers

### Time To Live (TTL)

* Prevents packets from looping forever.
* Decreases at each router hop.
* Packet is discarded when TTL reaches 0.

### Checksum

* Used to verify data integrity.
* Detects packet corruption during transmission.

### Source Address

* Sender's IP address.

### Destination Address

* Receiver's IP address.

---

## My Learning Notes

Before this room, I thought packets were simply chunks of data. Learning about TTL, checksums, and addressing helped me understand that packets contain important routing and validation information in addition to the actual data.

The envelope analogy made encapsulation much easier to visualize.

---

# Task 2: TCP/IP and the Three-Way Handshake

## TCP/IP Layers

TCP/IP consists of four layers:

1. Application
2. Transport
3. Internet
4. Network Interface

Like the OSI model, data is encapsulated as it moves through these layers.

---

## What is TCP?

TCP (Transmission Control Protocol) is:

* Connection-oriented
* Reliable
* Ordered
* Error-checked

TCP guarantees delivery of data.

---

## Advantages of TCP

* Reliable communication
* Data integrity verification
* Ordered packet delivery
* Synchronization between devices

## Disadvantages of TCP

* Slower than UDP
* Requires more processing
* Uses more resources
* Can become a bottleneck on slow connections

---

## Important TCP Headers

### Source Port

Randomly selected sender port.

### Destination Port

Port of the receiving service.

Example:

```text
HTTP = Port 80
HTTPS = Port 443
SSH = Port 22
```

### Source IP

Sender address.

### Destination IP

Receiver address.

### Sequence Number

Used to track packet order.

### Acknowledgement Number

Confirms receipt of data.

### Checksum

Validates data integrity.

### Flags

Control packet behavior.

Examples:

```text
SYN
ACK
FIN
RST
```

---

# TCP Three-Way Handshake

TCP establishes communication through three steps:

## Step 1: SYN

Client requests connection.

```text
Client → SYN → Server
```

## Step 2: SYN/ACK

Server acknowledges request.

```text
Server → SYN/ACK → Client
```

## Step 3: ACK

Client confirms connection.

```text
Client → ACK → Server
```

Connection is now established.

---

## Why Sequence Numbers Matter

TCP assigns data a sequence number.

Example:

```text
Packet 1 = Sequence 0
Packet 2 = Sequence 1
Packet 3 = Sequence 2
```

This allows:

* Correct ordering
* Missing packet detection
* Reliable reconstruction

---

## My Learning Notes

The Three-Way Handshake was a concept I had heard many times but never fully understood.

Seeing the communication flow step-by-step helped me understand that the handshake is essentially two devices agreeing on how they will communicate before any actual data is transferred.

Instead of memorizing:

```text
SYN
SYN/ACK
ACK
```

I now understand the purpose behind each message.

---

# TCP Connection Termination

TCP closes connections using FIN and ACK packets.

Typical sequence:

```text
FIN
ACK
FIN
ACK
```

This ensures both devices have finished transmitting data before the connection is removed.

---

## My Learning Notes

Learning how TCP closes a connection gave me a more complete understanding of the protocol lifecycle.

Most explanations focus only on establishing connections, but understanding termination is equally important.

---

# Task 4: UDP/IP

## What is UDP?

UDP (User Datagram Protocol) is:

* Connectionless
* Stateless
* Faster than TCP
* Less reliable

UDP does not perform:

* Handshakes
* Acknowledgements
* Packet ordering
* Delivery guarantees

---

## UDP Headers

UDP uses fewer headers than TCP.

Common headers include:

### Time To Live (TTL)

Packet expiration timer.

### Source Address

Sender IP.

### Destination Address

Receiver IP.

### Source Port

Sender port.

### Destination Port

Receiver port.

### Data

Actual payload.

---

# TCP vs UDP

| TCP                 | UDP            |
| ------------------- | -------------- |
| Reliable            | Faster         |
| Connection-Oriented | Connectionless |
| Ordered Delivery    | No Ordering    |
| Uses ACKs           | No ACKs        |
| More Overhead       | Less Overhead  |

---

## Common UDP Use Cases

### Video Streaming

Minor packet loss is acceptable.

### Voice Calls

Real-time delivery is more important than perfect delivery.

### Online Gaming

Speed is prioritized.

---

## My Learning Notes

One important lesson from this room was realizing that reliability is not always the most important factor.

For activities like voice calls or streaming, receiving data quickly is often more valuable than ensuring every packet arrives perfectly.

This helped me understand why UDP exists despite lacking many of TCP's protections.

---

# Task 5: Ports 101

## What Are Ports?

Ports act as communication endpoints for services and applications.

Port Range:

```text
0 - 65535
```

---

# Common Ports

| Protocol | Port |
| -------- | ---- |
| FTP      | 21   |
| SSH      | 22   |
| HTTP     | 80   |
| HTTPS    | 443  |
| SMB      | 445  |
| RDP      | 3389 |

---

## Protocol Notes

### FTP (21)

File transfer service.

### SSH (22)

Secure remote terminal access.

### HTTP (80)

Website communication.

### HTTPS (443)

Encrypted website communication.

### SMB (445)

File and printer sharing.

### RDP (3389)

Remote desktop access.

---

## My Learning Notes

Port numbers initially seem overwhelming because there are so many of them.

However, I noticed that the same ports appear repeatedly throughout networking and cybersecurity content.

This room reinforced several important ports that I will likely encounter frequently during future labs and assessments.

---

# Practical Challenge

Connected to:

```text
IP Address: 8.8.8.8
Port: 1234
```

Successfully established communication and received the flag.

---

## What This Challenge Reinforced

To communicate with a service, two key pieces of information are required:

1. IP Address
2. Port Number

Without both values, a connection cannot reach the intended service.

---

# Key Takeaways

* Packets operate at Layer 3 and contain IP information.
* Frames operate at Layer 2 and encapsulate packets.
* Encapsulation adds networking information as data moves through layers.
* TCP uses the Three-Way Handshake to establish reliable communication.
* Sequence numbers and acknowledgements ensure packet ordering.
* FIN packets are used to gracefully close TCP connections.
* UDP sacrifices reliability for speed.
* Ports identify specific services running on devices.
* Common ports are foundational knowledge for cybersecurity.

---

# Concepts Worth Revisiting

* OSI Model
* TCP/IP Model
* Encapsulation vs Decapsulation
* TCP Flags
* Sequence and Acknowledgement Numbers
* Common Ports and Services
* TCP vs UDP Use Cases

---

# Final Reflection

This room strengthened my networking fundamentals and helped connect several concepts that previously felt separate. Understanding how packets, frames, protocols, and ports work together made network communication much easier to visualize. The biggest improvement for me was moving beyond memorization and understanding why TCP and UDP behave differently depending on the situation.
