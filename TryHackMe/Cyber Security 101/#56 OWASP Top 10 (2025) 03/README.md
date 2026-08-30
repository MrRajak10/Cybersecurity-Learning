# TryHackMe – OWASP Top 10 2025: Insecure Data Handling

This repository contains my learning notes and experience from the TryHackMe room focused on **Insecure Data Handling** and three security areas from the **OWASP Top 10 2025**:

* **A04 – Cryptographic Failures**
* **A05 – Injection**
* **A08 – Software or Data Integrity Failures**

The room uses small practical labs to introduce how weaknesses in cryptography, user-controlled input, and untrusted serialized data can lead to security issues.

The goal of these notes is not simply to record solutions. Instead, they document the concepts, reasoning, mistakes, and practical lessons that are useful for someone beginning their cybersecurity journey.

---

# Learning Objectives

By completing this room, I learned how to:

* Understand the purpose of the relevant OWASP Top 10 2025 categories.
* Recognize common causes of cryptographic failures.
* Understand why weak encryption algorithms and short keys are dangerous.
* Understand the security risks of trusting user input.
* Identify the basic idea behind Server-Side Template Injection (SSTI).
* Understand why applications should establish trust boundaries.
* Understand the risks of processing untrusted serialized objects.
* Recognize why Python `pickle` can become dangerous when untrusted data is deserialized.
* Think about vulnerabilities from an application's trust and data-flow perspective rather than only looking for flags.

---

# OWASP Top 10 Concepts Covered

## A04 – Cryptographic Failures

Cryptographic failures happen when sensitive information is not adequately protected.

Common causes include:

* Weak or outdated cryptographic algorithms.
* Weak or short encryption keys.
* Improper key management.
* Reusing cryptographic keys where it creates additional risk.
* Storing credentials or secrets insecurely.
* Implementing custom cryptographic algorithms instead of using established standards.

A major lesson from the room is that **cryptography should not be invented unnecessarily**. Applications should rely on well-established, reviewed, and appropriately implemented cryptographic mechanisms.

For passwords, slow password-hashing algorithms such as **bcrypt, scrypt, or Argon2** are more appropriate than general-purpose fast hashes.

For encryption, authenticated modern modes such as **AES-GCM** are preferable to insecure approaches that provide confidentiality without proper authentication.

### Key lesson

Strong cryptography is not only about choosing an algorithm. The key, mode of operation, implementation, storage, and overall design all matter.

---

# Cryptography Lab

The first practical lab demonstrates why a weak encryption design can be attacked.

The application uses a weak XOR-based encryption scheme with:

* A very short key.
* A predictable key format.
* The same key for multiple pieces of encrypted data.

Because XOR encryption is reversible and the key space is extremely small, the key can be discovered through **brute force**.

The exercise demonstrates an important principle:

> Encryption becomes weak when the key space is small enough to search.

A short key may appear to provide encryption, but if an attacker can efficiently try every possible key, the protection becomes ineffective.

### What I learned

The important part of this lab was not merely recovering the plaintext. The real lesson was understanding **why the encryption failed**.

The weakness came from the design:

`Short key → small search space → feasible brute force → plaintext recovery`

### Better approach

Use:

* Strong, randomly generated keys.
* Modern authenticated encryption.
* Secure key storage.
* Proper key management.
* Established cryptographic libraries.

Never rely on custom cryptographic designs simply because they appear to work.

---

# A05 – Injection

Injection occurs when an application treats attacker-controlled input as instructions rather than ordinary data.

Examples include:

* SQL Injection
* Command Injection
* Server-Side Template Injection (SSTI)
* Other interpreter or parser injection vulnerabilities

The fundamental problem is the same:

`Untrusted input → interpreted as code/instructions`

Instead of:

`Untrusted input → treated only as data`

---

# Server-Side Template Injection (SSTI)

The room demonstrates SSTI using a template engine.

A useful first step when testing an application is to determine whether user-controlled input is being interpreted by the template engine.

For example, a mathematical expression can be supplied as input. If the server evaluates the expression instead of displaying it literally, this can indicate that the input is reaching the template engine.

Conceptually:

```text
Input:
{{ expression }}

Expected if treated as text:
{{ expression }}

Potential vulnerable behavior:
result of the expression
```

This type of behavior can indicate that server-side template evaluation is occurring.

### Why SSTI matters

A template engine normally interprets template syntax so that applications can dynamically generate pages.

If an attacker can control template expressions, the attacker may be able to interact with objects or functions available to the template environment.

Depending on the template engine and application configuration, this can escalate from simple expression evaluation to much more serious behavior, including access to application resources or operating-system functionality.

---

# How to Think About Injection

When investigating an injection vulnerability, ask:

1. What part of the input is controlled by the user?
2. Where does that input go?
3. Is it passed to an interpreter, parser, shell, database, or template engine?
4. Is the input treated as data or instructions?
5. Can the application separate data from executable syntax?

This way of thinking is more valuable than memorizing individual payloads.

---

# Preventing Injection

Applications should:

* Treat all external input as untrusted.
* Prefer parameterized queries for SQL.
* Avoid constructing commands directly from user input.
* Apply appropriate contextual output encoding.
* Use safe APIs instead of interpreters where possible.
* Restrict template functionality and dangerous objects.
* Perform appropriate input validation.

The strongest protection is usually to **avoid mixing user-controlled data with executable syntax**.

---

# A08 – Software or Data Integrity Failures

This category focuses on situations where an application trusts software, code, updates, dependencies, or data without adequately verifying their integrity or origin.

The key concept is the **trust boundary**.

An application should not automatically assume:

> “This data or code was provided, therefore it must be trustworthy.”

Examples include:

* Loading software updates without verifying their authenticity.
* Trusting external dependencies without integrity verification.
* Processing serialized objects without validating their source.
* Loading scripts or artifacts from untrusted locations.
* Accepting modified data without integrity checks.

The room connects this concept with **secure deserialization**.

---

# Python Pickle and Insecure Deserialization

Python's `pickle` module can serialize Python objects so they can later be reconstructed.

The dangerous part is that `pickle` is capable of representing objects whose reconstruction can trigger code execution.

Therefore:

```text
Trusted pickle data
        ↓
Deserialization
        ↓
Object reconstruction
```

can become extremely dangerous when the pickle data is controlled by an attacker:

```text
Attacker-controlled pickle
        ↓
Application accepts it
        ↓
Unsafe deserialization
        ↓
Potential code execution
```

The vulnerability is not simply that serialization exists.

The problem is **deserializing untrusted data without establishing trust and integrity**.

---

# Pickle Lab

The practical exercise demonstrates how an application accepts a serialized Python object and processes it without properly verifying that the object is trustworthy.

The key learning process was:

1. Understand the serialization format being accepted.
2. Identify that the application performs deserialization.
3. Recognize that the serialized object is attacker-controlled.
4. Understand that a malicious object can perform actions during reconstruction.
5. Use this behavior to demonstrate the impact of the vulnerability.

The important takeaway is the relationship between:

`Untrusted serialized data + unsafe deserialization = potentially severe security impact`

---

# Trust Boundaries

A trust boundary defines where trusted and untrusted data meet.

For example:

```text
User
  ↓
Web Application
  ↓
Input Validation
  ↓
Trusted Processing
```

If data crosses the boundary without verification, the application may accidentally trust attacker-controlled content.

Security controls should therefore be placed around these boundaries.

---

# Personal Challenges and Lessons

One of the most useful parts of this room was learning to reason from the application's behavior instead of immediately searching for a payload.

Several observations became especially important:

### 1. Small security weaknesses can completely change the attack

A cryptographic system may technically use encryption, but a short key can make brute forcing practical.

### 2. Input behavior reveals vulnerability classes

When an application evaluates an expression supplied as input, that behavior can provide an important clue that template injection is occurring.

### 3. Serialization does not automatically mean safety

A serialized object may look like ordinary data, but some serialization mechanisms can perform dangerous operations while rebuilding objects.

### 4. Trust must be explicit

Applications should verify the origin and integrity of external code, dependencies, updates, and data rather than assuming they are safe.

### 5. Understanding the vulnerability is more important than memorizing payloads

The most valuable skill is being able to explain:

`Input → Application component → Security boundary → Vulnerable behavior → Impact`

That reasoning transfers to many other security challenges.

---

# Beginner Practice Activities

## Practice 1 – Weak-Key Thinking

Create a small toy encryption example using a deliberately tiny keyspace.

Try to answer:

* How many possible keys exist?
* How quickly could they be tested?
* What happens as the keyspace increases?

The goal is to understand why key length and randomness matter.

---

## Practice 2 – Identify SSTI Behavior

Build a small local application using a template engine.

Provide:

```text
{{ 2 + 3 }}
```

Observe whether the application:

* Displays the expression literally, or
* Evaluates it.

Then investigate why the difference occurs.

Only perform security testing against applications you own or are explicitly authorized to test.

---

## Practice 3 – Serialization Safety

Create a simple Python program that serializes an object.

Then compare the security implications of:

* Trusted local data.
* User-uploaded serialized data.
* Signed serialized data.
* Safer data-only formats such as JSON.

The goal is to understand why data provenance matters.

---

# Key Takeaways

* Do not design custom cryptography when established algorithms and libraries are available.
* Weak keys can make encryption vulnerable to brute force.
* Cryptographic security includes proper key management, not just choosing an algorithm.
* Injection occurs when untrusted data is interpreted as instructions.
* SSTI can occur when user-controlled input reaches a server-side template engine.
* Parameterization and proper separation of data from executable syntax are fundamental defenses against injection.
* Applications must establish clear trust boundaries.
* Untrusted serialized objects can be dangerous to deserialize.
* Python `pickle` should not be treated as a safe interchange format for untrusted data.
* Software, dependencies, updates, and external data should be verified before being trusted.
* The ability to explain *why* a vulnerability exists is more valuable than memorizing exploitation steps.

---

# Overall Learning Outcome

This room provided a compact introduction to three important OWASP Top 10 2025 categories.

The labs demonstrate three different security failures:

```text
A04 → Weak cryptographic protection
A05 → Untrusted input interpreted as instructions
A08 → Untrusted data or software accepted without adequate integrity verification
```

Although the vulnerabilities are different, they share a common security principle:

> **Never assume that data, code, or cryptographic protection is trustworthy simply because it appears to work.**

Understanding that principle helps build a stronger foundation for application security, penetration testing, and further TryHackMe learning.
