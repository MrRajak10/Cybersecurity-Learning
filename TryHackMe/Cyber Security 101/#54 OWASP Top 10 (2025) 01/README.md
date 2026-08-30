# TryHackMe — OWASP Top 10 2025: A01, A07 & A09

This repository documents my learning from a TryHackMe room focused on three OWASP Top 10 2025 categories related to failures in **Identity, Authentication, Authorization, and Accountability (IAAA)**:

* **A01 — Broken Access Control**
* **A07 — Authentication Failures**
* **A09 — Logging & Alerting Failures**

The room is beginner-friendly and focuses on understanding the security weaknesses behind these categories through practical web application challenges.

---

## Learning Objectives

By completing this room, the main goals are to understand:

* How identity is represented in a web application
* How authentication verifies who a user is
* How authorization determines what a user is allowed to access
* Why accountability depends on reliable security logging
* How implementation mistakes can allow attackers to access unauthorized data or accounts
* How seemingly small application design flaws can become security vulnerabilities

A useful way to remember the concepts is:

> **Identity → Authentication → Authorization → Accountability**

These four areas help explain how an application identifies users, verifies them, controls their permissions, and records their actions.

---

# A01 — Broken Access Control

Broken Access Control occurs when an application does not properly enforce **who is allowed to access a resource or perform an action**.

Access control decisions must be enforced by the server for every relevant request. The application should never rely only on assumptions made by the client.

One common example is **IDOR (Insecure Direct Object Reference)**.

### IDOR

An IDOR vulnerability can occur when an application exposes an object identifier directly in a URL or request and fails to verify whether the current user is authorized to access that object.

For example:

```text
/profile?id=1
```

Changing the identifier to:

```text
/profile?id=2
```

should not automatically grant access to another user's information.

If the application returns the second user's data without performing an authorization check, the application contains an access-control vulnerability.

### Horizontal Privilege Escalation

The room demonstrates how changing object identifiers can result in **horizontal privilege escalation**.

Horizontal escalation means moving from one user's level of access to another user's data or resources while remaining at approximately the same privilege level.

Example:

```text
User A → User B's account
```

This is different from vertical privilege escalation, where an ordinary user obtains higher-level privileges such as administrator access.

### Defensive Principles

Applications should:

* Perform authorization checks on the server for every request.
* Verify that the authenticated user has permission to access the requested resource.
* Avoid trusting predictable object identifiers as proof of authorization.
* Consider indirect or otherwise non-predictable references where appropriate.

The important lesson is that **changing an identifier should never be enough to access another user's data**.

---

# A07 — Authentication Failures

Authentication failures occur when an application cannot reliably verify or properly bind a user's identity to the authenticated session.

The room highlights several common problems associated with authentication:

* Username enumeration
* Weak authentication logic
* Missing brute-force protection
* Missing rate limiting
* Poor login or registration logic
* Insecure session or cookie handling
* Authentication bypass conditions

### Username Enumeration

An application may accidentally reveal whether a username exists.

For example, different responses for:

```text
User does not exist
```

and:

```text
Incorrect password
```

can help an attacker identify valid accounts.

Once valid usernames are discovered, attackers can focus their password attacks on those accounts.

### Brute-Force Protection

Login functionality should prevent attackers from making unlimited authentication attempts.

Important defensive mechanisms include:

* Rate limiting
* Account protection mechanisms
* Monitoring repeated failed attempts
* Strong password policies
* Appropriate lockout or throttling strategies

The room demonstrates an authentication scenario where weak application logic can allow an attacker to obtain access to an account.

The key lesson is that authentication security is not simply about having a login form. The **entire authentication flow** must be designed securely.

---

# A09 — Logging & Alerting Failures

Logging and alerting failures occur when security-relevant events are not properly recorded, monitored, or turned into actionable alerts.

This category is closely connected to **accountability**.

A secure application should provide enough logging information for defenders to answer questions such as:

* Who performed the action?
* When did it happen?
* What resource was accessed?
* What request was made?
* What was the result?
* Where did the request originate?
* Was the activity successful or suspicious?

### Detecting Brute-Force Activity

The room uses a simulated security monitoring interface to identify suspicious authentication activity.

A brute-force attack can produce a pattern such as:

```text
Failed login
Failed login
Failed login
Failed login
Successful login
```

When repeated failures originate from the same source and are followed by a successful authentication, this can become an important indicator of compromise.

### Investigating Logs

The room demonstrates how useful log information can include:

* Timestamp
* Source IP address
* Requested URL
* HTTP method
* Username
* Password attempt
* Response status
* Authorization result

For example, repeated failed requests followed by a successful request can help investigators reconstruct what happened during an attack.

### Why Logging Matters

Logging is not useful simply because data exists somewhere.

Security monitoring requires:

```text
Event → Log → Detection → Alert → Investigation → Response
```

If important events are not logged or alerts are not generated, defenders may have little visibility into an attack.

---

# Key Concepts

## Identity

Identity represents **which account or principal is involved**.

Example:

```text
username = admin
```

## Authentication

Authentication answers:

> "Who are you?"

Examples include:

* Username and password
* Multi-factor authentication
* Certificates
* Tokens

## Authorization

Authorization answers:

> "What are you allowed to do?"

For example:

```text
Normal User → View own profile
Admin → Manage users
```

## Accountability

Accountability answers:

> "What happened, who did it, and can we investigate it?"

This depends heavily on reliable logging and monitoring.

---

# Practical Investigation Mindset

When testing a web application, do not only ask whether a feature works.

Ask:

### Access Control

* Can I access another user's object?
* Can I change an identifier?
* Is authorization checked on the server?
* Can a lower-privileged user access an administrative resource?

### Authentication

* Can usernames be enumerated?
* Is brute-force protection present?
* Is rate limiting implemented?
* Are there weaknesses in registration or login logic?
* Can authentication be bypassed?

### Logging & Alerting

* Are failed logins recorded?
* Are successful logins recorded?
* Are suspicious patterns detectable?
* Can an investigator identify the source IP?
* Can the sequence of an attack be reconstructed?

This mindset is often more valuable than memorizing individual vulnerabilities.

---

# Beginner Practice Activities

## Activity 1 — IDOR Practice

Create or use a simple application with URLs such as:

```text
/profile?id=1
/profile?id=2
/profile?id=3
```

Test whether changing the identifier allows one user to access another user's information.

Then implement a server-side authorization check and verify that unauthorized requests are denied.

---

## Activity 2 — Authentication Testing

Create a basic login page and test:

```text
Valid username + invalid password
Invalid username + invalid password
Repeated failed attempts
```

Observe whether the application leaks information about account existence.

Then add rate limiting and compare the behavior.

---

## Activity 3 — Log Analysis

Generate a small set of authentication logs containing:

```text
Failed login
Failed login
Failed login
Successful login
```

Identify:

* Source IP
* Target username
* Time of attack
* Number of attempts
* Successful authentication

Then define a simple rule for detecting possible brute-force activity.

---

# Important Lessons

### 1. Never trust client-controlled identifiers

An identifier in a URL or request does not prove that the requester is authorized to access the corresponding object.

### 2. Authentication is more than a login form

Secure authentication requires protection against enumeration, brute force, bypasses, weak session handling, and other implementation flaws.

### 3. Authorization must be enforced on every relevant request

A user being authenticated does not mean they are authorized to access every resource.

### 4. Logs are part of security

Without useful logs and alerts, defenders may be unable to detect or investigate attacks.

### 5. Patterns matter

A single failed login may be normal. Dozens of failures followed by a successful authentication from the same source can represent a very different security event.

---

# Final Takeaway

The three OWASP categories covered in this room can be understood as failures in different parts of the application security chain:

```text
Identity
   ↓
Authentication
   ↓
Authorization
   ↓
Accountability
```

A weakness in any of these areas can have significant consequences.

**A01** focuses on whether users can access resources they should not access.

**A07** focuses on whether the application can reliably authenticate users and protect the authentication process.

**A09** focuses on whether security-relevant activity is recorded, monitored, and turned into actionable alerts.

The most important lesson is to understand **why the vulnerability exists**, not simply how to reproduce it. That understanding makes it easier to recognize similar weaknesses in unfamiliar applications.
