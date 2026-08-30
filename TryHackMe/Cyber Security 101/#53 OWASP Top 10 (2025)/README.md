# TryHackMe — Top 10 2025: Application Design Flaws

## Overview

This room focuses on application security weaknesses that originate from insecure configuration, software dependencies, cryptographic choices, and application design decisions.

The room is based on selected categories from the **OWASP Top 10 2025** and provides practical challenges that demonstrate how security weaknesses can appear even when an application does not contain an obvious coding vulnerability.

The main categories covered are:

* **A02 — Security Misconfiguration**
* **A03 — Software Supply Chain Failures**
* **A04 — Cryptographic Failures**
* **A06 — Insecure Design**

The most important lesson from this room is that security cannot simply be added after an application has been built. Secure requirements, threat modeling, dependency management, authentication and authorization, safe configuration, and appropriate cryptographic controls need to be considered during the design and development process.

---

## Learning Objectives

By completing this room, I learned how to:

* Understand the security implications of application and server misconfiguration.
* Recognize verbose error messages as potential information-disclosure vulnerabilities.
* Understand how insecure software dependencies can introduce vulnerabilities into otherwise trusted applications.
* Identify risks associated with outdated, unverified, or improperly managed third-party components.
* Understand why weak cryptographic algorithms and insecure encryption modes are dangerous.
* Analyze client-side JavaScript and application source code for security-relevant information.
* Understand how insecure assumptions in application design can expose backend APIs.
* Perform basic API enumeration and understand parent/child API relationships.
* Recognize why authentication and authorization must be enforced on backend services rather than assumed from the client.
* Develop a more structured approach to application security testing.

---

# A02 — Security Misconfiguration

Security misconfiguration occurs when an application, server, framework, API, cloud service, or other component is deployed with insecure settings.

This is different from a traditional programming bug. The underlying software may work exactly as designed, but an unsafe configuration exposes functionality or information that should not be publicly available.

### Common Examples

Examples of security misconfiguration include:

* Default credentials.
* Weak passwords.
* Unnecessary services or endpoints.
* Publicly accessible administrative interfaces.
* Exposed cloud storage.
* Excessively detailed error messages.
* Debug functionality enabled in production.
* Outdated or improperly configured software.
* Information leakage through application responses.

### Important Concept: Verbose Errors

One of the most useful lessons from this section was learning how error messages can reveal information about an application's internal implementation.

For example, an application may normally return a generic response such as:

```text
Record not found
```

A poorly configured application might instead reveal:

```text
Invalid user ID format
```

or provide implementation details, database information, stack traces, debugging information, or other internal details.

This information can help an attacker understand:

* Expected input types.
* Internal application logic.
* Backend technologies.
* Database behavior.
* Debug functionality.
* Potential attack paths.

### Practical Lesson

When testing an application, intentionally providing unexpected input can reveal how the application handles errors.

Useful examples include:

```text
abc
```

```text
'
```

```text
"
```

```text
-1
```

```text
999999
```

The objective is not simply to make the application fail. The objective is to observe **how it fails** and determine whether the response exposes information that should remain internal.

---

# A03 — Software Supply Chain Failures

Modern applications rarely consist entirely of code written by the development team.

Applications commonly depend on:

* Open-source libraries.
* Frameworks.
* Package managers.
* Third-party services.
* Build systems.
* Container images.
* External APIs.
* Development tools.

This creates a software supply chain.

A vulnerability in a trusted dependency can therefore become a vulnerability in the application that depends on it.

## Why Supply Chain Security Matters

A particularly important lesson from this room was that developers often trust software components simply because they come from an external package repository or another trusted organization.

That trust can be dangerous.

A supply chain attack may occur when a malicious or compromised component is introduced somewhere in the development, build, update, or distribution process.

A well-known real-world example is the **SolarWinds compromise**, which demonstrated how attackers can compromise a trusted software distribution process and reach downstream organizations through legitimate updates.

## Common Supply Chain Problems

Typical weaknesses include:

* Using vulnerable dependencies.
* Using outdated libraries.
* Automatically installing updates without verification.
* Trusting third-party components without sufficient review.
* Failing to maintain dependency inventories.
* Not verifying package integrity.
* Using compromised build infrastructure.
* Allowing unnecessary dependencies.

## Key Lesson

A dependency should not be treated as trustworthy simply because:

> "It is a popular package."

Security teams should consider:

* Where did the dependency come from?
* Is the version known?
* Is it maintained?
* Has it been modified unexpectedly?
* Can its integrity be verified?
* Is the version vulnerable?
* Is the dependency actually necessary?

Dependency management is therefore part of application security, not merely software maintenance.

---

# A04 — Cryptographic Failures

Cryptography protects sensitive information such as:

* Credentials.
* Authentication tokens.
* Personal information.
* Financial information.
* Confidential communications.
* Sensitive application data.

Cryptographic failures occur when cryptography is absent, incorrectly implemented, or used with inappropriate algorithms or configurations.

## Common Problems

Examples include:

* Weak hashing algorithms.
* Weak encryption algorithms.
* Insecure encryption modes.
* Hard-coded cryptographic keys.
* Poor key management.
* Improper secret storage.
* Missing encryption for sensitive data.
* Weak TLS configuration.
* Reusing secrets incorrectly.

## ECB Example

One concept that stood out in this room was **Electronic Codebook (ECB)** mode.

ECB is problematic because identical plaintext blocks produce identical ciphertext blocks.

This means patterns in the original data can remain visible in the encrypted output.

For modern applications, authenticated encryption modes such as **AES-GCM** are generally preferable because they provide both confidentiality and integrity.

The important lesson is not simply to memorize algorithm names. The real lesson is:

> Using encryption does not automatically make a system secure.

The algorithm, mode, key management, implementation, storage, and surrounding architecture all matter.

---

# A06 — Insecure Design

Insecure design is fundamentally different from a simple implementation mistake.

An implementation bug can occur when a developer incorrectly implements a secure design.

An insecure design occurs when the underlying system was designed with unsafe assumptions in the first place.

## Example: Trusting the Client

One important scenario in the room involved an application designed primarily for mobile users.

The application's frontend suggested that certain functionality should only be accessible through the mobile application.

However, the backend exposed API endpoints that could be accessed directly.

This demonstrates a critical principle:

> A security control enforced only by the client is not a reliable security boundary.

An attacker does not have to use the intended mobile application.

They can interact directly with the backend API.

## Important Questions

When assessing an application, ask:

* What does the client assume?
* What does the server actually enforce?
* Can backend endpoints be accessed directly?
* Is authentication checked server-side?
* Is authorization checked for every sensitive operation?
* Can API endpoints be called without the intended frontend?
* Are there hidden assumptions about how users interact with the system?

---

# API Enumeration Lessons

This room also improved my understanding of API enumeration.

When working with a web application, it is useful to determine:

1. What endpoints exist?
2. Which HTTP methods are supported?
3. What parameters are required?
4. What data format is expected?
5. What does the application return?
6. Are there related child endpoints?
7. What authentication and authorization controls exist?

For example, an application may expose a structure conceptually similar to:

```text
/api/users
/api/users/{id}
```

Once the relationship is understood, it becomes possible to investigate whether additional resources exist below that structure.

The important idea is to understand the **API structure and application behavior**, rather than blindly guessing endpoints.

---

# Tools and Techniques Used

During the room, I worked with several common web-security techniques and tools.

### Browser Developer Tools

Developer tools were useful for inspecting:

* Network requests.
* HTTP methods.
* API endpoints.
* Request parameters.
* JavaScript files.
* Response data.

A useful habit is to inspect the browser's network activity before immediately reaching for more advanced tooling.

This helps establish how the application actually communicates with its backend.

### Burp Suite

Burp Suite was useful for:

* Intercepting requests.
* Sending requests to Repeater.
* Modifying parameters.
* Testing different HTTP methods.
* Inspecting responses.
* Sending requests to Intruder for controlled enumeration.

### Command-Line Testing

Tools such as `curl` can be useful for reproducing API requests directly from the terminal.

For example, an API may require:

```http
Content-Type: application/json
```

and a JSON request body.

Testing endpoints manually with `curl` helps separate application behavior from browser behavior and improves understanding of the underlying HTTP communication.

### Endpoint Enumeration

Directory and endpoint enumeration can help identify exposed functionality, but this room also demonstrated an important limitation:

> Enumeration tools only find what you successfully identify or what their wordlists contain.

A missed endpoint does not necessarily mean that the functionality does not exist.

Application context, source code, API relationships, and observed behavior should therefore be combined with automated enumeration.

---

# Challenges I Faced

One of the most significant difficulties I experienced in this room was the **Software Supply Chain Failures** task.

The challenge initially provided limited information, which made the intended attack path difficult to understand.

I spent considerable time testing:

* Different request formats.
* HTTP methods.
* JSON parameters.
* Error conditions.
* Endpoint behavior.
* Enumeration approaches.
* `curl` requests.
* Burp Suite requests.

The challenge became much clearer once the relevant source code was available.

The source revealed a debugging condition in which a particular input caused additional debugging information to be returned.

This experience taught me an important practical lesson:

> When automated enumeration and repeated guessing are producing no useful results, stop and reassess the application logic.

Blindly trying more payloads is often less productive than understanding what the application is actually doing.

---

# Lessons From Mistakes

Several mistakes and inefficient approaches during this room became useful learning experiences.

## 1. Relying Too Much on Enumeration

I initially spent a lot of time using automated enumeration and trying many possible values.

This reinforced the importance of understanding the target before increasing the number of requests.

Enumeration is useful, but it should support reasoning rather than replace it.

## 2. Assuming Every Unexpected Result Is the Intended Vulnerability

Some behavior initially appeared similar to vulnerabilities such as IDOR.

However, the actual lesson of the task was related to configuration and information disclosure.

This highlighted the importance of correctly identifying the **root cause and vulnerability category** rather than simply labeling interesting behavior as a known vulnerability.

## 3. Spending Too Long on a Dead End

At several points I continued experimenting with approaches that were not producing useful information.

A better methodology is to establish a hypothesis, test it, and move on when the evidence does not support it.

## 4. Underestimating Source Code

The source code provided a major clue in one of the challenges.

This reinforced the value of reviewing:

* HTML.
* JavaScript.
* API documentation.
* Client-side logic.
* Configuration information.

Even when the page itself appears simple, source code can reveal functionality that is not immediately visible.

---

# Security Mindset Developed

The biggest value of this room was not memorizing four OWASP categories.

It was learning to think more carefully about **why a system becomes vulnerable**.

A useful mindset is:

```text
Application
    ↓
Architecture
    ↓
Configuration
    ↓
Dependencies
    ↓
Cryptography
    ↓
Authentication / Authorization
    ↓
Business Logic
    ↓
API Exposure
```

Each layer can introduce security weaknesses.

A secure application therefore requires security controls across the entire lifecycle.

---

# Practical Exercises

The following exercises can be used to reinforce the concepts from this room.

## Exercise 1 — Error Handling

Create or use a simple web application and test how it responds to:

```text
Invalid IDs
Negative IDs
Large numeric values
Alphabetic input
Special characters
Missing parameters
Unexpected HTTP methods
Malformed JSON
```

Record which responses reveal useful internal information.

The objective is to identify the difference between:

```text
Safe error handling
```

and:

```text
Verbose information disclosure
```

---

## Exercise 2 — Dependency Review

Choose a small Python, JavaScript, or similar project.

Inspect its dependencies and answer:

* Which third-party packages are used?
* Which versions are installed?
* Are they outdated?
* Are any known to contain vulnerabilities?
* Are all dependencies actually required?

The goal is to understand that dependency security is part of application security.

---

## Exercise 3 — Cryptographic Comparison

Study the difference between:

```text
ECB
CBC
GCM
```

Focus on:

* Confidentiality.
* Integrity.
* Authentication.
* Pattern leakage.
* Appropriate use cases.

The objective is to understand **why** certain modes are considered unsafe rather than memorizing that one is "bad."

---

## Exercise 4 — API Security

Create or identify a simple REST API and map its structure.

For example:

```text
/api/users
/api/users/1
/api/users/2
/api/messages
/api/messages/1
```

Then investigate:

* Which endpoints are public?
* Which require authentication?
* Which require authorization?
* Can resources be accessed by changing IDs?
* Does the API rely on assumptions made by the frontend?

This exercise helps connect API enumeration with real application-security architecture.

---

# Key Takeaways

### Security Misconfiguration

Secure software can become vulnerable because of insecure deployment or configuration.

### Software Supply Chain Failures

Third-party dependencies are part of the application's attack surface.

### Cryptographic Failures

Using cryptography incorrectly can provide a false sense of security.

### Insecure Design

Security weaknesses often originate from unsafe architectural assumptions made before implementation begins.

### API Security

Backend APIs must independently enforce authentication, authorization, and security requirements.

### Error Handling

Errors should help legitimate users and developers troubleshoot problems without exposing unnecessary internal information.

### Security Testing

Good testing combines:

```text
Observation
+
Enumeration
+
Source-code analysis
+
HTTP analysis
+
Hypothesis-driven testing
```

rather than relying on one technique alone.

---

# Final Reflection

This room helped me understand that application security is not limited to finding obvious coding vulnerabilities.

A system can fail because:

* It is configured incorrectly.
* It trusts an unsafe dependency.
* It uses cryptography incorrectly.
* It makes insecure architectural assumptions.
* It exposes backend functionality without adequate controls.

The most useful lesson I took from this room is that **secure design starts before exploitation**.

When approaching a new application, I now want to ask:

> What assumptions did the developers make?

> What does the backend actually enforce?

> What information does the application reveal when something goes wrong?

> Which dependencies does it trust?

> How is sensitive data protected?

> Where are the security boundaries?

These questions provide a much stronger foundation for security testing than simply searching for known vulnerabilities.

---

## Room Topics

```text
OWASP Top 10 2025
├── A02 — Security Misconfiguration
├── A03 — Software Supply Chain Failures
├── A04 — Cryptographic Failures
└── A06 — Insecure Design
```

## Skills Practiced

```text
Web Application Reconnaissance
API Enumeration
HTTP Request Analysis
Burp Suite
Developer Tools
Source Code Inspection
Error Analysis
Dependency Security
Cryptographic Analysis
Security Architecture
Threat-Oriented Thinking
```

## Conclusion

The room demonstrated an important principle of modern application security:

**Strong security requires a secure foundation.**

Configuration, dependencies, cryptography, API security, and application architecture all need to work together. Fixing security only at the final stage of development is not enough.

This room strengthened my understanding of how seemingly small design or configuration decisions can create significant security consequences—and how a structured security mindset can be used to identify those weaknesses.
