# TryHackMe — Networking Secure Protocols

> A beginner-friendly learning repository documenting my journey through the **Networking Secure Protocols** room on TryHackMe. This repository focuses on understanding **why secure protocols exist, how they work, and where they are used** rather than simply completing the room.

---

## About This Room

Modern networks rely on many protocols to exchange data between systems. Earlier protocols were designed without strong security, which meant attackers could capture network traffic and read sensitive information such as usernames, passwords, emails, and other confidential data.

This room introduces the secure versions of common protocols and explains how technologies such as **TLS, HTTPS, SSH, SFTP, FTPS, and VPNs** protect communication over untrusted networks.

---

# Learning Objectives

After completing this room, I was able to understand:

* Why plain-text protocols are insecure
* The importance of Confidentiality, Integrity, and Authenticity (CIA)
* How TLS protects network communication
* The difference between SSL and TLS
* How HTTPS works internally
* Why digital certificates are required
* What Certificate Authorities (CA) do
* Why self-signed certificates generate browser warnings
* Why SSH replaced Telnet
* Secure email protocols
* Secure file transfer protocols
* How VPN creates encrypted communication across public networks
* Basic TLS traffic analysis using Wireshark

---

# Topics Covered

* TLS (Transport Layer Security)
* SSL vs TLS
* Digital Certificates
* Certificate Authority (CA)
* Self-Signed Certificates
* HTTPS
* Secure Email Protocols
* SSH
* SFTP
* FTPS
* VPN
* TLS Decryption using Wireshark

---

# Key Concepts Learned

## Why Plain Text Protocols Are Dangerous

Protocols such as:

* HTTP
* Telnet
* SMTP
* POP3
* IMAP

send data in plain text.

Anyone monitoring the network may be able to read:

* Usernames
* Passwords
* Emails
* Messages
* Sensitive information

---

## The Three Security Goals

### Confidentiality

Only authorized users should be able to read the data.

---

### Integrity

Data should not be modified during transmission.

---

### Authenticity

Users should be able to verify that they are communicating with the genuine server instead of an attacker.

---

## TLS (Transport Layer Security)

TLS adds encryption to existing application protocols.

Its primary goals are:

* Confidentiality
* Integrity
* Authenticity

TLS is the modern replacement for SSL.

Current modern implementations generally use **TLS 1.3**.

---

## Secure Versions of Common Protocols

| Insecure Protocol | Secure Version |
| ----------------- | -------------- |
| HTTP              | HTTPS          |
| SMTP              | SMTPS          |
| POP3              | POP3S          |
| IMAP              | IMAPS          |
| Telnet            | SSH            |

---

## Digital Certificates

A digital certificate works like an online identity card.

It contains information such as:

* Domain name
* Public key
* Expiration date
* Certificate issuer
* Certificate Authority

Digital certificates help browsers verify that the website is genuine.

---

## Certificate Authority (CA)

A Certificate Authority verifies website ownership before issuing a certificate.

Browsers trust certificates signed by trusted Certificate Authorities.

Examples include:

* Google Trust Services
* Let's Encrypt

---

## Self-Signed Certificates

A self-signed certificate is created by the website owner without a trusted Certificate Authority.

Browsers usually display warnings because the server's identity cannot be independently verified.

---

## HTTPS

HTTPS combines:

HTTP + TLS

Before encrypted communication begins:

1. TCP Three-Way Handshake
2. TLS Negotiation
3. Encrypted Data Transfer

Unlike HTTP, HTTPS traffic cannot be easily read inside packet captures without the required decryption keys.

---

## Secure Email Protocols

| Protocol | Default Port |
| -------- | -----------: |
| SMTP     |           25 |
| SMTPS    |    465 / 587 |
| POP3     |          110 |
| POP3S    |          995 |
| IMAP     |          143 |
| IMAPS    |          993 |

---

## SSH

SSH securely replaces Telnet.

Benefits include:

* Encrypted communication
* Secure authentication
* Data integrity
* Remote administration

Default Port:

22

---

## SFTP vs FTPS

### SFTP

* Uses SSH
* Port 22
* Simpler deployment
* Commonly used

### FTPS

* Uses TLS
* Uses certificates
* Commonly uses Port 990

---

## VPN

VPN creates an encrypted tunnel over the Internet.

Benefits:

* Protects communication
* Hides traffic from attackers
* Enables secure remote access
* Allows remote offices to access internal company resources

---

# Wireshark Learning

This room introduced:

* Viewing TLS traffic
* HTTP vs HTTPS packet comparison
* TLS negotiation packets
* TLS decryption using session keys
* Identifying login credentials after importing TLS key logs

---

# Practical Skills Developed

* Understanding encrypted communication
* Reading TLS packet captures
* Recognizing insecure protocols
* Identifying secure protocol alternatives
* Understanding browser certificates
* Basic packet analysis
* VPN architecture basics

---

# Key Takeaways

* Encryption protects sensitive information.
* TLS is responsible for securing many Internet protocols.
* HTTPS is HTTP running over TLS.
* SSH replaces Telnet because Telnet sends data in plain text.
* Certificate Authorities verify website identities.
* VPN protects communication over public networks.
* Wireshark can decrypt TLS traffic only when the appropriate session keys are available.

---

# Room Summary

This room provides an excellent introduction to secure network communication. Instead of focusing only on protocol names and port numbers, it explains why encryption is necessary and how modern Internet communication remains secure. Understanding these concepts builds a strong foundation for networking, penetration testing, SOC analysis, and packet analysis.
