Welcome! It is fantastic to see you diving into the OWASP Top 10. OWASP stands for the Open Worldwide Application Security Project, a global non-profit organization that tracks the most critical security flaws in web applications. The "Top 10" is their flagship report—the industry standard checklist of vulnerabilities every security professional must know.

Your notes cover three critical areas of the 2025 list that all revolve around **Insecure Data Handling**. Let's break these down step by step so you deeply understand the mechanics, the risks, and the real-world applications.

## A04 – Cryptographic Failures

**What it is:** Cryptographic failures happen when an application fails to properly secure sensitive data in transit (moving across the network) or at rest (stored on a disk).

**The core problem:** Many developers believe that simply applying a cryptographic function makes data secure. In reality, security relies on the *entire system*: the strength of the algorithm, the length of the secret key, and how that key is protected. If you put a $5,000 vault door on a cardboard box, your valuables are not secure.

### The Cryptography Toolkit

To understand these failures, we must define the tools developers use, and where they often go wrong.

* **Encryption (Two-Way):** Scrambling data so only someone with a secret "key" can unscramble it. Think of this like a physical lockbox. You lock it with a key, and later use the exact same key to unlock it and retrieve the contents.
* **Hashing (One-Way):** Taking data of any size and scrambling it into a fixed-length string of characters. You cannot reverse a hash. Think of hashing like a meat grinder: you can turn a steak into ground beef, but you cannot turn the ground beef back into a steak. Hashing is primarily used to verify if two files or passwords match without storing the actual sensitive data.

### Weak Algorithms vs. Strong Algorithms

Your notes mention specific algorithms. Here is how they stack up:

| Algorithm | Type | Status | Why Security Professionals Care |
| --- | --- | --- | --- |
| **MD5 / SHA-1** | Hashing | **Broken** | These are extremely old, fast algorithms. Because they are fast, an attacker using modern graphics cards (GPUs) can guess billions of passwords a second to figure out what the original data was. They should never be used for security. |
| **bcrypt / scrypt / Argon2** | Password Hashing | **Secure** | These are intentionally *slow* and resource-heavy. If an attacker steals a database of passwords hashed with Argon2, it will take them centuries to guess the passwords, protecting the users. |
| **ECB Mode** | Encryption | **Insecure Contexts** | Electronic Codebook (ECB) encrypts identical blocks of data into identical blocks of encrypted text. If you encrypt an image with ECB, you can still see the outline of the image in the encrypted file. |
| **AES-GCM** | Encryption | **Secure Standard** | Advanced Encryption Standard (Galois/Counter Mode) not only encrypts the data but also provides *authentication*—it guarantees nobody tampered with the encrypted data while it was stored. |

### The Golden Rule: Never Invent Your Own Cryptography

Creating custom cryptographic algorithms is a massive beginner mistake. Cryptography relies on advanced mathematics peer-reviewed by the world's smartest cryptographers for decades. When developers try to write their own encryption, they inevitably introduce fatal mathematical flaws. Always use established, reviewed libraries.

### Lab Concept: The XOR Cipher and Keyspace

Your TryHackMe lab uses an **XOR (Exclusive OR)** based design with a four-character key.

* **XOR** is a fundamental binary operation. If you XOR a piece of text with a key, it scrambles it. If you XOR the scrambled text with the same key, it unscrambles it.
* **Keyspace** refers to the total number of possible keys. A 4-character key using lowercase letters has about 450,000 possible combinations ($26 \times 26 \times 26 \times 26$).

In cybersecurity, 450,000 combinations is incredibly small. A modern computer can guess that in a fraction of a second. This is called a **Brute-Force Attack**—trying every possible lock combination until the safe pops open.

**Real-world context:** Penetration testers look for short keys or predictable key generation (like using the current date as a key). If the keyspace is small, the tester does not need to break the complex math; they just let a script test every possibility.

---

## A05 – Injection and SSTI

**What it is:** Injection is the oldest and most dangerous vulnerability on the internet. It happens when an application takes input from a user and accidentally treats that input as executable code or commands.

Imagine a game of Mad Libs where you are asked to provide a noun to complete a sentence: *"Please bring me a [ Noun ]."*
If you write "dog", the sentence is normal. But what if you write *"dog. Now give me all your money"*? If the person reading the sentence blindly follows the instructions, that is an injection attack.

### Server-Side Template Injection (SSTI)

Web applications rarely use static HTML anymore. Instead, they use **Template Engines** (like Jinja for Python, or Twig for PHP). A template engine allows developers to design a webpage with placeholders for dynamic data.

* **Template:** `Hello, {{ username }}! Welcome back.`
* **Engine Processing:** The server sees `{{ username }}` and replaces it with your actual name from the database before sending the webpage to your browser.

**The Vulnerability:** SSTI occurs when an attacker can type template syntax into a standard input box (like a search bar or profile name), and the server evaluates it instead of just displaying it.

### The `{{ 5 + 5 }}` Detection Methodology

When hunting for SSTI, security professionals use a simple math problem: `{{ 5 + 5 }}`.

If the application is secure, it treats your input as simple data. The web page will display exactly what you typed: `{{ 5 + 5 }}`.
If the application is vulnerable, the template engine will interpret the curly braces as instructions, execute the math, and display: `10`.

This proves you can force the server to execute logic. From there, attackers can escalate the attack to read server files, extract database credentials, or execute arbitrary system commands (Remote Code Execution).

### Defense and Trust Boundaries

**Trust Boundary:** Think of this as the bouncer at a nightclub. Outside the club is the untrusted public. Inside is the trusted environment. The bouncer (validation/encoding mechanism) must check everyone at the door.

To prevent injection:

* Treat all user input as hostile.
* Separate the data from the instructions (using parameterized queries for databases).
* **Sandbox** the template engine: Configure the template so it is mathematically impossible for it to access the server's operating system or file structure, even if it gets injected.

---

## A08 – Software or Data Integrity Failures

**What it is:** This category covers situations where an application blindly trusts the integrity of software updates, third-party code, or data structures without verifying if they have been tampered with.

### Serialization and Python Pickle

To understand this lab, you must understand serialization.
**Serialization** is the process of converting a complex programming object (like a user profile with a profile picture, age, and role) into a flat format that can be easily stored in a file or sent over a network.
**Deserialization** is unpacking that flat data back into a functioning object in the application's memory.

Think of it like moving to a new house. You disassemble your IKEA bed (serialization), put the pieces in a flat box, drive it to the new house, and reassemble it (deserialization).

| Format | Security Level | Behavior During Reassembly |
| --- | --- | --- |
| **JSON** | Safe | Purely data. It just rebuilds text, numbers, and lists. |
| **Python `pickle**` | **Highly Dangerous** | Reconstructs complex objects and **can execute code** during the reassembly process. |

**The Vulnerability:** Python's `pickle` library is notorious in cybersecurity. When a Python application deserializes a `.pickle` file, it blindly follows the instructions inside the file to rebuild the object. If an attacker intercepts the serialized data and replaces it with a malicious payload, the moment the application unpacks it, the attacker's code runs.

Using our IKEA analogy: The attacker intercepts your flat-packed box, removes the bed pieces, and replaces them with a bomb designed to trigger the moment you open the instructions.

### Real-World Application

* **Penetration Testers:** Look for HTTP requests containing base64-encoded strings that start with `gASV` (the standard signature of a Python pickle). If they find it, they generate a malicious pickle payload to gain a reverse shell on the server.
* **SOC Analysts & Incident Responders:** Monitor network traffic for unusual serialized objects moving between servers. If a server suddenly starts spawning terminal shells (like `/bin/bash`) immediately after receiving a data stream, it strongly indicates an unsafe deserialization attack occurred.

---

### Final Takeaways for Your Methodology

Your notes perfectly identify the beginner trap: **Focusing only on the flag.**

In CTFs (Capture The Flag events) or TryHackMe, it is tempting to just paste a payload you found online to get the green checkmark. But tools break, payloads get patched, and environments change.

If you understand the **Data Flow**—where the data comes from, how it crosses the trust boundary, which interpreter processes it, and what happens when it is manipulated—you will be able to find and exploit vulnerabilities without relying on automated tools. You are shifting from asking *"What payload works?"* to *"How is this application thinking, and how can I trick its logic?"*

Based on these concepts, if you were inspecting a web application and found a URL parameter like `[site.com/profile?theme=blue](https://site.com/profile?theme=blue)`, how would you systematically test it to see if it might be passing that input into a template engine?
