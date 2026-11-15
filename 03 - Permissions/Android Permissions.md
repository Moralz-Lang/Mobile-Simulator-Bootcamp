# 📄Android Permissions

## What are Permissions?
Permissions are rules that control what an Android app can access on a device.

They act as a security boundary between:
- App code
- System resources
- User data

---

## Permission Categories

### 1. Normal Permissions
Automatically granted by the system.

Examples:
- INTERNET
- ACCESS_NETWORK_STATE

Impact:
- Low risk
- No user approval needed

---

### 2. Dangerous Permissions (How is this possible from devs ??)
Require explicit user approval.

Examples:
- READ_CONTACTS
- ACCESS_FINE_LOCATION
- READ_SMS
- CAMERA
- MICROPHONE

Impact:
- High risk if misused

---

### 3. Signature Permissions (How can we do so??)
Granted only if:
- App is signed with same certificate as system app

Examples:
- System-level settings access

---

## Security Insight

Permissions are NOT guarantees of safety.

An app with permissions can:
- Collect sensitive data
- Track user behavior
- Exfiltrate information (if malicious)

---

## Key Concept

> Android security = "Trust + Permission Control"

If user grants permission, system assumes intent is valid.