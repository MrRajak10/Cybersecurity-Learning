# TryHackMe - Public Key Cryptography Basics

> A learning-focused repository documenting my journey through the **Public Key Cryptography Basics** room on TryHackMe.

---

## Overview

This repository contains my notes, concepts learned, observations, and lessons from completing the **Public Key Cryptography Basics** room.

The purpose of this repository is **not** to provide a flag walkthrough. Instead, it serves as a learning resource for beginners who want to understand the fundamentals of public key cryptography and how it is used in real-world cybersecurity.

---

## Learning Objectives

During this room I learned about:

- Public Key Cryptography
- Symmetric vs Asymmetric Encryption
- Authentication
- Authenticity
- Integrity
- Confidentiality
- RSA Algorithm
- Diffie-Hellman Key Exchange
- SSH Authentication
- Digital Signatures
- Digital Certificates
- TLS Certificates
- PGP
- GPG

---

## Topics Covered

### Introduction to Cryptography

The room begins by explaining why cryptography is necessary in modern communication.

It introduces four important security goals:

- Authentication
- Authenticity
- Integrity
- Confidentiality

These concepts form the foundation of secure communication.

---

### Symmetric vs Asymmetric Encryption

The room explains the difference between two major encryption approaches.

**Symmetric Encryption**

- Uses one shared key
- Fast
- Primarily protects confidentiality

**Asymmetric Encryption**

- Uses a Public Key and a Private Key
- Solves key sharing problems
- Supports authentication, authenticity, and integrity

---

### Public and Private Keys

One of the biggest learning points was understanding that:

- Public Keys can be shared.
- Private Keys must never be shared.

Data encrypted with a public key can only be decrypted using the matching private key.

---

### RSA

The room introduces RSA, one of the most common public key cryptography algorithms.

Topics learned include:

- Prime numbers
- Public key generation
- Private key generation
- Encryption
- Decryption
- Why factorization is computationally difficult
- Why RSA remains secure

Rather than memorizing formulas, I focused on understanding how RSA protects communication.

---

### Diffie-Hellman Key Exchange

This section explains how two people can securely create the same shared secret over an insecure network.

Important concepts include:

- Shared secret generation
- Public values
- Private values
- Secure key exchange

This shared secret is later used by symmetric encryption.

---

### SSH Authentication

The room explains how SSH verifies both:

- The server
- The client

Topics covered include:

- Host keys
- known_hosts
- authorized_keys
- SSH key pairs
- Password authentication
- Key-based authentication
- Passphrases

I also learned why protecting private SSH keys is extremely important.

---

### Digital Signatures

Digital signatures provide:

- Authenticity
- Integrity
- Non-repudiation

The room explains how:

- A hash is generated.
- The hash is signed using the sender's private key.
- The receiver verifies the signature using the sender's public key.

---

### Digital Certificates

The room introduces certificates used in HTTPS.

Concepts learned:

- Certificate Authority (CA)
- TLS Certificates
- Website identity verification
- Trust chain
- Browser certificate validation

I also learned why browsers trust websites only when certificates are issued by trusted Certificate Authorities.

---

### PGP and GPG

This section introduces:

- Pretty Good Privacy (PGP)
- GNU Privacy Guard (GPG)

Topics learned:

- Key pair generation
- Encrypting files
- Decrypting files
- Importing keys
- Secure communication

---

## Skills Practiced

- Understanding asymmetric encryption
- Reading RSA examples
- Understanding mathematical foundations
- Understanding Diffie-Hellman workflow
- SSH key management
- Digital signature verification
- Certificate validation
- GPG key import
- File decryption using GPG

---

## Key Takeaways

- Encryption alone is not enough.
- Identity verification is equally important.
- Public keys are designed to be shared.
- Private keys must remain secret.
- RSA security depends on the difficulty of factoring very large numbers.
- Diffie-Hellman solves the secure key exchange problem.
- SSH uses cryptography to securely authenticate servers and users.
- Digital signatures prove authenticity and integrity.
- Digital certificates establish trust on the Internet.
- GPG is widely used for secure communication and file encryption.

---

## Beginner Practice

After completing this room, beginners can reinforce their understanding by practicing the following:

- Generate SSH key pairs on a Linux machine.
- Connect to a remote system using SSH keys.
- Explore the `known_hosts` file.
- Explore the `authorized_keys` file.
- Generate GPG keys.
- Encrypt and decrypt a text file with GPG.
- Import an existing GPG key.
- Examine the TLS certificate of a website using a browser.
- Research different RSA key sizes.
- Learn how HTTPS uses asymmetric and symmetric encryption together.

---

## Real-World Applications

The concepts in this room are widely used in:

- HTTPS websites
- Secure Shell (SSH)
- VPNs
- Email encryption
- Digital signatures
- Software package verification
- Cloud infrastructure
- Secure remote administration
- Public Key Infrastructure (PKI)

---

## Challenges Faced

While completing this room, some topics required extra attention:

- Understanding RSA mathematics
- Differentiating authentication and authenticity
- Understanding how Diffie-Hellman generates a shared key
- Visualizing digital signature verification
- Understanding certificate trust chains

Studying the communication flow step-by-step made these concepts much easier to understand.

---

## Final Thoughts

This room provides an excellent introduction to public key cryptography. Instead of focusing only on encryption, it explains how cryptography also establishes trust, verifies identity, protects data integrity, and enables secure communication across the Internet.

The concepts learned here form the foundation for many cybersecurity domains, including SOC operations, penetration testing, cloud security, network security, incident response, and secure software development.
