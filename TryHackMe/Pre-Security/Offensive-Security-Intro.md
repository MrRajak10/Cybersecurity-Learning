# Introduction to Offensive Security

## Overview of the Concepts
This guide introduces **Offensive Security**, showing how ethical hackers find weak spots in computer systems before malicious attackers can take advantage of them.
To practice this safely, we use a simulated lab environment called **FakeBank**. This allows beginners to safely explore how websites are put together and how attackers uncover hidden web pages.

---

## 1. What is Offensive Security?
Think of offensive security like hiring a professional lockpicker to test the security of your house. Instead of physical locks, security professionals test computer systems, software, and networks by thinking exactly like a cybercriminal.
The goal is to help, not hurt. By testing systems offensively, professionals can:
  * Find hidden weak spots.
  * Test if the current security alarms are working.
  * Fix issues to lower the risk of getting hacked.

> *"To outsmart a hacker, you need to think like one."*

## 2. What is an Ethical Hacker?
An ethical hacker is a cybersecurity professional who breaks into systems **legally**.
Unlike bad actors (often called malicious hackers), ethical hackers always:
  * Ask for **Permission** first.
  * Follow the law and strict rules.
  * Report everything they find to the company.
  * Help the company fix the weak spots.

---

## 3. The Core Concept: Enumeration
**Enumeration** is just a fancy word for "Information Gathering" or "Mapping out the Target." It is usually the very first step an attacker takes.
In website security, enumeration means looking for clues, such as:
  * Finding hidden folders.
  * Locating secret admin login pages.
  * Mapping out how the website is built.

---

## 4. The Tool: Gobuster
**Gobuster** is a command-line tool (a program run by typing text commands rather than clicking buttons). Websites often have hidden pages that don't have links pointing to them. Gobuster works by rapidly guessing thousands of possible web page names from a list (a "wordlist") to see if any of them actually exist.

**The Command Used:**
```
gobuster -u http://fakebank.thm -w wordlist.txt dir

```
**What this command means:**
* **`-u`**: The target website address (URL).
* **`-w`**: The wordlist (a text file full of guessed page names).
* **`dir`**: Tells Gobuster to look for directories (folders).
* 
---

## 5. The Practical Lab: FakeBank Findings
In the simulated **FakeBank** lab, the goal was to find a hidden page that regular users were never meant to see. Using Gobuster, we found two hidden folders:
  1. `/images`
  2. `/bank-transfer`
The `/bank-transfer` page was hidden, but it wasn't locked. It allowed anyone who found it to transfer money between accounts. This shows exactly how attackers exploit forgotten or unprotected pages.

## 6. The Vulnerability: Broken Access Control
When a hidden page (like a bank transfer page or an admin panel) is left wide open without requiring a password or proper permissions, it is a major security flaw.

**The Risks of this Vulnerability:**
  * Anyone on the internet can access secret areas.
  * Private customer data can be stolen.
  * The company can lose money or face legal trouble.
  * The business could be temporarily shut down.

---

## 7. Key Terms for Beginners
|------------------------------------------------------------------------------------------------------------------------|
|       Term         |                                       Simple Definition                                           |
|--------------------|---------------------------------------------------------------------------------------------------|
| **Vulnerability**  | A flaw or weakness in a system that a hacker can take advantage of.                               |
| **Attack Surface** | All the possible doors, windows, and entry points a hacker could try to use to get into a system. |
| **Access Control** | The digital "bouncer" at the door. It checks if you are allowed to view a specific page or file.  |
| **Enumeration**    | Gathering detailed information to map out exactly how a target system works.                      |
|------------------------------------------------------------------------------------------------------------------------|

---

## 8. Real-World Relevance & Takeaways
Companies all over the world hire ethical hackers to perform "Penetration Tests" (practice hacks). They do this to find hidden pages and misconfigurations before real hackers do.

**Summary to remember:**
  * Offensive Security stops attacks before they happen by finding flaws first.
  * Ethical hackers must always have permission.
  * Gathering information (Enumeration) is the most critical step of testing.
  * Leaving administrative tools hidden but unlocked is a massive security risk.

---
