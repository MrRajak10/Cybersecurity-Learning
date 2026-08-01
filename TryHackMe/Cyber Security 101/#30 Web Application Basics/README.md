# TryHackMe — Web Application Basics

## Overview

This repository documents my learning journey through the **Web Application Basics** room on TryHackMe.

The purpose of this repository is to build a strong foundation in how web applications work before moving into web application security, penetration testing, and bug bounty hunting. Rather than focusing on challenge answers or flags, these notes focus on understanding the concepts that every cybersecurity beginner should know.

This repository is intended for educational purposes only.

---

## Learning Objectives

During this room I learned:

* How a web application works
* The difference between Front-end and Back-end
* The structure of a URL
* How browsers communicate with web servers
* HTTP Requests and Responses
* HTTP Methods
* HTTP Status Codes
* Request Headers and Response Headers
* Request and Response Bodies
* Security Headers
* Basic HTTP request manipulation

---

## Topics Covered

### Web Application Overview

* Front-end
* Back-end
* Database
* Web Server
* Web Application Firewall (WAF)

### URL Structure

* Scheme
* User Information
* Host / Domain
* Port
* Path
* Query String
* Fragment

### HTTP Communication

* HTTP Request
* HTTP Response
* Request Line
* Status Line
* Headers
* Body

### HTTP Methods

* GET
* POST
* PUT
* PATCH
* DELETE
* HEAD
* OPTIONS

### HTTP Status Codes

* 1xx Informational
* 2xx Success
* 3xx Redirection
* 4xx Client Error
* 5xx Server Error

### HTTP Headers

Request Headers

* Host
* User-Agent
* Referer
* Cookie
* Content-Type

Response Headers

* Content-Type
* Content-Length
* Date
* Server
* Set-Cookie
* Cache-Control
* Location

### Security Headers

* Content-Security-Policy (CSP)
* Strict-Transport-Security (HSTS)
* X-Content-Type-Options
* Referrer-Policy

---

## Practical Skills Learned

During this room I practiced:

* Reading and understanding URLs
* Identifying different HTTP methods
* Understanding browser-server communication
* Reading HTTP Requests
* Reading HTTP Responses
* Identifying common HTTP headers
* Understanding response status codes
* Performing basic GET requests
* Performing POST requests
* Performing DELETE requests

---

## Key Takeaways

* Every web application consists of a client and a server communicating over HTTP or HTTPS.
* The browser acts as the client while the web server processes requests and returns responses.
* Understanding HTTP is essential before learning web vulnerabilities.
* URLs contain multiple components that each have a specific purpose.
* HTTP methods define what action should be performed on a resource.
* Status codes help identify whether a request succeeded or failed.
* Headers carry important metadata that controls communication.
* Security headers provide an additional layer of defense against common web attacks.
* HTTPS protects data in transit through encryption.
* Small implementation mistakes can introduce security vulnerabilities.

---

## Challenges Encountered

While completing this room, I found that:

* Understanding the complete URL structure required careful attention.
* Differentiating Request Headers from Response Headers took practice.
* Remembering when each HTTP method is used required repetition.
* Security headers initially seemed confusing until I understood the problems they solve.
* Some concepts became much clearer after observing practical request examples.

---

## Lessons Learned

This room reinforced several important lessons:

* Strong cybersecurity knowledge starts with strong networking and web fundamentals.
* Before learning attacks, it is important to understand normal application behavior.
* Every HTTP request contains useful information for defenders and attackers alike.
* Security is built into every layer of a web application—not just authentication.
* Reading documentation carefully is as important as completing practical exercises.

---

## Recommended Next Topics

After completing this room, good next topics include:

* HTTP Cookies
* Sessions
* Authentication
* Authorization
* Burp Suite
* OWASP Top 10
* Cross-Site Scripting (XSS)
* SQL Injection
* Cross-Site Request Forgery (CSRF)
* IDOR
* Web Proxies

---

## Educational Disclaimer

This repository is intended for learning and documentation purposes only.

No challenge solutions, flags, or walkthrough answers are included. The focus is understanding concepts and building a strong cybersecurity foundation.
