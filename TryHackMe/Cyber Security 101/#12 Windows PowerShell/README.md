# Windows PowerShell - TryHackMe Learning Repository

## Overview

This repository documents my learning journey through the **Windows PowerShell** TryHackMe room. Instead of focusing on finding flags, this repository focuses on understanding PowerShell from a beginner's perspective, learning why it is important in cybersecurity, and building practical skills that can be used in real-world environments.

PowerShell is much more than a command-line tool. It is Microsoft's automation and scripting framework that allows administrators, defenders, and penetration testers to manage Windows systems efficiently.

---

# Learning Objectives

After completing this room, I learned how to:

* Understand what Windows PowerShell is.
* Differentiate PowerShell from Command Prompt (CMD).
* Understand object-based output.
* Learn the Cmdlet naming convention.
* Navigate the Windows file system using PowerShell.
* Create, copy, move, and delete files and folders.
* Read file contents.
* Use help commands to learn new cmdlets.
* Filter, sort, and search PowerShell output.
* Gather system and network information.
* Monitor processes and services.
* Generate file hashes.
* Understand the basics of PowerShell scripting.
* Understand why PowerShell is important in cybersecurity.

---

# Room Summary

The room begins by introducing PowerShell as Microsoft's command-line shell, scripting language, and automation framework. Unlike Command Prompt, which mainly returns plain text, PowerShell works with objects. These objects contain both data and functionality, making automation and system management much easier.

The room then introduces Cmdlets, which follow a Verb-Noun naming convention. Understanding this naming structure makes learning new PowerShell commands much easier.

The later tasks focus on practical usage, including file system navigation, object filtering, pipelines, system enumeration, process monitoring, networking commands, hashing, and scripting fundamentals.

---

# Key Concepts Learned

## PowerShell

* Microsoft command-line shell
* Scripting language
* Automation framework

---

## CMD vs PowerShell

CMD

* Text-based output
* Limited automation
* Older Windows shell

PowerShell

* Object-based output
* Powerful automation
* Advanced scripting
* Better system administration

---

## Objects

PowerShell works with objects instead of plain text.

Every object contains:

* Properties
* Methods

Example:

Process Object

Properties

* Name
* Process ID
* CPU Usage
* Memory Usage

Methods

* Stop
* Kill
* Restart

---

## Cmdlets

PowerShell commands are called **Cmdlets**.

Format

Verb-Noun

Examples

* Get-Command
* Get-Help
* Get-Process
* Set-Location
* Get-Content
* Copy-Item

---

# Important Cmdlets Covered

### Discovery

* Get-Command
* Get-Help

### File System

* Get-ChildItem
* Set-Location
* New-Item
* Remove-Item
* Copy-Item
* Move-Item
* Get-Content

### Searching Modules

* Find-Module
* Install-Module

### Filtering

* Where-Object
* Select-Object
* Select-String
* Sort-Object

### System Information

* Get-ComputerInfo
* Get-LocalUser
* Get-NetIPConfiguration
* Get-NetIPAddress

### Monitoring

* Get-Process
* Get-Service
* Get-NetTCPConnection
* Get-FileHash

### Remote Administration

* Invoke-Command

---

# Important PowerShell Features

## Pipelines

PowerShell pipelines pass objects from one command directly into another command.

This allows multiple commands to work together without manually copying output.

---

## Filtering

Instead of displaying everything, PowerShell can filter only the required information using Where-Object.

---

## Sorting

Sort-Object helps organize output based on different properties like:

* Name
* Length
* Date
* Size

---

## Searching

Select-String allows searching inside files, similar to grep in Linux.

---

## PowerShell Scripting

A PowerShell script is simply a text file containing multiple PowerShell commands that execute automatically.

Benefits include:

* Automation
* Reduced manual work
* Faster administration
* Fewer human errors
* Repeatable tasks

---

# Cybersecurity Relevance

## Blue Team

PowerShell is commonly used to:

* Analyze logs
* Monitor systems
* Collect forensic information
* Investigate incidents
* Audit Windows environments

---

## Red Team

PowerShell is commonly used to:

* Execute remote commands
* Automate assessments
* Perform system enumeration
* Execute scripts
* Simulate attacks during authorized engagements

---

# Biggest Takeaways

* PowerShell is object-oriented.
* Cmdlets follow the Verb-Noun format.
* Pipelines make automation powerful.
* Objects can be filtered, sorted, and searched easily.
* PowerShell is a core Windows administration skill.
* PowerShell knowledge is valuable for both offensive and defensive security roles.

---

# Challenges Faced During Learning

While learning this room, some concepts were initially confusing:

* Understanding object-based output.
* Remembering Cmdlet naming conventions.
* Learning the difference between CMD commands and PowerShell Cmdlets.
* Understanding pipelines.
* Filtering objects using properties.
* Reading long command syntax.

Repeated practice made these concepts much easier.

---

# Beginner Practice

Practice the following commands yourself:

* List files inside a directory.
* Change directories.
* Create a new folder.
* Create a text file.
* Read file contents.
* Copy a file.
* Move a file.
* Delete a file.
* List running processes.
* List services.
* View network configuration.
* Generate a file hash.
* Search inside a text file.
* Filter output using Where-Object.
* Sort files by size.

---

# Skills Gained

* Windows PowerShell fundamentals
* Windows administration basics
* Object-oriented command execution
* File management
* System enumeration
* Network enumeration
* Process monitoring
* Service monitoring
* Data filtering
* Automation basics
* PowerShell scripting fundamentals

---

# Final Thoughts

This room provides an excellent introduction to Windows PowerShell. Rather than memorizing commands, the biggest lesson is understanding how PowerShell thinks—working with objects, combining commands through pipelines, and automating repetitive tasks. These fundamentals form the foundation for Windows administration, SOC operations, incident response, digital forensics, and penetration testing.
