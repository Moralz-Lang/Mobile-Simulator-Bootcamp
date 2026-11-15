# iOS Architecture

## Overview
iOS is a closed ecosystem designed with strong sandboxing and strict application control.

---

## Architecture Layers

### 1. Core OS (Kernel Layer)
- Based on XNU kernel
- Handles:
  - Memory management
  - File system
  - Security enforcement

---

### 2. Core Services Layer
- System services like:
  - Networking
  - Database handling
  - Location services

---

### 3. Media Layer
- Graphics and audio processing
- Frameworks:
  - Metal
  - AVFoundation

---

### 4. Cocoa Touch Layer
- Application interface layer
- Handles:
  - Touch events
  - UI rendering
  - App lifecycle

---

## Security Model

- Strong sandbox per application
- Code signing required for apps
- Strict App Store validation
- Limited system-level access

---

## Key Insight

iOS security is based on:
- Code signing enforcement
- App sandboxing
- Controlled API access