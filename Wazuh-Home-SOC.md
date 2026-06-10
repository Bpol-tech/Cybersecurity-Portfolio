# Enterprise XDR/SIEM Deployment & Local Endpoint Telemetry Monitoring

##  Project Overview
This hands-on lab demonstrates the deployment, configuration, and auditing of an enterprise-grade XDR/SIEM solution (**Wazuh**) within a hybrid local architecture. The environment features a centralized Wazuh Manager running on an Ubuntu Linux instance via **WSL2**, actively monitoring a **Windows 11 host** endpoint in real-time. 

The core objective of this deployment is to establish centralized log ingestion, map endpoint behaviors, and gain experience in analyzing security telemetries and investigating false positives.

---

##  Architecture & Component Breakdown
* **SIEM/XDR Server:** Wazuh Manager & Dashboard v4.10 deployed on Ubuntu (WSL2 Environment).
* **Monitored Endpoint:** Windows 11 Host running the lightweight, persistent Wazuh Agent service.
* **Network Ingestion:** Local network routing streaming security telemetry via secure ports `1514` (Log shipping) and `1515` (Agent registration).

---

##  Implementation & Engineering Challenges

### 1. Endpoint Agent Registration Triage
During the initial deployment phase, the Windows agent failed to check-in due to validation errors at the manager level:
`ERROR: Invalid agent name: Pol (from manager)`
`ERROR: Unable to add agent (from manager)`

* **Root Cause Analysis:** The automated bootstrap script extracted a generic, non-compliant host string from the system, which violated the manager's strict endpoint identity schema.
* **Remediation Action:** The local configuration file (`ossec.conf`) on the Windows host was manually audited via an elevated administrative context. The agent identity was hardcoded to a standardized corporate naming convention (`Win11-HomeSOC`), forcing a successful key exchange and securing an `Active` status on the monitoring dashboard.

### 2. Windows Event Channel Ingestion Tuning
Initial testing showed that local Windows events weren't triggering alerts on the dashboard despite active connectivity.
* **Remediation Action:** Enforced systemic logging policies via PowerShell (Admin) to explicitly audit authentication anomalies across the OS subsystem:
```powershell
auditpol /set /category:"Inicio/Cierre de sesión" /success:enable /failure:enable
