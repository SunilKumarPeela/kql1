# 🛡️ Valdorian Times Cybersecurity Breach: A Real-World SOC Investigation 🧠

🎥 **[Watch Full Investigation Video (kql.mp4)](kql.mp4)**  
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

