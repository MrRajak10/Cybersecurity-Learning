# TryHackMe - Active Directory

## Overview

This repository documents my learning journey through the **Active Directory** room on TryHackMe. The goal of this room is to build a beginner-friendly understanding of how Windows domains work, how Active Directory manages users and computers, and how administrators use centralized management to control an enterprise environment.

This repository focuses on **learning the concepts**, understanding **why they matter**, and documenting the practical activities completed during the room. It is **not intended to be a flag walkthrough**.

---

# Learning Objectives

After completing this room, I was able to understand:

* What Active Directory (AD) is
* Why organizations use Windows Domains
* The purpose of a Domain Controller (DC)
* How users, computers, and groups are managed centrally
* Organizational Units (OUs) and why they exist
* Active Directory security groups
* Delegation of administrative permissions
* Managing users and computers inside AD
* Group Policy Objects (GPOs)
* Kerberos authentication
* NTLM authentication
* Trees, Forests, and Trust Relationships

---

# Skills Practiced

* Navigating Active Directory Users and Computers
* Creating and managing Organizational Units
* Managing user accounts
* Managing computer accounts
* Understanding machine accounts
* Working with Active Directory groups
* Delegating administrative privileges
* Resetting passwords using PowerShell
* Creating and linking Group Policy Objects
* Applying security policies
* Organizing enterprise resources
* Understanding enterprise authentication

---

# Key Concepts Learned

## Windows Domain

A Windows Domain allows an organization to manage many computers and users from a single centralized location instead of configuring every computer individually.

Instead of visiting every employee's computer, administrators manage everything from the Domain Controller.

---

## Active Directory

Active Directory is the central database that stores information about users, computers, printers, groups, and many other objects inside the network.

It acts as the identity management system for a Windows enterprise environment.

---

## Domain Controller (DC)

The Domain Controller is the server that runs Active Directory Domain Services (AD DS).

Its responsibilities include:

* Authenticating users
* Managing domain resources
* Applying policies
* Storing domain information
* Managing permissions

---

## Organizational Units (OU)

Organizational Units are containers used to organize users and computers.

They make administration easier by allowing different departments to receive different policies.

Example departments:

* Management
* Sales
* Marketing
* IT

---

## Active Directory Groups

Some important built-in groups include:

* Domain Admins
* Server Operators
* Backup Operators
* Account Operators
* Domain Users
* Domain Computers
* Domain Controllers

Each group has different administrative responsibilities.

---

## Delegation

Delegation allows administrators to give specific permissions to selected users without making them Domain Administrators.

Example:

A department manager can reset employee passwords without having full administrative control over the entire domain.

---

## Managing Computers

Computers should be organized into separate OUs based on their role.

Examples include:

* Workstations
* Servers
* Domain Controllers

This allows different security policies to be applied to different systems.

---

## Group Policy Objects (GPO)

Group Policy Objects allow administrators to configure security settings across many computers.

Examples include:

* Password policies
* Lock screen settings
* Restricting Control Panel
* Desktop settings
* Security configurations

A single policy can automatically affect hundreds or thousands of computers.

---

## Authentication

This room introduced two authentication protocols.

### Kerberos

* Modern authentication protocol
* Default authentication method in Active Directory
* Uses Ticket Granting Tickets (TGT) and Ticket Granting Service (TGS)

### NTLM

* Legacy authentication protocol
* Maintained for backward compatibility
* Uses a challenge-response mechanism
* Passwords are never sent across the network in plain text

---

## Trees and Forests

As organizations grow, multiple domains may exist.

A collection of domains sharing the same namespace forms a **Tree**.

Multiple trees with different namespaces connected together form a **Forest**.

Trust relationships allow users from one domain to access resources in another domain.

---

# Practical Activities Completed

During this room I practiced:

* Exploring Active Directory Users and Computers
* Viewing Organizational Units
* Removing unnecessary objects
* Creating Organizational Units
* Delegating permissions
* Resetting user passwords
* Using PowerShell for account management
* Creating Group Policy Objects
* Linking GPOs to Organizational Units
* Restricting Control Panel access
* Organizing workstations and servers
* Exploring Group Policy Management

---

# Biggest Takeaways

* Active Directory is the backbone of most Windows enterprise environments.
* Centralized administration saves enormous time compared to managing devices individually.
* Organizational Units help organize resources logically.
* Delegation improves security by following the principle of least privilege.
* Group Policies allow administrators to enforce security consistently.
* Kerberos is the standard authentication protocol in modern Windows domains.
* Proper organization of users and computers makes enterprise administration much easier.

---

# Beginner Tips

* Learn Windows fundamentals before Active Directory.
* Practice creating users and Organizational Units repeatedly.
* Understand why each object exists instead of memorizing names.
* Explore every console inside Active Directory.
* Read Microsoft's documentation whenever a policy is unfamiliar.
* Practice inside a lab environment without worrying about making mistakes.

---

# Conclusion

This room provides a strong introduction to Windows enterprise administration. Instead of focusing only on solving tasks, it builds an understanding of how organizations manage users, computers, authentication, and security at scale. It serves as an excellent foundation for future Active Directory, SOC, Blue Team, and Windows administration learning.
