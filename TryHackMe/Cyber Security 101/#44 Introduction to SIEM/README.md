# Introduction to SIEM — TryHackMe

## About This Room

This repository documents my learning journey through the **Introduction to SIEM** room on TryHackMe.

A **SIEM (Security Information and Event Management)** system is a security platform that collects logs from different sources, brings them into one central location, makes different log formats easier to analyze, connects related events, and helps security analysts identify suspicious activity.

This room introduces the fundamentals of SIEM technology and shows how security operations teams use logs, detection rules, alerts, dashboards, and investigation workflows to identify potentially malicious activity.

---

## Learning Objectives

By completing this room, I learned:

* What SIEM means and why it is important in a SOC.
* Why modern environments generate huge amounts of logs.
* The difference between **host-centric** and **network-centric** logs.
* Why analyzing logs manually becomes difficult at scale.
* How SIEM platforms centralize and normalize logs.
* How SIEM systems correlate events from different sources.
* Common ways logs are sent to a SIEM.
* How detection rules generate security alerts.
* The difference between **true positives** and **false positives**.
* Why detection rules require continuous tuning.
* How a SOC analyst can investigate and respond to an alert.
* How dashboards help analysts understand large amounts of security data.

---

## 1. What Is SIEM?

**SIEM stands for Security Information and Event Management.**

A SIEM is used to collect and analyze security-related information from many systems in an organization.

Instead of an analyst checking logs individually on every computer, server, firewall, application, or other device, a SIEM brings those logs into a centralized platform.

The main idea is:

```text
Different Devices
       ↓
     Logs
       ↓
   SIEM Platform
       ↓
Normalization + Correlation
       ↓
 Detection Rules
       ↓
     Alerts
       ↓
 SOC Analyst Investigation
```

A SIEM does not simply store logs. It helps security teams turn large amounts of raw log data into information that can be investigated.

---

## 2. Why Logs Matter

Almost every modern system produces logs.

Examples include:

* Windows computers
* Linux systems
* Web servers
* Firewalls
* Routers
* Applications
* Databases
* VPN systems
* Network devices
* Cloud services

A log is essentially a record of something that happened.

For example, a system may record:

```text
User logged in
Process started
File accessed
Command executed
Network connection created
Authentication failed
USB device connected
```

Logs are extremely useful during security investigations because they provide evidence about activity that occurred inside an environment.

The problem is not usually the lack of logs.

The problem is the **huge volume of logs**.

A large organization can generate an enormous amount of log data, making it unrealistic for a human analyst to manually inspect everything.

---

## 3. Host-Centric vs Network-Centric Logs

One of the important concepts introduced in the room is the difference between **host-centric** and **network-centric** logs.

### Host-Centric Logs

Host-centric logs describe activity occurring on a particular device.

For example:

```text
Process started
Registry changed
File accessed
Command executed
User logged in
Process terminated
```

For example, if a Windows computer records that a PowerShell process was launched, that is host-centric activity.

Host-centric logs can exist even when the device is not connected to the Internet because the activity is happening locally on the system.

### Network-Centric Logs

Network-centric logs describe communication or activity involving communication between systems.

Examples include:

```text
VPN connection
SSH connection
FTP connection
Web request
Network file-share activity
Connection to an external IP
```

For example, when a user connects to a VPN, the activity generates network-related information.

### Simple Comparison

| Type            | What It Describes             | Example                    |
| --------------- | ----------------------------- | -------------------------- |
| Host-centric    | Activity on a device          | PowerShell process started |
| Network-centric | Communication between systems | VPN connection             |

These categories are useful for understanding where evidence may come from during an investigation, although real environments can contain more complex relationships between different types of events.

---

## 4. Why Centralization Is Important

Without a SIEM, security analysts may have to examine logs separately on many systems.

Imagine an organization with:

```text
1000 Windows endpoints
50 Linux servers
Multiple firewalls
Multiple web servers
VPN infrastructure
Cloud services
Security products
```

Each system may produce logs in different formats and locations.

This creates several problems:

### Too Many Log Sources

There may be far more logs than a human can manually review.

### No Centralized View

Logs may exist on individual systems instead of one central location.

### Different Formats

Windows, Linux, web servers, firewalls, and applications may produce very different log structures.

### Difficult Correlation

An attack may involve activity across multiple systems.

One event by itself may not look suspicious, but several related events occurring close together can reveal the attack.

### Lack of Context

Analysts need information from multiple sources to understand what actually happened.

A SIEM helps solve these problems by bringing information together.

---

## 5. Core SIEM Functions

### Log Collection

A SIEM collects logs from different sources.

Examples:

```text
Windows
Linux
Firewalls
VPN
Web Servers
Applications
Cloud Services
Endpoints
```

### Log Normalization

Different systems produce different log formats.

A SIEM can parse and normalize these logs so that information from different sources can be searched and analyzed more consistently.

For example:

```text
Windows log
Linux log
Web server log
Firewall log
```

may all contain information about users, IP addresses, processes, timestamps, and actions, even though their original formats are different.

Normalization makes these fields easier to work with.

### Log Correlation

Correlation connects related events from different sources.

Consider this example:

```text
10:01 — User connects through VPN
10:02 — User accesses a shared document
10:03 — PowerShell starts on the endpoint
10:05 — Endpoint connects to an external IP
```

Each event alone may not provide enough context.

When they are correlated within a short time period, they can provide a much clearer picture of what is happening.

### Real-Time Alerting

SIEM platforms can monitor incoming events and trigger alerts when predefined conditions are met.

This helps security teams identify suspicious activity quickly.

### Dashboards and Reporting

SIEM dashboards present security information in a more understandable form.

Examples include:

```text
Failed login attempts
Top processes
Network connections
Triggered detection rules
Suspicious activity
MITRE ATT&CK mappings
RDP connections
Event ingestion
```

This allows analysts to understand larger patterns without manually reading every individual log.

---

## 6. Common SIEM Log Sources

### Windows

Windows provides logs through **Event Viewer**.

Important information can include:

```text
Event ID
Timestamp
Source
Task Category
User
Process
Event Details
```

Windows event IDs are particularly useful because they identify specific types of events.

### Linux

Linux commonly stores logs under:

```text
/var/log/
```

Different files may contain information related to different system services and activities.

For example:

```text
Cron logs
Authentication logs
System logs
Web server logs
```

### Web Servers

Web servers can generate:

```text
Request logs
Response information
Error logs
Client IP information
```

These logs can be valuable when investigating suspicious web activity.

---

## 7. How Logs Reach a SIEM

A SIEM needs a method for receiving logs from different systems.

Common approaches include:

### Agents / Forwarders

Software can be installed on endpoints or servers to collect and forward logs to the SIEM.

Conceptually:

```text
Endpoint
   ↓
Agent / Forwarder
   ↓
SIEM
```

This can allow logs to be forwarded as activity occurs.

### Syslog

**Syslog** is commonly used to transport log information from networked systems to a central logging system.

Conceptually:

```text
Device
   ↓
Syslog
   ↓
SIEM
```

### Manual Upload

Logs can sometimes be exported and manually uploaded.

This may be useful in limited situations, such as lab environments or investigations where logs were collected separately.

### Port-Based Forwarding

Some SIEM configurations listen on specific ports for incoming log data.

Endpoints or other systems can forward their log data to those listening services.

The exact collection architecture depends on the organization's infrastructure and SIEM platform.

---

## 8. Detection Rules

Collecting logs is only part of the process.

The SIEM must also determine what activity deserves attention.

This is where **detection rules** are used.

A detection rule is essentially a logical condition:

```text
IF something suspicious happens
THEN generate an alert
```

Examples:

```text
5 failed logins within 10 seconds
```

```text
Successful login after multiple failures
```

```text
USB device connected
```

```text
Windows event log cleared
```

```text
Suspicious process created
```

The exact rules used by an organization depend on its environment, users, applications, infrastructure, and threat model.

---

## 9. Example: Event Log Clearing

Attackers may attempt to remove traces of their activity after compromising a system.

One example introduced in the room is **Windows Event ID 104**, which indicates that an event log was cleared.

A SIEM detection rule can monitor for this activity.

Conceptually:

```text
Log Source = Windows Event Log
+
Event ID = 104
        ↓
Trigger Alert
```

The alert can then notify the SOC analyst that an important security event occurred.

The key lesson is that logs can also reveal attempts by attackers to hide their activity.

---

## 10. Example: Suspicious Process Detection

Another example involves monitoring newly created processes.

A detection rule might use information such as:

```text
Log Source = Windows Event Log
Event ID = 4688
Process Name = suspicious keyword
```

Windows Event ID **4688** relates to the creation of a new process.

A rule could detect process names containing suspicious terms and generate an alert for investigation.

For example:

```text
New Process Created
        ↓
Process Name Contains Suspicious Term
        ↓
Detection Rule Matches
        ↓
Alert Generated
```

This demonstrates how a SIEM can turn raw events into security detections.

---

## 11. Detection Rules Need Tuning

Detection rules are not automatically perfect.

A rule can produce:

### True Positive

The alert represents genuinely suspicious or malicious activity.

Example:

```text
A compromised account performs suspicious actions.
```

### False Positive

The alert was triggered, but the activity was actually legitimate.

Example:

```text
A legitimate employee repeatedly fails to log in because they forgot their password.
```

If a rule generates too many false positives, analysts may receive large numbers of unnecessary alerts.

This is why detection rules must be continuously reviewed and fine-tuned.

The goal is to make detections useful enough that analysts can focus their time on genuinely important events.

---

## 12. SOC Analyst Alert Workflow

A simplified SIEM-driven investigation can look like this:

```text
Log Generated
      ↓
Log Sent to SIEM
      ↓
Detection Rule Evaluated
      ↓
Alert Triggered
      ↓
Analyst Reviews Event
      ↓
True Positive or False Positive?
      ↓
Investigation / Tuning
      ↓
Containment or Other Response
```

When an alert appears, the analyst needs to investigate rather than immediately assume that an attack occurred.

The analyst may examine:

```text
User
Host
Process
Timestamp
IP Address
Event ID
Command
Network Activity
Related Events
```

The analyst then determines whether the alert is legitimate, malicious, or a detection that needs tuning.

---

## 13. Alert Investigation Example

A simplified investigation from the practical portion of the room involved suspicious cryptocurrency-mining activity.

The investigation followed the relationship between the alert, the process, the user, the host, and the detection rule.

The suspicious process was:

```text
cudominer.exe
```

The investigation identified the associated user and host and then examined the rule that triggered the alert.

The important lesson was not simply identifying the process name.

The important lesson was understanding the investigation chain:

```text
Alert
 ↓
Triggered Event
 ↓
Process
 ↓
User
 ↓
Host
 ↓
Detection Rule
 ↓
Analyst Decision
```

This demonstrates how a SOC analyst uses SIEM data to move from a high-level alert toward technical evidence.

---

## 14. Practical Skills Learned

This room introduced several skills that are important for a beginner SOC analyst.

### Log Analysis

Understanding what logs represent and why they are valuable during investigations.

### Log Classification

Recognizing whether activity is primarily host-centric or network-centric.

### SIEM Fundamentals

Understanding why organizations centralize and normalize logs.

### Detection Engineering Basics

Understanding how logical detection rules identify suspicious behavior.

### Alert Investigation

Following an alert back to its underlying event and examining the available context.

### False Positive Analysis

Understanding why alerts can be legitimate and why rules need tuning.

### Security Monitoring

Understanding how SOC teams use dashboards, detections, and alerts to monitor an environment.

---

## 15. Beginner Practice Activities

### Practice 1 — Explore Windows Logs

On a Windows machine, open:

```text
Event Viewer
```

Explore:

```text
Windows Logs
    ├── Application
    ├── Security
    ├── System
```

Observe the different event types and identify the following fields:

```text
Event ID
Time
Source
User
Description
```

The goal is to become comfortable reading raw Windows events.

### Practice 2 — Explore Linux Logs

On a Linux machine, inspect:

```bash
ls /var/log/
```

Identify different log files and investigate what each one records.

The goal is to understand that Linux logs may be organized differently from Windows logs.

### Practice 3 — Think Like a Detection Engineer

Create simple detection ideas such as:

```text
5 failed logins in a short time
```

```text
Successful login immediately after multiple failures
```

```text
Unexpected process creation
```

```text
Event logs cleared
```

For each rule, ask:

```text
Why would this be suspicious?
Could it be legitimate?
What evidence would I investigate next?
```

### Practice 4 — Investigate an Alert

Take one suspicious event and answer:

```text
Who performed the activity?
What happened?
When did it happen?
Which host was involved?
Which process was involved?
Which IP address was involved?
Why did the detection trigger?
Is it a true positive or false positive?
```

This is a useful way to start developing an analyst mindset.

---

## 16. Key Takeaways

The most important lesson from this room is that **security teams are dealing with enormous amounts of data**.

Logs are produced by almost every modern system, but having logs alone does not automatically provide security.

A SIEM helps turn this raw information into something that analysts can use by providing:

```text
Centralization
Normalization
Correlation
Detection
Alerting
Visualization
Investigation Support
```

Another important lesson is that alerts are not automatically incidents.

A detection rule can identify something unusual, but a SOC analyst still needs to investigate the event and determine whether it represents malicious activity, legitimate activity, or a detection that needs improvement.

This is why SIEM knowledge is one of the foundational skills for a SOC analyst.

---

## 17. Important Terms

| Term                | Simple Meaning                                              |
| ------------------- | ----------------------------------------------------------- |
| SIEM                | Platform that collects and analyzes security logs           |
| Log                 | Record of something that happened                           |
| Host-Centric Log    | Log describing activity on a device                         |
| Network-Centric Log | Log describing network communication                        |
| Normalization       | Making different log formats easier to analyze consistently |
| Correlation         | Connecting related events from different sources            |
| Detection Rule      | Logic used to identify suspicious activity                  |
| Alert               | Notification generated when a detection rule matches        |
| True Positive       | Alert representing real suspicious activity                 |
| False Positive      | Alert caused by legitimate activity                         |
| Log Source          | System or device producing logs                             |
| Event ID            | Identifier for a specific Windows event                     |
| SIEM Dashboard      | Visual interface showing security information               |
| SOC                 | Security Operations Center                                  |
| Syslog              | Common method for transporting log information              |

---

## 18. Final Reflection

The Introduction to SIEM room provides the foundation for understanding how modern security operations handle large amounts of security data.

The key progression is:

```text
Systems Generate Logs
        ↓
Logs Are Collected
        ↓
SIEM Centralizes Them
        ↓
Logs Are Normalized
        ↓
Events Are Correlated
        ↓
Detection Rules Analyze Them
        ↓
Alerts Are Generated
        ↓
SOC Analysts Investigate
        ↓
Security Actions Are Taken
```

Understanding this workflow is important before moving into more advanced SIEM topics such as searching, query languages, detection engineering, threat hunting, incident investigation, and alert triage.

This room serves as a strong starting point for building practical SOC analyst fundamentals.
