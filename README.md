# 🛡️ Cybersecurity-Writeups

### SOC • Blue Team • Detection Engineering • DFIR • Network Security

> **A hands-on cybersecurity portfolio documenting labs, investigations, security research, and practical security engineering.**

<p align="center">

[![Cybersecurity](https://img.shields.io/badge/Cybersecurity-Portfolio-111827?style=for-the-badge)](https://github.com/Qusai-Abdullah/Cybersecurity-Writeups)
[![SOC](https://img.shields.io/badge/SOC-Blue%20Team-1d4ed8?style=for-the-badge)](https://github.com/Qusai-Abdullah/Cybersecurity-Writeups)
[![DFIR](https://img.shields.io/badge/DFIR-Forensics-7c3aed?style=for-the-badge)](https://github.com/Qusai-Abdullah/Cybersecurity-Writeups)
[![Detection](https://img.shields.io/badge/Detection-Engineering-b45309?style=for-the-badge)](https://github.com/Qusai-Abdullah/Cybersecurity-Writeups)

</p>

---

## 👋 About

This repository is my **Cybersecurity Portfolio & Technical Knowledge Base**, built around hands-on learning, security labs, investigation, detection engineering, and technical documentation.

My approach:

> **Learn → Build → Investigate → Detect → Document**

The goal is not simply to collect tools, but to understand the **telemetry, evidence, behavior, and detection logic** behind them.

---

# 🚀 Featured Write-ups

### 🧠 Detection Engineering

Practical work covering detection logic, telemetry, threat behavior, and security frameworks.

* 📖 [Detection Engineering](./Detection%20Engineering.md)
* 📖 [MITRE ATT&CK](./MITRE.md)
* 📖 [Sigma](./Sigma.md)
* 📖 [YARA](./YARA.md)
* 📖 [Cyber Kill Chain](./Cyber%20Kill%20Chain.md)
* 📖 [Pyramid of Pain](./Pyramid%20Of%20Pain.md)

---

### 📊 SIEM & Security Monitoring

Working with endpoint and security telemetry for monitoring and investigation.

* 📖 [Splunk](./Splunk.md)
* 📖 [Wazuh](./Wazuh.md)
* 📖 [Sysmon](./Sysmon.md)
* 📖 [Windows Logging for SOC](./Forensics/Windows%20Logging%20for%20SOC.md)
* 📖 [SOAR](./SOAR.md)

---

### 🌐 Network Security

Network monitoring, IDS/IPS, traffic analysis, and security infrastructure.

* 📖 [pfSense](./PFsense.md)
* 📖 [Suricata](./Suricata.md)
* 📖 [Snort](./Snort.md)

---

### 🕵️ Digital Forensics & Incident Response

Practical research covering Windows artifacts, investigations, and incident response.

* 📖 [Introduction to Digital Forensics](./Forensics/Intro%20to%20Digital%20Forensics.md)
* 📖 [Windows Forensics](./Forensics/Windows%20forensics%201.md)
* 📖 [Registry Forensics](./Forensics/Forensics%20%28Senario%29-%20Registry%20Furensics.md)
* 📖 [Identification & Scoping](./Identification%20%26%20Scoping.md)

---

### 🪟 Windows Security & Internals

Understanding Windows from both a security and operating-system perspective.

* 📖 [Windows Fundamentals](./Windows%20Fundamentals%201.md)
* 📖 [Windows Security](./Windows%20security.md)
* 📖 [PowerShell](./PowerShell%20in%20windows.md)
* 📖 [Windows Internals](./Windows%20Internals.md)

---

# 🧰 Security Stack

| Domain                  | Technologies                              |
| ----------------------- | ----------------------------------------- |
| 🛡️ **SOC / SIEM**      | Splunk • Wazuh                            |
| 🪟 **Endpoint**         | Windows • Sysmon                          |
| 🧠 **Detection**        | Sigma • YARA • MITRE ATT&CK               |
| 🌐 **Network Security** | pfSense • Suricata • Snort                |
| 🕵️ **DFIR**            | Windows Forensics • Registry • Event Logs |
| ⚙️ **Automation**       | PowerShell • Security Automation          |

---

# 🔬 Security Lab

The practical environment connects endpoint and network telemetry into security monitoring and investigation workflows.

```text
                    ┌──────────────┐
                    │   Network    │
                    │   Traffic    │
                    └──────┬───────┘
                           │
                  ┌────────┴────────┐
                  │                 │
              Suricata            Zeek
                  │                 │
                  └────────┬────────┘
                           │
                           ▼
                    Security Events
                           │
                           ▼
                    ┌──────────────┐
                    │    SIEM      │
                    │ Splunk/Wazuh │
                    └──────┬───────┘
                           │
                           ▼
                    Investigation
                           │
                           ▼
                     Detection
```

Endpoint telemetry follows a similar workflow:

```text
Windows Endpoint
      │
      ├── Windows Event Logs
      └── Sysmon
             │
             ▼
           Wazuh
             │
             ▼
           Splunk
             │
             ▼
      Hunt / Detection
```

---

# 🎯 Core Skills

* 🔎 Security Monitoring
* 🚨 Alert Triage
* 🧠 Detection Engineering
* 🕵️ Threat Hunting
* 🔬 Digital Forensics
* 🚑 Incident Response
* 🪟 Windows Security
* ⚙️ PowerShell
* 🌐 Network Security
* 📊 SIEM & Log Analysis
* 🧪 Security Labs
* 📚 Technical Documentation

---

# 🗺️ Learning Path

```text
Windows Fundamentals
        ↓
Windows Security
        ↓
PowerShell
        ↓
Windows Internals
        ↓
Networking
        ↓
Network Security
        ↓
SIEM & Log Analysis
        ↓
SOC Operations
        ↓
Detection Engineering
        ↓
DFIR
        ↓
Security Automation
```

---

# 📈 Roadmap

* [x] Cybersecurity Fundamentals
* [x] Windows Security
* [x] PowerShell Fundamentals
* [x] Network Security Foundations
* [x] SIEM & Log Analysis
* [x] Windows Forensics Foundations
* [x] MITRE ATT&CK Foundations
* [x] Detection Engineering Foundations
* [ ] Advanced Threat Hunting
* [ ] Advanced Detection Engineering
* [ ] Advanced DFIR
* [ ] Advanced Windows Internals
* [ ] Security Automation
* [ ] Advanced SIEM Engineering

---

# 📂 Repository

All write-ups are organized around practical cybersecurity domains.

**Start exploring:**

👉 [Detection Engineering](./Detection%20Engineering.md)
👉 [Windows Internals](./Windows%20Internals.md)
👉 [Splunk](./Splunk.md)
👉 [Wazuh](./Wazuh.md)
👉 [Suricata](./Suricata.md)
👉 [Windows Forensics](./Forensics/Windows%20forensics%201.md)
👉 [MITRE ATT&CK](./MITRE.md)

---

# 🤝 Connect

**GitHub:** [Qusai-Abdullah](https://github.com/Qusai-Abdullah)

**Portfolio:** [Cybersecurity-Writeups](https://github.com/Qusai-Abdullah/Cybersecurity-Writeups)

---

<div align="center">

### 🛡️ Learn. Build. Detect. Investigate. Document.

**Understanding the evidence behind the attack.**

</div>
