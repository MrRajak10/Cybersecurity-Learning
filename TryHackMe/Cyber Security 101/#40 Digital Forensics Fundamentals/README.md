# TryHackMe – Digital Forensics Fundamentals

## Overview

This repository documents my learning journey through the **Digital Forensics Fundamentals** room from the **Cyber Security 101 – Defensive Security** module on TryHackMe.

The room introduced the fundamentals of digital forensics, including the digital forensics methodology, evidence acquisition, chain of custody, Windows forensics, forensic imaging, volatile and non-volatile data, and basic forensic investigation using file metadata.

The main goal of this room was not simply to solve a forensic case, but to understand **how digital evidence is collected, preserved, examined, analyzed, and reported without compromising its integrity**.

---

## Learning Objectives

By completing this room, I learned:

* What digital forensics is and why it is important.
* The four major phases of the digital forensics methodology.
* The difference between collection, examination, analysis, and reporting.
* Different types of digital forensics.
* The importance of evidence acquisition.
* Why authorization is required before collecting evidence.
* What chain of custody means.
* Why hash values are important for maintaining evidence integrity.
* What a write blocker does.
* The difference between disk images and memory images.
* Why volatile memory should be collected before shutting down a running system.
* Basic Windows forensic concepts.
* How file metadata can provide useful investigative information.
* How PDF and image metadata can support a forensic investigation.
* Basic usage of `pdfinfo` and `exiftool`.

---

## Digital Forensics Fundamentals

**Digital forensics** is the process of investigating digital devices and digital data to identify, preserve, examine, and analyze evidence related to an incident or crime.

Digital evidence can exist in many places, including computers, mobile devices, hard drives, USB devices, networks, databases, cloud environments, email systems, and memory.

A forensic investigation must be performed carefully because digital evidence can easily be changed, deleted, or destroyed. The investigator therefore needs procedures that preserve the original evidence and allow other investigators or legal authorities to verify how the evidence was handled.

---

## Digital Forensics Methodology

The room introduced the general four-phase methodology associated with NIST:

### 1. Collection

The first phase is identifying and collecting relevant digital evidence.

An investigator may encounter computers, laptops, mobile phones, USB drives, hard drives, cameras, or other digital devices.

The evidence must be collected carefully while protecting the original data from modification.

Documentation is also important because investigators need to know what was collected, when it was collected, who collected it, and where it was stored.

### 2. Examination

The collected evidence can contain a huge amount of information.

The examination phase focuses on filtering and extracting the information that is relevant to the investigation.

For example, an investigator may have thousands of files but only need files created or modified during a specific time period.

### 3. Analysis

During analysis, investigators examine and correlate the extracted information to determine what happened.

Multiple pieces of evidence may need to be connected to reconstruct events chronologically.

This phase is where investigators attempt to turn individual artifacts into an understandable explanation of the incident.

### 4. Reporting

The final phase is documenting the investigation and its findings.

A forensic report can contain the investigation methodology, evidence examined, findings, conclusions, and recommendations.

Reports should be understandable to their intended audience. Technical findings may need to be explained in simple language when the report is presented to management or other non-technical stakeholders.

---

## Types of Digital Forensics

Digital forensics is a broad field containing multiple specialized areas.

### Disk Forensics

Focuses on investigating storage devices such as hard drives and other storage media.

Investigators may examine documents, images, deleted files, browser history, metadata, and other artifacts.

### Memory Forensics

Focuses on analyzing volatile data stored in RAM.

Memory can contain information about running processes, open files, network connections, and other information that may disappear when the system is powered off.

### Network Forensics

Focuses on investigating network activity.

Network traffic, logs, connections, and other network evidence can help reconstruct suspicious activity.

### Mobile Forensics

Focuses on investigating mobile devices and their associated data, such as messages, call records, application data, and location information.

### Database Forensics

Focuses on investigating databases for unauthorized access, modification, or data theft.

### Email Forensics

Focuses on investigating email-related evidence, including phishing, fraud, malicious communication, and insider activity.

### Cloud Forensics

Focuses on investigating evidence stored within cloud infrastructure.

Cloud investigations can be more challenging because investigators may have limited direct access to the underlying infrastructure.

### Malware Forensics

Focuses on examining malicious software to understand its behavior, capabilities, and impact.

---

## Evidence Acquisition

Evidence acquisition is one of the most important parts of a forensic investigation.

The investigator must obtain evidence in a way that preserves its original state.

### Authorization

Evidence should be collected only with appropriate legal or organizational authorization.

Depending on the investigation, this may involve a search warrant, organizational authorization, or another appropriate legal basis.

The investigator must also remain within the scope of that authorization.

### Chain of Custody

The **chain of custody** is the documented history of evidence from the moment it is collected until the investigation is completed.

It helps answer questions such as:

* What evidence was collected?
* Who collected it?
* When was it collected?
* Where was it stored?
* Who accessed it?
* When was it accessed?
* How was it transferred?
* Was its integrity maintained?

Maintaining a proper chain of custody helps demonstrate that the evidence was handled correctly.

### Hash Values

Hash values can be used to verify the integrity of digital evidence.

A forensic image can be hashed when it is acquired. The resulting hash can later be compared with another hash of the same evidence.

If the expected hash changes unexpectedly, it can indicate that the evidence was modified.

Common hashing algorithms encountered in forensic contexts include **MD5** and **SHA-1**, although modern investigations may also use stronger algorithms such as SHA-256.

### Write Blocker

A **write blocker** is a hardware or software mechanism designed to prevent data from being written to the original evidence storage device.

For example, when a forensic investigator connects a suspect's hard drive to a forensic workstation, the workstation should not accidentally modify files, timestamps, or other data on the original drive.

A write blocker helps preserve the original evidence while allowing investigators to acquire and examine it.

---

## Windows Forensics

Windows is widely used on personal computers, making Windows forensic knowledge particularly important for digital investigators.

A Windows investigation can involve many different artifacts, including files, metadata, user activity, browser information, processes, memory, and other operating-system artifacts.

One important concept introduced in this room is the difference between **disk evidence** and **memory evidence**.

### Disk Image

A disk image is a forensic copy of data stored on a storage device.

It contains non-volatile data, meaning the data normally remains available even after the system is restarted or powered off.

Examples include:

* Documents
* Images
* Videos
* Browser history
* Stored application data
* Other files on the storage device

### Memory Image

A memory image is a capture of the system's RAM.

RAM is volatile memory, meaning its contents can disappear when the system is powered off or restarted.

Memory can contain valuable information such as:

* Running processes
* Open files
* Active network connections
* Data currently held in memory

Therefore, when investigating a running system, acquiring volatile memory can be a high priority before shutting the system down.

---

## Forensic Tools

The room introduced several tools commonly associated with digital forensics.

### FTK Imager

**FTK Imager** can be used to acquire forensic images and examine digital evidence.

### Autopsy

**Autopsy** is an open-source digital forensics platform that can analyze forensic images and provide capabilities such as file analysis, deleted-file recovery, metadata examination, and keyword searching.

### DumpIt

**DumpIt** can be used to acquire a memory image from a Windows system.

### Volatility

**Volatility** is an open-source memory forensics framework used to analyze memory images.

It provides plugins that allow investigators to examine different types of artifacts within memory.

---

## Practical Investigation

The practical portion of the room demonstrated how file metadata can provide useful investigative information.

The investigation involved a ransom-related document and an image.

Instead of relying only on the visible contents of a file, metadata was examined to identify additional information.

### PDF Metadata

The `pdfinfo` utility can display metadata associated with a PDF file.

Example:

```bash
pdfinfo ransom-letter.pdf
```

Information may include:

* Title
* Subject
* Author
* Creation date
* Modification date
* Number of pages
* File size
* PDF version
* Encryption status

This demonstrates an important forensic principle:

> A file can contain useful information that is not immediately visible when opening the file normally.

### Image Metadata

The `exiftool` utility can extract metadata from images.

Example:

```bash
exiftool letter-image.jpg
```

Depending on the image, metadata may contain information such as:

* Camera manufacturer
* Camera model
* Date and time
* Lens information
* Image dimensions
* GPS information
* Other EXIF data

GPS metadata can potentially provide geographic information that helps investigators determine where an image was captured.

---

## Key Takeaways

The most important lessons from this room were:

1. **Digital forensics is about evidence, not simply finding information.**

2. **Evidence integrity is critical.** Investigators must ensure that the original evidence is not unnecessarily modified.

3. **Chain of custody provides accountability.** Every important interaction with evidence should be documented.

4. **Hash values help verify evidence integrity.**

5. **Write blockers help prevent accidental modification of original storage media.**

6. **Volatile data can disappear.** RAM should be considered carefully when investigating a running system.

7. **Disk and memory images serve different purposes.**

8. **Metadata can be extremely valuable.** Information hidden inside files can reveal details that are not visible from the file's normal contents.

9. **Forensic investigations involve multiple stages.** Collection, examination, analysis, and reporting each have a specific purpose.

10. **Technical findings must eventually be communicated clearly.** A forensic investigation is incomplete if its findings cannot be understood by the people responsible for acting on them.

---

## Beginner Practice Activities

### Activity 1 – Examine a PDF

Find a PDF on your own system or create a test PDF.

Use:

```bash
pdfinfo sample.pdf
```

Record the metadata you find.

Ask yourself:

* Who is listed as the author?
* When was the document created?
* When was it modified?
* How many pages does it contain?
* Is it encrypted?

### Activity 2 – Examine Image Metadata

Take a test image and run:

```bash
exiftool image.jpg
```

Look for:

* Camera information
* Date/time information
* GPS information
* File information

Do not modify the original image during the exercise.

### Activity 3 – Think Like a Forensic Investigator

Imagine that an investigator receives a laptop that is currently powered on.

Before doing anything, ask:

**What information could disappear if the machine is immediately shut down?**

This should lead you toward the concept of **volatile memory** and the importance of memory acquisition.

### Activity 4 – Build a Chain of Custody

Create a fictional forensic evidence record containing:

* Evidence ID
* Evidence description
* Collector
* Collection date/time
* Storage location
* Access history
* Transfer history
* Evidence hash

The goal is to understand how evidence accountability works.

---

## Personal Learning

This room helped connect several defensive-security concepts into a complete investigation process.

The biggest lesson was that digital forensics is not simply about opening files and searching for suspicious information. The investigator must first think about **how the evidence was collected, whether it was preserved correctly, how its integrity can be verified, what information is relevant, and how the final findings can be explained**.

The distinction between volatile and non-volatile evidence was particularly important. A disk may preserve information after a shutdown, while information stored in RAM can disappear immediately. Understanding this difference changes how an investigator approaches a live system.

The practical metadata investigation also demonstrated that seemingly ordinary files can contain valuable forensic information. File metadata can provide additional context and help investigators build a timeline or establish relationships between pieces of evidence.

---

## Conclusion

Digital Forensics Fundamentals provides a foundation for understanding how investigators work with digital evidence.

The room introduces the complete forensic mindset: **preserve the evidence, maintain its integrity, examine relevant artifacts, correlate findings, and document the investigation clearly**.

These fundamentals provide a strong base for further learning in areas such as Windows forensics, memory forensics, malware analysis, incident response, and Digital Forensics and Incident Response (DFIR).
