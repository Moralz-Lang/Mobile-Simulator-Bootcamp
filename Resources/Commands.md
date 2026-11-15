[DROZER]
**Basic Cheatsheet of Drozer**

Exploiting Content Provider
```bash
`run app.provider.info -a package_name`

`run scanner.provider.finduris -a package_name`

`run app.provider.query uri`

`run app.provider.update uri --selection conditions selection_arg column data`

`run scanner.provider.sqltables -a package_name`

`run scanner.provider.injection -a package_name`

`run scanner.provider.traversal -a package_name`

Exploiting Service

`run app.service.info -a package_name`

`run app.service.start --action action --component package_name component_name`

`run app.service.send package_name component_name --msg what arg1 arg2 --extra type key value --bundle-as-obj`
```


---
# Mobile Security Commands Reference

> A quick-reference guide for common commands used throughout the Mobile Security Bootcamp. These commands are intended for authorized lab environments and defensive security work.

---

# Android Debug Bridge (ADB)

## Verify Device Connection

```
adb devices
```

Lists connected Android devices and emulators.

---

## Start ADB Server

```
adb start-server
```

---

## Stop ADB Server

```
adb kill-server
```

---

## Open Interactive Shell

```
adb shell
```

Provides shell access to the Android device.

---

## Install APK

```
adb install app.apk
```

---

## Reinstall APK

```
adb install -r app.apk
```

---

## Remove Application

```
adb uninstall package.name
```

---

## List Installed Packages

```
adb shell pm list packages
```

---

## Find Package Location

```
adb shell pm path package.name
```

---

## Dump Package Information

```
adb shell dumpsys package package.name
```

Useful for:

- permissions
- receivers
- activities
- services
- install information

---

## List Running Processes

```
adb shell ps -A
```

---

## Running Services

```
adb shell dumpsys activity services
```

---

## Running Activities

```
adb shell dumpsys activity
```

---

## Memory Usage

```
adb shell dumpsys meminfo
```

---

## Battery Status

```
adb shell dumpsys battery
```

---

## Battery Statistics

```
adb shell dumpsys batterystats
```

---

## Network Statistics

```
adb shell dumpsys netstats
```

---

## View System Properties

```
adb shell getprop
```

---

## Capture Logs

```
adb logcat
```

---

## Clear Logs

```
adb logcat -c
```

---

## Screen Capture

```
adb shell screencap /sdcard/screen.png
adb pull /sdcard/screen.png
```

---

## Device Storage

```
adb shell df -h
```

---

## File Transfer

Push file:

```
adb push file.txt /sdcard/
```

Pull file:

```
adb pull /sdcard/file.txt
```

---

# APK Analysis

## APK Information

```
aapt dump badging app.apk
```

---

## Decode APK

```
apktool d app.apk
```

---

## Build APK

```
apktool b folder
```

---

## APK Signing Information

```
apksigner verify app.apk
```

---

## SHA256 Hash

Linux

```
sha256sum app.apk
```

Windows PowerShell

```
Get-FileHash app.apk -Algorithm SHA256
```

---

# Network Analysis

## Active Connections

```
adb shell netstat
```

or

```
adb shell ss
```

---

## Capture Traffic (host)

```
tcpdump
```

---

## Wireshark

Capture Android emulator traffic using the emulator network adapter.

---

# Android Emulator

Launch emulator

```
emulator -avd Pixel_API_34
```

---

List available AVDs

```
emulator -list-avds
```

---

# Apache

Start

```
sudo systemctl start apache2
```

---

Stop

```
sudo systemctl stop apache2
```

---

Restart

```
sudo systemctl restart apache2
```

---

Status

```
systemctl status apache2
```

---

Web Root

```
/var/www/html/
```

---

# Linux

Current directory

```
pwd
```

---

List files

```
ls -lah
```

---

Copy

```
cp
```

---

Move

```
mv
```

---

Remove

```
rm
```

---

Search

```
find
```

---

Process List

```
ps aux
```

---

Open Ports

```
ss -tuln
```

---

IP Address

```
ip addr
```

---

Disk Usage

```
df -h
```

---

# VirtualBox

List VMs

```
VBoxManage list vms
```

---

Start VM

```
VBoxManage startvm VMNAME
```

---

Snapshots

```
VBoxManage snapshot VMNAME list
```
---
# Evidence Collection

Always document:

- Device model
- Android version
- Build number
- Installed packages
- Running processes
- Running services
- Battery statistics
- Network activity
- Screenshots
- Logcat output
- APK hashes
- Investigation notes

---

# Mobile Investigation Workflow

```
Receive Alert
      │
      ▼
Preserve Device
      │
      ▼
Collect Evidence
      │
      ▼
Review Installed Apps
      │
      ▼
Analyze Permissions
      │
      ▼
Review Services
      │
      ▼
Review Processes
      │
      ▼
Review Network Activity
      │
      ▼
Review Logs
      │
      ▼
Correlate IoCs
      │
      ▼
MITRE ATT&CK Mapping
      │
      ▼
Risk Assessment
      │
      ▼
Containment
      │
      ▼
Recovery
      │
      ▼
Lessons Learned
```

---

# Best Practices

- Work on a copy of evidence whenever possible.
- Record hashes before analysis.
- Correlate multiple data sources instead of relying on a single indicator.
- Preserve timestamps and maintain chain of custody.
- Document every command you execute during an investigation.
- Compare findings against a known-good baseline to reduce false positives.