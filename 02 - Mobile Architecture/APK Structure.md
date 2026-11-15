# APK Structure

## What is an APK?
An APK (Android Package Kit) is the file format used to distribute and install apps on Android.

---

## Internal Structure

An APK is essentially a ZIP archive containing:

### 1. AndroidManifest.xml
- Declares app permissions
- Defines app components

---

### 2. classes.dex
- Compiled bytecode executed by ART
- Contains app logic

---

### 3. res/ folder
- UI resources
- Images, layouts, strings

---

### 4. assets/
- Raw files bundled with app

---

### 5. lib/
- Native libraries (.so files)

---

### 6. META-INF/
- Signature and integrity files

---

## Security Perspective

APK analysis focuses on:
- Permission abuse
- Hardcoded secrets
- Malicious embedded logic
- Network endpoints

---

## Key Insight

If APK is the “package”, Manifest is the “rulebook”.