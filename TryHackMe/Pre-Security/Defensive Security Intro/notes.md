# 🛡️ Intro to Defensive Security: Study Notes
Hey everyone! 👋 Welcome to my notes on **Defensive Security**. I'm putting these together as I build out more IT and cybersecurity educational resources. Whether you are prepping for a certification or just trying to wrap your head around how the "good guys" defend networks, I hope this helps you out.
These notes cover the basics of how organizations protect their systems, detect threats, and respond to incidents. Let's dive in!

---

## 🎯 What is Defensive Security?
While offensive security (Red Teaming) is all about breaking in, Defensive Security (the **Blue Team**) focuses on protecting the castle.
The three main goals of any defensive strategy are:
  1. **Prevent** intrusions before they happen.
  2. **Detect** intrusions if an attacker manages to slip through.
  3. **Respond** to incidents quickly to minimize damage.

### Common Blue Team Activities
To hit those goals, defensive teams spend their time on things like:
  * Running security awareness training for employees.
  * Managing assets (knowing exactly what devices are on the network).
  * Keeping systems updated and patched.
  * Deploying Firewalls and Intrusion Prevention Systems (IPS).
  * Setting up logging and monitoring to watch for weird behavior.

---

## 🏢 The SOC (Security Operations Center)
The SOC is essentially the control room. It's a dedicated team responsible for continuously monitoring networks and systems for malicious activity.

**What does a SOC actually look out for?**
  * **Vulnerabilities:** Finding weak spots and patching them to reduce the "attack surface" (the number of ways a hacker could get in).
  * **Policy Violations:** Catching internal mistakes, like someone uploading confidential company data to an unauthorized cloud service.
  * **Unauthorized Activity:** Spotting stolen credentials or suspicious logins happening at weird times or from strange locations.
  * **Network Intrusions:** Detecting malware links being clicked or public-facing servers being exploited.

---

## 🧠 Threat Intelligence (Know Your Enemy)
Threat Intelligence is the process of collecting and analyzing information about potential and existing cyber threats. The goal is to build a defense strategy based on actual data, not just guessing.

**The Intelligence Lifecycle:**
  1. **Data Collection:** Gathering raw data from network logs, security tools, threat reports, and public sources.
  2. **Data Processing:** Organizing that messy data into a usable, readable format.
  3. **Analysis:** Figuring out the "Who, What, and Why." Who is the threat actor? What are their motivations? What are their **TTPs** (Tactics, Techniques, and Procedures)?
  4. **Recommendations:** Turning that analysis into actionable defensive steps to improve security.

---

## 🔍 Digital Forensics & Incident Response (DFIR)

### Digital Forensics
When something goes wrong, we need evidence. Digital Forensics is the investigation of digital clues to establish exactly what happened. We look at:
  * **File Systems:** To find installed software, hidden files, or modified data.
  * **Memory (RAM):** Crucial for finding "fileless" malware that only runs in active memory and leaves no trace on the hard drive.
  * **System Logs:** Checking Windows Event Logs, Linux logs, and application histories.
  * **Network Logs:** Tracing where the suspicious communication came from and where it went.

### Incident Response
The goal here is to put out the fire, minimize the damage, and get the business running again. Incidents can range from data breaches and ransomware to simple misconfigurations.

**The 4 Steps of Incident Response:**
  1. **Preparation:** Training the team, writing the playbooks, and putting security controls in place *before* disaster strikes.
  2. **Detection & Analysis:** Spotting the alert and figuring out how bad it is.
  3. **Containment, Eradication, & Recovery:** Stopping the spread (Contain), deleting the threat (Eradicate), and restoring from backups (Recovery).
  4. **Post-Incident Activity:** Writing the report, documenting lessons learned, and fixing the holes so it doesn't happen again.

---

## 🦠 Malware Analysis
Malware is just malicious software designed to harm systems.

**Common Types:**

| Type | How it Works |
| --- | --- |
| **Virus** | Attaches to legitimate programs and replicates itself, modifying or deleting files. |
| **Trojan Horse** | Disguises itself as a normal, helpful program but contains hidden malicious code inside. |
| **Ransomware** | Locks and encrypts your files, demanding a crypto payment to give you the key. |

**How Analysts Study Malware:**
  * **Static Analysis:** Looking at the code and structure *without* actually running it. (Safe and fast).
  * **Dynamic Analysis:** Running the malware inside a safe, isolated environment (a sandbox) to see exactly what it tries to do.

---

## 🚨 SIEM & The Role of a SOC Analyst

A **SIEM** (Security Information and Event Management) is a massive platform that collects logs from every computer, firewall, and server in the company and centralizes them into one dashboard. It automatically generates alerts when it sees bad behavior.
As a SOC Analyst, your job is to:
  * Review these alerts.
  * Investigate the suspicious activity.
  * Validate if it's a real threat or a false alarm.
  * Escalate to senior teams if necessary, and recommend action.

> 💡 **Golden Rule of the SOC:** Not every alert is an attack! Many alerts are just users forgetting their passwords, making honest mistakes, or running poorly configured legitimate software. **Always investigate before blocking.**

### My Practical Investigation Workflow
If you're wondering how to handle an alert day-to-day, here is a solid flow to follow:
  1. An alert pops up in the SIEM.
  2. Read the details (Who, what, when, where?).
  3. Look for Indicators of Compromise (suspicious IPs, weird file names).
  4. Check the reputation of those IPs/files using threat intel tools.
  5. Determine if it's genuinely malicious or a false positive.
  6. Escalate to Tier 2/Tier 3 if it's serious.
  7. Block the malicious activity (e.g., ban the IP on the firewall).
  8. Document everything you did in a ticket.

---

## 📝 Personal Takeaways
  * Defensive Security is fundamentally about protecting the house, not attacking others.
  * The SOC is the frontline, and analysts spend their days living in the SIEM investigating alerts.
  * Threat intel is crucial because you can't defend against an attacker you don't understand.
  * If an incident happens, forensics finds the clues, and incident response cleans up the mess.
  * *Note to self:* This foundational stuff is super logical. The room I used to study this was great because it built the concepts up step-by-step!
