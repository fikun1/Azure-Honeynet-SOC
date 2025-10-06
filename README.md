# 🕵️‍♂️ Azure Cloud Honeynet (SOC Homelab)
**Simulating Real-World Cyber Attacks and Hardening a Cloud Environment**

---
![Azure Honeynet Architecture](./images/architecture/Azure-Cloud-honeynet.png)
![Windows VM Attack Map](./images/attacks/Attack%20Map.png)
### 📘 Overview
This project demonstrates how I built a **honeynet in Microsoft Azure** to simulate real-world cyberattacks, monitor malicious activity, and then apply **incident response and security hardening** measures.  
The goal was to observe how attackers operate in a vulnerable environment and to measure the security improvements after applying Azure and NIST-aligned best practices.

---

### 🎯 Objectives
- Deploy intentionally vulnerable VMs within an Azure Virtual Network.  
- Collect and analyze telemetry using **Microsoft Sentinel** and **Log Analytics (KQL)**.  
- Simulate and respond to cyberattacks in a live environment.  
- Apply **NIST SP 800-53** and **NIST SP 800-61** guidelines to harden the system.  
- Measure the impact of hardening using pre- and post-implementation metrics.

---

### 🧰 Technologies & Azure Components
| Category | Tools & Services |
|-----------|------------------|
| **Cloud Infrastructure** | Azure Virtual Machines, Virtual Network (VNet), Network Security Groups (NSG) |
| **Security & Monitoring** | Microsoft Sentinel (SIEM), Defender for Cloud, Log Analytics Workspace (KQL) |
| **Access & Secrets Management** | Azure Key Vault, Private Endpoints |
| **Automation & Management** | Azure CLI, PowerShell |
| **Frameworks & Compliance** | NIST SP 800-53 (Security Controls), NIST SP 800-61 (Incident Response) |

---

### ⚙️ Methodology

#### 1. Environment Setup
- Deployed **2 Windows** and **1 Linux** virtual machines in a public VNet.  
- Configured NSGs to allow **all inbound traffic**, simulating a vulnerable system.  
- Disabled firewalls to attract malicious traffic and generate telemetry.

#### 2. Log Collection & SIEM Configuration
- Deployed a **Log Analytics Workspace (LAW)** and connected all VMs.  
- Integrated **Microsoft Sentinel** with LAW for correlation and visualization.  
- Imported a **GeoIP watchlist** to enrich attack logs with country and ASN data.

#### 3. Attack Observation
- Left the environment exposed for 24 hours.  
- Captured thousands of failed **RDP**, **SMB**, and **SSH** attempts.  
- Visualized results through Sentinel **Attack Maps** and **KQL queries**.

#### 4. Hardening & Response
- Restricted NSGs to allow access **only from my IP**.  
- Re-enabled and tuned built-in VM firewalls.  
- Migrated resources to **Private Endpoints** to remove public exposure.  
- Validated all changes through Sentinel’s live data stream.

#### 5. Post-Hardening Analysis
- Re-monitored for another 24 hours to compare telemetry results.  
- Verified reduction in attack volume and incidents.

---

### 🌍 Attack Visualizations

#### Attack Map — Before Hardening
![Attack Map Before](./images/attacks/attack-map-before.png)
*Figure 1: Global attack map showing malicious RDP/SSH attempts from multiple countries (data enriched via GeoIP watchlist).*

| Country | Attempts (24h) |
|----------|----------------|
| Russia 🇷🇺 | 4,321 |
| China 🇨🇳 | 1,876 |
| Brazil 🇧🇷 | 412 |
| United States 🇺🇸 | 265 |
| India 🇮🇳 | 201 |

> **Note:** Country attribution is based on GeoIP lookups and represents approximate network-level origins, not individuals.

#### Attack Map — After Hardening
![Attack Map After](./images/attacks/attack-map-after.png)
*Figure 2: No malicious activity detected within 24 hours post-hardening.*

---

### 📊 Security Metrics

| Metric | Before Hardening | After Hardening | Improvement |
|---------|------------------|-----------------|-------------|
| Security Events (Windows VM) | 21,182 | 783 | 🔻 96% |
| Syslog Events (Linux VM) | 4,877 | 23 | 🔻 99% |
| Sentinel Incidents | 343 | 0 | ✅ Eliminated |
| NSG Inbound Malicious Flows | 969 | 0 | ✅ Blocked |

---

### 🧩 Architecture Overview

#### Before Hardening
- All resources publicly accessible (0.0.0.0/0).  
- NSGs and VM firewalls wide open.  
- Storage and database endpoints publicly exposed.

#### After Hardening
- NSGs restricted to trusted IPs only.  
- Private Endpoints implemented for sensitive resources.  
- Built-in VM firewalls configured for least-privilege access.  

*(Add your “Before” and “After” architecture diagrams here once uploaded.)*

---

### 🧠 Key Learnings
- Practical understanding of **cloud attack surfaces** and how they’re exploited.  
- Hands-on experience with **Microsoft Sentinel** and **KQL** query development.  
- Reinforced **incident response lifecycle** — *Detect → Analyze → Remediate → Harden → Validate*.  
- Quantified security posture improvement using measurable metrics.

---

### 🧾 Resume Summary Example
> **Azure Cloud Honeynet (SOC Homelab)** — Deployed vulnerable VMs in Azure to attract and analyze real cyberattacks. Used Microsoft Sentinel for SIEM, built KQL attack maps, and implemented NIST-aligned security controls. Reduced malicious flows and incidents by 100% post-hardening.

---

### 🧱 Future Improvements
- Integrate **Defender for Identity** and **Logic App Playbooks** for automated incident response.  
- Forward logs to **Splunk** for cross-platform SIEM correlation.  
- Extend honeynet to hybrid infrastructure (Azure + on-prem lab).

---

### 🛡️ Cybersecurity & Blue Team Tools

**🔍 Security Monitoring & SIEM**
- Microsoft Sentinel, Log Analytics (KQL), Splunk (SPL Queries)

**💻 System & Endpoint Monitoring**
- Linux (`syslog`, `auditd`) and Windows Event Logs (4624/4625 Analysis)

**🌐 Network Analysis**
- Wireshark, Nmap, Snort (IDS), Packet Tracing & Flow Analysis

**🧪 Continuous Learning**
- TryHackMe (SOC Level 1 Labs)  
- HackTheBox (Blue/Red Team Exercises)

---

### 📎 References
- [Microsoft Azure Portal](https://portal.azure.com)  
- [Kusto Query Language Documentation](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)  
- [NIST SP 800-53 Rev.5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)  
- [NIST SP 800-61 Rev.2](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final)

---

*© 2025 — Project by [Your Name]. This homelab is for educational and research purposes only.*
