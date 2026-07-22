# README.md

# TryHackMe — Networking Core Protocols

A learning-focused repository documenting my journey through the **Networking Core Protocols** room on TryHackMe. This repository is designed for beginners who want to understand how common network protocols work, why they exist, and how they are used in both everyday networking and cybersecurity.

> **Note:** This repository focuses on learning, understanding, and practical experimentation. It is **not** intended to be a complete walkthrough or flag solution.

---

## Room Overview

Modern computer networks rely on many different protocols, with each protocol designed to solve a specific problem. During this room, I learned how computers:

* Resolve domain names into IP addresses
* Discover domain registration information
* Communicate with websites
* Transfer files
* Send emails
* Receive emails
* Synchronize email across multiple devices

Understanding these protocols is an essential foundation for anyone interested in:

* Cybersecurity
* Penetration Testing
* SOC Analysis
* Digital Forensics
* Network Engineering

---

# Learning Objectives

By completing this room, I learned how to:

* Understand the purpose of core networking protocols
* Recognize the default ports used by common protocols
* Differentiate between TCP and UDP usage
* Interact with services using Telnet
* Use networking tools such as:

  * `nslookup`
  * `whois`
  * `ftp`
  * `telnet`
* Read and understand protocol communication
* Observe protocol traffic and commands
* Gain confidence working directly with network services

---

# Protocols Covered

## DNS (Domain Name System)

Learned how DNS converts human-readable domain names into IP addresses.

Topics covered:

* A Record
* AAAA Record
* CNAME Record
* MX Record
* DNS Queries
* DNS Responses
* `nslookup`

---

## WHOIS

Learned how to investigate domain registration information.

Topics covered:

* Domain registration
* Creation date
* Registrar
* Organization information
* Domain status

Command used:

```bash
whois domain.com
```

---

## HTTP / HTTPS

Learned how web browsers communicate with web servers.

Topics covered:

* HTTP Requests
* HTTP Responses
* HTML
* GET
* POST
* PUT
* DELETE
* HTTP Status Codes
* Secure communication using HTTPS

Also learned how to manually send HTTP requests using Telnet.

---

## FTP (File Transfer Protocol)

Learned how files are transferred between a client and server.

Topics covered:

* Anonymous login
* Listing files
* Downloading files
* Uploading files

Common commands:

* USER
* PASS
* LIST
* RETR
* STOR

---

## SMTP (Simple Mail Transfer Protocol)

Learned how email is sent between mail servers.

Topics covered:

* HELO / EHLO
* MAIL FROM
* RCPT TO
* DATA
* Message termination using `.`
* QUIT

---

## POP3

Learned how email clients download messages from a mail server.

Topics covered:

* Authentication
* Listing messages
* Retrieving messages
* Deleting messages

---

## IMAP

Learned how email synchronization works across multiple devices.

Topics covered:

* Login
* Selecting mailboxes
* Fetching emails
* Moving emails
* Copying emails
* Synchronization

---

# Tools Used

* TryHackMe AttackBox
* Linux Terminal
* Telnet
* FTP Client
* nslookup
* whois

---

# Key Concepts Learned

* Every protocol has a specific purpose.
* Different protocols use different default ports.
* Many protocols communicate using structured commands.
* DNS makes websites easier to access by translating names into IP addresses.
* HTTP delivers web pages.
* FTP transfers files.
* SMTP sends emails.
* POP3 downloads emails.
* IMAP synchronizes emails across devices.
* WHOIS provides publicly available domain registration information.

---

# Challenges I Faced

Throughout this room, I learned that understanding protocol communication is more important than memorizing commands.

Some areas that required extra attention included:

* Remembering protocol ports
* Understanding protocol-specific commands
* Distinguishing between SMTP, POP3, and IMAP
* Following manual communication using Telnet

Working through these challenges improved my understanding of how network services actually operate.

---

# Key Takeaways

* Networking protocols are the foundation of cybersecurity.
* Understanding how protocols work makes packet analysis much easier.
* Manual interaction with services provides valuable insight into client-server communication.
* Knowing default ports is useful during security assessments, SOC investigations, and penetration testing.
* Building strong networking fundamentals makes advanced cybersecurity topics easier to understand.

---

# Suggested Practice

After completing this room, try practicing the following:

1. Use `nslookup` on different websites and identify their DNS records.
2. Use `whois` to investigate several domains.
3. Manually connect to an HTTP server using Telnet.
4. Practice downloading files from an FTP server.
5. Observe protocol traffic using Wireshark.
6. Create a table of common protocols and their default ports.
7. Compare SMTP, POP3, and IMAP to understand how email systems work.

---

# Skills Developed

* Networking Fundamentals
* Protocol Analysis
* Command-Line Usage
* DNS Investigation
* Web Communication
* Email Protocols
* File Transfer
* Traffic Observation
* Client-Server Communication

---

# Conclusion

This room strengthened my understanding of the networking protocols that power the Internet. Rather than simply learning commands, I developed a better understanding of how clients and servers communicate, how data moves across networks, and why these protocols are essential in real-world cybersecurity. These concepts provide a strong foundation for future learning in packet analysis, penetration testing, SOC operations, and network security.
