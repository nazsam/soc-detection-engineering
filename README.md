<div align="center">

# 🎯 SOC Detection Engineering

**Production-style detections (Microsoft Sentinel KQL + Splunk SPL) mapped to MITRE ATT&CK, plus incident-response playbooks — from 15+ years running 24/7 Security Operations Centers.**

![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-Mapped-C00?style=for-the-badge)
![Microsoft Sentinel](https://img.shields.io/badge/Microsoft_Sentinel-KQL-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Splunk](https://img.shields.io/badge/Splunk-SPL-000000?style=for-the-badge&logo=splunk&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

</div>

---

## 📖 Overview

Detections are only useful if they're **high-fidelity, mapped, and paired with a response.** This
repo is a working detection library: each rule states the threat, the ATT&CK technique it covers,
the query (Sentinel KQL or Splunk SPL), tuning guidance to cut false positives, and the response
playbook to run when it fires.

## 🗺️ Detection Coverage (MITRE ATT&CK)

| # | Detection | Tactic | Technique | Platform |
|---|-----------|--------|-----------|----------|
| 1 | [Password spray → success](detections/sentinel/brute-force-then-success.yaml) | Credential Access | T1110.003 | Sentinel |
| 2 | [Impossible travel sign-in](detections/sentinel/impossible-travel.yaml) | Initial Access | T1078 | Sentinel |
| 3 | [Illicit OAuth consent grant](detections/sentinel/illicit-oauth-consent.yaml) | Persistence | T1528 | Sentinel |
| 4 | [Defender/AV tampering](detections/sentinel/defender-tampering.yaml) | Defense Evasion | T1562.001 | Sentinel |
| 5 | [Brute force (Windows)](detections/splunk/windows-brute-force.spl) | Credential Access | T1110 | Splunk |
| 6 | [Mass file download / exfil](detections/splunk/mass-download-exfil.spl) | Exfiltration | T1567 | Splunk |

## 📓 Incident Response Playbooks

- 🎣 **[Phishing / BEC](playbooks/phishing-response.md)**
- 🔑 **[Compromised account](playbooks/compromised-account.md)**
- 🔒 **[Ransomware](playbooks/ransomware-response.md)**

Each follows **Prepare → Detect → Analyze → Contain → Eradicate → Recover → Lessons Learned**
(NIST SP 800-61 aligned).

## 🧱 Detection format

Every Sentinel rule uses a consistent YAML schema (id, name, severity, ATT&CK tactics/techniques,
query, entity mappings, tuning notes) — see **[docs/DETECTION-FORMAT.md](docs/DETECTION-FORMAT.md)**.
This makes rules reviewable in PRs and portable into Sentinel via API/Bicep.

## 🎚️ Engineering principles
- **Fidelity over volume.** A noisy rule that gets muted protects nothing. Tune to signal.
- **Every alert has an owner and a playbook.** Detection without response is theatre.
- **Map to ATT&CK.** Coverage gaps should be visible, not discovered during an incident.
- **Test detections.** Validate with atomic tests / purple-team before trusting them.

## 📚 Contents
```
soc-detection-engineering/
├── detections/
│   ├── sentinel/*.yaml     # KQL analytic rules
│   └── splunk/*.spl        # SPL searches
├── playbooks/*.md          # NIST 800-61 IR playbooks
├── docs/DETECTION-FORMAT.md
└── README.md · LICENSE · CONTRIBUTING.md
```

## 🤝 Contributing & License
See **[CONTRIBUTING.md](CONTRIBUTING.md)**. Licensed **[MIT](LICENSE)** © 2026 devsecforge (S. Naz).

> ⚠️ Detections are examples to adapt to your data sources and baseline. Test in a dev workspace and
> tune thresholds before production.
