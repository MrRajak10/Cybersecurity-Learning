Welcome back! Moving from operating system fundamentals to **Networking Secure Protocols** is a massive leap forward. If the OS is the fortress, the network is the highway connecting all the fortresses. If you don't secure the highway, attackers will simply intercept your supplies (data) while they are in transit.

Your notes provide a fantastic outline. Let's expand on these concepts, break down the technical mechanics, and look at how attackers and defenders interact with these protocols in the real world.

---

## 1. Core Security Principles (The CIA Triad + Authenticity)

Before we talk about *how* to secure a network, we need to define *what* we are trying to achieve. Every secure protocol aims to protect three main properties, often referred to as the **CIA Triad** (Confidentiality, Integrity, Availability), alongside a crucial fourth property: **Authenticity**.

* **Confidentiality:** Ensuring that only authorized people can read the data.
* *Real-World Analogy:* Sending a letter in a sealed, opaque envelope instead of a transparent postcard.
* *How we achieve it:* **Encryption**. We scramble the data so that even if an attacker intercepts it, it looks like gibberish.


* **Integrity:** Ensuring the data has not been altered in transit.
* *Real-World Analogy:* A wax seal on a letter. If the seal is broken, you know someone tampered with the contents.
* *How we achieve it:* **Hashing**. If an attacker flips even a single bit of a file during download, the hash changes, and your computer drops the file.


* **Authenticity:** Verifying the identity of the person or server you are communicating with.
* *Real-World Analogy:* Checking a person's driver's license before letting them withdraw money from a bank.
* *How we achieve it:* **Digital Certificates**. You want to be sure you are actually sending your password to `google.com` and not a fake server set up by an attacker.



> **Security Perspective:** Penetration testers constantly look for breaks in these pillars. If a website lacks confidentiality, they steal passwords. If it lacks integrity, they inject malicious code into file downloads.

---

## 2. The Evolution of Secure Transport: SSL vs. TLS

### What are they?

**SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are cryptographic protocols designed to provide secure communication over a computer network.

### Why do they exist?

Early network protocols were designed for academic and military networks where everyone trusted each other. When the public internet exploded, e-commerce became impossible because anyone could steal a credit card number in transit. SSL was created in the 1990s to encrypt that web traffic.

### SSL vs. TLS: What is the difference?

* **SSL** is the older, original protocol. Over time, security researchers found massive flaws in it (like the famous POODLE vulnerability). SSL versions 1.0, 2.0, and 3.0 are entirely deprecated and considered highly insecure today.
* **TLS** is the direct successor to SSL. It is a completely rewritten, heavily fortified version. When you see a padlock in your browser, you are using TLS (specifically TLS 1.2 or TLS 1.3), not SSL.

> **Common Beginner Mistake:** People still use the term "SSL Certificate" or say "We need to set up SSL" out of habit. In reality, modern networks use TLS. If a SOC analyst sees actual SSLv3 traffic on a modern network, it triggers an immediate high-priority alert.

---

## 3. Web Traffic: HTTP vs. HTTPS

### HTTP (Hypertext Transfer Protocol)

HTTP is the foundation of data communication for the World Wide Web. However, it transmits everything in **plain text**. If you log into an HTTP website on public Wi-Fi, anyone running a packet sniffer can literally read your username and password as they float through the air.

### HTTPS (HTTP Secure)

HTTPS is simply HTTP wrapped inside a secure TLS tunnel.

### How the HTTPS Connection Works (The Handshake)

Before your browser can send a password securely, it has to agree on a secret code with the server. This negotiation happens in milliseconds.

1. **TCP Three-Way Handshake:** Establishing the connection.
Before any encryption happens, your computer and the server must establish a basic network connection using a SYN, SYN-ACK, ACK sequence.


2. **Client Hello & Server Hello:** Negotiating the rules.
Your browser sends a "Client Hello" message detailing which TLS versions and encryption algorithms it supports. The server replies with a "Server Hello," selecting the strongest algorithm they both understand.


3. **Certificate Exchange:** Proving identity.
The server sends its Digital Certificate to your browser to prove it is the legitimate website.


4. **Key Generation:** Creating the lock and key.
Using complex mathematics (like Diffie-Hellman), the client and server securely generate a shared **Session Key**. This is a temporary, one-time-use password for this specific visit.


5. **Encrypted Communication:** The secure tunnel is open.
Both sides now use the Session Key to encrypt and decrypt all HTTP traffic. The TLS Handshake is complete.


---

## 4. Trusting the Internet: Digital Certificates & CAs

When you connect to a bank, how does your browser *know* it is actually the bank? Through Digital Certificates.

### What is a Digital Certificate?

Think of it as an electronic passport for a website. It contains:

* The **Domain Name** (e.g., [www.tryhackme.com](https://www.google.com/search?q=https%3A%2F%2Fwww.tryhackme.com))
* The server's **Public Key** (used for encryption)
* The **Expiration Date**
* The **Digital Signature** of the organization that issued it.

### Certificate Authorities (CA)

A CA is a trusted third-party organization (like Let's Encrypt, DigiCert, or Google Trust Services). They act like the passport agency. Before they issue a certificate to a website, they verify that the person requesting it actually owns the domain.

Your operating system and browser come pre-loaded with a list of CAs they trust unconditionally.

### Self-Signed Certificates

Anyone can generate a digital certificate for free on their own computer—this is called a **Self-Signed Certificate**.

* **The Problem:** Because no trusted third-party (CA) verified it, your browser has no idea if you are the real owner or an attacker intercepting traffic.
* **The Result:** Your browser throws a massive, scary warning: "Your connection is not private."
* **Red Team Context:** Attackers often use self-signed certificates on their malicious infrastructure (Command and Control servers). Defenders look for self-signed certificates as a strong indicator of compromise.

---

## 5. Secure Protocol Upgrades and Ports

As the internet matured, engineers realized *every* protocol needed a secure version. We took old, plain-text protocols and wrapped them in TLS/SSL to make them secure.

| Purpose | Insecure Protocol (Plain Text) | Port | Secure Protocol (Encrypted) | Port |
| --- | --- | --- | --- | --- |
| **Web Browsing** | HTTP | 80 | HTTPS | 443 |
| **Sending Email** | SMTP | 25 | SMTPS | 465 / 587 |
| **Receiving Email** | POP3 | 110 | POP3S | 995 |
| **Receiving Email** | IMAP | 143 | IMAPS | 993 |
| **Remote Shell** | Telnet | 23 | SSH | 22 |
| **File Transfer** | FTP | 21 | SFTP / FTPS | 22 / 990 |

> **CTF/TryHackMe Tip:** Memorizing these ports is mandatory. When you run an `nmap` scan and see port 21 open, you immediately know FTP is running, and you can likely capture credentials if you intercept the traffic. If you see port 22 open, you know it is SSH, which is heavily encrypted and requires finding a key or guessing a strong password.

---

## 6. Remote Administration: SSH, SFTP, and FTPS

### SSH (Secure Shell)

**What it is:** A cryptographic network protocol for operating network services securely over an unsecured network.
**Why it exists:** It was designed specifically to replace **Telnet**, an ancient protocol that transmitted all commands—including administrator passwords—in plain text.
**How to use it:** `ssh username@hostname_or_ip`

* *Security Context:* SSH is the backbone of remote server management. It uses strong encryption and supports authentication via cryptographic keys (SSH Keys) instead of passwords, making it highly resistant to brute-force attacks.

### SFTP vs. FTPS

These sound similar, but they are entirely different technologies under the hood.

* **SFTP (SSH File Transfer Protocol):** This is literally just a file transfer subsystem built *inside* SSH. It runs over Port 22. It is incredibly secure and easy to configure because if you have SSH running, you already have SFTP.
* **FTPS (FTP over SSL/TLS):** This is the old FTP protocol wrapped in a TLS tunnel. It uses Port 990. It is much harder to configure through firewalls because FTP inherently uses multiple ports to transfer data.

---

## 7. Virtual Private Networks (VPN)

### What it is

A VPN creates a secure, encrypted tunnel from your device, across the public internet, into a private network.

### Why it exists

Imagine you are working from a coffee shop, but you need to access a confidential HR server located inside your company's headquarters. That server does not have a public IP address—it is completely hidden from the internet.

When you connect to the corporate VPN, your laptop acts as if a very long, invisible Ethernet cable was plugged directly from your coffee shop table straight into the switch at the corporate office.

### Security Context

TryHackMe uses OpenVPN to assign your virtual machine an IP address on *their* internal lab network. Without the VPN, you could never reach the target machines, because those IP addresses (like `10.10.x.x`) are not routable on the public internet.

---

## 8. Analyzing Traffic: The Wireshark Perspective

Wireshark is a packet analyzer. It captures every single 1 and 0 moving across your network card.

* **HTTP in Wireshark:** If you capture HTTP traffic, you can right-click the packet, select "Follow TCP Stream," and read the exact HTML of the webpage, along with the user's plain-text passwords.
* **HTTPS in Wireshark:** You will see the TLS Handshake (Client Hello, Server Hello). But after that, the payload is just marked as "Application Data." If you "Follow TCP Stream," it looks like complete garbage text.
* **Decrypting in Wireshark:** As a defender (or an attacker who has compromised a machine), if you can dump the **Session Keys** from the computer's memory and load them into Wireshark, Wireshark will use those keys to strip away the TLS encryption, revealing the plain-text HTTP underneath!

---
