# Putting It All Together - TryHackMe

## Room Overview

This room brings together all the fundamental web concepts covered in previous modules and demonstrates how different web technologies work together to deliver a website to users. Instead of learning individual components separately, this room helped me understand the complete journey of a web request, from entering a domain name in a browser to receiving a fully rendered webpage.

The room covers important concepts such as DNS, HTTP, Load Balancers, CDNs, Databases, WAFs, Web Servers, Virtual Hosts, Static Content, Dynamic Content, and Backend Technologies.

---

## Learning Objectives

By completing this room, I learned:

* How a browser communicates with a website
* The role of DNS in finding a website's IP address
* How HTTP is used for web communication
* How Load Balancers distribute traffic across multiple servers
* How CDNs improve website speed and performance
* Why websites use databases
* How WAFs help protect web applications
* How web servers deliver content to users
* The difference between static and dynamic content
* The purpose of backend programming languages
* The complete lifecycle of a web request

---

## Key Concepts Learned

### DNS (Domain Name System)

DNS acts like the internet's phonebook. When a user enters a domain name into a browser, DNS translates that human-readable name into an IP address that computers can understand.

Without DNS, users would need to remember numerical IP addresses for every website they visit.

---

### HTTP (HyperText Transfer Protocol)

HTTP is the communication protocol used between a browser and a web server.

The browser sends requests, and the server responds with resources such as:

* HTML
* CSS
* JavaScript
* Images
* Videos

These resources are then rendered by the browser to display the website.

---

### Load Balancers

Load Balancers help websites handle large amounts of traffic by distributing requests across multiple servers.

Some common balancing methods include:

* Round Robin
* Weighted Distribution

Load Balancers also perform health checks to determine whether servers are functioning properly.

If a server becomes unavailable, traffic is automatically redirected to healthy servers.

#### What I Learned

Before this room, I thought a website usually ran on a single server. Learning about Load Balancers helped me understand how large platforms remain available even when one server fails.

---

### Content Delivery Networks (CDNs)

CDNs store static content on servers distributed across different geographical locations.

Instead of downloading content from a distant server, users receive files from the nearest CDN server.

Benefits include:

* Faster loading times
* Reduced latency
* Lower load on the main server
* Improved user experience

Examples of static content:

* Images
* CSS files
* JavaScript files
* Videos

#### What I Learned

The CDN concept helped me understand why global services like streaming platforms can deliver content quickly to users worldwide.

---

### Databases

Databases allow websites to store and retrieve information.

Common examples include:

* MySQL
* MSSQL
* MongoDB
* PostgreSQL

Databases store:

* User accounts
* Password hashes
* Blog posts
* Product information
* Application data

#### What I Learned

This room helped me realize that websites are not simply collections of pages. Most modern websites rely heavily on databases to generate content dynamically.

---

### Web Application Firewall (WAF)

A WAF sits between users and web servers.

Its purpose is to detect and block malicious requests before they reach the web application.

Common protections include:

* Attack detection
* Bot filtering
* Rate limiting
* Denial-of-Service protection

#### What I Learned

As someone interested in cybersecurity, this was one of the most interesting concepts because it showed how websites defend themselves against common web-based attacks.

---

## How Web Servers Work

A web server listens for incoming requests and responds with web content.

Common web servers include:

* Apache
* Nginx
* IIS
* NodeJS

Web servers deliver files from a root directory configured on the server.

Examples:

Linux:

* /var/www/html

Windows:

* C:\inetpub\wwwroot

---

## Virtual Hosts

Virtual Hosts allow a single web server to host multiple websites.

The web server checks the hostname in the incoming HTTP request and serves the appropriate website based on its configuration.

Example:

* one.com → /var/www/website_one
* two.com → /var/www/website_two

#### What I Learned

I found it surprising that one server can host many websites simultaneously. This helped me understand how hosting providers manage multiple websites on the same infrastructure.

---

## Static vs Dynamic Content

### Static Content

Content that remains unchanged.

Examples:

* Images
* CSS
* JavaScript
* Fixed HTML pages

### Dynamic Content

Content that changes based on:

* User input
* Database information
* Search queries
* Application logic

Examples:

* Search results
* Social media feeds
* Blog homepages
* User dashboards

#### What I Learned

This section connected many previous concepts together. I finally understood why websites need databases and backend languages to generate personalized content.

---

## Backend Languages

Backend languages process information behind the scenes and generate content for users.

Examples include:

* PHP
* Python
* Ruby
* NodeJS
* Perl

Backend applications can:

* Communicate with databases
* Process user input
* Generate dynamic pages
* Connect to external services

The user only sees the final output, not the backend code itself.

---

## Practical Understanding

One of the most valuable parts of this room was understanding the complete flow of a web request.

A simplified request flow:

1. User enters a website URL
2. Browser checks local DNS cache
3. DNS resolves the domain name
4. Request passes through security controls such as a WAF
5. Load Balancer distributes the request
6. Web Server receives the request
7. Backend application processes data
8. Database is queried if necessary
9. Response is generated
10. Browser renders the website

This process helped me connect all previous web concepts into one complete picture.

---

## Challenges Faced

While completing the room, I initially understood each technology individually but struggled to visualize how they worked together during a real web request.

The final request-flow exercise helped me connect the entire process from DNS resolution to webpage rendering.

Another challenge was remembering where components such as WAFs, Load Balancers, Databases, and CDNs fit into the request path. After working through the room and reviewing the flow multiple times, the architecture became much clearer.

---

## Key Takeaways

* DNS translates domain names into IP addresses.
* HTTP enables communication between browsers and servers.
* Load Balancers improve availability and distribute traffic.
* CDNs improve performance by serving content closer to users.
* Databases store and retrieve website information.
* WAFs protect applications from malicious traffic.
* Web Servers deliver website content.
* Virtual Hosts allow multiple websites on one server.
* Static content remains unchanged.
* Dynamic content is generated through backend processing.
* Modern websites rely on multiple technologies working together.

---

## Final Thoughts

This room served as an excellent summary of the foundational web concepts covered throughout the learning path. Instead of introducing completely new topics, it helped reinforce existing knowledge and showed how every component fits together in a real-world web environment.

For me, the biggest lesson was understanding that when a website loads, dozens of technologies work together behind the scenes. Seeing the complete request lifecycle made many previously separate concepts finally click together and gave me a much clearer understanding of how modern web applications operate.
