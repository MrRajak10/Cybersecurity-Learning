# README.md

# TryHackMe — Nmap Basics

A beginner-focused learning repository documenting my journey through the **Nmap Basics** room on TryHackMe. This repository is intended to reinforce concepts, document lessons learned, and serve as a reference while progressing in cybersecurity.

> **Note:** This repository focuses on learning and understanding concepts. It is **not** intended to be a flag walkthrough or answer sheet.

---

# Learning Objectives

After completing this room, I understood how to:

* Understand what Nmap is and why it is widely used.
* Discover live hosts on a network.
* Perform basic TCP and UDP port scanning.
* Understand the difference between Connect Scan and SYN Scan.
* Identify running services and their versions.
* Detect the operating system of a target.
* Control scan speed using timing templates.
* Increase scan output using verbosity and debugging.
* Save scan results in different output formats.

---

# Topics Covered

* Introduction to Nmap
* Host Discovery
* Target Specification
* Local vs Remote Network Scanning
* ARP Discovery
* ICMP Discovery
* TCP Connect Scan
* TCP SYN Scan
* UDP Scan
* Port Selection
* Service Version Detection
* Operating System Detection
* Timing Templates
* Verbose and Debug Modes
* Saving Scan Results

---

# Key Concepts Learned

## What is Nmap?

Nmap (Network Mapper) is an open-source network scanning tool used to discover hosts, identify open ports, detect running services, determine service versions, and perform operating system detection.

---

## Host Discovery

Learned how Nmap determines whether a system is online before performing further scanning.

Covered:

* IP Range Scanning
* Subnet Scanning
* Hostname Scanning

Also learned the difference between:

* Local network host discovery
* Remote network host discovery

---

## Port Scanning

Learned how Nmap checks which ports are open on a target machine.

Important concepts:

* Open Port
* Closed Port
* Listening Service

---

## TCP Connect Scan

Understood how a full TCP Three-Way Handshake works during scanning.

---

## TCP SYN Scan

Learned why SYN Scan is faster and quieter than Connect Scan.

---

## UDP Scan

Learned how UDP services can also be discovered using Nmap.

---

## Version Detection

Learned how to identify:

* Running services
* Service versions

---

## Operating System Detection

Learned that Nmap can estimate the operating system running on a target using TCP/IP fingerprinting.

---

## Timing Templates

Learned how scan speed can be adjusted depending on the situation.

---

## Output Control

Learned how to:

* Increase scan information
* Debug scans
* Save scan results in multiple formats

---

# Important Nmap Options Learned

| Option         | Purpose                       |
| -------------- | ----------------------------- |
| `-sn`          | Host Discovery                |
| `-sT`          | TCP Connect Scan              |
| `-sS`          | TCP SYN Scan                  |
| `-sU`          | UDP Scan                      |
| `-sV`          | Service Version Detection     |
| `-O`           | Operating System Detection    |
| `-A`           | Aggressive Scan               |
| `-Pn`          | Skip Host Discovery           |
| `-F`           | Scan Top 100 Ports            |
| `-p`           | Scan Specific Ports           |
| `-T0` to `-T5` | Timing Templates              |
| `-v`           | Verbose Output                |
| `-d`           | Debug Mode                    |
| `-oN`          | Normal Output                 |
| `-oX`          | XML Output                    |
| `-oG`          | Grepable Output               |
| `-oA`          | Save All Major Output Formats |

---

# Practical Learning

During this room I practiced:

* Discovering active hosts.
* Understanding how local and remote discovery differ.
* Identifying open ports.
* Detecting running web services.
* Identifying service versions.
* Detecting operating systems.
* Reading Nmap scan results.
* Understanding packet flow conceptually.

---

# Challenges Faced

Some concepts required additional learning before becoming clear:

* CIDR notation and subnet calculations.
* Difference between ARP discovery and ICMP discovery.
* TCP Three-Way Handshake.
* Difference between Connect Scan and SYN Scan.
* Understanding why SYN Scan is considered stealthier.
* Understanding how timing templates affect scanning behavior.

---

# Key Takeaways

* Nmap automates tasks that would otherwise be slow and repetitive.
* Host discovery and port scanning are different phases.
* Open ports usually indicate running services.
* Different scan types have different purposes.
* Faster scans are not always the best choice.
* Understanding networking fundamentals makes Nmap much easier to learn.

---

# Beginner Practice Ideas

* Scan your own lab machine.
* Scan a private subnet and identify live hosts.
* Compare Connect Scan and SYN Scan results.
* Detect service versions on a practice machine.
* Experiment with different timing templates.
* Save scan results in different output formats and compare them.

---

# Skills Gained

* Network Enumeration
* Host Discovery
* Port Enumeration
* Service Enumeration
* Version Detection
* Operating System Detection
* Basic Network Reconnaissance
* Reading Nmap Output
* Understanding TCP/IP Scanning Concepts

---

# Conclusion

This room provided a strong foundation in using Nmap for reconnaissance. More importantly, it explained the networking concepts behind each scan, making it easier to understand what Nmap is doing rather than simply memorizing commands.
