# How Websites Work - TryHackMe

## Overview

This repository documents my learning journey through the **How Websites Work** room on TryHackMe. The room introduces the fundamental technologies used to build websites and explains how users interact with web applications through browsers and web servers. It also provides an introduction to common web security issues such as Sensitive Data Exposure and HTML Injection.

Rather than focusing only on solving the room, this repository focuses on understanding the concepts behind the tasks and how they relate to real-world web application security.

---

# Learning Objectives

After completing this room, I was able to:

* Understand how browsers communicate with web servers.
* Differentiate between Front-End and Back-End components.
* Understand the purpose of HTML, CSS, and JavaScript.
* Read and analyze basic HTML code.
* Understand how JavaScript adds interactivity to websites.
* Identify exposed information within webpage source code.
* Understand how HTML Injection vulnerabilities occur.
* Recognize the importance of input sanitization.

---

# Room Topics Covered

## 1. How Websites Work

Every website interaction begins with a request and response process.

When a user visits a website, the browser sends a request to a web server. The web server processes that request and sends back data that the browser uses to display the webpage.

### Key Components

### Front-End (Client-Side)

The Front-End is everything visible to the user.

Examples:

* Text
* Images
* Buttons
* Forms
* Menus
* Layouts

This is what the browser renders and displays.

### Back-End (Server-Side)

The Back-End handles processing behind the scenes.

Examples:

* User authentication
* Database operations
* Business logic
* Data processing

The server receives requests, performs the necessary operations, and returns responses to the browser.

### What I Learned

Before this room, I used websites every day without thinking about what happens behind the scenes. This room helped me understand that every webpage I open starts with a request from my browser and a response from a web server. Understanding this simple communication flow made many web security concepts easier to understand later.

---

## 2. HTML Fundamentals

HTML (HyperText Markup Language) is the foundation of every webpage.

HTML defines the structure and content of a website.

### Common HTML Elements

| Element    | Purpose                  |
| ---------- | ------------------------ |
| `<html>`   | Root element of the page |
| `<head>`   | Stores page information  |
| `<title>`  | Sets page title          |
| `<body>`   | Contains visible content |
| `<h1>`     | Main heading             |
| `<p>`      | Paragraph                |
| `<img>`    | Displays images          |
| `<button>` | Creates buttons          |

### HTML Attributes

Attributes provide additional information about elements.

Examples:

* `class`
* `id`
* `src`

### Understanding IDs and Classes

#### Class

A class can be reused by multiple elements.

Example:

```html
<p class="text">
```

#### ID

An ID must be unique.

Example:

```html
<p id="example">
```

IDs are commonly used by JavaScript to identify specific elements.

### Practical Activities Completed

* Rendered HTML content.
* Fixed a broken image.
* Added a new image element.
* Worked with image source attributes.

### What I Learned

This was one of the most useful sections for me because I realized that websites are built from small building blocks called elements. I had seen HTML code before, but this room helped me understand the purpose of tags, attributes, IDs, and classes in a practical way.

Fixing the broken image also showed me how important file paths and source attributes are in web development.

---

## 3. JavaScript Basics

JavaScript is responsible for making websites interactive.

Without JavaScript, webpages would mostly be static.

### Common JavaScript Capabilities

* Updating webpage content
* Reacting to button clicks
* Animations
* Form validation
* Dynamic page updates

### Example Concept

JavaScript can locate an HTML element and change its contents dynamically.

For example:

* Find an element by its ID.
* Modify the text displayed on the page.
* Respond to user actions.

### Events

Events allow JavaScript to react to user actions.

Common events include:

* onclick
* onhover
* onsubmit

### Practical Activities Completed

* Modified webpage content using JavaScript.
* Changed text dynamically.
* Triggered actions through button clicks.
* Worked with event-based interactions.

### What I Learned

This section helped me understand that HTML creates the structure, but JavaScript controls behavior.

The most interesting part was seeing webpage content change instantly after clicking a button. It made me realize how modern websites rely heavily on JavaScript to create interactive user experiences.

---

## 4. Sensitive Data Exposure

Sensitive Data Exposure occurs when information that should remain hidden becomes accessible to users.

This information is often found in:

* HTML source code
* JavaScript files
* Comments
* Hidden links
* Configuration files

### Examples of Exposed Information

* Usernames
* Passwords
* API Keys
* Internal URLs
* Administrative paths

### Why This Matters

Attackers often inspect webpage source code before attempting more advanced attacks.

Even small pieces of exposed information can help an attacker gain additional access.

### Practical Activity Completed

* Viewed webpage source code.
* Located hidden credentials inside HTML comments.
* Used discovered information to access the application.

### What I Learned

This was probably the biggest eye-opening moment of the room.

I always assumed that if information was not visible on a webpage, users could not access it. This task showed me that hidden does not always mean secure.

I learned why security professionals frequently inspect source code during web application assessments. Sometimes sensitive information is accidentally left behind by developers and can become an entry point for attackers.

---

## 5. HTML Injection

HTML Injection occurs when user input is displayed on a webpage without proper filtering.

If user input is not sanitized, attackers can inject their own HTML code into the page.

### How HTML Injection Works

1. User submits input.
2. Application accepts input.
3. Input is displayed without validation.
4. Browser interprets injected HTML.
5. Attacker gains control over page content.

### Risks

HTML Injection can allow attackers to:

* Modify webpage content.
* Insert malicious links.
* Mislead users.
* Prepare for more advanced attacks.

### Importance of Input Sanitization

Developers should never trust user input.

All user-supplied data should be validated and sanitized before being processed or displayed.

### Practical Activity Completed

* Injected HTML into a vulnerable form.
* Created a custom hyperlink.
* Observed how unsanitized input changed webpage behavior.

### What I Learned

This task helped me understand how dangerous user-controlled input can be.

At first, it seemed harmless that a website simply displayed what users entered. However, after seeing HTML Injection in action, I understood how attackers can manipulate webpage content if proper validation is missing.

The lesson "Never Trust User Input" became much more meaningful after completing this exercise.

---

# Key Security Concepts Learned

* Front-End vs Back-End
* HTML Structure
* JavaScript Interactivity
* Page Source Analysis
* Sensitive Data Exposure
* HTML Injection
* Input Sanitization
* Basic Web Application Security

---

# Beginner Takeaways

* Every website operates through requests and responses.
* HTML provides structure.
* CSS provides styling.
* JavaScript provides functionality.
* Always inspect source code during assessments.
* Hidden information can sometimes be exposed in comments or scripts.
* User input should never be trusted.
* Input validation and sanitization are critical security controls.

---

# Personal Reflection

This room provided an excellent introduction to both web technologies and web security fundamentals.

The room started with basic concepts such as browser-server communication and gradually introduced real security issues that can occur when websites are not developed securely.

The most valuable lesson for me was learning that security issues are often caused by simple mistakes. Something as small as leaving credentials inside source code comments or failing to sanitize user input can create serious vulnerabilities.

By the end of the room, I had a much clearer understanding of how websites function behind the scenes and why understanding web technologies is essential for anyone pursuing cybersecurity, penetration testing, or web application security.

This room strengthened my foundation and gave me confidence to continue learning more advanced web security topics in future TryHackMe rooms.
