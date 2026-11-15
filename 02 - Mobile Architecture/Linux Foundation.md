Status:: 🌱 Learning
Module:: Android Architecture
Lesson:: 2
Difficulty:: ⭐⭐⭐☆☆
Confidence:: ★☆☆☆☆

Tags::
#android #linux #architecture #mobile-security

---

# Definition

Android is built on top of the Linux kernel.

Linux is responsible for:

- Process management
- Memory management
- Scheduling
- Filesystems
- Device drivers
- User isolation
- Security enforcement

Android does NOT replace Linux.

Android extends Linux with mobile-specific components.

---

# Why It Exists

Linux provides an operating system that is:

- Stable
- Secure
- Portable
- Efficient
- Open Source

Instead of writing an operating system from scratch, Android builds on Linux and adds:

- Application Framework
- ART Runtime
- Binder IPC
- HAL
- System Services

---

# Mental Model

Imagine Linux as the foundation of a skyscraper.

You rarely see it.

But every floor depends on it.

Android simply builds additional floors on top.

---

# Android Stack

Applications

↓

Android Framework

↓

ART Runtime

↓

Binder

↓

Linux Kernel

↓

Hardware

Everything above eventually depends on Linux.

---

# Linux Responsibilities

## Process Management

Linux creates and manages running applications.

Every Android app is a Linux process.

---

## Memory Management

Linux controls:

- RAM
- Virtual Memory
- Memory Protection

Apps cannot freely read another app's memory.

---

## Scheduling

Many apps run simultaneously.

Linux decides:

- which process runs
- when it runs
- how long it runs

---

## Filesystem

Linux manages:

- Internal Storage
- Cache
- Databases
- APK installation paths

---

## Device Drivers

Linux communicates with:

- Camera
- GPS
- Display
- USB
- Wi-Fi
- Bluetooth
- NFC

Applications never communicate with drivers directly.

---

# Security Importance

Linux provides Android with:

✔ Process Isolation

✔ User IDs (UIDs)

✔ File Permissions

✔ SELinux Enforcement

✔ Driver Isolation

These become Android's first security boundary.

---

# Execution Flow

User opens Camera

↓

Camera App

↓

Android Framework

↓

Binder

↓

Camera Service

↓

Linux Driver

↓

Camera Hardware

Notice:

Linux is the first software that actually talks to hardware.

---

# Reverse Engineering Perspective

Questions to ask:

Which Linux feature supports this Android behavior?

Is this:

- Filesystem?
- Process?
- Driver?
- Memory?
- Scheduler?

Does execution leave Android and enter the kernel?

---

# Blue Team Perspective

Monitor:

- Process creation
- File access
- Driver interactions
- SELinux denials
- Permission enforcement

---

# Common Mistakes

❌ Android replaced Linux

❌ Linux only manages files

❌ Apps access hardware directly

❌ Binder replaces Linux

Binder actually runs on top of Linux.

---

# Real World Examples

Instagram

↓

Linux creates Instagram process

↓

Instagram requests Camera

↓

Linux schedules process

↓

Linux driver communicates with camera hardware

---

Google Maps

↓

GPS Request

↓

Linux Driver

↓

GPS Chip

↓

Coordinates Returned

---

# Related Concepts

[[Android Architecture]]

[[Linux Kernel]]

[[Processes]]

[[Memory]]

[[Binder IPC]]

[[System Services]]

[[Application Lifecycle]]

---

# Related Labs

[[Lab 1 - Android Emulator]]

[[Lab 5 - APK Static Analysis]]

---

# Reverse Engineer Questions

What Linux subsystem supports this feature?

Which system call eventually executes?

Can this be observed?

Where does Android stop?

Where does Linux begin?

---

# Defender Questions

How is Linux enforcing security?

Can another process access this?

What logs would show abnormal behavior?

---

# Neural Connections

Depends On

[[Operating Systems]]

[[Computer Architecture]]

Explains

[[Processes]]

[[Memory]]

[[Binder IPC]]

[[Permissions]]

[[Storage]]

Leads To

[[Linux Kernel]]

[[SELinux]]

[[System Calls]]

[[JNI]]

---

# Key Insight

Android is not a separate operating system.

Android is a mobile software platform built on top of the Linux kernel.

---

## 🔗 Future Concepts

[[Linux Kernel]]

[[Processes]]

[[Threads]]

[[Memory]]

[[Virtual Memory]]

[[Paging]]

[[CPU Scheduler]]

[[Filesystem]]

[[ext4]]

[[Device Drivers]]

[[Kernel Space]]

[[User Space]]

[[System Calls]]

[[SELinux]]

[[UID]]

[[GID]]

[[Binder IPC]]

[[HAL]]

[[System Services]]

[[ART Runtime]]

[[JNI]]

[[Android Boot Process]]

[[Init Process]]

[[Zygote]]

[[SurfaceFlinger]]

[[Activity Manager]]

[[Package Manager]]

[[Android Security Model]]

---
# 📖 Recommended Reading

As with previous lessons, keep a "Further Reading" section and prioritize primary sources:

- Android Developers — Android Architecture and Processes
- Android Open Source Project (AOSP) — Kernel and platform architecture
- Linux Kernel Documentation — Process management, scheduling, memory, and device drivers
- OWASP Mobile Application Security Testing Guide (MASTG) — Android platform architecture and security model

---

# 📈 Learning Path

Your dependency graph now looks like this:

```
Android Architecture
        │
        ▼
Linux Foundation
        │
        ▼
Processes
        │
        ▼
Threads
        │
        ▼
Memory
        │
        ▼
System Calls
        │
        ▼
Binder IPC
        │
        ▼
System Services
        │
        ▼
Permissions
```

## My recommendation

Rather than jumping directly to **Processes**, I'd like to spend the next few lessons covering the **Android boot process**:

**Boot ROM → Bootloader → Linux Kernel → init → Zygote → System Server → Launcher → Your App**

Understanding this sequence makes everything else—processes, Binder, ART, permissions, and reverse engineering—fit together naturally because you'll know **how the entire operating system comes to life before your APK ever runs**. It's one of the biggest conceptual leaps in understanding Android internals.