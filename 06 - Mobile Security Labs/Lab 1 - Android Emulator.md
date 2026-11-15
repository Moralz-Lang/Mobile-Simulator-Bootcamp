# Objective

Deploy a reproducible Android testing environment.

## Step 1

Launch Android Studio:

Device Manager

Create:

Pixel 7

Android 14


---
## Step 2

Verify boot:

adb devices

Expected:

emulator-5554 device

---

## Step 3

Collect device information:


adb shell getprop

Record

- Android Version
- SDK
- ABI
- Build Fingerprint

---
## Step 4

Verify networking:

adb shell ip addr

Observe:

wlan0

IP address

---
## Step 5

Open:

Chrome

Settings

Contacts

Camera

Verify:

- UI responsiveness
- Networking
- Storage
---
## Deliverables

Screenshot:

adb devices

Screenshot:

Android home screen

---

# Lab Notes

Document

Device

Android Version

SDK

ABI

Networking

Observations
