# Permission Abuse Case Studies

## Case Study 1: Over-Permissioned App

### Scenario
A flashlight app requests:
- Contacts
- SMS
- Location
- Microphone

### Analysis
None of these are required for flashlight functionality.

### Risk
- Data harvesting
- Surveillance behavior
- Hidden tracking

---

## Case Study 2: Social Engineering Prompt Abuse

### Scenario
App repeatedly asks for:
> "Allow location for better experience"

User eventually clicks "Allow"

### Risk
- Continuous location tracking
- Behavioral profiling

---

## Case Study 3: Background Data Access

### Scenario
App granted storage + internet access

### Risk
- Uploading files silently
- Data exfiltration in background

---

## Defensive Takeaway

Always evaluate:
> "Does this permission match the app’s purpose?"