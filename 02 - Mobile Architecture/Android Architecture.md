# Android Architecture

## Overview
Android is a layered operating system built on top of the Linux kernel. Every application runs inside a controlled environment called a sandbox.

---

## Architecture Layers

### 1. Linux Kernel Layer
- Handles:
  - Memory management
  - Process management
  - Device drivers
  - Security foundation of Android

---

### 2. Hardware Abstraction Layer (HAL)
- Bridges hardware and Android system
- Examples:
  - Camera HAL
  - Audio HAL
  - Bluetooth HAL

---

### 3. Android Runtime (ART)
- Executes app bytecode (.dex files)
- Manages:
  - Garbage collection
  - Runtime execution

---

### 4. Native Libraries
- C/C++ based components
- Examples:
  - SQLite (database)
  - SSL libraries
  - Media frameworks

---

### 5. Application Framework
- APIs used by apps
- Includes:
  - Activity Manager
  - Package Manager
  - Location Manager

---

### 6. Applications Layer
- User-installed apps
- System apps

---

## Security Perspective

- Each app runs in its own UID sandbox
- Apps cannot directly access other app data
- Permissions control access to sensitive APIs

---

## Key Insight

Android security is built on:
- Process isolation
- Permission enforcement
- Kernel-level separation
---
# Definition

Android is a layered operating system built on top of the Linux kernel.

It provides:

- application framework
- runtime
- system services
- hardware abstraction
- security mechanisms

Applications never communicate directly with hardware.

Every request flows through operating system layers.

---
# Why It Exists

Android separates responsibilities.

Instead of applications controlling hardware directly:

Applications request services.

Android manages:

- security

- permissions

- scheduling

- hardware access

- process isolation

This allows thousands of applications to safely coexist.

# ARCHITECTURE

```
flowchart TD

App[Application]

Framework[Application Framework]

Binder[Binder IPC]

Services[System Services]

HAL[Hardware Abstraction Layer]

Kernel[Linux Kernel]

Hardware[Hardware]

App --> Framework

Framework --> Binder

Binder --> Services

Services --> HAL

HAL --> Kernel

Kernel --> Hardware
```
---
# Security Importance

Every mobile attack eventually crosses one or more architecture layers.

Examples:

Application

↓

Binder

↓

System Service

↓

Kernel

↓

Hardware

Understanding these boundaries helps identify:

- privilege boundaries
- trust boundaries
- attack surfaces
---
# Reverse Engineering Perspective

Questions to ask:

Which layer am I looking at?

Is this Java?

Native?

Binder?

Kernel interaction?

Where does execution leave the application?

What Android API is being used?

---
# Blue Team Perspective

Monitor:

- permission requests

- Binder interactions

- exported components

- application lifecycle

- storage access

- network requests
---
# Common Mistakes

❌ Assuming apps access hardware directly

❌ Ignoring Binder

❌ Ignoring Linux process isolation

❌ Treating Android as only Java

❌ Forgetting native code

---

# Real World Examples

Instagram

Camera

↓

CameraManager

↓

Binder

↓

CameraService

↓

Kernel

↓

Camera


Google Maps

GPS

↓

LocationManager

↓

Binder

↓

Location Service

↓

Kernel

↓

GPS Hardware


Banking App

Authentication

↓

TLS

↓

Server

↓

Session Token

↓

Android Keystore

---
# Related Concepts

[[Linux]]

[[Processes]]

[[Binder IPC]]

[[System Services]]

[[Application Lifecycle]]

[[Android Permissions]]

[[Android Storage]]

[[TLS]]

[[JNI]]

[[Android Keystore]]

# Related Labs

[[Lab 1 - Android Emulator]]

[[Lab 3 - Application Permissions]]

[[Lab 4 - Traffic Observation]]

[[Lab 5 - APK Static Analysis]]

---
# Neural Connections

Depends On

[[Linux]]

[[Operating Systems]]

[[Processes]]

---

Explains

[[Binder IPC]]

[[Android Storage]]

[[Application Lifecycle]]

[[Permissions]]

---

Required Before

[[JNI]]

[[TLS]]

[[Cryptography]]

[[Reverse Engineering]]

[[Dynamic Analysis]]

---
# Mental Model

Think of Android like a secure office building.

- Your app is an employee.
- Binder is the receptionist.
- System Services are department managers.
- The Linux Kernel is building security.
- Hardware is the locked equipment room.

Employees never walk into the equipment room directly—they must request access through the proper channels.