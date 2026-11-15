Objective

Identify indicators of potentially suspicious mobile application behavior in a controlled environment.

---

Observe

Settings

Apps

Battery Usage

Network Usage

Permissions

Notifications

Storage

Background Activity

Accessibility Services

Device Admin Apps

VPN Settings

Installed Certificates

Developer Options

---

Collect

Running Processes:

adb shell ps

Installed Packages:

adb shell pm list packages

Foreground Activity:

adb shell dumpsys activity

Battery:

adb shell dumpsys batterystats

Memory:

adb shell dumpsys meminfo

Network Interfaces:

adb shell ip addr

---
Indicators

Unexpected background services

Unusual battery consumption

High network usage

Frequent wake locks

Unexpected accessibility service

Suspicious permissions

Unknown packages

Excessive notifications

Unexpected certificate installation

---

MITRE ATT&CK Mapping

Initial Access

Execution

Persistence

Privilege Escalation

Credential Access

Discovery

Collection

Command and Control

Exfiltration

---

Incident Report

Record

Application

Package

Version

Permissions

Indicators

Evidence

Risk Rating

Recommendation

MITRE Techniques
