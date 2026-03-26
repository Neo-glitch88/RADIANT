# 🔴 Project RADIANT-AI

### AI-Enhanced Open-Source SOC Platform | Threat Intelligence + Detection + Automated Response

![Status](https://img.shields.io/badge/Status-In%20Development-yellow)
![Platform](https://img.shields.io/badge/Platform-vSphere%20%2F%20Docker-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---------

#Overview

Project RADIANT-AI is a full-stack, 
open-source Security Operations Center (SOC) 
platform built on a vSphere lab environment. 
It integrates threat intelligence ingestion, 
network intrusion detection, AI-powered alert 
triage, and automated incident response into 
a single end-to-end pipeline — demonstrating 
how modern SOC operations can be enhanced 
with open-source tooling and AI/ML.

Built as both a class Proof of Concept (PoC) 
and a personal portfolio project, RADIANT-AI 
covers the full analyst workflow from 
detection to containment to recovery.

----

## Architecture
```
Threat Feeds (Abuse.ch / CIRCL / OTX)
         ↓
     MISP (ATI)          ← threat intelligence platform
         ↓ IOC sync
   Suricata (ADI)        ← network intrusion detection
         ↓ eve.json alerts
   LangChain AI Agent    ← alert triage + enrichment
    ↙           ↘
VirusTotal    ChromaDB   ← threat intel + memory
AbuseIPDB     VectorDB
         ↓
   SOAR Response Layer
    ├── ServiceNow ticket
    ├── Block IP (pfSense)
    └── Slack notification
         ↓
   Grafana / Streamlit   ← SOC analyst dashboard
```

## Tech Stack

### Phase 1 — Core Detection (Project RADIANT)
| Component | Tool | Role |

| Firewall / Gateway | pfSense | Network segmentation |
| Threat Intelligence | MISP | IOC ingestion + feed management |
| Network IDS | Suricata | Traffic inspection + alerting |
| Deployment | Docker + vSphere | Lab infrastructure |
| Attack Simulation | PCAP replay / tcpreplay | Realistic traffic datasets |

### Phase 2 — AI + SOAR Layer (RADIANT-AI)
| Component | Tool | Role |
|---|---|---|
| AI Agent | LangChain + Claude | Alert triage + reasoning |
| Threat Enrichment | VirusTotal + AbuseIPDB | IOC reputation lookup |
| Incident Memory | ChromaDB | Vector similarity search |
| Ticketing | ServiceNow | Auto-incident creation |
| SIEM | Microsoft Sentinel | Log aggregation + KQL |
| Dashboard | Streamlit + Grafana | SOC analyst interface |
| CI/CD | GitHub Actions | Automated deployments |

---

## Detection Scenarios

Five real-world attack scenarios demonstrated 
using live PCAP datasets from 
malware-traffic-analysis.net:

| Scenario | Detection Method | AI Action |
|---|---|---|
| SSH Brute Force | Suricata rule | Auto-ticket + block IP |
| Port Scan | Suricata threshold | Flag for review |
| Lateral Movement | Suricata + Wazuh | Escalate + isolate |
| Data Exfiltration | DNS anomaly rule | Block + notify |
| Malware Hash Match | MISP IOC sync | Sandbox via Hatching Triage |

---

## AI Add-ons

- **Hatching Triage** — automated malware 
  sandbox analysis via API
- **StamusML** — ML anomaly scoring on 
  Suricata events, false positive reduction
- **LangChain Agent** — reads alert → queries 
  threat intel → reasons severity → triggers 
  automated response

---

---

## Incident Response Workflow

1. DETECTION   → Suricata fires alert from PCAP
2. ENRICHMENT  → AI agent queries VirusTotal + MISP
3. TRIAGE      → LangChain scores severity + category
4. CONTAINMENT → pfSense blocks src IP automatically
5. TICKETING   → ServiceNow incident auto-created
6. ERADICATION → Rules updated with new IOCs from MISP
7. RECOVERY    → VM snapshot restore + documentation

---

## Project Structure
```
radiant-ai/
├── infrastructure/        # vSphere + Docker configs
├── threat-intel/          # MISP setup + feed sync
├── detection/             # Suricata rules + config
│   └── sigma_rules/       # Custom detection rules
├── ai-agent/              # LangChain triage engine
│   ├── agent.py
│   ├── prompts.py
│   └── tools/
├── automation/            # SOAR response actions
│   ├── servicenow.py
│   └── block_ip.py
├── dashboard/             # Streamlit SOC UI
├── pcap-datasets/         # Sample traffic files
├── docs/
│   ├── architecture.md
│   ├── runbook.md
│   └── incident-workflow.md
└── .github/workflows/     # CI/CD pipelines
```

---

## Roadmap

- [x] Lab network design + pfSense config
- [x] MISP deployment + threat feed integration
- [x] Suricata deployment + rule sync
- [ ] PCAP replay + alert validation
- [ ] LangChain AI triage engine
- [ ] ServiceNow SOAR integration
- [ ] Streamlit dashboard
- [ ] Azure Sentinel integration
- [ ] CI/CD pipeline
- [ ] AI add-ons (Hatching Triage + StamusML)

---

## References

- MISP Project — misp-project.org
- Suricata — suricata.io
- Hatching Triage — tria.ge
- StamusML — stamus-networks.com
- malware-traffic-analysis.net
- LangChain — langchain.com
