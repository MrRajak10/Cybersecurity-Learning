# Search Skills - Notes

## Room Summary

The **Search Skills** room teaches how to search for technical information efficiently, evaluate the credibility of online sources, and use specialized cybersecurity resources. Instead of memorizing every command or concept, cybersecurity professionals must know **how to find reliable information quickly**.

---

# Why Search Skills Matter

Research is a daily part of cybersecurity.

Professionals frequently search for:

* Linux commands
* Windows commands
* Error messages
* CVEs
* Exploits
* Malware information
* Security documentation
* Threat intelligence
* Tool documentation
* Configuration guides

Good search skills reduce troubleshooting time and improve investigation accuracy.

---

# Evaluating Search Results

Not every search result is trustworthy.

Before relying on information, consider:

* Is the source reputable?
* Is evidence provided?
* Does the explanation make logical sense?
* Can the information be verified from multiple sources?
* Is there any obvious bias?

For simple tasks (such as checking a Linux command), quick verification may be enough.

For security decisions, always verify information from multiple reliable sources.

---

# Search Engine Operators

Search operators make searches more precise.

### Exact Phrase

Use quotation marks to search for an exact phrase.

Example:

```text
"passive reconnaissance"
```

---

### Search Within a Website

Limit results to a specific website.

Example:

```text
site:tryhackme.com reconnaissance
```

---

### Exclude Words

Remove unwanted topics from search results.

Example:

```text
pyramids -tourism
```

---

### Search by File Type

Find specific document types.

Example:

```text
filetype:pdf cyber warfare
```

Useful file types include:

* PDF
* DOC
* DOCX
* XLS
* PPT

---

# Specialized Search Engines

## Shodan

Searches for internet-connected devices.

Useful for:

* Open ports
* Running services
* Server banners
* Device information

---

## Censys

Searches internet hosts, websites, and certificates.

Useful for:

* Internet exposure
* Certificates
* Hosts
* Domains

---

## VirusTotal

Analyzes:

* Files
* URLs
* Domains
* IP addresses
* File hashes

Checks submissions using multiple security engines to determine whether they have been identified as malicious.

---

## Have I Been Pwned

Checks whether an email address has appeared in known public data breaches.

Useful for:

* Personal security
* Password hygiene
* Breach awareness

---

# Vulnerability Research

## CVE

A **Common Vulnerabilities and Exposures (CVE)** identifier is a unique ID assigned to a publicly disclosed security vulnerability.

Example:

```text
CVE-2024-3094
```

---

## National Vulnerability Database (NVD)

Provides:

* Vulnerability description
* Severity
* References
* Affected software
* Technical details

---

## Exploit Database

Contains:

* Public exploits
* Proof-of-concept code
* Exploit references

Useful during vulnerability research and penetration testing.

---

## GitHub

Commonly used to find:

* Security tools
* Proof-of-concept exploits
* Detection rules
* Research projects
* Scripts

Always verify repositories before trusting or using their contents.

---

# Technical Documentation

Official documentation should usually be the first resource consulted.

Examples include:

* Linux manual pages
* Microsoft documentation
* Official product documentation

---

## Linux Manual Pages

Display documentation using:

```bash
man <command>
```

Example:

```bash
man cat
```

Manual pages typically include:

* Description
* Syntax
* Options
* Examples

---

## Command Help

Some commands also support:

```bash
--help
```

or

```bash
-h
```

Example:

```bash
ip --help
```

---

# Microsoft Documentation

Official Microsoft documentation provides information about:

* Windows commands
* PowerShell
* Windows Server
* Active Directory
* Azure
* Microsoft Defender
* Networking

Official documentation is generally more reliable than third-party tutorials.

---

# Official Product Documentation

Many products provide official documentation.

Examples:

* Apache HTTP Server
* Snort
* PHP
* Nginx
* Docker
* Kubernetes

Reading official documentation improves understanding and reduces reliance on unofficial sources.

---

# Social Media in Cybersecurity

Social media can support:

* Threat intelligence
* OSINT
* Company research
* Employee research
* Security news
* Community learning

However, excessive public information may also increase security risks.

Always consider privacy when sharing personal information online.

---

# Important Takeaways

* Strong search skills are essential in cybersecurity.
* Verify information before trusting it.
* Use search operators to improve search accuracy.
* Prefer official documentation whenever possible.
* Specialized search engines provide targeted security information.
* Research skills improve with consistent practice.

---

# Practice Exercises

## Exercise 1

Search for a Linux command using:

* Google
* Official documentation
* AI assistant

Compare the results.

---

## Exercise 2

Practice using:

* Exact phrase search
* `site:`
* `filetype:`
* Exclusion (`-`)

Observe how search results change.

---

## Exercise 3

Research a public CVE and identify:

* Description
* Severity
* Affected software
* Mitigation
* Public exploit availability

---

## Exercise 4

Search a file hash or URL using VirusTotal and review the available analysis.

---

## Exercise 5

Read the official documentation for one Linux command and summarize its most commonly used options.

---

# Personal Learning Reflection

This room reinforced that successful cybersecurity professionals are not expected to memorize everything. Instead, they develop the ability to locate reliable information quickly, verify its accuracy, and apply it effectively. Strong research habits save time, improve technical understanding, and support better decision-making across all cybersecurity roles.
