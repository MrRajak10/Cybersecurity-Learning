# DNS in Detail

## Room Overview

This room introduced the fundamentals of the Domain Name System (DNS), one of the most important services on the internet. The room explained how DNS translates human-readable domain names into IP addresses, how domain names are structured, the different types of DNS records, and how DNS requests travel across the internet to find the correct answer.

Rather than focusing only on answering the room questions, I used this room as an opportunity to understand what happens behind the scenes every time I open a website in my browser.

---

## What is DNS?

DNS stands for Domain Name System.

Computers communicate using IP addresses, but remembering numerical addresses for every website would be extremely difficult for humans. DNS solves this problem by acting like the internet's phonebook.

For example:

* Human-friendly name: `tryhackme.com`
* IP address: `104.26.10.229`

Instead of remembering numbers, users can simply remember domain names and DNS handles the translation process.

### My Learning Experience

Before this room, I knew that DNS somehow converted domain names into IP addresses, but I never really understood how that process worked. This room helped me connect the website names I type every day with the actual servers that host them.

It was interesting to realize that every website visit begins with a DNS lookup before any webpage can even load.

---

## Understanding Domain Hierarchy

DNS follows a hierarchical structure.

### Top-Level Domain (TLD)

The TLD is the rightmost portion of a domain name.

Examples:

* `.com`
* `.org`
* `.edu`
* `.gov`
* `.net`

There are two major categories:

#### Generic Top-Level Domains (gTLD)

Examples:

* `.com`
* `.org`
* `.edu`
* `.gov`

Originally these indicated the purpose of a website.

#### Country Code Top-Level Domains (ccTLD)

Examples:

* `.in`
* `.ca`
* `.uk`
* `.co.uk`

These represent specific countries or geographical regions.

### Second-Level Domain (SLD)

In:

`tryhackme.com`

The Second-Level Domain is:

`tryhackme`

This is usually the name registered by an individual, company, or organization.

### Subdomain

A subdomain appears before the Second-Level Domain.

Example:

`admin.tryhackme.com`

Here:

`admin` is the subdomain.

Additional examples:

* blog.example.com
* mail.example.com
* support.example.com

Organizations use subdomains to separate different services while keeping them under the same domain.

### My Learning Experience

The domain hierarchy section cleared up a confusion I had for a long time. I had seen addresses like:

* mail.google.com
* accounts.google.com
* docs.google.com

but never fully understood that these were subdomains rather than completely separate websites.

After learning the hierarchy structure, domain names started making much more sense when looking at web applications and online services.

---

## DNS Record Types

DNS stores different types of records depending on the information being requested.

### A Record

Maps a domain name to an IPv4 address.

Example:

```text
tryhackme.com → 104.26.10.229
```

### AAAA Record

Maps a domain name to an IPv6 address.

Example:

```text
2606:4700:20::681a:be5
```

### CNAME Record

Points one domain name to another domain name.

Example:

```text
store.tryhackme.com
      ↓
shops.shopify.com
```

The DNS system must then resolve the second domain name to find its IP address.

### MX Record

Mail Exchange records specify which servers handle email for a domain.

Example:

```text
alt1.aspmx.l.google.com
```

MX records also contain priority values.

Lower priority numbers are usually attempted first.

### TXT Record

TXT records store text-based information.

Common uses:

* SPF records
* DMARC policies
* Domain ownership verification
* Email authentication

### My Learning Experience

The most useful part for me was understanding MX and TXT records.

I had previously seen SPF, DMARC, and TXT records mentioned in cybersecurity discussions but never understood where they came from.

After this room, I understood that many email security mechanisms rely on DNS records behind the scenes. This helped me connect DNS concepts with real-world security practices.

---

## How DNS Resolution Works

One of the most valuable lessons from this room was learning the complete DNS lookup process.

### Step 1: Local Cache Check

The computer first checks its local DNS cache.

If a recent answer exists, the process stops here.

### Step 2: Recursive DNS Server

If no local record exists, the request is sent to a Recursive DNS Server.

This server is usually provided by the ISP.

Examples:

* Google DNS
* Cloudflare DNS
* ISP DNS servers

### Step 3: Root DNS Server

The recursive server asks a Root DNS Server where to find the appropriate Top-Level Domain server.

Example:

For `tryhackme.com`, the root server points toward the `.com` TLD servers.

### Step 4: TLD Server

The TLD server identifies the Authoritative Name Server responsible for the domain.

### Step 5: Authoritative DNS Server

The Authoritative Server contains the actual DNS records.

It returns the requested information.

Example:

```text
tryhackme.com → 104.26.10.229
```

### Step 6: Response and Caching

The answer is returned:

* Authoritative Server
* Recursive Server
* Client

The recursive server stores the result for future requests.

---

## TTL (Time To Live)

TTL determines how long a DNS response remains cached.

Example:

```text
TTL = 3600
```

This means the record can remain cached for 3600 seconds (1 hour).

Caching improves:

* Performance
* Speed
* Scalability
* Reduced DNS traffic

### My Learning Experience

The TTL concept helped me understand why DNS changes sometimes take time to appear across the internet.

Previously, I assumed DNS updates happened instantly. After learning about caching and TTL values, I understood why administrators often talk about "waiting for DNS propagation."

---

## Practical DNS Investigation

In the practical section, I performed DNS lookups and explored different record types.

Activities included:

* Looking up CNAME records
* Viewing TXT records
* Checking MX records
* Identifying mail priorities
* Resolving A records

This practical exercise reinforced the theory taught throughout the room and showed how DNS information can be gathered directly from live queries.

### My Learning Experience

The practical section made the room much more engaging.

Instead of simply reading about record types, I was able to see real DNS responses and understand how each record appears during an actual lookup.

This helped bridge the gap between theory and practical usage.

---

## Key Takeaways

* DNS translates domain names into IP addresses.
* TLDs, SLDs, and Subdomains form the DNS hierarchy.
* A records map domains to IPv4 addresses.
* AAAA records map domains to IPv6 addresses.
* CNAME records point domains to other domains.
* MX records control email delivery.
* TXT records store verification and security information.
* Recursive DNS Servers perform lookups on behalf of clients.
* Root, TLD, and Authoritative Servers work together to resolve requests.
* TTL values determine cache duration.

---

## Final Thoughts

This room provided a strong foundation in DNS fundamentals and helped me understand one of the most important services that powers the internet. The biggest lesson for me was realizing how many steps occur behind the scenes before a website loads in a browser.

As someone learning cybersecurity, understanding DNS is important because DNS appears everywhere—from web applications and network troubleshooting to threat hunting, phishing investigations, email security, and penetration testing.

This room transformed DNS from a concept I had heard about into a process I can now visualize and explain with confidence.
