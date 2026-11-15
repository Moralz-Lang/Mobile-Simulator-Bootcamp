# 📂 Resources

```text
📂 Resources
├── Commands.md
├── Cheat Sheet.md   ← You are here
├── Glossary.md
└── References.md
```

---

# 📄 Cheat Sheet.md

# Mobile Security Bootcamp Cheat Sheet

> A condensed reference covering the most important concepts, commands, workflows, and defensive practices from the Mobile Security Bootcamp.

---

# 1. Mobile Security Investigation Workflow

```text
Alert
  ↓
Verify
  ↓
Preserve Evidence
  ↓
Collect Device Information
  ↓
Collect Installed Apps
  ↓
Review Permissions
  ↓
Review Running Processes
  ↓
Review Running Services
  ↓
Review Network Activity
  ↓
Review Logs
  ↓
Correlate IoCs
  ↓
MITRE ATT&CK Mapping
  ↓
Risk Assessment
  ↓
Containment
  ↓
Recovery
  ↓
Lessons Learned
```

---

# 2. Android Architecture

```
Applications
↓

Application Framework

↓

Android Runtime (ART)

↓

Native Libraries

↓

Linux Kernel
```

Remember:

- Linux Kernel provides process isolation and hardware access.
    
- ART executes Android applications.
    
- Applications run inside isolated sandboxes.
    
- Permissions regulate access to sensitive resources.
    

---

# 3. APK Structure

```
AndroidManifest.xml
classes.dex
resources.arsc
assets/
res/
META-INF/
lib/
```

Most important files:

|File|Purpose|
|---|---|
|AndroidManifest.xml|Permissions and components|
|classes.dex|Executable bytecode|
|META-INF|Application signatures|
|lib|Native libraries|
|assets|Developer files|

---

# 4. Android Components

Activities

- User interface
    

Services

- Background tasks
    

Broadcast Receivers

- Respond to system events
    

Content Providers

- Share structured data
    

---

# 5. Dangerous Permissions

Be especially cautious when applications request combinations of:

- SMS
    
- Contacts
    
- Phone
    
- Camera
    
- Microphone
    
- Location
    
- Storage
    
- Calendar
    
- Call Logs
    

A single dangerous permission is not necessarily malicious, but unrelated or excessive permissions deserve investigation.

---

# 6. Common Indicators of Compromise (IoCs)

Performance

- Slow device
    
- Frequent crashes
    
- Overheating
    

Battery

- Rapid battery drain
    
- High background usage
    

Network

- Unusual uploads
    
- Frequent outbound connections
    
- Unknown domains
    

Applications

- Unknown installs
    
- Side-loaded APKs
    
- Unexpected updates
    

Permissions

- Excessive permission requests
    
- Recently granted sensitive permissions
    

Persistence

- Boot receivers
    
- Foreground services
    
- Background services
    

User Indicators

- Random pop-ups
    
- SMS sent automatically
    
- Camera or microphone activation
    
- Browser redirects
    

---

# 7. ADB Commands

Connect device

```bash
adb devices
```

Interactive shell

```bash
adb shell
```

Installed packages

```bash
adb shell pm list packages
```

Package details

```bash
adb shell dumpsys package package.name
```

Processes

```bash
adb shell ps -A
```

Services

```bash
adb shell dumpsys activity services
```

Battery

```bash
adb shell dumpsys battery
```

Battery statistics

```bash
adb shell dumpsys batterystats
```

Logs

```bash
adb logcat
```

Storage

```bash
adb shell df -h
```

Properties

```bash
adb shell getprop
```

---

# 8. APK Analysis Tools

|Tool|Purpose|
|---|---|
|apktool|Decode APK|
|aapt|APK information|
|apksigner|Signature verification|
|jadx|Java decompilation|
|Android Studio|Dynamic testing|
|adb|Device interaction|

---

# 9. Investigation Priorities

Always determine:

1. What happened?
    
2. When did it happen?
    
3. Which application is involved?
    
4. What permissions exist?
    
5. Is persistence present?
    
6. Is there active network communication?
    
7. What evidence supports the conclusion?
    

---

# 10. Mobile Malware Behaviors

Common behaviors include:

- Data theft
    
- SMS abuse
    
- Contact harvesting
    
- Credential theft
    
- Surveillance
    
- Remote command execution
    
- Advertising fraud
    
- Banking overlays
    
- Ransomware
    
- Spyware
    

---

# 11. Mobile EDR Workflow

```
Collect Telemetry
↓

Behavior Analysis

↓

Detection

↓

Alert

↓

Investigation

↓

Containment

↓

Recovery
```

---

# 12. Mobile Threat Defense (MTD)

Protects against:

- Phishing
    
- Malicious applications
    
- Unsafe Wi-Fi
    
- Network attacks
    
- Jailbroken/rooted devices
    
- Risky configurations
    

---

# 13. Mobile Identity Detection and Response (IDR)

Protects identities by detecting:

- Impossible travel
    
- MFA fatigue attacks
    
- Token theft
    
- Session hijacking
    
- Account compromise
    
- Conditional access bypass
    

---

# 14. MDM Responsibilities

- Device enrollment
    
- Security policies
    
- Compliance enforcement
    
- Remote lock
    
- Remote wipe
    
- Application inventory
    
- Certificate deployment
    
- OS update management
    

---

# 15. Mobile Incident Response Lifecycle

```
Preparation

↓

Identification

↓

Containment

↓

Eradication

↓

Recovery

↓

Lessons Learned
```

---

# 16. MITRE ATT&CK (Mobile) Examples

|Behavior|ATT&CK Tactic|
|---|---|
|Malicious APK installation|Initial Access|
|Auto-start on boot|Persistence|
|Camera use|Collection|
|Contact access|Collection|
|SMS interception|Credential Access / Collection|
|Outbound C2 traffic|Command and Control|
|Data exfiltration|Exfiltration|

---

# 17. Defensive Best Practices

Users should:

- Install applications only from trusted sources.
    
- Keep the operating system updated.
    
- Review permission requests carefully.
    
- Enable MFA where possible.
    
- Avoid unknown links and attachments.
    
- Back up important data regularly.
    

Organizations should:

- Deploy MDM/UEM solutions.
    
- Use Mobile Threat Defense.
    
- Monitor with EDR/XDR platforms.
    
- Restrict application sideloading.
    
- Require device encryption.
    
- Train users on phishing and social engineering.
    

---

# 18. Common Investigation Questions

Ask:

- Is this application expected?
    
- Is the permission appropriate?
    
- Does behavior match the application's purpose?
    
- Has anything changed recently?
    
- Can the behavior be explained by normal use?
    
- Are multiple IoCs present?
    
- What additional evidence is needed?
    

---

# 19. Common False Positives

Not every anomaly indicates malware.

Examples:

- New OS update increases battery usage.
    
- Navigation apps consume GPS and battery.
    
- Video calls use the camera and microphone.
    
- Backup applications generate network traffic.
    
- Streaming services increase data usage.
    
- Antivirus scans increase CPU usage.
    
- Cloud synchronization transfers large amounts of data.
    

Always investigate before concluding compromise.

---

# 20. Blue Team Investigation Checklist

☐ Preserve evidence

☐ Record device information

☐ Identify installed applications

☐ Review permissions

☐ Check running processes

☐ Review services

☐ Collect logs

☐ Review network activity

☐ Compare against a baseline

☐ Map findings to MITRE ATT&CK

☐ Assess risk

☐ Recommend containment

☐ Document findings

---

# 21. Mobile Security Mindset

Think like an investigator:

- Verify before acting.
    
- Correlate evidence from multiple sources.
    
- Avoid assumptions.
    
- Preserve evidence whenever possible.
    
- Maintain detailed documentation.
    
- Follow repeatable investigation procedures.
    
- Base conclusions on observable facts rather than a single indicator.
    

---

# Exam Tips

- Memorize Android's application components (Activities, Services, Broadcast Receivers, Content Providers).
    
- Know the difference between MDM, MTD, EDR, XDR, and IDR.
    
- Practice the core ADB commands until they become second nature.
    
- Understand that permissions alone do not prove malicious intent—context matters.
    
- Be comfortable mapping observed behaviors to the MITRE ATT&CK framework.
    
- Remember the incident response lifecycle: Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned.
    

---
# 📂 Resources

```text
📂 Resources
├── Commands.md
├── Cheat Sheet.md
├── Glossary.md   ← You are here
└── References.md
```

---

# 📄 Glossary.md

# Mobile Security Bootcamp Glossary

> A comprehensive glossary of mobile security, Android, iOS, enterprise mobility, digital forensics, malware analysis, networking, and defensive security terminology used throughout this bootcamp.

---

# A

## AAPT (Android Asset Packaging Tool)

A command-line utility included with the Android SDK used to inspect APK metadata, package resources, and application manifests.

---

## ADB (Android Debug Bridge)

A command-line tool that enables communication between a computer and an Android device or emulator for debugging, file transfer, application management, and forensic collection.

---

## Activity

An Android application component responsible for presenting a user interface (UI). Activities represent individual screens within an application.

---

## Android Emulator

A virtual Android device used for development, testing, and security research without requiring physical hardware.

---

## Android Framework

The layer of Android that provides APIs and system services used by applications.

---

## Android Runtime (ART)

The managed runtime environment responsible for executing Android applications.

---

## APK (Android Package)

The installation package format used to distribute Android applications. It contains compiled code, resources, assets, the manifest, and application signatures.

---

## APKTool

An open-source utility used to decode and rebuild Android APK files for analysis.

---

## App Sandbox

Android's security mechanism that isolates each application into its own process and user ID, limiting access to other applications and system resources.

---

## Attack Surface

The collection of all possible entry points through which an attacker may attempt to compromise a device or application.

---

## Authentication

The process of verifying the identity of a user, device, or service before granting access.

---

## Authorization

The process of determining which actions or resources an authenticated user is permitted to access.

---

# B

## Baseline

A known-good system state used for comparison during investigations to identify deviations or suspicious changes.

---

## Behavioral Detection

A detection approach that identifies malicious activity by observing actions and patterns rather than relying solely on known malware signatures.

---

## Broadcast Receiver

An Android component that listens for and responds to system-wide events, such as device boot completion or connectivity changes.

---

## BYOD (Bring Your Own Device)

A policy that allows employees to use personally owned mobile devices for work purposes.

---

# C

## Certificate

A digital credential used to verify identity and establish trust between systems.

---

## Chain of Custody

A documented process that tracks the collection, handling, transfer, and storage of digital evidence to preserve its integrity.

---

## Code Signing

The process of digitally signing an application to verify its authenticity and integrity.

---

## Collection

The forensic process of acquiring digital evidence from a device while preserving its integrity.

---

## Command and Control (C2)

An external infrastructure used by attackers to communicate with compromised devices, issue commands, or receive stolen data.

---

## Content Provider

An Android component that securely manages and shares structured data between applications.

---

## CVE (Common Vulnerabilities and Exposures)

A standardized identifier assigned to publicly disclosed software vulnerabilities.

---

# D

## Data Exfiltration

The unauthorized transfer of sensitive information from a device or organization to an external destination.

---

## Digital Forensics

The discipline of identifying, preserving, analyzing, and presenting digital evidence.

---

## Dynamic Analysis

The examination of an application while it is executing to observe its runtime behavior.

---

# E

## EDR (Endpoint Detection and Response)

A security platform that continuously monitors endpoints, detects suspicious behavior, and supports investigation and response activities.

---

## Emulator

Software that replicates the functionality of a physical device for testing or research.

---

## Encryption

The process of converting readable data into ciphertext to protect confidentiality.

---

## Enterprise Mobility Management (EMM)

A collection of technologies used to manage and secure enterprise mobile devices and applications.

---

## Evidence

Information collected during an investigation that supports or refutes a hypothesis.

---

## Exploit

Software or code that takes advantage of a vulnerability to perform unauthorized actions.

---

# F

## False Positive

A legitimate activity incorrectly identified as malicious.

---

## File Hash

A fixed-length cryptographic value representing a file's contents, used to verify integrity.

---

## Forensics

The scientific investigation and analysis of digital systems following a security event.

---

## Foreground Service

An Android service that performs user-visible tasks and displays a persistent notification.

---

# G

## Google Play Protect

Google's built-in Android security service that scans applications for known malicious behavior.

---

# H

## Hash

A unique cryptographic fingerprint generated from data to verify integrity or identify changes.

---

## Hooking

A technique used to intercept or modify function calls during application execution.

---

# I

## IAM (Identity and Access Management)

The policies, processes, and technologies used to manage digital identities and control access to resources.

---

## Incident Response (IR)

A structured process for identifying, containing, eradicating, recovering from, and documenting security incidents.

---

## Indicator of Compromise (IoC)

Observable evidence suggesting that a system may have been compromised, such as unusual processes, suspicious network connections, or unauthorized applications.

---

## IPA

The application package format used for Apple iOS applications.

---

## Integrity

The assurance that information has not been altered in an unauthorized manner.

---

# J

## Jailbreak

The process of removing Apple's software restrictions to obtain elevated privileges on an iOS device.

---

## JSON

(JavaScript Object Notation) A lightweight data-interchange format frequently used by APIs and mobile applications.

---

# K

## Kernel

The core operating system component responsible for process scheduling, memory management, hardware communication, and security enforcement.

---

## Keystore

A secure storage mechanism used to protect cryptographic keys on mobile devices.

---

# L

## Least Privilege

The security principle of granting only the minimum permissions necessary for a user or application to perform its intended function.

---

## Logcat

Android's logging system used to record application, system, and debugging events.

---

# M

## Malware

Software intentionally designed to perform unauthorized or harmful actions.

---

## Manifest (AndroidManifest.xml)

A configuration file describing an Android application's components, permissions, hardware requirements, and other metadata.

---

## Meterpreter

An advanced in-memory payload used during authorized penetration testing that provides post-exploitation capabilities. It is commonly discussed in security training but should only be used in approved lab environments.

---

## MDM (Mobile Device Management)

Software used to enroll, configure, monitor, and secure mobile devices within an organization.

---

## Mobile Application Management (MAM)

Management of enterprise applications without requiring full device management.

---

## Mobile Threat Defense (MTD)

Security software focused on detecting and mitigating threats targeting mobile devices.

---

## MITRE ATT&CK

A publicly available knowledge base of adversary tactics and techniques used to classify and describe attacker behavior.

---

# N

## Network Telemetry

Information describing network activity, including connections, bandwidth usage, DNS queries, and protocols.

---

## Non-Repudiation

The assurance that an action or transaction cannot later be denied by the responsible party.

---

# O

## Obfuscation

Techniques used to make application code more difficult to understand or reverse engineer.

---

## OEM

Original Equipment Manufacturer responsible for producing mobile hardware.

---

# P

## Package Manager

The Android subsystem responsible for installing, updating, and managing applications.

---

## Penetration Testing

An authorized security assessment that simulates attacks to evaluate security controls.

---

## Permission

Authorization granted to an application allowing access to protected resources or functionality.

---

## Persistence

Techniques used by malicious software to remain active across reboots or user sessions.

---

## Phishing

A social engineering attack that attempts to trick users into revealing sensitive information or installing malicious software.

---

## Play Store

Google's official Android application marketplace.

---

## Process

An executing instance of an application or service.

---

# R

## Reverse Engineering

The process of analyzing software to understand its design, functionality, and behavior.

---

## Root

Privileged administrative access on Android devices.

---

## Runtime Permission

A dangerous permission that Android requests from the user while the application is running.

---

# S

## Sandbox

An isolated execution environment that limits an application's ability to affect other applications or the operating system.

---

## Service

An Android component designed to perform long-running operations in the background.

---

## Side-loading

Installing applications from sources outside the official application store.

---

## Signature-Based Detection

A detection method that identifies known malware by matching predefined patterns or signatures.

---

## SOC (Security Operations Center)

A team responsible for monitoring, detecting, investigating, and responding to cybersecurity incidents.

---

## Static Analysis

Examining an application without executing it to identify code structure, resources, permissions, and potential security issues.

---

# T

## Telemetry

Operational data collected from devices or applications to support monitoring and threat detection.

---

## Threat Intelligence

Information about current threats, attacker tactics, techniques, procedures (TTPs), and indicators used to improve defense.

---

## TTPs (Tactics, Techniques, and Procedures)

Descriptions of how adversaries achieve objectives, commonly referenced using the MITRE ATT&CK framework.

---

# U

## UEM (Unified Endpoint Management)

A platform that manages desktops, laptops, mobile devices, tablets, and other enterprise endpoints from a single console.

---

## URL Filtering

A security capability that blocks access to malicious or unauthorized websites.

---

# V

## VirusTotal

A cloud-based service that analyzes files, URLs, and hashes using multiple security engines to help identify known malicious content.

---

## VPN (Virtual Private Network)

A secure encrypted tunnel that protects network communications over untrusted networks.

---

# W

## Wireshark

A network protocol analyzer used to capture and inspect network traffic.

---

## Work Profile

An Android Enterprise feature that separates corporate applications and data from personal content on a BYOD device.

---

# X

## XDR (Extended Detection and Response)

A security platform that correlates telemetry from multiple sources (such as endpoints, identity systems, cloud services, email, and networks) to improve detection and response capabilities.

---

## Xcode

Apple's integrated development environment (IDE) used for iOS and macOS application development, testing, and simulation.

---

# Z

## Zero-Day Vulnerability

A previously unknown software vulnerability for which no official patch or mitigation is available when it is discovered or exploited.

---

# Acronyms Quick Reference

|Acronym|Meaning|
|---|---|
|ADB|Android Debug Bridge|
|APK|Android Package|
|ART|Android Runtime|
|ATT&CK|Adversarial Tactics, Techniques, and Common Knowledge|
|BYOD|Bring Your Own Device|
|C2|Command and Control|
|CVE|Common Vulnerabilities and Exposures|
|EDR|Endpoint Detection and Response|
|EMM|Enterprise Mobility Management|
|IAM|Identity and Access Management|
|IoC|Indicator of Compromise|
|IPA|iOS Application Archive|
|IR|Incident Response|
|MAM|Mobile Application Management|
|MDM|Mobile Device Management|
|MTD|Mobile Threat Defense|
|OEM|Original Equipment Manufacturer|
|SOC|Security Operations Center|
|TTP|Tactics, Techniques, and Procedures|
|UEM|Unified Endpoint Management|
|VPN|Virtual Private Network|
|XDR|Extended Detection and Response|

---

## Study Tips

- Learn the glossary terms together with practical labs rather than memorizing definitions in isolation.
    
- Be able to explain not only _what_ each term means, but also _when_ and _why_ it is important during a mobile security investigation.
    
- Cross-reference these definitions with your notes on Android architecture, permissions, application analysis, incident response, and enterprise mobile security for better retention.
    

---
