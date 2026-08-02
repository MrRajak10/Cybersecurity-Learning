# Burp Suite: The Basics — TryHackMe

> A beginner-focused learning repository documenting my journey through the **Burp Suite: The Basics** room on TryHackMe.

---

## Overview

This repository documents my learning experience while completing the **Burp Suite: The Basics** room on TryHackMe.

Instead of focusing only on challenge answers or walkthrough steps, this repository focuses on understanding how Burp Suite works, why penetration testers use it, and how its core features are applied during web application security testing.

The room introduces Burp Suite as one of the most important tools used in web application penetration testing and bug bounty hunting. Throughout the room, I learned how Burp Suite intercepts HTTP/HTTPS traffic, how different modules work together, how browsers communicate through Burp Proxy, and how manual testing becomes possible by modifying requests before they reach the target server.

---

# Learning Objectives

After completing this room, I understood:

* What Burp Suite is and why it is considered an industry-standard web application testing tool.
* How Burp Suite acts as an intercepting proxy between a browser and a web server.
* The difference between Community, Professional, and Enterprise editions.
* The purpose of Burp Suite's most important modules.
* How HTTP requests and responses can be intercepted and modified.
* How to configure a browser to communicate through Burp Proxy.
* How Site Map helps visualize an application's attack surface.
* Why Scope is important during professional penetration tests.
* The basics of intercepting HTTPS traffic.
* How a simple client-side filter can be bypassed by modifying intercepted requests.
* The role Burp Suite plays during vulnerability assessment and penetration testing.

---

# Topics Covered

* Burp Suite Introduction
* Burp Suite Editions
* Burp Proxy
* Repeater
* Intruder
* Decoder
* Comparer
* Sequencer
* Installation Basics
* Dashboard Navigation
* Burp Settings
* Event Log
* HTTP History
* Browser Configuration
* FoxyProxy
* Burp Browser
* Site Map
* Scope
* Issue Definitions
* HTTPS Proxying
* Request Interception
* Response Interception
* Match and Replace
* Basic XSS Demonstration

---

# Burp Suite Editions

During this room I learned that Burp Suite is available in multiple editions.

### Community Edition

* Free version
* Ideal for beginners
* Includes manual testing features
* Perfect for learning Burp Suite fundamentals

### Professional Edition

* Paid version
* Includes automated vulnerability scanner
* Project saving
* Reporting features
* Additional automation capabilities

### Enterprise Edition

* Server-based deployment
* Designed for organizations
* Continuous scanning
* Enterprise security testing

---

# Important Burp Suite Modules Learned

## Proxy

The Proxy module is the heart of Burp Suite.

It allows a penetration tester to intercept traffic between the browser and the web server before the request reaches its destination.

Using Proxy, requests can be:

* Intercepted
* Viewed
* Modified
* Dropped
* Forwarded

---

## Repeater

Repeater allows sending the same HTTP request repeatedly after making manual modifications.

It is commonly used during:

* SQL Injection testing
* Authentication testing
* Parameter manipulation
* Manual vulnerability verification

---

## Intruder

Intruder automates sending multiple payloads against a target.

Typical use cases include:

* Brute force attacks
* Login testing
* Fuzzing
* Parameter discovery

---

## Decoder

Decoder converts data between different formats.

Examples include:

* URL Encoding
* URL Decoding
* Base64 Encoding
* Base64 Decoding

---

## Comparer

Comparer highlights differences between two requests or responses.

Useful when:

* Comparing application behavior
* Authorization testing
* Response analysis

---

## Sequencer

Sequencer evaluates randomness of tokens.

Typical targets include:

* Session Cookies
* CSRF Tokens
* Session IDs

The objective is to determine whether generated tokens are sufficiently random.

---

# Practical Concepts Learned

During this room I practiced:

* Intercepting browser requests
* Forwarding requests
* Dropping requests
* Viewing HTTP History
* Using Site Map
* Setting Scope
* Configuring browser proxy settings
* Understanding HTTPS interception
* Modifying intercepted requests
* Observing server responses

---

# Hands-on Activities

This room included practical exercises involving:

* Browser proxy configuration
* FoxyProxy setup
* Intercepting requests
* Exploring application endpoints
* Using Site Map
* Scope configuration
* Basic reflected XSS demonstration

These activities helped connect theory with practical web application testing.

---

# Key Takeaways

* Burp Suite is much more than a proxy; it is a complete web application testing platform.
* Understanding HTTP requests and responses is essential before using Burp effectively.
* Manual testing provides deep insight into how applications behave.
* Scope configuration helps reduce unnecessary traffic and keeps assessments focused.
* Site Map provides an excellent overview of application structure.
* Learning Burp Suite requires continuous practice rather than memorization.

---

# Beginner Practice Suggestions

To reinforce the concepts from this room, try the following exercises:

1. Configure Burp Suite with your browser and intercept a request.
2. Turn interception on and observe how browser requests pause.
3. Forward requests one by one and watch the page load.
4. Compare GET and POST requests in HTTP History.
5. Visit multiple pages of a practice website and inspect the generated Site Map.
6. Configure Scope and observe how captured traffic changes.
7. Send a request to Repeater and modify individual parameters.
8. Practice URL encoding and decoding using Decoder.
9. Compare two different responses using Comparer.
10. Explore Burp's interface until navigating between modules becomes natural.

---

# Skills Gained

* Web Application Testing Fundamentals
* HTTP Request Analysis
* HTTP Response Analysis
* Proxy Configuration
* Request Manipulation
* Browser Proxying
* Traffic Inspection
* Basic Vulnerability Testing Workflow
* Burp Suite Navigation
* Beginner Web Pentesting Concepts

---

# Prerequisites

A basic understanding of:

* HTTP
* HTTPS
* Web Browsers
* Client-Server Communication

will make this room easier to understand.

---

# Conclusion

This room serves as an excellent introduction to Burp Suite and lays the foundation for future web application security learning. Rather than teaching advanced attacks immediately, it focuses on understanding how requests flow between browsers and servers and how Burp Suite gives security professionals visibility and control over that communication.

Mastering these fundamentals is essential before moving to more advanced Burp Suite modules and web exploitation techniques.
