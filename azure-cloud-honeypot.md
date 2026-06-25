# Cloud-Native Honeypot Deployment & Defense in Depth (Microsoft Azure)

## 📝 Project Overview
This hands-on lab demonstrates the provisioning of an exposed virtual machine instance within Microsoft Azure, initially configured as a **Honeypot** to capture, parse, and analyze real-world cyber attacks via a centralized **Wazuh SIEM/XDR** manager. After isolating and profiling targeted threat actors, a systematic **Defense in Depth** strategy was engineered to completely remediate vulnerabilities, secure the cloud infrastructure, and enforce automated access control.

---

## 🕵️‍♂️ Phase 1: Incident Analysis & Threat Intelligence

During the initial exposure window, the Wazuh agent recorded aggressive, automated brute-force campaigns targeting the standard SSH port (22). Forensic triage of the raw JSON telemetries allowed the isolation of a persistent threat actor:

### 🌐 Threat Actor Profile
* **Source IP Address:** `2.57.122.238`
* **Geographical Origin:** Timisoara, Romania 🇷🇴
* **Network Provider (ISP):** TECHOFF SRV LIMITED
* **Infrastructure Type:** Data Center / VPS Transit (Privacy Hosting: True)
* **Global Reputation (VirusTotal):** Flagged as **Malicious / Malware / Phishing** by multiple security vendors (Fortinet, BitDefender, SOCRadar).

### 🧠 Táctical Analysis & Modus Operandi
Deep log inspection of the `data.srcuser` field revealed targeted dictionary attacks testing highly specific usernames: 
`solana`, `sol`, `solv`, `ethereum`, `node`, `ubuntu`, `validator`.

* **SecOps Conclusion:** This was not a generic random scanner. The telemetry indicates a specialized **Crypto-Botnet** programmed to compromise Web3/Blockchain validation nodes and infrastructure, searching for default setups or weak credentials on cloud-native servers.
* **Networking Note:** The logs showed that the source port (`srcport`) changed dynamically with every single attempt (e.g., `36574`, `41232`). This represents normal TCP/IP architecture behavior: the attacker targets a static destination port (22), while their OS assigns dynamic **ephemeral outbound ports** to handle each unique concurrent authentication request.

---

## 🚀 Phase 2: Mitigation & Multi-Layered Hardening

To neutralize the active botnet and secure the server, a multi-layered security hardening framework was implemented:

### 🧱 Layer 1: Perimeter Isolation (Tailscale Mesh VPN)
The server was integrated into a private overlay network using **Tailscale**. This reduced the public attack surface to zero, forcing all legitimate management traffic through a secure, encrypted wireguard-based tunnel accessible only by authorized devices.

### 🔒 Layer 2: Static Host Hardening (SSH Daemon Tuning)
The native SSH configuration (`/etc/ssh/sshd_config`) was audited and stripped of insecure defaults to block automated reconnaissance:
1. **Port Obfuscation:** Migrated the listening service from standard port `22` to high port **`2222`**.
2. **Password Deactivation:** Enforced `PasswordAuthentication no`, mitigating all credential-guessing or brute-force threat vectors.
3. **Asymmetric Cryptography:** Enforced `PubkeyAuthentication yes`, binding access exclusively to authorized cryptographic key pairs.

### 👮‍♂️ Layer 3: Dynamic IPS Defense (Fail2ban Deployment)
**Fail2ban** was deployed as an active Intrusion Prevention System (IPS) to patrol `/var/log/auth.log` under a strict jail policy (`sshd.local`):
* **Max Retries (`maxretry`):** 3 authentication failures.
* **Evaluation Window (`findtime`):** 10 minutes.
* **Ban Duration (`bantime`):** Complete network-level isolation via local firewall (`UFW`) for **1 day (24 hours)**.

---

## 🛠️ Engineering Challenges & Troubleshooting

### 🚨 Systemd Service Lifecycle Conflict (Connection Refused Triage)
Following the initial SSH hardening phase, a system reboot resulted in a critical **"Connection Refused"** error, locking out remote access.

* **Root Cause Analysis:** In modern Ubuntu cloud images, Azure manages SSH orchestration via Sockets (`ssh.socket`). When the socket was disabled to force the traditional standalone service path, the configuration lacked the persistence instruction for system startup. Upon a clean boot, the server was running, but the SSH daemon process was completely inactive in RAM.
* **Remediation Action:** The **Azure Serial Console** was utilized as a cloud-native out-of-band management tool to bypass network stacks and interact directly with the Linux kernel. Once logged in, the service was manually restored and set to persist across reboots using systemic commands:
  ```bash
  sudo systemctl start ssh
  sudo systemctl enable ssh
