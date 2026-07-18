Welcome to one of the most important topics in all of cybersecurity: **Active Directory (AD)**.

If you want to work in enterprise IT, penetration testing, or SOC operations, you must understand Active Directory. Over 90% of large organizations use it. When a massive company suffers a devastating ransomware attack, it almost always involves the attackers compromising Active Directory to take control of the entire network.

Let’s break down your notes step-by-step, moving from the basic building blocks to how it all scales up.

---

## 1. The Core Infrastructure

Imagine a company with 5,000 employees. If the IT team had to manually create a user account, set a password, and configure security settings on 5,000 separate laptops, it would be impossible. They need a centralized way to manage everything.

### The Windows Domain

A **Windows Domain** is a logical group of computers, users, and resources that share a central directory database. Instead of your laptop verifying your password locally, it asks the Domain if your password is correct.

### Active Directory (AD) & AD DS

* **Active Directory (AD):** This is the actual database. Think of it as a massive digital phonebook that stores the details of every user, computer, printer, and security policy in the company.
* **Active Directory Domain Services (AD DS):** This is the underlying engine (the service) that keeps the AD database running, allows it to be searched, and processes login requests.

### The Domain Controller (DC)

If AD is the database, the **Domain Controller (DC)** is the physical (or virtual) server that holds that database.

* **Why it exists:** It is the ultimate authority in the network. When you type your password into your work computer, that request goes directly to the DC to be verified.
* **Security Context:** For an attacker, the DC is the "crown jewel." If a penetration tester or ransomware operator compromises the Domain Controller, they effectively own the entire company's network.

---

## 2. The Residents: Domain Objects

Everything inside Active Directory is considered an **Object**.

### Machine Accounts (Computer Accounts)

You noted that every computer joined to the domain gets its own account ending with a **`$`** symbol (e.g., `HR-PC$`).

* **Why do computers need accounts?** Because a computer needs to prove its identity to the Domain Controller *before* a human even logs in, so it can download security updates and policies.
* **How it works:** Just like users, computers have passwords. However, Windows automatically changes this machine password in the background every 30 days.
* **Security Context:** Because machine passwords are long, complex, and rotate automatically, attackers rarely try to guess them. Instead, they focus on cracking human user passwords.

### Security Groups

Instead of assigning permissions to 500 individual users, administrators put those users into **Security Groups** and assign permissions to the group.

| Group | The Real-World Reality | Security Context |
| --- | --- | --- |
| **Domain Admins** | The absolute rulers of the domain. | The ultimate target for attackers. Anyone in this group can do *anything*. |
| **Server Operators** | Can manage servers and backup data. | Highly dangerous. Attackers can use this to extract AD databases. |
| **Account Operators** | Can create and reset user accounts. | Attackers can use this to reset an admin's password and take over. |
| **Domain Users** | Every standard employee. | The starting point for an attacker after a successful phishing email. |

---

## 3. Organizing the Chaos

### Organizational Units (OUs)

An **Organizational Unit (OU)** is simply a folder inside Active Directory used to organize objects.

* **Why it exists:** A flat list of 5,000 users and computers is unmanageable. OUs allow you to group things logically (e.g., separating the `Sales` computers from the `IT` computers).
* **What problem it solves:** It allows you to apply different security rules to different departments. For example, you might want to block USB drives for the `Customer Service` OU, but allow them for the `IT` OU.

### Delegation

Delegation is the practice of giving someone just enough permission to do their job, without making them a full Domain Admin. This follows the **Principle of Least Privilege**.

* **Real-World Example:** You have a Helpdesk employee whose only job is resetting forgotten passwords. Instead of giving them full Domain Admin rights (which is a massive security risk), you right-click the `Sales` OU and **Delegate** them the specific right to "Reset User Passwords" only for the people in that folder.

---

## 4. The Law of the Land

### Group Policy Objects (GPO)

A **Group Policy Object (GPO)** is a set of rules and configurations pushed down from the Domain Controller to the computers and users.

* **Where it is used:** GPOs dictate everything from "What is the desktop wallpaper?" to "Is the Windows Firewall turned on?" to "Are users allowed to open Command Prompt?"
* **How it works:** You create a GPO, link it to an OU, and every computer inside that OU automatically downloads and applies those rules.

### SYSVOL

**SYSVOL** is a hidden shared folder that lives on every Domain Controller.

* **What it does:** It stores all the GPO files and login scripts. When a computer boots up, it connects to SYSVOL to read its assigned policies.
* **Beginner Mistake / Security Risk:** Because *every* user in the domain needs to read GPOs, *every* user has read access to the SYSVOL share. Historically, administrators mistakenly put scripts containing plain-text passwords into SYSVOL, allowing any standard user to find them and escalate their privileges.

---

## 5. Proving Who You Are: Authentication

Authentication is how you prove your identity. Active Directory primarily uses two protocols.

### Kerberos (The Default)

Kerberos is the modern, highly secure authentication protocol used by Windows. It relies on a system of **tickets**.

<img width="760" height="404" alt="image" src="https://github.com/user-attachments/assets/e2db3a4a-788d-4315-b939-c54c00d0508a" />


**The Amusement Park Analogy:**

1. **TGT (Ticket Granting Ticket):** You enter an amusement park and show your ID at the front gate. They give you a daily wristband. This wristband is your **TGT**. It proves you are allowed in the park, but it doesn't get you on a specific ride.
2. **TGS (Ticket Granting Service Ticket):** You walk up to the roller coaster. You show the ride operator your wristband (TGT). The operator hands you a specific ticket just for that roller coaster. This is your **TGS**.

* **Security Context:** Attackers love to steal these tickets from a computer's memory. If an attacker steals your TGT, they can impersonate you on the network without ever needing to know your password. This is called a **Pass-the-Ticket** attack.

### NTLM (The Legacy Backup)

NTLM is an older protocol. Instead of tickets, it uses a **Challenge-Response** mechanism.

* **How it works:** The server sends a math problem (the challenge). Your computer uses a mathematical representation of your password (called a **hash**) to solve the problem and sends the answer back.
* **Security Context:** Because the underlying hash never changes, if an attacker steals your NTLM hash from memory, they can just pass that hash to the server to log in, completely bypassing the need for the plaintext password. This is the famous **Pass-the-Hash** attack.

---

## 6. Scaling Up: Trees and Forests

When companies grow, buy other companies, or expand globally, a single Domain is no longer enough.

<img width="335" height="298" alt="image" src="https://github.com/user-attachments/assets/353ed461-8500-452b-8562-e6301336d26e" />


* **Tree:** A collection of domains that share a continuous name. If `company.com` creates child domains for `hr.company.com` and `sales.company.com`, that forms a Tree.
* **Forest:** The absolute top-level container. If `company.com` buys `partner.com`, they don't share a name, but they can be linked together inside the same Forest.
* **Trusts:** A Trust is a digital bridge. If `company.com` trusts `partner.com`, it means a user in the partner domain can log in and access a file share in the company domain.
* **Security Context:** Penetration testers map out these Trusts. If they compromise a weak, poorly secured child domain, they will attempt to exploit the Trust relationships to attack the highly secure parent domain.
