(macOS)

---

## Objective

Deploy iOS Simulator

---

Launch:

Xcode

Open Developer Tools

Simulator

---
Choose:

iPhone 15

Latest iOS

---
Verify

Safari

Settings

Camera

Maps

---
Open:

Terminal

List Simulators:

xcrun simctl list devices

---
Boot Simulator:

```bash
xcrun simctl boot <device>
```

---

Collect:

xcrun simctl getenv booted HOME

Observe simulator filesystem location.

---
Deliverables

Simulator screenshot

Device list