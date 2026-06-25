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
* **Phase 3:** SOC Incident Response Audits (LetsDefend / Blue Team Labs) -> Documenting systematic remediation of real-world malware execution, phishing campaigns, and privilege escalation vectors.

---

##  Tech Stack & Tools
* **SIEM/XDR:** Wazuh Ecosystem, OpenSearch Dashboard.
* **Networking & IPS:** Tailscale Mesh VPN, Fail2ban, UFW / Netfilter.
* **Operating Systems:** Windows 11, Linux (Ubuntu Subsystem via WSL2 & Native Cloud Images).
* **Cloud & Automation:** Microsoft Azure (Infrastructure Security Core), Bash Scripting, PowerShell Administration.
