# 📄Runtime Permissions

## What Are They?
Runtime permissions are requested while the app is running, not during installation.

---

## Flow

1. App requests feature
2. System prompts user
3. User grants or denies
4. App adapts behavior

---

## Example Flow

- App opens camera
- Prompt appears:
  "Allow camera access?"
- User selects:
  - Allow
  - Deny
  - Ask again later

---

## Security Implications

Attackers (or malicious apps) may:
- Request permissions repeatedly
- Use social engineering prompts
- Disable functionality if denied

---

## Defensive Insight

Users often click:
> "Allow" without understanding impact

This is one of the biggest real-world security weaknesses.