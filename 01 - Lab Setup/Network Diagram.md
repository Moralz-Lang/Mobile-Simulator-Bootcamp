# Mobile Security Lab Network Diagram

## Architecture

[ Kali Linux ]  ← security testing environment
       |
       |
[ Local Network / Virtual Switch ]
       |
       |
[ Android Emulator ] -----> [ Apache Web Server ]
       |
       |
[ iOS Simulator ]

---

## Flow Description
- Apps request data from server
- Emulator simulates user behavior
- Kali observes traffic (lab-only)

---

## Key Learning Point
Understanding data flow is essential for both attackers and defenders.
But here we focus on defense and analysis.