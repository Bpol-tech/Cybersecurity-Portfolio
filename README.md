# Cybersecurity & SecOps Portfolio

Welcome to my cybersecurity portfolio! I am a Systems Engineering student and a self-taught information security enthusiast. This repository is dedicated to documenting my hands-on labs, incident analysis, and technical deployments focused on Security Operations (SecOps), active defense, and cloud infrastructure monitoring.

---

## Active Labs & Case Studies
Detailed technical write-ups and architectural breakdowns of the security environments I have deployed and audited:

###  Case 001: Enterprise XDR/SIEM Deployment & Local Endpoint Monitoring (Wazuh)
* **Description:** Hybrid-environment deployment of a Wazuh SIEM/XDR Manager on Ubuntu (WSL2) to ingest, parse, and analyze real-time security telemetries from a Windows 11 host.
* **Skills Applied:** Log analysis, Windows Advanced Audit Policy configuration (`auditpol`), agent identity validation troubleshooting, and forensic triage of host-based anomaly false positives (Rootcheck).
* **Status:**  Completed
* **Documentation:**  [Read the Full Technical Report Here (wazuh-home-soc.md)](wazuh-home-soc.md)

###  Case 002: Cloud-Native Honeypot & Defense in Depth (Microsoft Azure)
* **Description:** Provisioning an exposed Linux VM instance in Azure to capture and profile real-world cyber attacks (isolating a targeted Web3/Crypto botnet), followed by a complete multi-layered security hardening framework.
* **Skills Applied:** Threat Intelligence, SSH infrastructure hardening, Mesh VPN networking (Tailscale), IPS deployment (Fail2ban), and Azure Serial Console out-of-band troubleshooting.
* **Status:**  Completed
* **Documentation:**  [Read the Full Technical Report Here (azure-cloud-honeypot.md)](azure-cloud-honeypot.md)

---

##  Upcoming Projects & Roadmap

###  Phase 3: Detection Engineering & Threat Hunting Lab (Sysmon + MITRE ATT&CK)
* **Description:** Elevating host-based monitoring by deploying Microsoft System Monitor (Sysmon) with an optimized security configuration. The project focuses on simulating real-world adversary techniques using open-source testing frameworks, mapping events to the MITRE ATT&CK matrix, creating custom Wazuh detection rules, and documenting formal SOC Incident Response Playbooks.
* **Core Focus:** - Detection Engineering, Threat Hunting, and Incident Simulation.

###  Phase 4: Network Security Monitoring (NSM) & Home Traffic Analysis
* **Description:** Overcoming the limitations of residential ISP hardware by implementing a centralized network-layer auditing solution using a custom DNS/Sinkhole architecture (Pi-hole) and traffic capture tools. The objective is to analyze real-time outbound connections, map active device telemetries across the home network, identify stealthy beaconing patterns, and enforce network-wide tracking and ad-filtering policies.
* **Core Focus:** - Network Traffic Analysis and Perimeter Hardening.

---

##  Tech Stack & Tools
* **SIEM/XDR:** Wazuh Ecosystem, OpenSearch Dashboard.
* **Networking & IPS:** Tailscale Mesh VPN, Fail2ban, UFW / Netfilter.
* **Operating Systems:** Windows 11, Linux (Ubuntu Subsystem via WSL2 & Native Cloud Images).
* **Cloud & Automation:** Microsoft Azure (Infrastructure Security Core), Bash Scripting, PowerShell Administration.
