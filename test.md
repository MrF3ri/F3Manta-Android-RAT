# F3‑MANTA — Mobile Attack & Network Testing Arena (Android RAT)

<!--
SEO: This README targets searches for: "Android RAT", "Android remote access trojan", "Android RAT sandbox", "mobile post-exploitation lab", "Android malware analysis", "Android pentest lab", "Android RAT demo", "Android WebView RAT".
Suggested GitHub topics/tags (add to repo): android, android-rat, rat, remote-access-trojan, mobile-security, malware-analysis, pentest, offensive-security, red-team, android-webview, sandbox, lab
-->

**Project:** [F3Manta-Android-RAT](https://github.com/MrF3ri/F3Manta-Android-RAT) • **Author:** mr f3ri • **Telegram:** `@sudoferi`

**Short description (for search):**  
F3‑MANTA — an **educational Android RAT sandbox** and **Android post‑exploitation lab** demonstrating Android WebView samples, safe payload concepts, build recipes, and defensive detection/hardening guidance for researchers and instructors.

**Audience:** Students, researchers, instructors, red/blue teams, and conference/lab attendees.  
**Purpose:** Reproduce and explain Android post‑exploitation (Android RAT) behaviors in a **safe, auditable, isolated** environment for **education, research, and defensive** training only.

---

![educational-sandbox](https://img.shields.io/badge/educational--sandbox-blue) ![license-placeholder](https://img.shields.io/badge/license--placeholder-lightgrey)

---

## TL;DR — Android RAT lab, analysis sandbox, and demo-ready artifacts

This repository contains a **benign Android WebView sample**, exact build steps, lab artifacts, and safe demo/playback guidance designed for **Android RAT** research and teaching. Use **only in isolated environments** (VM snapshots, host‑only networks). Obtain **written authorization** prior to testing any systems you do not own.

> Keywords included for discoverability: **Android RAT**, **Android Remote Access Trojan**, **Android malware analysis**, **Android post‑exploitation**, **mobile pentest lab**, **Android WebView RAT**, **red team Android**.

---

## Table of Contents

- [F3‑MANTA — Mobile Attack \& Network Testing Arena (Android RAT)](#f3manta--mobile-attack--network-testing-arena-android-rat)
  - [TL;DR — Android RAT lab, analysis sandbox, and demo-ready artifacts](#tldr--android-rat-lab-analysis-sandbox-and-demo-ready-artifacts)
  - [Table of Contents](#table-of-contents)
  - [About / Searchable summary](#about--searchable-summary)
  - [Why F3‑MANTA (Android RAT sandbox)](#why-f3manta-android-rat-sandbox)
  - [Features (what this Android RAT demo shows)](#features-what-this-android-rat-demo-shows)
  - [Disclaimer \& Ethics (required)](#disclaimer--ethics-required)
  - [Prerequisites (exact commands — unchanged)](#prerequisites-exact-commands--unchanged)

---

## About / Searchable summary

F3‑MANTA is an **educational Android RAT sandbox** and **mobile post‑exploitation lab** that demonstrates core concepts commonly discussed in Android RAT research:

- Android RAT architecture (implant ↔ handler/listener)
- WebView‑based Android samples and safe instrumentation
- APK build/rebuild workflows for analysis and auditing
- Static and dynamic indicators of tampering (smali / manifest changes)
- Lab hygiene and isolation for safe malware analysis

This README intentionally uses common and alternate search terms (Android RAT, Android remote access trojan, mobile RAT, Android malware analysis, Android pentest lab) so researchers looking for Android RAT sandboxes and demos will find F3‑MANTA.

---

## Why F3‑MANTA (Android RAT sandbox)

- Designed specifically for **education and defensive research** into Android RAT techniques and detection.
- Includes **benign demo artifacts** and a clear, auditable build process so instructors can teach Android post‑exploitation concepts without exposing live exploit recipes in the public repo.
- Emphasizes **lab isolation**, reproducible demos, and detection/mitigation guidance for defenders.

---

## Features (what this Android RAT demo shows)

- 🔴 Real time monitoring (demo telemetry)  
- 🌐 Custom WebView sample (benign demo app)  
- 🔔 Notification reader (demo telemetry)  
- 🛰️ Receive device location (for lab demo)  
- ✉️ Read target messages (demo / simulated)  
- ✉️ Send SMS with target device (lab-only)  
- 👤 List and export target contacts (demo)  
- 💻 Enumerate installed apps (analysis artifact)  
- 📷 Capture front & back camera (demonstration, emulator)  
- 🎙 Microphone capture (with duration limits in demo)  
- ✅️ Auto start after device boot (demo behaviour)  
- 🤖 Auto permission handling (demo / simulated flows)  
- 🖥️ Screenshot capture (for analysis playback)  
- 🔐 Injection (conceptual — injection examples are not published here)  
- 🔐 Open phishing pages in a controlled demo environment (simulated)  
- 📒 Gallery puller (pull gallery assets from lab device)  
- 📁 File receive/delete/file manager (lab-only demonstration)  
- 🤖 Claims of "undetectable" are **presented as research claims** — treat these as analysis topics, not recommendations; this repo does **not** provide evasion recipes.  
- And more — focused on teaching defenders how to detect these behaviours.

> NOTE: Feature list mirrors the original repository content; all operational commands remain unchanged below.

---

## Disclaimer & Ethics (required)

> **Important:** This repository is strictly for **educational, research, and defensive** purposes. You must have **explicit written permission** to test or interact with any device, network, or resource you do not own.

Misuse of materials in this repository may be illegal and unethical. If you are unsure whether an action is permitted, **stop** and escalate to your legal/compliance team.

---

## Prerequisites (exact commands — unchanged)

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

