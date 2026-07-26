# Hashing Basics (TryHackMe)

## Room Overview

This room introduces the fundamentals of **hashing**, one of the most important concepts in cybersecurity. Hashing is widely used to verify file integrity, securely store passwords, detect data tampering, and support authentication systems. Unlike encryption, hashing is a **one-way process**, meaning the original data cannot be recovered from its hash.

---

# Learning Objectives

After completing this room, you should understand:

- What hashing is and why it is important
- How hash functions work
- Common hashing algorithms
- File integrity verification
- Password hashing and secure password storage
- Hash collisions
- Rainbow tables
- Password salting
- Recognizing password hashes
- Password cracking using Hashcat and John the Ripper
- HMAC (Hash-based Message Authentication Code)
- Hashing for integrity verification

---

# What is Hashing?

Hashing is the process of converting any digital data into a fixed-length value called a **hash** or **hash value**.

The input can be:

- Text
- Password
- Image
- Document
- Video
- Executable file
- Any digital data

The output is always a fixed-size string produced by a **hash function**.

Example:

```
Input:
password123

SHA-256 Output:
ef92b778bafe771e89245b89ecbc08a44a4e166c06659911881f383d4473e94f
```

---

# Why Do We Use Hashing?

Hashing is mainly used to:

- Verify file integrity
- Store passwords securely
- Detect data modification
- Authenticate users
- Verify downloaded files

Example:

You download a **6 GB ISO file** from the Internet.

How do you know it wasn't modified?

Simply compare:

Original File Hash

↓

Downloaded File Hash

If both hashes match

→ File is original.

If hashes differ

→ File has been modified or corrupted.

---

# Hash Function

A **hash function** accepts an input of any size and produces an output of fixed length.

```
Input
      ↓
 Hash Function
      ↓
 Hash Value
```

Popular hash functions include:

- MD5
- SHA-1
- SHA-256
- SHA-512

---

# Encryption vs Hashing

| Encryption | Hashing |
|------------|----------|
| Reversible | One-way |
| Uses Keys | No Keys |
| Data can be decrypted | Original data cannot be recovered |
| Used for confidentiality | Used for integrity and authentication |

---

# Avalanche Effect

A tiny change in the input produces a completely different hash.

Example

```
Input 1:
T

Input 2:
U
```

Only one character changed.

However,

```
MD5(T)
≠
MD5(U)
```

The hashes become completely different.

This property is called the **Avalanche Effect**.

---

# Common Hash Algorithms

| Algorithm | Output Size |
|------------|------------|
| MD5 | 128 bits (16 Bytes) |
| SHA-1 | 160 bits (20 Bytes) |
| SHA-256 | 256 bits (32 Bytes) |
| SHA-512 | 512 bits (64 Bytes) |

---

# Why MD5 and SHA-1 are Insecure

Older algorithms such as **MD5** and **SHA-1** are considered insecure because attackers can create **hash collisions**.

Modern systems should use:

- SHA-256
- SHA-512
- bcrypt
- scrypt
- Argon2

---

# Hash Collision

A hash collision occurs when **two different inputs generate the same hash value**.

```
Input A
      \
       \
        → Same Hash

Input B
```

Although collisions are rare, weaker algorithms like MD5 are vulnerable.

---

# Pigeonhole Principle

Hash functions have:

- Infinite possible inputs
- Finite possible outputs

Eventually, different inputs must produce the same output.

This is called the **Pigeonhole Principle**, which explains why collisions are mathematically possible.

---

# Password Storage

## Incorrect Method

```
Username

admin

Password

Password123
```

If the database is stolen, attackers immediately know the password.

---

## Correct Method

Store

```
Password123

↓

Hash Function

↓

Hash Value
```

Database stores only:

```
Username

admin

Hash

482c811da5...
```

When the user logs in:

1. User enters password
2. Password is hashed
3. New hash is compared with stored hash
4. If hashes match
   Login succeeds

---

# Plain Text Password Storage

Never store passwords as plain text.

Many historical breaches occurred because companies stored passwords directly.

Example:

RockYou breach

Millions of passwords leaked because passwords were stored without hashing.

Linux commonly includes:

```
rockyou.txt
```

A famous password wordlist used in password cracking.

---

# Why Not Encryption?

Encryption can be reversed using a key.

If the encryption key is stolen,

all passwords can be decrypted.

Hashing is preferred because it is one-way.

---

# Rainbow Tables

A Rainbow Table is a database containing:

Password

↓

Corresponding Hash

Example

| Password | MD5 |
|-----------|-----|
| hello | abc123... |
| football | 7e8d... |
| basketball | 55af... |

Attackers compare stolen hashes with rainbow tables.

If found,

the password is recovered instantly.

---

# Salting

A **salt** is a random value added before hashing.

Instead of:

```
password
```

Store:

```
password + RandomSalt
```

Example

```
Password

football

Salt

k39$d!

Combined

footballk39$d!

↓

Hash
```

Benefits

- Prevents rainbow table attacks
- Makes every password hash unique
- Improves password security

---

# Secure Password Hashing Algorithms

Recommended algorithms:

- Argon2
- bcrypt
- scrypt
- yescrypt

Avoid:

- MD5
- SHA-1

---

# Recognizing Password Hashes

Linux stores password hashes in:

```
/etc/shadow
```

Windows stores password hashes in:

```
SAM (Security Account Manager)
```

Example prefixes:

| Prefix | Algorithm |
|---------|-----------|
| $1$ | MD5 |
| $5$ | SHA-256 |
| $6$ | SHA-512 |
| $2a$ | bcrypt |
| $y$ | yescrypt |

---

# Password Cracking

Common tools:

## Hashcat

- GPU based
- Very fast
- Supports hundreds of algorithms

Example

```bash
hashcat -m 1000 -a 0 hash.txt rockyou.txt
```

---

## John the Ripper

- CPU based
- Popular password cracking tool
- Supports many formats

---

# File Integrity Verification

Hashing verifies downloaded files.

Process:

Original File

↓

Hash

↓

Download File

↓

Hash

↓

Compare

If hashes match

✔ Original

Otherwise

✘ Modified

---

# HMAC

HMAC stands for:

**Hash-based Message Authentication Code**

It combines:

- Secret Key
- Hash Function

Purpose:

- Verify integrity
- Verify authenticity
- Detect tampering

---

# Base64 is NOT Hashing

Base64 is:

- Encoding

NOT

- Encryption
- Hashing

Base64 can always be decoded.

---

# Key Linux Commands

Generate MD5

```bash
md5sum file.txt
```

Generate SHA-1

```bash
sha1sum file.txt
```

Generate SHA-256

```bash
sha256sum file.txt
```

Generate SHA-512

```bash
sha512sum file.txt
```

View first 20 lines

```bash
head -n 20 rockyou.txt
```

Count lines

```bash
wc -l rockyou.txt
```

Decode Base64

```bash
base64 -d encoded.txt
```

---

# Important Concepts

- Hashing is one-way.
- Hash functions always produce fixed-size output.
- Small input changes produce completely different hashes.
- MD5 and SHA-1 are no longer secure.
- Passwords should never be stored as plain text.
- Passwords should be hashed with a unique salt.
- Rainbow tables can crack unsalted hashes.
- Hashcat and John the Ripper are widely used password-cracking tools.
- Hashing is essential for integrity verification and authentication.

---

# Key Takeaways

- Hashing verifies integrity.
- Hashing securely stores passwords.
- Hashes cannot be reversed.
- Always use modern password hashing algorithms.
- Salt every password.
- Prefer SHA-256 or stronger for integrity checking.
- Prefer bcrypt, scrypt, Argon2, or yescrypt for password storage.

---

# Skills Gained

After completing this room, you can:

- Explain how hashing works
- Differentiate hashing from encryption
- Verify file integrity
- Understand password storage best practices
- Identify common hash algorithms
- Recognize Linux and Windows password hashes
- Understand rainbow table attacks
- Explain password salting
- Use basic hashing commands in Linux
- Understand the basics of password cracking tools

---

**Room:** TryHackMe - Hashing Basics  
**Difficulty:** Easy  
**Category:** Cryptography
