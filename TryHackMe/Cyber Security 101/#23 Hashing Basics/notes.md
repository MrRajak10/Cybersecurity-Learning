Welcome back! It is great to see you diving into cryptography and data integrity. Hashing is one of the most fundamental concepts in cybersecurity. Whether you are dealing with malware analysis, digital forensics, network security, or web application penetration testing, you will encounter hashes constantly.

Many beginners confuse hashing with encryption or encoding, but by the end of this session, you will see exactly how they differ and why they are used. Let's break down your notes and build a deep, practical understanding of hashing.

---

## 1. What is Hashing?

At its core, **hashing** is a mathematical process that takes digital data of any size and turns it into a unique, fixed-size string of characters called a **hash** (or **digest**).

Think of a hash as a **digital fingerprint** for a file or a piece of text. Just as a human fingerprint uniquely identifies a person without revealing what they look like, a hash uniquely identifies data without revealing the original content.

### Why does it exist?

Hashing exists to solve two major problems:

1. **Integrity:** How do I know a file hasn't been corrupted or secretly modified by an attacker?
2. **Secure Verification:** How can a website verify my password is correct without actually storing the password itself?

### The Core Properties of a Hash Function

To be useful in cybersecurity, a hash function must follow four strict rules:

1. **Fixed-Length Output:** No matter the input size, the output is always the same length. If you hash a single letter 'A', or if you hash a 100 GB movie file, the resulting SHA-256 hash will always be exactly 256 bits (64 characters long).
2. **Deterministic:** The same input will *always* produce the exact same output. If you and I both hash the word "hello" on different computers, we will get the exact same hash.
3. **Avalanche Effect:** A microscopic change in the input completely changes the output. If you change a single pixel in an image, or change a capital 'T' to a lowercase 't', the entire hash changes. This makes it instantly obvious if a file has been tampered with.
4. **One-Way Function:** You cannot reverse a hash back into the original data. If you have a hash, there is no mathematical key or formula to "decrypt" it back into a password or a file.

---

## 2. Hashing vs. Encryption vs. Encoding

This is a classic trap for beginners. Let's define the exact differences so you never mix them up in an interview or a CTF.

| Concept | Purpose | Is it Reversible? | Requires a Key? |
| --- | --- | --- | --- |
| **Encoding (Base64)** | Data format compatibility | Yes, easily by anyone | No |
| **Encryption (AES, RSA)** | Data confidentiality | Yes, if you have the key | Yes |
| **Hashing (SHA-256)** | Data integrity & verification | No, it is a one-way street | No |

**Encoding (like Base64)** is just translating data so a computer system can transport it without errors. It is like translating English to Spanish. It is not meant to be a secret. If you see text ending in `==`, it is often Base64, and you can decode it instantly using the command `base64 -d encoded.txt`.

**Encryption** is a two-way street. You use a key to lock the data into a secret format, and you (or someone else) uses a key to unlock it later.

**Hashing** is taking a document and putting it through a paper shredder. You can't put the paper back together (one-way), but if you have a copy of the original document, you can shred it and compare the pieces to prove they were identical.

---

## 3. Hash Algorithms and Collisions

Different mathematical formulas create hashes. Some are old and broken; some are modern and secure.

* **MD5 (128-bit) & SHA-1 (160-bit):** These are outdated. We still see them in CTFs and legacy systems, but they are vulnerable to **Hash Collisions**.
* **SHA-256 & SHA-512:** Part of the SHA-2 family. These are the current industry standards for file integrity.

### What is a Hash Collision?

Because a hash is a fixed length (e.g., 128 bits), there is a limited number of possible hashes. However, there is an infinite number of possible files in the universe.

Because of the **Pigeonhole Principle** (if you have 10 pigeons and 9 holes, at least one hole must contain two pigeons), eventually, two completely different files will generate the exact same hash.

If attackers can intentionally create a malicious file that has the *exact same MD5 hash* as a safe, trusted file, they have achieved a collision. They can swap the files, and security systems relying on the hash will think the malicious file is the safe one. This is why we no longer trust MD5 or SHA-1 for critical security.

---

## 4. Practical Application: File Integrity Verification

When you download a piece of software (like Kali Linux), the creators usually post a SHA-256 hash on their website.

### Why Security Professionals Use This

Attackers often compromise software download servers. If you download a tool, how do you know an attacker didn't quietly inject a backdoor into it?

1. **Download the File:**
Download the software installer to your local machine, but do not execute it yet.


2. **Generate the Local Hash:**
Open your Linux terminal and run the hashing tool against the file:
`sha256sum downloaded_file.iso`


3. **Compare with the Source:**
Look at the hash output on your terminal, and compare it to the hash published on the software vendor's official website.


4. **Determine Authenticity:**
If the hashes match exactly, the file is authentic. If even one character is different, delete the file immediately — it has been corrupted or tampered with.


---

## 5. Passwords, Rainbow Tables, and Salting

### The Problem: Why we don't store plain text

If a company stores passwords in plain text in a database, a single data breach exposes every user's account. This happened in the famous RockYou breach, which is why penetration testers still use the `rockyou.txt` wordlist today.

We also cannot use **Encryption** for passwords. If we encrypt passwords, the server must hold the decryption key. If an attacker steals the database, they will likely steal the key too, unlocking all the passwords.

### The Solution: Password Hashing

When you create an account, the server hashes your password and stores *only* the hash. When you log in, the server hashes what you typed and compares it to the database. If they match, you are granted access. The server never actually knows your real password.

### The Attack: Rainbow Tables

Attackers know that many people use simple passwords (like `password123` or `football`). Since hashing is deterministic, `football` will always produce the exact same MD5 hash.

A **Rainbow Table** is a gigantic, pre-computed database of millions of common passwords and their corresponding hashes. Instead of trying to reverse the hash, the attacker just looks up the stolen hash in their rainbow table. If it finds a match, they know the password instantly.

### The Defense: Salting

To defeat Rainbow Tables, we use a **Salt**. A salt is a random string of characters added to a user's password *before* it is hashed.

If two users have the password `football`, the database might look like this:

1. User A: `football` + Salt (`X7@91!`) = Hashes to `ABCD...`
2. User B: `football` + Salt (`P#2m9$`) = Hashes to `WXYZ...`

Because the input is now entirely different, the output hash is different. The attacker's rainbow table is now useless because it doesn't contain pre-computed hashes for `footballX7@91!`.

> **SOC & Development Context:** Modern systems don't use basic SHA-256 for passwords anymore because GPUs can calculate them too fast. We use **bcrypt, scrypt, Argon2, or yescrypt**. These algorithms are intentionally designed to be slow and require a lot of memory, which makes brute-forcing them incredibly expensive for an attacker.

---

## 6. Password Cracking in the Real World

As a penetration tester, if you manage to dump the `/etc/shadow` file from a Linux system (which requires root privileges), you will find the salted password hashes.

You can identify the algorithm used by looking at the prefix in the hash string:

* `$1$` = MD5
* `$5$` = SHA-256
* `$6$` = SHA-512
* `$2a$` / `$2b$` / `$2y$` = bcrypt

### The Tools

**John the Ripper**

* **What it is:** A CPU-based password cracker.
* **When to use it:** Great for quick cracking on your local machine, and it auto-detects many hash formats seamlessly.

**Hashcat**

* **What it is:** A highly advanced, GPU-based password cracker.
* **When to use it:** When you have a massive list of complex hashes and need raw speed. GPUs can process thousands of mathematical calculations simultaneously, making them vastly superior to CPUs for hashing.

Let's break down your Hashcat command:
`hashcat -m 3200 -a 0 hash.txt rockyou.txt`

* `hashcat`: Calls the program.
* `-m 3200`: The **mode**. `3200` tells Hashcat that we are trying to crack bcrypt hashes. (You look these codes up in the Hashcat manual).
* `-a 0`: The **attack mode**. `0` means a Straight Dictionary Attack (testing every word in the wordlist exactly as written).
* `hash.txt`: The file containing the stolen hashes you want to crack.
* `rockyou.txt`: The famous wordlist file containing millions of compromised passwords to test against the hashes.

---

## 7. HMAC (Hash-based Message Authentication Code)

HMAC takes hashing one step further.
While a standard hash proves that data wasn't accidentally corrupted, it doesn't stop a hacker from modifying a file and simply generating a *new* hash for it.

**HMAC solves this by combining the hash with a secret key.**

Only the sender and the receiver know the secret key. The sender hashes the data *along with* the key. When the receiver gets the data, they do the same. If the HMAC matches, it proves two things simultaneously:

1. **Integrity:** The data was not altered in transit.
2. **Authenticity:** The message absolutely came from the sender, because no one else has the secret key required to generate that specific HMAC.

You will see HMAC used heavily in web application security, specifically in **JSON Web Tokens (JWTs)** used for logging into websites.

---

This is a fantastic set of notes, and mastering these differences now will make advanced cryptography much easier to digest later.
