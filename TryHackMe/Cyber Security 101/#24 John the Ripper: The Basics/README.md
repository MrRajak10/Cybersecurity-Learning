# TryHackMe — John the Ripper: The Basics

## Room Information

| Category | Details |
|----------|----------|
| Platform | TryHackMe |
| Room | John the Ripper: The Basics |
| Difficulty | Easy |
| Topic | Password Cracking |
| Tool | John the Ripper (Jumbo John) |

---

# Overview

This room introduces **John the Ripper (JtR)**, one of the most popular password cracking tools used by penetration testers, red teamers, security researchers, and CTF players.

Instead of reversing hashes (which is practically impossible for secure hashing algorithms), John the Ripper generates hashes from candidate passwords and compares them with the target hash. When both hashes match, the original password has been found.

Throughout this room, you will learn how John the Ripper cracks different password-protected resources such as:

- Password hashes
- Windows NTLM hashes
- Linux Shadow hashes
- ZIP archives
- RAR archives
- SSH private keys

---

# Learning Objectives

After completing this room, you should be able to:

- Understand how password cracking works
- Explain dictionary attacks
- Explain brute-force attacks
- Identify common hash formats
- Crack basic password hashes
- Crack Windows authentication hashes
- Crack Linux shadow hashes
- Use Single Crack Mode
- Understand custom rules
- Crack ZIP archives
- Crack RAR archives
- Crack encrypted SSH private keys

---

# Prerequisites

Before starting this room, you should understand:

- Cryptography Basics
- Public Key Cryptography
- Hashing Basics

Recommended TryHackMe rooms:

- Cryptography Basics
- Public Key Cryptography Basics
- Hashing Basics

---

# What is John the Ripper?

John the Ripper (JtR) is an open-source password recovery and password auditing tool.

Its primary purpose is to recover plaintext passwords from password hashes.

Unlike encryption, hashes cannot simply be "decrypted."

Instead, John repeatedly:

1. Takes a candidate password.
2. Generates its hash.
3. Compares it with the target hash.
4. If both hashes match, the password has been recovered.

---

# Why John the Ripper is Popular

John the Ripper is widely used because it:

- Supports hundreds of hash formats
- Has extremely fast cracking performance
- Supports dictionary attacks
- Supports brute-force attacks
- Supports rule-based attacks
- Works on Windows, Linux, and macOS
- Is heavily used during penetration testing
- Is widely used in Capture The Flag (CTF) competitions

---

# How John the Ripper Works

```
Password List
      │
      ▼
Candidate Password
      │
      ▼
Generate Hash
      │
      ▼
Compare with Target Hash
      │
      ▼
Hash Match?
   │        │
 Yes       No
 │          │
 ▼          ▼
Password   Try Next Word
Found
```

---

# Password Cracking Workflow

```
Target Hash
      │
      ▼
Identify Hash Type
      │
      ▼
Choose Attack Method
      │
      ▼
Run John the Ripper
      │
      ▼
Password Recovered
```

---

# Dictionary Attack

A dictionary attack uses a predefined list of passwords.

Instead of guessing every possible combination, John tests passwords that already exist inside a wordlist.

Example wordlist:

```
password
123456
football
welcome
admin
qwerty
dragon
letmein
```

For every password:

```
Password
     │
     ▼
Generate Hash
     │
     ▼
Compare
     │
     ▼
Match?
```

If a match occurs, the original password is recovered.

---

# Brute Force Attack

Unlike a dictionary attack, brute force does not rely on an existing password list.

Instead, it tries every possible combination.

Example:

```
a
b
c
...
aa
ab
ac
...
aaa
aab
aac
...
```

Brute force is:

- Slower
- More exhaustive
- More likely to find unknown passwords

---

# Common Hash Algorithms

John supports many hashing algorithms, including:

- MD4
- MD5
- SHA-1
- SHA-224
- SHA-256
- SHA-384
- SHA-512
- Whirlpool
- NTLM
- bcrypt
- yescrypt
- SHA512crypt

and many more.

---

# Hash Identification

Before cracking a hash, you must determine its format.

Common tools include:

- hashid
- hash-identifier
- hashcat --example-hashes

Example:

```bash
python3 hash-id.py
```

Input:

```
5f4dcc3b5aa765d61d8327deb882cf99
```

Possible output:

```
MD5
Domain Cached Credentials
NTLM
...
```

---

# Basic John Syntax

```bash
john [options] <hash_file>
```

Example:

```bash
john hashes.txt
```

---

# Specify a Wordlist

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

---

# Specify Hash Format

```bash
john --format=raw-md5 \
--wordlist=/usr/share/wordlists/rockyou.txt \
hash.txt
```

---

# Common John Formats

Examples include:

```
raw-md5
raw-sha1
raw-sha256
raw-sha512
NT
bcrypt
whirlpool
zip
rar
ssh
```

---

# Windows NTLM Hashes

Windows stores password hashes using the **NTLM** format.

John can crack NTLM hashes using:

```bash
john \
--format=NT \
--wordlist=/usr/share/wordlists/rockyou.txt \
ntlm.txt
```

---

# Linux Shadow Passwords

Linux stores password hashes inside:

```
/etc/shadow
```

User information exists inside:

```
/etc/passwd
```

Before cracking:

```
/etc/passwd
        +
/etc/shadow
        │
        ▼
unshadow
        │
        ▼
Combined File
        │
        ▼
John the Ripper
```

Example:

```bash
unshadow passwd shadow > hashes.txt
```

Then:

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
hashes.txt
```

---

# Single Crack Mode

Single Crack Mode attempts to generate passwords using:

- Username
- Full Name
- User information (GECOS field)

Example:

```bash
john \
--single \
--format=raw-md5 \
hashes.txt
```

---

# Custom Rules

John supports custom password mutation rules.

Example mutations:

```
password
Password
Password1
Password123
Password!
Password@123
```

These rules improve password cracking success by generating realistic password variations.

---

# ZIP Password Cracking

Convert ZIP archive into a crackable hash:

```bash
zip2john secure.zip > zip.hash
```

Crack:

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
zip.hash
```

Extract:

```bash
unzip secure.zip
```

---

# RAR Password Cracking

Generate hash:

```bash
rar2john secure.rar > rar.hash
```

Crack:

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
rar.hash
```

Extract:

```bash
unrar x secure.rar
```

---

# SSH Private Key Cracking

Generate hash:

```bash
ssh2john id_rsa > ssh.hash
```

Crack:

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
ssh.hash
```

---

# Important Tools

| Tool | Purpose |
|------|---------|
| john | Password cracking |
| hash-id | Identify hash type |
| zip2john | ZIP → Hash |
| rar2john | RAR → Hash |
| ssh2john | SSH Key → Hash |
| unshadow | Merge passwd & shadow |

---

# Common Wordlist

The most widely used password list:

```
rockyou.txt
```

Location:

```bash
/usr/share/wordlists/rockyou.txt
```

---

# Skills Learned

- Password auditing
- Hash identification
- Dictionary attacks
- Brute-force attacks
- NTLM cracking
- Linux password auditing
- ZIP password recovery
- RAR password recovery
- SSH private key recovery
- Rule-based password cracking

---

# Real-World Use Cases

John the Ripper is commonly used during:

- Penetration Testing
- Red Team Operations
- Internal Security Audits
- Active Directory Assessments
- Password Policy Audits
- Incident Response
- Digital Forensics
- Capture The Flag (CTF) Challenges

---

# Key Takeaways

- Hashes cannot normally be reversed.
- Password cracking works by comparing generated hashes.
- Wordlists greatly improve cracking speed.
- Correctly identifying the hash type is essential.
- Windows uses NTLM hashes.
- Linux stores password hashes in `/etc/shadow`.
- `unshadow` prepares Linux hashes for John.
- `zip2john`, `rar2john`, and `ssh2john` convert protected files into crackable hashes.
- Rule-based attacks generate smarter password candidates.
- John the Ripper is one of the most widely used password recovery tools in cybersecurity.

---

# References

- TryHackMe — John the Ripper: The Basics
- Openwall John the Ripper Documentation
- rockyou.txt Wordlist
- John Jumbo Edition

---

# Author

Prepared as personal study notes while completing the **TryHackMe – John the Ripper: The Basics** room.

> These notes are intended for educational purposes, cybersecurity learning, and authorized security assessments only.
