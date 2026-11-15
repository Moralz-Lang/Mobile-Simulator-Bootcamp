# IPA Structure (iOS Apps)

## What is an IPA?
IPA (iOS App Store Package) is the file format used for iOS applications.

---

## Internal Structure

An IPA is a ZIP archive containing:

### 1. Payload/
- Contains the .app directory

---

### 2. Info.plist
- Configuration file
- Defines:
  - App permissions
  - Metadata
  - Bundle ID

---

### 3. App Binary
- Compiled executable code

---

### 4. Frameworks/
- Shared libraries

---

### 5. Resources/
- Images, UI files, assets

---

## Security Perspective

- Code signing is mandatory
- Jailbreaking required for deep inspection
- Strict entitlement system

---

## Key Insight

IPA security relies heavily on:
- Apple signing enforcement
- Sandbox isolation