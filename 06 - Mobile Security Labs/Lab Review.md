
# 📂 Module 6.7 — Lab Review & Knowledge Consolidation

```text
📂 06 - Mobile Security Labs
│
└── Lab Review.md
```

---

# Objective

After completing the labs, you should be able to:

- Explain what each tool does.
    
- Understand why each command was used.
    
- Recognize normal vs. suspicious mobile application behavior.
    
- Document findings like a security analyst.
    
- Connect each lab to real-world mobile security operations.
    

---

# Lab 1 Review — Android Emulator

## What You Learned

You created a safe environment to analyze Android applications without using a physical device.

### Why use an emulator?

- Safe testing environment
    
- Easy to snapshot and restore
    
- No risk to personal data
    
- Easier debugging
    
- Repeatable experiments
    

### Key Components

|Component|Purpose|
|---|---|
|Android Studio|Development IDE|
|Android Emulator|Virtual Android device|
|Android SDK|Android libraries and tools|
|ADB|Android Debug Bridge|

---

## Questions

### Why is an emulator preferable during security research?

Answer:

Because mistakes can easily be rolled back, applications cannot affect your personal phone, and experiments are reproducible.

---

### What does ADB allow you to do?

Answer:

ADB provides a bridge between the workstation and Android device, allowing file transfers, shell access, logging, application management, and system inspection.

---

# Lab 2 Review — iOS Simulator

## Important Difference

Android Emulators

↓

Emulate an entire Android device.

iOS Simulator

↓

Simulates an iPhone environment but does **not** emulate ARM hardware.

---

### Why is this important?

Some malware or low-level exploits that rely on ARM-specific behavior may not execute in the simulator, so physical devices are often required for advanced iOS security testing.

---

# Lab 3 Review — Permissions

One of Android's most important security mechanisms is its permission model.

---

## Normal Permissions

Automatically granted.

Examples

- Internet
    
- Vibration
    
- Network state
    

---

## Dangerous Permissions

Require user approval.

Examples

- Camera
    
- Microphone
    
- Contacts
    
- SMS
    
- Phone
    
- Calendar
    
- Storage
    
- Location
    

---

## Why Permissions Matter

An application requesting more permissions than necessary may increase its attack surface and privacy risk. Reviewing permissions is a key part of assessing application behavior.

---

### Exercise

Consider an application that requests:

- Camera
    
- SMS
    
- Contacts
    
- Microphone
    
- Location
    

Question:

Would all of these permissions make sense for a flashlight application?

Expected Answer:

No. A flashlight application typically only needs access to the camera flash. Requests for SMS, contacts, microphone, or location would warrant further scrutiny.

---

# Lab 4 Review — Traffic Observation

Applications constantly communicate over networks.

During packet capture you observed:

DNS

↓

Domain lookup

HTTPS

↓

Encrypted application traffic

TLS

↓

Encryption negotiation

TCP

↓

Reliable transport

---

## Typical Flow

Application

↓

DNS Query

↓

DNS Response

↓

TCP Handshake

↓

TLS Handshake

↓

HTTPS Request

↓

HTTPS Response

---

### Questions

Why can't Wireshark read HTTPS data?

Answer:

Because HTTPS encrypts application-layer content using TLS. Without the appropriate session keys, Wireshark can only observe metadata such as IP addresses, ports, and certificate information.

---

# Lab 5 Review — APK Static Analysis

Static analysis means:

No execution.

Only inspection.

---

### Files Reviewed

AndroidManifest.xml

classes.dex

resources.arsc

res/

META-INF/

---

### What the Manifest Contains

Package name

Permissions

Activities

Services

Receivers

Content Providers

SDK versions

Intent filters

---

## Questions

Why inspect the manifest first?

Answer:

It provides a high-level overview of the application's declared capabilities, required permissions, and exposed components before examining code.

---

# Lab 6 Review — Defensive Detection

This lab emphasized identifying behaviors that could indicate misuse or compromise.

---

## Important Commands

```bash
adb shell ps
```

List running processes.

---

```bash
adb shell pm list packages
```

List installed packages.

---

```bash
adb shell dumpsys activity
```

Show current activities.

---

```bash
adb shell dumpsys batterystats
```

Battery information.

---

```bash
adb shell dumpsys meminfo
```

Memory usage.

---

## What Can You Detect?

Unexpected background processes

Unknown packages

Applications with excessive permissions

Battery anomalies

High resource usage

Unexpected network activity

---

# Putting It All Together

Suppose you observe the following:

- A notes application requests Camera, Contacts, SMS, and Microphone permissions.
    
- It consumes significant battery while idle.
    
- It maintains frequent outbound network connections.
    
- It appears in the running processes list even when not in use.
    

These observations do not, by themselves, prove malicious activity. However, they would justify a deeper investigation to determine whether the behavior is expected for that application or indicative of a security issue.

---

# Knowledge Check

### Question 1

What file contains an Android application's declared permissions?

**Answer:** `AndroidManifest.xml`

---

### Question 2

What command lists installed Android packages?

**Answer:**

```bash
adb shell pm list packages
```

---

### Question 3

What protocol encrypts HTTPS traffic?

**Answer:** TLS

---

### Question 4

What tool is commonly used to decompile Android applications for static analysis?

**Answer:** JADX

---

### Question 5

What Android tool allows shell access to an emulator or device?

**Answer:** ADB (Android Debug Bridge)

---

# Mini Case Study

## Scenario

A security team receives reports that an employee-installed application is draining battery life and requesting access to contacts and location despite being advertised as a simple wallpaper app.

### Your Tasks

1. Review the application's requested permissions.
    
2. Capture and analyze its network traffic.
    
3. Perform static analysis of the APK.
    
4. Check for unusual background processes or services.
    
5. Document findings, assess risk, and recommend appropriate actions based on the evidence collected.
    

---

# Reflection Questions

Add the following to your daily log:

- Which lab was the most challenging?
    
- Which tool did you use the most?
    
- What Android component (Activities, Services, Receivers, or Providers) do you understand best now?
    
- Which concept needs more practice?
    
- If you were briefing a manager, how would you summarize today's findings in three sentences?
    

---

# Module 6 Completion Checklist

- ☐ Android emulator configured and verified
    
- ☐ iOS simulator explored (if applicable)
    
- ☐ Application permissions reviewed
    
- ☐ Network traffic captured and analyzed
    
- ☐ APK statically analyzed
    
- ☐ System state examined with ADB
    
- ☐ Findings documented
    
- ☐ Knowledge check completed
    
- ☐ Reflection written
    

---

## 🎉 Module 6 Complete

At this point, you have built a solid foundation in **mobile application analysis**, **network observation**, **static APK inspection**, and **defensive detection techniques**. The next module shifts from performing analysis to understanding how defenders identify, monitor, and respond to mobile threats at scale.

**Next up:** **📂 Module 7 — Blue Team**, where we'll cover mobile indicators of compromise (IoCs), mobile malware detection, Mobile Device Management (MDM), Enterprise Mobility Management (EMM), Endpoint Detection and Response (EDR), and mapping mobile threats to the MITRE ATT&CK framework.