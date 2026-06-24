# Offensive Security Intro – TryHackMe

## Overview

This repository documents my learning journey through the **Offensive Security Intro** room on TryHackMe. The room provides a beginner-friendly introduction to offensive security, explains the mindset of an ethical hacker, and demonstrates how vulnerabilities can be discovered and exploited in a controlled environment.

The room also includes a practical exercise where a vulnerable banking application is assessed using basic enumeration techniques to discover hidden functionality and perform a simulated attack.

---

## Learning Objectives

By completing this room, I learned:

* What Offensive Security is
* The difference between Offensive Security and Defensive Security
* Why organizations test their own systems for vulnerabilities
* The importance of thinking like an attacker
* How hidden web pages can be discovered
* Basic use of the Gobuster tool
* How vulnerable applications can expose sensitive functionality
* The role of hands-on practice in cybersecurity learning

---

## Key Concepts Learned

### Offensive Security

Offensive Security focuses on identifying weaknesses in systems before malicious attackers can exploit them.

This involves:

* Finding vulnerabilities
* Discovering security weaknesses
* Testing applications and systems
* Simulating real-world attacks
* Understanding attacker behavior

The goal is not to damage systems but to help secure them by finding weaknesses before criminals do.

---

### Offensive vs Defensive Security

#### Offensive Security

* Finds vulnerabilities
* Simulates attacks
* Thinks like an attacker
* Identifies weaknesses before criminals discover them

#### Defensive Security

* Protects systems
* Detects attacks
* Monitors environments
* Prevents unauthorized access

Both areas work together to improve overall security.

---

### Vulnerabilities and Loopholes

A vulnerability is a weakness that can be exploited by an attacker.

Examples include:

* Misconfigured systems
* Exposed web pages
* Weak authentication
* Software bugs
* Poor access controls

Finding these weaknesses allows organizations to strengthen their defenses.

---

### Enumeration

Enumeration is the process of gathering information about a target.

In this room, enumeration was performed against a web application to identify hidden pages that were not directly visible through normal navigation.

Enumeration is often one of the most important phases of ethical hacking because hidden information frequently leads to security findings.

---

### Gobuster

Gobuster is a directory and file enumeration tool.

It uses a wordlist containing possible page names and attempts to discover hidden resources on a website.

During this room, Gobuster was used to:

* Scan the target website
* Search for hidden directories
* Identify an undisclosed page
* Reveal functionality that was not accessible through the main website interface

---

### Hidden Pages

Web applications often contain multiple pages.

Some pages may not be linked from the homepage but still remain accessible.

Examples include:

* Admin panels
* Backup pages
* Testing environments
* Internal tools
* Transfer portals

If these pages are not properly protected, they may expose sensitive functionality.

---

## Practical Exercise Summary

The room provides a vulnerable banking application for practice.

The objective was to:

1. Explore the application
2. Use Gobuster to discover hidden content
3. Access a hidden page
4. Interact with exposed banking functionality
5. Complete the challenge successfully

This exercise demonstrates how attackers often begin by searching for information that developers accidentally expose.

---

## What I Learned From This Room

* Cybersecurity is a practical skill that requires consistent hands-on learning.
* Enumeration is often more important than complex exploitation.
* Small misconfigurations can create serious security risks.
* Ethical hackers must understand how attackers think.
* Discovering hidden functionality can reveal critical weaknesses.
* Regular practice is essential for long-term improvement.

---

## Career Paths Mentioned

This room introduces several offensive security career options.

### Penetration Tester

Responsible for testing systems, applications, and infrastructure to identify exploitable vulnerabilities.

### Red Teamer

Simulates real-world attackers and provides organizations with insight into how an adversary might compromise their environment.

### Security Engineer

Designs, implements, monitors, and maintains security controls that help protect systems and networks.

---

## Beginner Takeaways

If you are new to cybersecurity, this room teaches an important lesson:

You do not become skilled overnight.

Cybersecurity is built through:

* Consistent learning
* Regular practice
* Curiosity
* Problem-solving
* Patience

Even simple rooms provide valuable experience because they build the foundation needed for more advanced topics later.

---

## Conclusion

The Offensive Security Intro room serves as an excellent starting point for beginners entering cybersecurity. It introduces the offensive security mindset, demonstrates basic web enumeration techniques, and shows how vulnerabilities can be identified within a controlled environment.

Most importantly, the room highlights that cybersecurity is a journey of continuous learning, practice, and curiosity.
