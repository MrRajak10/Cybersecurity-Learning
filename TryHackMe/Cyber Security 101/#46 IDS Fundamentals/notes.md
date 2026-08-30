Welcome! It is great to see you diving into Intrusion Detection Systems (IDS) and Snort. These concepts are the absolute backbone of network defense, Security Operations Centers (SOC), and threat hunting. Let's break down your notes and rebuild them into a deep, conceptual understanding so you are not just memorizing commands, but truly learning how a network defends itself.

## The Core Concept: What is an IDS?

An **Intrusion Detection System (IDS)** is a passive security tool that monitors network traffic or system activities for malicious behavior or policy violations. Think of it as the ultimate observer.

**Why it exists:** Firewalls are great, but they are not perfect. A firewall sits at the perimeter of your network and blocks traffic based on simple rules (e.g., "Don't allow traffic on port 23"). But what happens if an attacker exploits a vulnerability on an allowed port (like port 443 for HTTPS)? The firewall lets it right through. An IDS exists to catch what the firewall misses by inspecting the *actual contents* and *behavior* of the traffic.

**IDS vs. IPS vs. Firewall (The Real-World Analogy)**

* **Firewall:** The bouncer at the door of a club. He checks IDs and enforces basic rules ("No sneakers allowed"). If you meet the rules, you get in.
* **IDS (Intrusion Detection System):** The CCTV cameras and the security guard watching the monitors *inside* the club. If you start a fight inside, the camera sees it and an alarm sounds, but the camera itself cannot physically stop you. **(Detects + Alerts)**
* **IPS (Intrusion Prevention System):** A security guard walking the floor. If they see you start a fight, they actively tackle you and throw you out. **(Detects + Prevents)**

> **Why don't organizations just use IPS everywhere to block everything?**
> *Business continuity.* If an IPS makes a mistake (a "false positive") and blocks legitimate traffic, it could take down a company's main website or interrupt critical business operations. Therefore, many organizations prefer an IDS: it alerts a human analyst to investigate without risking an accidental outage.

---

## Deployment: Where Do We Put the IDS?

To catch intruders, you need visibility. Where you place your "cameras" changes what you can see.

| Feature | HIDS (Host-Based) | NIDS (Network-Based) |
| --- | --- | --- |
| **Location** | Installed directly on individual machines (laptops, servers). | Placed at strategic choke points on the network (e.g., behind the firewall). |
| **What it sees** | Everything happening *inside* that specific computer (file changes, registry edits, memory usage, local logs). | All traffic flowing *across* the network segment between multiple computers. |
| **Pros** | Can see decrypted traffic (since it's on the host); highly detailed. | One sensor covers hundreds of devices; easier to deploy at scale. |
| **Cons** | Uses CPU/RAM on the user's machine; hard to manage if you have 10,000 laptops. | Cannot see what happens entirely inside a host; struggles with encrypted traffic. |

**In the real world:** A mature SOC uses **both**. A NIDS watches the highways (network), while HIDS acts as the security system inside the houses (hosts).

---

## Detection Methods: How Does It Catch the Bad Guys?

Once the IDS has visibility, how does it actually know something is malicious?

* **Signature-Based Detection:** The IDS has a dictionary of known "bad" patterns (signatures). If a packet matches a signature exactly, it alerts.
* *Analogy:* Police looking for a suspect with a specific physical description and a tiger tattoo on their left arm.
* *Pros & Cons:* Extremely fast and highly accurate for known threats. Useless against brand-new, zero-day attacks because there is no signature for it yet.


* **Anomaly-Based Detection:** The IDS spends a week learning what "normal" looks like on your network (creating a baseline). If traffic suddenly spikes or acts weird, it alerts.
* *Analogy:* A bank teller noticing a customer who usually withdraws $50 suddenly trying to transfer $500,000 to an offshore account.
* *Pros & Cons:* Excellent at catching new, unknown attacks. However, it generates a massive amount of **False Positives** (alerting on innocent behavior just because it's unusual).


* **Hybrid:** Combines both. Uses signatures for the known bad stuff, and anomaly detection to catch the sneaky, new stuff. This is the modern standard.

---

## Meet Snort

**Snort** is the industry-standard, open-source NIDS. It is essentially a highly optimized packet-reading engine.

**Snort's 3 Modes of Operation:**

1. **Packet Sniffer Mode (`-v`):** Like Wireshark in the terminal. It just reads packets flowing across the wire and prints them to your screen. Used for quick, live troubleshooting.
2. **Packet Logging Mode (`-l`):** Takes those packets and saves them to a file on the hard drive (usually a **PCAP** - Packet Capture file). Used for retaining evidence.
3. **NIDS Mode (`-c`):** The main event. Snort actively reads packets, compares them against its rulebook (`snort.conf` and `local.rules`), and generates alerts if it finds a match.

**Key Locations to Remember in Linux:**

* `/etc/snort` → The main brain/configuration directory.
* `/etc/snort/rules` → The filing cabinet where all the rulebooks live.
* `/etc/snort/rules/local.rules` → Your personal notebook where you write custom detection rules.

---

## Writing Snort Rules (Detection Engineering)

Writing rules is the art of **Detection Engineering**. Let's break down the anatomy of a rule designed to detect someone pinging your server (ICMP traffic).

```text
alert icmp any any -> 192.168.1.10 any (msg:"Ping Detected"; sid:100001; rev:1;)

```

**The Rule Header (The "Who and What")**

* `alert`: The **Action**. (What should Snort do? Alert, log, drop?)
* `icmp`: The **Protocol**. (TCP, UDP, ICMP, IP).
* `any any`: The **Source IP** and **Source Port**. (`any` means we don't care who is sending it).
* `->`: The **Direction**. (Traffic moving from source to destination).
* `192.168.1.10 any`: The **Destination IP** and **Destination Port**. (The server being targeted).

**The Rule Options (The "Metadata and Details")**

* `msg:"Ping Detected";`: The **Message**. This is what the SOC analyst sees on their screen. Make it descriptive!
* `sid:100001;`: The **Signature ID**. Every rule needs a unique ID number. Custom rules should always start at 1000000 or higher to avoid clashing with official Snort rules.
* `rev:1;`: The **Revision**. If you edit this rule tomorrow to make it better, you change this to `rev:2`. It helps teams track version history.

---

## The SOC Analyst Mindset: Investigating Alerts

One of the biggest beginner mistakes is assuming **Alert = Successful Hack**.

An alert is just a flashing light. It is **evidence**, not a conviction. If an attacker fires a known exploit at a Linux server, Snort will scream. But what if the server is actually running Windows? The attack failed entirely, but the alert still triggered.

**When an alert pops up, ask yourself:**

1. **Who is talking?** (Check source and destination IPs).
2. **What language are they using?** (Protocol and Port, e.g., SSH on Port 22).
3. **Did the connection actually succeed?** (If the server replied with a reset/error packet, the attack failed).
4. **Is this a False Positive?** (e.g., An alert for "mass data exfiltration" might just be a user legitimately downloading a large company database for their job).

To prove what happened, analysts look at **PCAP (Packet Capture)** files. A PCAP is a literal, bit-for-bit recording of the network traffic. By pointing Snort at a PCAP (using a command like `snort -r traffic.pcap -c /etc/snort/snort.conf`), you can run historical traffic through your rules to see what you missed yesterday.
