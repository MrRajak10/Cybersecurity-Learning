Welsome back! It is fantastic to see you moving into network analysis. Mastering Wireshark is a major milestone in your cybersecurity journey.

If operating systems are the buildings of the digital world, networks are the highways connecting them. Wireshark is like a traffic camera that lets you pause time, open up every single delivery truck on that highway, and inspect exactly what is inside.

As you rightly noted, Wireshark is just a tool — it doesn't solve crimes; the analyst does. Let's break down your notes, define the core terminology, and structure this so you understand *how* to investigate, rather than just clicking buttons.

---

## 1. What is Wireshark (and what is a PCAP)?

### Terminology Check

* **PCAP / PCAPNG:** Stands for **Packet Capture**. When data travels across a network, it is broken down into tiny chunks called "packets." A PCAP file is simply a saved recording of those packets. PCAPNG is just the "Next Generation" version of this file format, which includes extra metadata (like which network interface captured the traffic).
* **SOC (Security Operations Center):** A centralized team of defenders who monitor an organization's network for cyber threats 24/7.
* **Incident Response (IR):** The process of investigating and containing a cyberattack *after* a breach has occurred.
* **Digital Forensics:** The science of recovering and investigating material found in digital devices (like dusting for digital fingerprints).
* **Penetration Testing:** Authorized, simulated cyberattacks against a system to find vulnerabilities before real hackers do.

### The Problem It Solves

Computers communicate incredibly fast. If you are a SOC analyst and an alert says, "Suspicious traffic detected from 192.168.1.10," you cannot just guess what happened. You need undeniable proof. Wireshark solves this by letting you look at the raw, unfiltered data that was actually sent over the wire.

> **Common Beginner Mistake:** As your notes pointed out, a huge trap is assuming Wireshark is an **IDS (Intrusion Detection System)**. An IDS (like Snort or Suricata) automatically yells, "Hey, this looks like malware!" Wireshark is silent. It just shows you the data. You have to be the detective.

---

## 2. The Main Interface: Slicing the Packet

Wireshark's interface is divided into three critical panels. Understanding how they work together is the secret to fast investigations.

<img width="367" height="272" alt="image" src="https://github.com/user-attachments/assets/f7d7350d-fafd-4d14-8835-e1a237505294" />


### Panel 1: The Packet List (The Logbook)

This is the top window. It shows a summary of every single packet in chronological order. You use this to spot broad trends — like seeing a massive flood of red lines (which might indicate network errors or a port scan).

### Panel 2: The Packet Details (The Dissection)

This is the middle window, and it is where you will spend 90% of your time. Wireshark expands the packet into layers, matching the **OSI Model** (a conceptual framework that describes how networks operate).

Think of a network packet like a nesting doll or an envelope inside another envelope.

<img width="439" height="227" alt="image" src="https://github.com/user-attachments/assets/4a6eee79-8f3d-49dd-8e5b-7b2df09c5ab6" />


Here is how to read those layers:

1. **Frame / Physical (Layer 1):** The raw bits and bytes on the wire. Usually just tells you how big the packet is.
2. **Ethernet / Data Link (Layer 2):** Shows **MAC Addresses**. A MAC address is a permanent, physical serial number stamped onto a computer's network card. It is used to deliver data on the *local* network (like your house or office building).
3. **IP / Network (Layer 3):** Shows **Source and Destination IP Addresses**. An IP address is like a street address used to route the packet across the internet. It also contains the **TTL (Time to Live)**, which is a self-destruct counter. Every time a packet passes through a router, the TTL drops by 1. If it hits 0, the packet is destroyed (so lost data doesn't bounce around the internet forever).
4. **TCP/UDP / Transport (Layer 4):** Shows **Ports**. If an IP address is a building, the Port is the specific apartment number.
* **TCP (Transmission Control Protocol):** Reliable data delivery (like a registered letter where the receiver has to sign for it). Used for web browsing (Port 80/443).
* **UDP (User Datagram Protocol):** Fast, unreliable delivery (like throwing a newspaper on a porch and driving away). Used for video streaming or DNS (Port 53).


5. **Application (Layer 7):** The actual software protocol being used (e.g., HTTP for web pages, DNS for looking up website names).
6. **Application Data / Payload:** The actual "thing" being sent — the text of an email, the code of a picture, or the malicious command from a hacker.

### Panel 3: Packet Bytes (The Hex Dump)

The bottom window shows the raw hexadecimal and ASCII data.

* **Security Context:** Malware authors often try to hide their code in weird parts of a packet. Malware analysts look at this hex dump to find hidden strings of text or executable code that Wireshark's middle panel didn't decode properly.

---

## 3. The Power of Filtering

If you capture traffic on a busy network for 60 seconds, you will collect hundreds of thousands of packets. Without filters, finding a hacker in a PCAP is like finding a needle in a haystack of needles.

### Capture Filters (The Bouncer)

Applied **before** you start recording. If you set a capture filter for `port 80`, Wireshark will completely ignore everything else.

* **Why use it?** PCAP files can become massively large (Gigabytes). Capture filters save hard drive space.

### Display Filters (The Search Engine)

Applied **after** you have the PCAP file. It hides the noise so you only see what you want, but the hidden packets are still saved in the file if you need them later.

### Quick Protocol Definitions

You mentioned a few protocols to filter for. Here is what they are:

* **HTTP:** Hypertext Transfer Protocol. Used to send unencrypted websites.
* **DNS:** Domain Name System. The phonebook of the internet (translates `google.com` to `142.250.190.46`).
* **ICMP:** Internet Control Message Protocol. Used for network diagnostics (this is what the `ping` command uses).
* **ARP:** Address Resolution Protocol. Used by computers to ask, "Hey, who owns this IP address? Tell me your MAC address!" (Attackers often spoof this in ARP Poisoning attacks).

---

## 4. Reconstructing the Crime: Follow Stream

One of the most powerful features you noted is **Follow Stream**.

When you download a picture over the internet, it is too big to fit in one packet. It gets chopped up into 50 different packets, sent across the network, and glued back together by your computer.

<img width="428" height="233" alt="image" src="https://github.com/user-attachments/assets/7bd6a480-d1ed-4e2e-9a1b-b4ee6f7d7a71" />


If you just look at the Packet List, you only see the individual chunks. If you right-click one of those packets and select **Follow -> TCP Stream**, Wireshark automatically gathers all 50 packets, glues them together, and shows you the entire conversation in one window.

* **Red Text:** What the client (user) sent.
* **Blue Text:** What the server replied.
* **Security Context (SOC/Pentesting):** If a user logs into a website without encryption (HTTP instead of HTTPS), you can use Follow Stream to instantly read their username and password in plain text.

---

## 5. Exporting Objects and File Properties

### Exporting Objects

If an employee downloads a suspicious file, the file's data is trapped inside the PCAP's packets. You can go to `File -> Export Objects -> HTTP`, and Wireshark will magically rebuild the original `.exe`, `.pdf`, or `.zip` file and save it to your desktop.

* **Malware Analysis Use Case:** Analysts use this to safely extract the malware from the network traffic so they can toss it into a sandbox and dissect it.

### File Properties (SHA-256 Hash)

A **Hash** is a cryptographic digital fingerprint of a file. If you change even one pixel in an image, its hash changes completely.

* **Why it matters in IR:** In a legal forensic investigation, you must prove that the PCAP you are analyzing hasn't been tampered with. You calculate the SHA-256 hash of the PCAP on day one, and verify it matches on day ten in court.

---
