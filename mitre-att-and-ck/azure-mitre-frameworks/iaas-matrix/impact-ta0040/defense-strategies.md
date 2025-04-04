# Defense Strategies

## **Defensive Strategies Against Impact in Azure Environments**

Impact is the loudest part of the attack chain — attackers delete, encrypt, crash, hijack, or expose resources to cause real damage.\
Defending against Impact in Azure focuses on access control, resilience, monitoring, and automated recovery.

***

### ❌ Account Access Removal (T1531)

| Defensive Action                                                               | Why It Matters                    |
| ------------------------------------------------------------------------------ | --------------------------------- |
| 🔒 Apply Privileged Identity Management (PIM) to all privileged Azure AD roles | No standing admin access          |
| 🚫 Use Conditional Access to require MFA for privileged accounts               | Prevent easy privilege abuse      |
| 📜 Monitor Azure AD audit logs for sudden user or role deletions               | Detect lockout attempts instantly |
| 🛡️ Enable Azure AD Access Reviews to detect unused/rogue accounts             | Continuous permission hygiene     |

✅ **Effect**: Attackers can't remove critical accounts without immediate detection.

***

### 💥 Data Destruction → Lifecycle-Triggered Deletion (T1485.001)

| Defensive Action                                                     | Why It Matters                                  |
| -------------------------------------------------------------------- | ----------------------------------------------- |
| 🔒 Restrict who can modify Azure Storage lifecycle policies          | Only storage admins allowed                     |
| 🚫 Protect storage accounts with Azure Resource Locks (CanNotDelete) | Prevent accidental/malicious deletion           |
| 📜 Monitor policy changes via Azure Activity Logs                    | Alert on new deletion policies or modifications |
| 🛡️ Enable Storage Account Soft Delete and Versioning                | Recover from unintended deletions easily        |

✅ **Effect**: Data can't be silently deleted or aged out.

***

### 🔒 Data Encrypted for Impact (T1486)

| Defensive Action                                                         | Why It Matters                                 |
| ------------------------------------------------------------------------ | ---------------------------------------------- |
| 🔒 Control Key Vault access tightly using RBAC and access policies       | Only key custodians can rotate keys            |
| 🚫 Enable Key Vault Soft Delete and Purge Protection                     | Protect keys from rogue rotations/deletion     |
| 📜 Monitor key rotations and key usage patterns (Defender for Key Vault) | Detect unauthorized key changes                |
| 🛡️ Use Customer-Managed Keys (CMK) with controlled lifecycle management | Maintain ownership of critical encryption keys |

✅ **Effect**: Data encryption can't be weaponized by attackers.

***

### 🎨 External Defacement (T1491.001)

| Defensive Action                                                                  | Why It Matters                                              |
| --------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| 🔒 Use Azure Front Door with WAF and origin restrictions                          | Shield public-facing apps                                   |
| 🚫 Apply strict RBAC to App Service deployments (Deployment Contributor only)     | Limit who can push code/content                             |
| 📜 Enable deployment logging and monitor changes to web apps and storage websites | Catch defacement uploads fast                               |
| 🛡️ Use Azure Defender for App Services                                           | Detect web shell uploads and anomalous deployment behaviors |

✅ **Effect**: Public defacement becomes harder and faster to catch.

***

### 🛑 Endpoint Denial of Service (Service Exhaustion Flood, Application Exhaustion Flood, Application/System Exploitation)

| Defensive Action                                                               | Why It Matters                                   |
| ------------------------------------------------------------------------------ | ------------------------------------------------ |
| 🔒 Use Azure DDoS Protection Standard for all public IPs                       | Auto-mitigate large-scale DoS attacks            |
| 🚫 Deploy Azure Application Gateway or Front Door with WAF rules               | Block malformed/malicious traffic early          |
| 📜 Monitor app and service health using Azure Monitor and Application Insights | Early detection of stress/failure patterns       |
| 🛡️ Enable auto-scaling on App Services, Functions, and Kubernetes workloads   | Absorb legitimate surges, resist small-scale DoS |

✅ **Effect**: Minimize downtime and absorb attacks gracefully.

***

### 🔄 Inhibit System Recovery (T1490)

| Defensive Action                                                                                      | Why It Matters                       |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------ |
| 🔒 Protect Azure Recovery Vaults and backups with RBAC and Resource Locks                             | Prevent deletion of backups          |
| 🚫 Enable Soft Delete for Recovery Services Vaults and Key Vaults                                     | Allow easy recovery even if deleted  |
| 📜 Monitor backup job failures and Vault changes (Azure Monitor, Defender for Cloud)                  | Alert on suspicious backup tampering |
| 🛡️ Regularly test backup restores as part of BCDR (Business Continuity and Disaster Recovery) drills | Confirm recovery readiness           |

✅ **Effect**: Attackers can’t destroy recovery mechanisms without being caught.

***

### 🌐 Network Denial of Service (Direct Network Flood, Reflection Amplification)

| Defensive Action                                                                 | Why It Matters                         |
| -------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Enable Azure DDoS Protection Standard on all critical public-facing resources | Block floods automatically             |
| 🚫 Harden DNS and NTP services, disable reflection vectors                       | Prevent being used as a DDoS amplifier |
| 📜 Monitor traffic spikes and public IP access patterns                          | Detect DDoS precursors                 |
| 🛡️ Rate limit public APIs and expose only necessary services publicly           | Shrink attack surface                  |

✅ **Effect**: Network resources stay resilient against DDoS attempts.

***

### 🖥️ Resource Hijacking (Compute Hijacking, Bandwidth Hijacking)

| Defensive Action                                                            | Why It Matters                                    |
| --------------------------------------------------------------------------- | ------------------------------------------------- |
| 🔒 Apply strict quotas on VM, AKS, ACI resource creation                    | Limit attacker's ability to spin up crypto miners |
| 🚫 Monitor resource utilization anomalies (e.g., sudden CPU/network spikes) | Detect crypto-mining or proxy abuse early         |
| 📜 Enable Defender for Containers, VMs, and App Services                    | Auto-detect resource hijacking behaviors          |
| 🛡️ Regularly audit subscription spend patterns for spikes                  | Financial impact of hijacking caught early        |

✅ **Effect**: Hijacked resources are caught fast, preventing silent abuse.

***

## 📊 **Defensive Coverage Table (Impact in Azure)**

| Attack Vector                          | Defensive Strategy                                                |
| -------------------------------------- | ----------------------------------------------------------------- |
| Account Access Removal                 | PIM, CA enforcement, audit deletions                              |
| Lifecycle-Triggered Deletion           | Storage locks, soft delete, audit policy changes                  |
| Data Encrypted for Impact              | Key Vault RBAC, Soft Delete, key rotation monitoring              |
| External Defacement                    | WAF protection, strict deployment RBAC, Defender for App Services |
| Endpoint DoS (Service/App/System)      | DDoS Protection, Front Door WAF, app health monitoring            |
| Inhibit System Recovery                | Recovery Vault locks, backup monitoring, restore testing          |
| Network DoS (Direct/Reflection)        | DDoS Protection, hardened DNS/NTP, rate limiting                  |
| Resource Hijacking (Compute/Bandwidth) | Quotas, Defender monitoring, spend analysis                       |

***

## 🎯 Final Summary

Defending against Impact in Azure focuses on:

* **Protecting identity, storage, and recovery layers**
* **Monitoring and controlling encryption key usage**
* **Resiliently absorbing DoS attempts**
* **Catching resource hijacking through usage anomalies and spend monitoring**
