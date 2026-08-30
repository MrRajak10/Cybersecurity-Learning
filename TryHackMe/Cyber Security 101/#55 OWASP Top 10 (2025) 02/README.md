# TryHackMe — OWASP Top 10 2025: Application Design Flaws

## Overview

This repository documents my learning journey through a TryHackMe room covering selected categories from the **OWASP Top 10 2025**, with a focus on weaknesses caused by insecure configuration, software dependencies, cryptography, and application design.

The room covered four categories:

* **A02 — Security Misconfiguration**
* **A03 — Software Supply Chain Failures**
* **A04 — Cryptographic Failures**
* **A06 — Insecure Design**

The main lesson from the room is that security problems are not always caused by programming bugs. A system can be vulnerable because of how it is configured, how dependencies are trusted, how cryptography is selected, or how the application was designed in the first place.

---

## Learning Objectives

By completing this room, I learned how to:

* Recognize common forms of security misconfiguration.
* Understand how verbose application errors can expose implementation details.
* Inspect web applications and their API communication.
* Enumerate API endpoints and understand parent/child endpoint relationships.
* Understand why undocumented API functionality can become an attack surface.
* Recognize risks introduced by third-party software and dependencies.
* Understand why software supply-chain security matters.
* Identify weak cryptographic choices such as insecure encryption modes.
* Understand why ECB mode is unsuitable for protecting structured data.
* Identify insecure assumptions in application architecture.
* Understand how business logic and application design can create vulnerabilities even when individual components appear functional.
* Use browser developer tools, Burp Suite, API requests, and command-line tools during reconnaissance and testing.
* Think beyond obvious endpoints and investigate the assumptions made by an application.

---

## Room Structure

### A02 — Security Misconfiguration

Security misconfiguration occurs when systems, applications, servers, cloud resources, or services are deployed with insecure settings.

This is different from a traditional coding vulnerability. The application may work exactly as programmed, but the surrounding configuration may expose information or functionality that should not be available.

Common examples include:

* Default credentials.
* Weak passwords.
* Unnecessary services.
* Exposed administrative interfaces.
* Publicly accessible cloud storage.
* Verbose error messages.
* Debug functionality left enabled.
* Old or insecure software configurations.
* APIs exposed without appropriate controls.

### What I learned

One important lesson was that **error messages are useful during reconnaissance**.

Instead of receiving a generic response such as:

> Record not found

an application might reveal additional information such as:

> User ID must be numeric.

That small difference provides information about how the application validates input.

This led to an important testing habit:

> Try unusual input and observe how the application reacts.

Invalid input can sometimes reveal:

* Expected data types.
* Validation logic.
* Internal implementation details.
* Database-related information.
* Debug information.
* Framework behavior.

### Important distinction

While testing the user-management API, changing identifiers appeared to expose other users. That behavior is more closely associated with **authorization failures / IDOR-style behavior** than security misconfiguration itself.

This was an important learning point because vulnerabilities can overlap during testing, but the classification of a vulnerability still matters.

---

## A03 — Software Supply Chain Failures

Modern applications rarely consist entirely of code written by one development team.

Applications commonly depend on:

* Open-source libraries.
* Frameworks.
* Package managers.
* External services.
* Build tools.
* Container images.
* Third-party components.

This creates a software supply chain.

A vulnerability in one trusted dependency can affect every application that includes it.

### Why the supply chain matters

A developer might install a library because it is popular and trusted. However, trusting a dependency does not automatically make the entire supply chain secure.

Important risks include:

* Malicious packages.
* Compromised dependencies.
* Unmaintained libraries.
* Vulnerable versions.
* Unverified updates.
* Build-system compromises.
* Compromised third-party services.

### SolarWinds lesson

The room uses the SolarWinds compromise as an example of why software supply-chain security matters.

The critical idea is that an attacker does not always need to attack every organization individually.

Compromising software that many organizations already trust can allow malicious changes to reach many victims through the normal update or distribution process.

### Defensive lessons

Some useful defensive practices include:

* Track dependencies.
* Keep dependencies updated.
* Verify packages and software sources.
* Use trusted repositories.
* Validate software integrity where possible.
* Monitor dependency vulnerabilities.
* Avoid blindly trusting third-party components.
* Control the software build and release pipeline.
* Review what external libraries actually do.

### Personal learning

This was the most frustrating section of the room for me.

The challenge initially did not provide enough information to make the intended path obvious, which led me to spend significant time testing different inputs and endpoints.

The important lesson was not simply finding the intended behavior. It was learning to step back when repeated testing produces no useful result.

A useful troubleshooting rule is:

> When experimentation keeps producing the same result, reconsider the assumptions and look for additional context.

The later source-code information made the intended behavior much clearer. In particular, examining the implementation showed how a specific input value triggered debug behavior.

---

## A04 — Cryptographic Failures

Cryptographic failures occur when sensitive information is not adequately protected through encryption or when cryptography is implemented incorrectly.

Cryptography is used in many places:

* Data transmission.
* Password protection.
* Tokens.
* Session data.
* Stored confidential information.
* Application-to-application communication.

### Common problems

Examples include:

* Weak cryptographic algorithms.
* Insecure encryption modes.
* Hard-coded keys.
* Poor key management.
* Reused secrets.
* Weak hashing.
* Missing encryption.
* Incorrect TLS configuration.
* Insufficient secret rotation.

### ECB Mode

One of the important concepts encountered in this room was **Electronic Codebook (ECB)** mode.

ECB encrypts each plaintext block independently using the same key.

That creates a serious weakness for structured or repetitive data because identical plaintext blocks produce identical ciphertext blocks.

In other words:

> ECB hides the actual plaintext, but it does not adequately hide patterns.

For protecting structured application data, authenticated encryption modes such as **AES-GCM** are generally much more appropriate.

Other modern designs may use constructions such as **ChaCha20-Poly1305**, depending on the implementation requirements.

### Key lesson

Finding a strong algorithm is not enough.

Secure cryptography also depends on:

* Correct mode selection.
* Secure key generation.
* Secure key storage.
* Proper initialization values/nonces.
* Key rotation.
* Correct implementation.
* Authentication/integrity protection.

Cryptographic security is therefore both an algorithm-selection problem and a key-management problem.

---

## A06 — Insecure Design

Insecure design is different from a simple implementation bug.

An implementation bug can happen when the developer incorrectly implements a secure design.

An insecure-design vulnerability exists when the underlying design itself makes unsafe assumptions.

Examples include:

* Trusting the client to enforce security rules.
* Assuming users will only access an intended interface.
* Relying on hidden functionality for security.
* Failing to define authorization requirements.
* Missing security controls in business workflows.
* Designing APIs without proper authentication.
* Assuming a specific device or application will always be used.

### The Mobile-Only Assumption

One of the most important lessons in this room came from an application that claimed to be designed exclusively for mobile users.

The application effectively assumed that users would interact with it only through the intended mobile interface.

However, the backend API could be accessed directly.

This creates a fundamental architectural problem:

> A security boundary cannot be created merely by hiding functionality behind a particular client application.

A mobile application is still a client.

A determined user can often inspect or reproduce the network requests generated by that application.

Therefore, security controls must exist on the server side.

### API Security Lesson

When an application exposes an API, the backend must independently enforce:

* Authentication.
* Authorization.
* Input validation.
* Access control.
* Rate limiting where appropriate.
* Business rules.
* Data exposure limits.

The fact that a feature is not visible in the normal interface does not make it secure.

### Endpoint Enumeration

Another important lesson was learning to think about APIs as structured systems.

For example, discovering one endpoint can provide clues about related functionality.

An endpoint such as:

```text
/users
```

may suggest related resources such as:

```text
/users/<id>
/users/<id>/messages
```

This does not mean every application uses the same structure, but the relationship between resources can guide further investigation.

This is much more effective than blindly guessing random paths.

---

## Tools and Techniques Used

### Browser Developer Tools

The browser's developer tools were useful for observing:

* Network requests.
* HTTP methods.
* API endpoints.
* Request parameters.
* Response data.
* JavaScript resources.

A useful habit is to inspect network traffic before immediately moving to more advanced tooling.

---

### Burp Suite

Burp Suite was used to:

* Intercept requests.
* Send requests to Repeater.
* Modify parameters.
* Test different input values.
* Use Intruder for enumeration.
* Observe application responses.

The most important lesson was not simply learning individual Burp features, but understanding when each feature is useful.

For example:

* **Proxy** → intercept traffic.
* **Repeater** → manually modify and replay requests.
* **Intruder** → automate parameter variations.
* **HTTP responses** → identify useful behavioral differences.

---

### Curl

Command-line HTTP requests were also useful for interacting directly with APIs.

A basic request-testing workflow is:

```bash
curl -i http://TARGET/
```

For JSON APIs, request headers and HTTP methods become particularly important.

For example:

```bash
curl -i -X POST \
  -H "Content-Type: application/json" \
  -d '{"data":"test"}' \
  http://TARGET/process
```

The exact endpoint and parameters depend on the application.

The important concept is being able to reproduce browser traffic manually.

---

### Gobuster

Gobuster was useful for endpoint discovery.

However, one major lesson from the room was:

> Directory enumeration is not the same as API enumeration.

An API may expose functionality through nested resources or predictable data structures that are not obvious from basic directory fuzzing.

Therefore, API testing should combine:

* Documentation.
* Browser traffic.
* Source inspection.
* Endpoint relationships.
* Parameter analysis.
* Manual request testing.

---

## Challenges I Faced

The software supply-chain task was the most difficult part of the room for me.

I spent considerable time:

* Testing different request formats.
* Modifying parameters.
* Trying different HTTP methods.
* Inspecting API responses.
* Using Burp Suite.
* Testing with curl.
* Attempting endpoint discovery.
* Looking for clues in the application.

Several approaches led to dead ends.

### What I learned from the frustration

The most valuable lesson was about troubleshooting methodology.

When a technique does not work:

1. Confirm that the request is actually reaching the intended endpoint.
2. Confirm the HTTP method.
3. Confirm headers such as `Content-Type`.
4. Confirm the expected data format.
5. Compare the response with a known-good request.
6. Inspect the source or available documentation.
7. Reconsider the vulnerability hypothesis.
8. Avoid repeatedly applying the same technique without obtaining new information.

This is an important skill in real penetration testing.

---

## Key Takeaways

### 1. Configuration is part of security

A secure application can still become vulnerable through insecure deployment.

### 2. Errors can reveal useful information

Verbose responses can expose implementation details that help an attacker understand an application.

### 3. Vulnerability classification matters

A behavior discovered while testing one vulnerability category may actually belong to another category, such as authorization failure or IDOR.

### 4. Dependencies are part of the attack surface

Third-party code should be treated as part of the application's security boundary.

### 5. Cryptography requires correct implementation

A strong algorithm does not automatically produce strong security.

### 6. Never trust the client

Mobile apps, web applications, and desktop programs are clients. Security controls must ultimately be enforced by the backend.

### 7. Think in terms of application architecture

Understanding how components communicate often reveals vulnerabilities faster than blindly fuzzing everything.

### 8. Dead ends are part of the learning process

Not every request produces a vulnerability.

Knowing when to stop, reassess, and change direction is an important penetration-testing skill.

---

## Beginner Practice Activities

### Practice 1 — Error Message Analysis

Create a small test application that accepts an integer parameter.

Test it with:

```text
1
0
-1
abc
null
```

Record how different inputs affect the application's responses.

Goal:

Identify what information can be learned from validation errors.

---

### Practice 2 — API Mapping

Choose a legal practice API and document:

```text
Endpoint
HTTP Method
Parameters
Authentication
Response Format
Possible Related Endpoints
```

Build a small API map showing how resources relate to one another.

---

### Practice 3 — Burp Repeater

Use a legal training application such as a TryHackMe or PortSwigger lab.

Capture a request in Burp Suite and send it to Repeater.

Modify:

* HTTP method.
* Parameters.
* Headers.
* JSON values.

Record what changes in the server response.

---

### Practice 4 — Cryptography

Experiment with a small dataset encrypted using ECB and a modern authenticated encryption mode.

Observe what happens when identical plaintext blocks are repeated.

The objective is to understand **why encryption mode matters**, not merely memorize the name of a weak mode.

---

### Practice 5 — Insecure Design Thinking

For a fictional mobile application, write down assumptions such as:

```text
Only the mobile application will call the API.
Users will only request their own data.
Hidden endpoints will not be discovered.
Clients will enforce business rules.
```

For each assumption, ask:

> What happens if an attacker does not follow this assumption?

This is a simple way to practice threat modeling.

---

## Final Reflection

This room reinforced an important principle:

> Security cannot be added only at the final stage of development.

Secure systems require:

* Clear security requirements.
* Threat modeling.
* Secure configuration.
* Controlled dependencies.
* Appropriate cryptography.
* Strong authentication and authorization.
* Server-side security controls.
* Continuous testing.

The most useful skill I gained from this room was learning to look beyond the obvious interface.

A button, mobile application, API endpoint, library, configuration file, error message, or cryptographic choice can all reveal something about the underlying architecture.

Understanding those relationships is what turns simple enumeration into meaningful security analysis.
