Welcome to Digital Forensics! This is a fascinating field where cybersecurity meets criminal investigation. You are no longer just looking at alerts; you are learning how to prove *exactly* what an attacker or insider threat did, in a way that stands up in a court of law.

Let's break down your notes step-by-step, explaining the concepts clearly so you can understand the "why" and "how" behind the procedures.

---

## 1. What Is Digital Forensics?

### The Concept

Imagine a traditional crime scene: a broken window, footprints on the floor, and a missing safe. Police tape off the area so nobody destroys the evidence. They take photos, collect fingerprints, and document everything.

**Digital Forensics** is doing exactly that, but inside computers, mobile phones, servers, and networks. It is the scientific process of identifying, preserving, extracting, and documenting digital evidence so that it can be presented in a court of law or used for an internal corporate investigation.

### Why Security Professionals Care

* **Incident Response (IR):** When a company is breached, IR teams use forensic techniques to find "Patient Zero" (the first infected machine) and figure out exactly what data was stolen.
* **Threat Hunting:** Hunters use forensic artifacts (like hidden processes or strange network connections) to find attackers who are secretly hiding in the network.

---

## 2. The Golden Rule: Evidence Integrity

Before we talk about *how* to investigate, we must talk about the most important rule in forensics: **Never alter the original evidence.**

If a defense attorney can prove you accidentally modified a file while investigating a suspect's laptop, the entire case can be thrown out. This brings us to three critical concepts: Authorization, Write Blockers, and Hash Values.

### Authorization

You cannot just take someone's laptop and start looking through it. You need legal permission.

* In law enforcement, this is a **Search Warrant** signed by a judge.
* In corporate environments, this is **Organizational Authorization** (usually defined in employment contracts and IT acceptable use policies).

### The Write Blocker

A **Write Blocker** is a piece of hardware (or sometimes software) that sits between the investigator's computer and the suspect's hard drive.

* **How it works:** When you plug a USB drive into your normal Windows computer, Windows immediately starts writing hidden files to it (like `Thumbs.db` or recycle bin data) just by opening the folder. A write blocker acts as a one-way valve. It allows the investigator's computer to *read* the data, but physically blocks any "write" commands from reaching the suspect's drive.

### Hash Values (Digital Fingerprints)

A hash function is a mathematical algorithm that takes a file (or an entire hard drive) and outputs a fixed-length string of characters. Common algorithms are **MD5**, **SHA-1**, and **SHA-256**.

Think of a hash as a digital fingerprint.

* If a hard drive has a hash of `ABC123`.
* You make a forensic copy of it.
* You hash your copy. It should also be `ABC123`.
* If even a single letter in a single text file on that drive is changed, the new hash will look completely different (e.g., `XYZ789`). This proves mathematically that your copy is a perfect, unaltered clone of the original.

---

## 3. The Digital Forensics Methodology

Every investigation follows a strict, repeatable process.

1. **Collection:** Secure and Acquire.
Identify devices (laptops, phones, USBs). Secure the scene. Use write blockers to make perfect, hashed copies (forensic images) of the original data.


2. **Examination:** Extract and Filter.
A 1-Terabyte hard drive has millions of files. Examination is the process of using forensic tools (like Autopsy) to filter out standard operating system files and focus only on user-created files, deleted files, or data from a specific date range.


3. **Analysis:** Connect the Dots.
This is the "detective work." You correlate different pieces of evidence. For example: "The registry shows a USB was plugged in at 2:00 PM. The file metadata shows a confidential document was copied to a D: drive at 2:02 PM."


4. **Reporting:** Document Everything.
Translate technical findings into a report that a judge, jury, or CEO can understand. It answers who, what, when, where, and how.


---

## 4. Chain of Custody

The **Chain of Custody** is a physical, paper document (or secure digital log) that tracks the evidence from the moment it is collected until the case is closed.

It answers: *Who had the evidence, when did they have it, and what did they do with it?*
If a laptop is sitting in an unlocked room for three days and there is a gap in the Chain of Custody, the defense will argue: "Someone else could have planted that malware during those three days!"

---

## 5. Memory Forensics vs. Disk Forensics

This is a massive concept for incident responders. It revolves around the **Order of Volatility**—meaning, what data disappears the fastest when a computer is turned off?

### Volatile Data (Memory/RAM)

RAM (Random Access Memory) is fast, temporary storage that holds everything the computer is *currently doing*.

* **What it holds:** Running malware processes, active network connections to a hacker's server, unencrypted passwords, and open documents.
* **The Catch:** RAM requires continuous electrical power. The moment you pull the plug or shut down the computer, **everything in RAM is permanently destroyed.**

### Non-Volatile Data (Disk/Hard Drive)

The Hard Drive (HDD or SSD) is where data is permanently saved.

* **What it holds:** Downloaded files, installed programs, browser history, and hidden system logs.
* **The Catch:** Data stays here even when the power is off.

> **Beginner Mistake:** A beginner walks into a room, sees a suspect's computer running, and immediately unplugs it from the wall to "secure" it. They just destroyed all the RAM evidence! An expert will perform a **live acquisition** (using a tool like `DumpIt`) to copy the RAM *before* touching the power cable.

---

## 6. Metadata: Data About Data

When you look at a photograph on your phone, you just see the picture. But embedded invisibly inside that file is **Metadata** ("data about data").

### Why it matters

A suspect might claim, "I didn't write that ransom note!" but the metadata of the PDF might show their username as the "Author" and the exact minute it was created.

### Tools of the Trade

* **`pdfinfo`:** Used in Linux to extract metadata from PDFs. It will show you the software used to create the PDF, creation dates, and whether it was encrypted.
* **`exiftool`:** A powerful command-line tool for image metadata. **EXIF** (Exchangeable Image File Format) data is attached to photos by digital cameras and smartphones.

#### Let's look at an `exiftool` command:

```bash
exiftool suspect_photo.jpg

```

* **What it does:** Reads the hidden EXIF headers in the `.jpg` file.
* **What you might see:**
* `Camera Model: iPhone 13 Pro`
* `Date/Time Original: 2024-05-12 14:30:00`
* `GPS Latitude / Longitude:` Exact coordinates of where the photographer was standing.



> **Real-World Context:** Many social media sites (like Facebook or Instagram) automatically strip EXIF data when you upload a photo to protect privacy. However, photos sent directly via email, USB, or uncompressed messaging apps usually retain all this tracking data.

---

## 7. Forensic Tools Summary

* **FTK Imager:** Used heavily in the industry to create those perfect, hashed copies (Disk Images) of hard drives. It can also capture live memory.
* **Autopsy:** A graphical interface used to examine the hard drive copy. You can use it to search for keywords across the whole drive or recover files the suspect tried to delete.
* **DumpIt:** A tiny, fast Windows tool you run from a USB drive to copy the live RAM to a file.
* **Volatility:** The gold standard for analyzing the RAM copy. It uses plugins to say, "Show me all the network connections that were open at the exact moment the RAM was copied."
