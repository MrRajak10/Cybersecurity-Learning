Welcome to **Windows Fundamentals 2**. This is where you transition from being a standard computer user to thinking like a system administrator and a cybersecurity professional.

The tools in this room are the exact same tools that IT professionals use daily to keep networks running, and the same tools that Security Operations Center (SOC) analysts use to hunt for hackers. Let's break down each of these utilities, understand how they work under the hood, and look at how attackers might try to abuse them.

---

## 1. System Configuration (`msconfig`)

### What it is and How it works

Think of `msconfig` as the control room for how your operating system "wakes up." When you turn on your computer, Windows has to load hundreds of drivers, background services, and graphical elements. MSConfig allows you to dictate exactly what gets loaded and what gets ignored.

<img width="688" height="446" alt="image" src="https://github.com/user-attachments/assets/2f4d2a87-df27-46cb-82c1-93d010d55f21" />


* **Safe Boot (Safe Mode):** This forces Windows to start with only the absolute bare minimum, Microsoft-signed drivers needed to run the OS. No third-party audio drivers, no heavy graphics cards, and no startup apps.
* **Selective Startup:** You can manually check boxes to stop loading system services or startup items.

### Why Security Professionals Care

* **Incident Response (IR):** If a machine is infected with malware that starts every time the computer boots, an Incident Responder will reboot the machine into **Safe Mode**. Because Safe Mode only loads essential Windows files, the malware usually won't start, allowing the responder to delete the malicious files safely.
* **Malware Analysis:** Sometimes, analysts will intentionally use `msconfig` to disable all third-party services to isolate a strange behavior and see if it is caused by Windows itself or an installed program.

---

## 2. Advanced System Settings

### The Page File (Virtual Memory)

RAM (Physical Memory) is extremely fast but limited. If you open too many Chrome tabs, your RAM fills up. Instead of crashing, Windows takes the data in RAM that you haven't used in a while and temporarily writes it to the hard drive in a hidden file called `pagefile.sys`.

* **Analogy:** Think of RAM as your physical desk. You can only fit so many papers on it. The `pagefile.sys` is a filing cabinet next to your desk. When your desk is full, you shove some papers into the cabinet. It takes a little longer to retrieve them later (which is why computers slow down when RAM is full), but it keeps you from dropping everything on the floor.

### Crash Dumps

When Windows encounters a fatal error (the infamous Blue Screen of Death), it dumps whatever was currently in the RAM into a file (e.g., `memory.dmp`) before shutting down so developers can figure out what went wrong.

> **Cybersecurity Context:** Penetration testers and forensic investigators *love* memory dumps and page files. Because they are snapshots of RAM, they often contain **plaintext passwords**, decryption keys, and the unencrypted payloads of malware. Attackers will often try to steal the `pagefile.sys` to extract passwords.

---

## 3. User Account Control (UAC)

### What it is

UAC is that familiar screen that pops up, dims your desktop, and asks, *"Do you want to allow this app to make changes to your device?"*

Even if you are logged in as an "Administrator," Windows actually treats you as a standard, low-privilege user for everyday tasks (like browsing the web or writing a document). If you try to do something that affects the whole system (like installing software), UAC pauses everything and forces you to explicitly confirm you want to use your Administrator powers.

### Cybersecurity Context

* **Privilege Escalation:** In penetration testing, simply getting a foothold on a machine isn't enough; you usually land as a standard user. To turn off antivirus or dump passwords, you need Administrator rights. Bypassing UAC (tricking Windows into granting admin rights without showing the popup to the user) is a massive part of Windows hacking.

---

## 4. Computer Management (`compmgmt.msc`)

This is the "Swiss Army Knife" of Windows administration. It bundles multiple tools into one window.

### Task Scheduler

* **What it does:** Allows you to tell Windows, "Run *this* specific program, at *this* specific time, or when *this* specific event happens."
* **Cybersecurity Context:** This is the number one way attackers achieve **Persistence**. If a hacker gets a reverse shell on a machine, they will lose access if the user reboots. So, they create a hidden Scheduled Task that says, "Run my malware every day at 9:00 AM or every time the user logs in."

### Event Viewer

This is arguably the most important tool for a defender. Windows records almost everything that happens in the background into log files.

<img width="442" height="226" alt="image" src="https://github.com/user-attachments/assets/26d4b2b8-f67c-494c-aaac-3ee74e33c47f" />


* **Application Logs:** Errors or crashes from software (like Microsoft Word or a web server).
* **Security Logs:** The holy grail for SOC analysts. This tracks logins, logoffs, and permission changes.
* **System Logs:** OS-level events, like drivers loading or hard drives failing.

> **Real-World SOC Operation:** Analysts don't read these manually. Logs are forwarded to a SIEM (like Splunk or Sentinel). If the SIEM sees **Event ID 4625 (Failed Login)** happen 500 times in two minutes, followed by **Event ID 4624 (Successful Login)**, the SOC analyst gets an alert for a successful brute-force attack!

### Local Users and Groups

* **Cybersecurity Context:** After an attacker gains admin access, they often create a hidden "backdoor" user account (e.g., creating a user named `BackupAdmin` and hiding it) so they can log back in later even if their malware is caught. Defenders check this menu to spot rogue accounts.

---

## 5. System Information and Resource Monitor

### `msinfo32` (System Information)

Takes a static snapshot of the computer's hardware, drivers, and environment variables. If an incident responder needs to know exactly what patch level and hardware a compromised machine is running, they pull this.

### `resmon` (Resource Monitor)

Shows you the *live pulse* of the machine. It breaks down exactly which applications are using the CPU, Memory, Disk, and Network.

<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/45910450-36cb-487a-9e1d-aea6a060580b" />


* **Cybersecurity Context:** If a computer is running slowly, a user might think it's just old. A SOC analyst will open the **Network tab** in `resmon`. If they see a weird, unknown process (like `svch0st.exe`—notice the zero instead of an 'o') uploading gigabytes of data to an IP address in a foreign country, they just caught data exfiltration in real-time.

---

## 6. Command Prompt Basics for Networking

Network troubleshooting is a core skill for any IT or security role. Here is how to read the commands:

### `ipconfig /all`

* **What it does:** Shows your complete network identity.
* **Key Outputs:**
* `IPv4 Address`: Your computer's local IP on the network (usually starts with 192.168.x.x or 10.x.x.x).
* `MAC Address`: The unchangeable, physical serial number of your network card.
* `Default Gateway`: The IP address of your router (the door out to the internet).



### `netstat` (Network Statistics)

* **What it does:** Shows every active network connection your computer is currently making with the outside world.
* **Key States to know:**
* `LISTENING`: Your computer has opened a port and is waiting for someone to connect to it (Servers do this).
* `ESTABLISHED`: A live, active connection where data is currently flowing back and forth.


* **Cybersecurity Context:** If a malware infection creates a reverse shell back to a hacker's Command and Control (C2) server, running `netstat` will show an `ESTABLISHED` connection to the hacker's IP address.

---

## 7. Registry Editor (`regedit`)

### What it is

The Windows Registry is the DNA of the operating system. It is a massive, hierarchical database that stores settings for the OS, hardware, and all installed software.

<img width="764" height="401" alt="image" src="https://github.com/user-attachments/assets/f99cc8ad-a286-4595-96e3-5f0af319b236" />


### How it works internally

Instead of files and folders, the Registry uses:

1. **Hives / Keys:** (Think of these like folders). E.g., `HKEY_CURRENT_USER` stores settings just for your logged-in profile.
2. **Values:** (Think of these like the files inside the folder). They contain the actual data, like `0` for OFF and `1` for ON.

### Cybersecurity Context

Because *everything* is in the registry, attackers manipulate it constantly:

* **Disabling Defenses:** Attackers will navigate to the Windows Defender registry keys and change the "DisableRealtimeMonitoring" value from `0` to `1`.
* **Persistence (Autoruns):** There are specific "Run" keys in the registry. Any program listed there automatically executes when the computer turns on. Attackers put their malware in these keys.
* **Credential Theft:** The registry stores a heavily encrypted database of all user passwords on the computer (called the SAM hive). Attackers will try to copy this hive to crack the passwords offline.

> **Common Beginner Mistake:** Changing things in `regedit` without knowing what they do. Because the registry controls the OS at a fundamental level, deleting the wrong key can instantly break Windows and prevent it from booting.

---
