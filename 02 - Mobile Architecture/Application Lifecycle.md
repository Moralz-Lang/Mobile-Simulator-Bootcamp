# Application Lifecycle

## Android Lifecycle

### Key States
- onCreate()
- onStart()
- onResume()
- onPause()
- onStop()
- onDestroy()

---

## Lifecycle Flow

App Launch → Create → Start → Resume → Active Use → Pause → Stop → Destroy

---

## iOS Lifecycle

### Key States
- DidFinishLaunching
- Active
- Inactive
- Background
- Terminated

---

## Security Importance

Lifecycle controls:
- When data is loaded
- When permissions are requested
- When background execution occurs

---

## Attack Surface Insight

Mismanaged lifecycle can lead to:
- Data leakage in background
- Unauthorized persistence
- Session hijacking risks (conceptual)