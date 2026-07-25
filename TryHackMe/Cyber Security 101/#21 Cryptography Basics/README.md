# TryHackMe - Cryptography Basics

> A beginner-friendly learning repository documenting my journey through the **Cryptography Basics** room on TryHackMe.

> **Note:** This repository focuses on understanding concepts, learning cryptography fundamentals, and documenting my learning experience. It is **not** intended to be a flag walkthrough or answer guide.

---

# Room Overview

Cryptography is one of the most important foundations of cybersecurity. Every day we use applications like WhatsApp, Instagram, online banking, UPI, email, SSH, HTTPS websites, and cloud services without realizing that cryptography is working behind the scenes.

This room introduces the fundamental concepts of cryptography and explains how encryption helps protect data from attackers while it travels across the Internet.

Throughout this room, I learned not only what cryptography is, but also why it exists, how it works, where it is used, and how modern systems combine different encryption techniques to secure communication.

---

# Learning Objectives

After completing this room, I understood:

- What cryptography is
- Why cryptography is necessary
- The three security goals of cryptography
- Plaintext and Ciphertext
- Encryption and Decryption
- Cipher and Keys
- Historical ciphers
- Caesar Cipher
- Symmetric Encryption
- Asymmetric Encryption
- Public Key and Private Key
- How HTTPS/TLS uses both encryption methods
- XOR operation
- Modular arithmetic
- Real-world applications of cryptography

---

# Why Cryptography Matters

The Internet itself is not a trusted environment.

Whenever data travels between two devices, attackers may attempt to:

- Read the data
- Modify the data
- Pretend to be someone else
- Intercept communication

Cryptography solves these problems by protecting communication.

---

# Core Security Principles

This room introduced three major goals of cryptography.

## Confidentiality

Only the intended recipient should be able to read the information.

Example:

Someone intercepting your password should never be able to read it.

---

## Integrity

Data must remain unchanged while travelling across the network.

Example:

A downloaded file should be exactly the same as the original.

---

## Authenticity

You should be able to verify that you are communicating with the genuine server or user.

Example:

The HTTPS lock icon confirms the website's identity through digital certificates.

---

# Topics Covered

This room covers:

- Cryptography fundamentals
- Real-world cryptography usage
- Encryption process
- Decryption process
- Cipher concepts
- Caesar Cipher
- Historical encryption methods
- Symmetric encryption
- Asymmetric encryption
- TLS/HTTPS overview
- XOR mathematics
- Modular arithmetic

---

# Real-World Examples

Some common places where cryptography is used include:

- HTTPS websites
- Online banking
- UPI payments
- Email
- SSH
- VPN
- Password transmission
- File integrity verification
- Digital certificates
- Secure software downloads

---

# Key Concepts Learned

## Plaintext

Readable original data.

Example:

```
Hello
```

---

## Ciphertext

Encrypted unreadable version of data.

Only someone with the correct key can convert it back.

---

## Encryption

Converting plaintext into ciphertext.

---

## Decryption

Converting ciphertext back into plaintext.

---

## Cipher

A mathematical algorithm used to encrypt and decrypt data.

---

## Key

A secret value used during encryption and decryption.

Without the correct key, encrypted data cannot be recovered.

---

# Historical Cryptography

This room introduced the Caesar Cipher.

The Caesar Cipher works by shifting every letter by a fixed number.

Example:

```
HELLO

Shift = 3

KHOOR
```

Although historically important, it is no longer secure because attackers can brute-force every possible shift.

---

# Symmetric Encryption

Symmetric encryption uses:

- One shared key
- Same key for encryption
- Same key for decryption

Advantages:

- Very fast
- Efficient
- Best for encrypting large amounts of data

Challenge:

The secret key must be shared securely.

Examples:

- AES
- DES
- 3DES

Modern systems primarily use AES.

---

# Asymmetric Encryption

Asymmetric encryption uses two different keys.

- Public Key
- Private Key

Public Key

- Shared with everyone
- Used for encryption

Private Key

- Kept secret
- Used for decryption

Examples:

- RSA
- Diffie-Hellman
- Elliptic Curve Cryptography (ECC)

---

# How HTTPS Uses Both

One of the most valuable lessons from this room was understanding why modern systems use both encryption methods.

Simplified process:

1. Browser contacts server.
2. Server sends its certificate.
3. Browser verifies the certificate.
4. Browser generates a symmetric AES session key.
5. AES key is encrypted using the server's public key.
6. Server decrypts it using its private key.
7. Both sides now share the same AES key.
8. Future communication uses fast symmetric encryption.

This combines:

- Authentication
- Secure key exchange
- Fast encrypted communication

---

# Mathematical Foundations

The room also introduced two important mathematical operations.

## XOR

Rules:

```
0 XOR 0 = 0
0 XOR 1 = 1
1 XOR 0 = 1
1 XOR 1 = 0
```

Important properties:

- Same values produce 0
- Different values produce 1

XOR is widely used inside modern encryption algorithms.

---

## Modular Arithmetic

Modulo returns the remainder after division.

Example:

```
23 mod 6 = 5

25 mod 5 = 0
```

Modular arithmetic is heavily used in public-key cryptography.

---

# Practical Takeaways

After completing this room, I now understand:

- Why encrypted communication is necessary
- How attackers intercept network traffic
- Why plaintext should never travel across the Internet
- Why HTTPS is trustworthy
- How certificates verify server identity
- Why AES is widely used
- Why RSA is used for secure key exchange
- Why XOR appears frequently in cryptography
- How mathematical operations support encryption

---

# Beginner Practice

To strengthen your understanding, try these exercises:

- Encrypt words using the Caesar Cipher with different shift values.
- Decrypt Caesar Cipher messages manually.
- Practice XOR calculations using binary numbers.
- Solve modulo arithmetic examples.
- Visit HTTPS websites and inspect their certificates.
- Compare HTTP and HTTPS.
- Research AES, RSA, ECC, and TLS.
- Understand how SSH creates secure encrypted sessions.

---

# Skills Developed

- Cryptography fundamentals
- Encryption concepts
- Secure communication
- Public Key Infrastructure (PKI)
- TLS basics
- Digital certificates
- Binary operations
- Mathematical thinking for cybersecurity

---

# Key Takeaways

- Cryptography protects confidentiality, integrity, and authenticity.
- Encryption converts readable information into unreadable ciphertext.
- Decryption restores the original message.
- Modern systems combine symmetric and asymmetric encryption.
- HTTPS relies on certificates, public keys, private keys, and AES.
- Cryptography is one of the most important foundations of cybersecurity.

---

# Learning Reflection

Before this room, cryptography seemed like a difficult topic involving complicated mathematics and algorithms.

After completing the room, I now understand the basic building blocks behind secure communication. More importantly, I learned *why* cryptography exists before learning *how* advanced algorithms work.

This room provided an excellent foundation for future topics such as Public Key Cryptography, Hashing, TLS, PKI, Digital Signatures, and Secure Authentication.
