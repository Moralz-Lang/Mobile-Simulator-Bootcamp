# Activities

## What is an Activity?
An Activity represents a single screen in an Android app.

---

## Lifecycle Behavior
- Created when screen opens
- Destroyed or paused when user leaves

---

## Examples
- Login screen
- Dashboard
- Settings page

---

## Security Perspective

Activities can:
- Display sensitive data
- Handle user input
- Trigger authentication flows

---

## Risk Scenarios

- Sensitive data shown without locking
- Session leakage in background state
- Poor state handling

---

## Key Insight

> Activities = User interaction surface