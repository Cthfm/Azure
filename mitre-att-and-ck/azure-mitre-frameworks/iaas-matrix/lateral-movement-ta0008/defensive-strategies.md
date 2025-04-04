# Defensive Strategies

## **Defensive Strategies Against Lateral Movement in Azure Environments**

Defending against lateral movement in Azure is about **shrinking attack surfaces**, **monitoring authentication artifacts** (tokens, cookies), and **blocking uncontrolled access between services and VMs**.\
Catch attackers before they can **expand horizontally** across your cloud environment.

***

### 🔀 Remote Services

***

#### ➡️ **Cloud Services (T1021.005)**

| Defensive Action                                                                                                                   | Why It Matters                         |
| ---------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| 🔒 Apply strict RBAC: Grant only least privilege at the resource level (e.g., "Storage Blob Data Reader" instead of "Contributor") | Limits service-to-service movement     |
| 🚫 Enforce network segmentation between services (VNET Integration, Private Endpoints)                                             | Isolate services from each other       |
| 📜 Monitor for suspicious use of `list-keys`, `list-blobs`, `list-credentials` API calls                                           | Early detection of lateral exploration |
| 🛡️ Enable Defender for Cloud anomaly detection (e.g., new storage key access, unexpected service access)                          | Alerts on lateral movement patterns    |

✅ **Effect**: Attackers can’t easily pivot across cloud services.

***

#### ➡️ **Direct Cloud VM Connections (T1021.001)**

| Defensive Action                                                               | Why It Matters                         |
| ------------------------------------------------------------------------------ | -------------------------------------- |
| 🔒 Restrict VM SSH/RDP access via NSGs (allow only trusted IPs or Private IPs) | Block direct VM-to-VM lateral movement |
| 🚫 Require Bastion Host for VM access — no public SSH/RDP (Azure Bastion)      | Centralized and monitored access point |
| 📜 Log all Bastion connections and alert on unusual VM access patterns         | Monitor who’s accessing which VMs      |
| 🛡️ Enable Just-In-Time (JIT) VM Access via Defender for Cloud                 | Temporary, approved VM access only     |

✅ **Effect**: Lock down VM access pathways.

***

### 🔑 Use Alternate Authentication Material

***

#### ➡️ **Application Access Token (T1550.001)**

| Defensive Action                                                                                                            | Why It Matters                       |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| 🔒 Use managed identity token restrictions — scope tokens to specific resources                                             | Limit token abuse after theft        |
| 🚫 Disable automatic mounting of service account tokens in Kubernetes unless needed (`automountServiceAccountToken: false`) | Protect workload identity            |
| 📜 Monitor token issuance and usage anomalies (unexpected IPs, services)                                                    | Detect token pivoting behaviors      |
| 🛡️ Rotate secrets and keys regularly and use token expiration policies                                                     | Reduce lifespan of any stolen tokens |

✅ **Effect**: Attackers can't easily reuse tokens to pivot across services.

***

#### ➡️ **Web Session Cookie (T1550.004)**

| Defensive Action                                                                                       | Why It Matters                     |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------- |
| 🔒 Enforce short session lifetimes in Azure Portal (Conditional Access policies)                       | Session theft window minimized     |
| 🚫 Require reauthentication for privileged operations (e.g., modifying keys, changing roles)           | Protect critical actions           |
| 📜 Monitor for session anomalies like new device IDs or IP geolocation changes (Azure AD Sign-In Logs) | Catch cookie replay attacks fast   |
| 🛡️ Use Identity Protection Risk Policies to challenge or block risky sessions automatically           | Auto-response to session hijacking |

✅ **Effect**: Session cookie theft results in quick detection and invalidation.

***

## 📊 **Defensive Coverage Table (Lateral Movement in Azure)**

| Attack Vector               | Defensive Strategy                                                             |
| --------------------------- | ------------------------------------------------------------------------------ |
| Cloud Services              | Least privilege RBAC, network segmentation, API access monitoring              |
| Direct Cloud VM Connections | Restrict SSH/RDP, enforce Bastion Host, JIT VM access                          |
| Application Access Token    | Token scoping, disable token mounting, rotate tokens                           |
| Web Session Cookie          | Short session lifetimes, reauth for critical actions, detect session hijacking |

***

## 🎯 Final Summary

Defending against Lateral Movement in Azure focuses on:

* **Shrinking access rights and privilege scopes between services**
* **Hardening authentication material like tokens and session cookies**
* **Monitoring API access patterns, especially lateral API calls**
* **Restricting direct access paths to VMs through segmentation and JIT access**
