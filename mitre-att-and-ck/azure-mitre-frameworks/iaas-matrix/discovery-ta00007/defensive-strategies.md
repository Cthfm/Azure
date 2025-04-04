# Defensive Strategies

## **Defensive Strategies Against Discovery in Azure Environments**

Discovery is a **critical pre-attack phase**.\
If you block or monitor it properly, you **detect adversaries early** before they escalate or pivot.

***

### 🔍 Account Discovery → Cloud Account (T1087.004)

| Defensive Action                                                                           | Why It Matters                        |
| ------------------------------------------------------------------------------------------ | ------------------------------------- |
| 🔒 Restrict Azure AD read permissions — use Conditional Access + limited Directory Readers | Not everyone needs to enumerate users |
| 🚫 Disable Azure AD Guest Inviter/External Users when possible                             | Reduce external enumeration risks     |
| 📜 Monitor for high-volume listing of Azure AD users/groups in Sign-In Logs                | Catch enumeration early               |

✅ **Effect**: Make account harvesting harder.

***

### 🌩️ Cloud Infrastructure Discovery (T1580)

| Defensive Action                                                            | Why It Matters                                  |
| --------------------------------------------------------------------------- | ----------------------------------------------- |
| 🔒 Apply least privilege RBAC — deny `Reader` role broadly unless necessary | Don't allow broad listing of cloud resources    |
| 📜 Monitor usage of `az resource list` or subscription-wide queries         | Alert on suspicious resource discovery patterns |
| 🚫 Use Management Groups and Scoped Access                                  | Narrow visibility across subscriptions          |

✅ **Effect**: Limit who can map your cloud infrastructure.

***

### 📊 Cloud Service Dashboard (T1538)

| Defensive Action                                                                    | Why It Matters                          |
| ----------------------------------------------------------------------------------- | --------------------------------------- |
| 🔒 Enable Conditional Access for Azure Portal login (require MFA, compliant device) | Block unauthorized GUI reconnaissance   |
| 📜 Monitor Azure AD Sign-In logs for risky browser-based logins                     | Catch portal-based exploration attempts |

✅ **Effect**: Lock portal access to trusted users and devices.

***

### ☁️ Cloud Service Discovery (T1526)

| Defensive Action                                                             | Why It Matters                               |
| ---------------------------------------------------------------------------- | -------------------------------------------- |
| 🔒 Enforce Azure Policy to restrict resource deployments and listings        | API discovery restricted to what’s necessary |
| 🚫 Use service-specific RBAC (e.g., Storage Account Reader, not full Reader) | Minimize discovery radius per service        |
| 📜 Enable Defender for Cloud anomaly alerts                                  | Detect anomalous API discovery bursts        |

✅ **Effect**: API-based service discovery tightly controlled.

***

### 📂 Cloud Storage Object Discovery (T1619)

| Defensive Action                                                   | Why It Matters                        |
| ------------------------------------------------------------------ | ------------------------------------- |
| 🔒 Require private endpoints for all storage accounts              | No public blobs or file shares        |
| 🚫 Enable Azure Storage Firewall to block public access by default | Stop open storage object discovery    |
| 📜 Monitor for unauthorized Storage Account access attempts        | Catch early scanning or object access |

✅ **Effect**: Protect storage from blind enumeration.

***

### 📜 Log Enumeration (T1560)

| Defensive Action                                                    | Why It Matters                     |
| ------------------------------------------------------------------- | ---------------------------------- |
| 🔒 Apply RBAC to restrict access to Activity Logs and Log Analytics | Limit access to audit data         |
| 🚫 Secure Diagnostic Settings with write protection (Azure Policy)  | Prevent logging pipeline tampering |
| 📜 Alert on mass Activity Log queries                               | Detect log enumeration patterns    |

✅ **Effect**: Protect your detection capabilities themselves.

***

### 🌐 Network Service Discovery (T1046)

| Defensive Action                                                                     | Why It Matters                |
| ------------------------------------------------------------------------------------ | ----------------------------- |
| 🔒 Apply NSGs (Network Security Groups) tightly — allow only necessary inbound ports | Hide exposed IPs and services |
| 🚫 Use Azure Private Endpoints where possible (no public access)                     | Shield internal services      |
| 📜 Monitor NSG Flow Logs for unusual port scanning behaviors                         | Detect enumeration attempts   |

✅ **Effect**: Hide and monitor your network footprint.

***

### 🌐 Network Sniffing (T1040)

| Defensive Action                                                         | Why It Matters                 |
| ------------------------------------------------------------------------ | ------------------------------ |
| 🔒 Disable packet capture capabilities on production VMs                 | Limit access to NICs           |
| 🚫 Harden VNET NSGs and use encrypted communication (TLS/SSL) internally | No useful traffic to sniff     |
| 📜 Monitor Azure Activity Logs for packet capture setup events           | Catch sniffer deployments fast |

✅ **Effect**: Kill network-level reconnaissance opportunities.

***

### 🛡️ Password Policy Discovery (T1201)

| Defensive Action                                                     | Why It Matters                                |
| -------------------------------------------------------------------- | --------------------------------------------- |
| 🔒 Apply strong password policies via Azure AD (complexity, lockout) | Good password hygiene regardless of discovery |
| 🚫 Restrict directory permission to view policies                    | Hide credential hardening details             |
| 📜 Audit password policy settings periodically                       | Ensure best practices maintained              |

✅ **Effect**: Even if policies are discovered, they aren't weak.

***

### 🛡️ Permission Groups Discovery → Cloud Groups (T1069.003)

| Defensive Action                                                           | Why It Matters                |
| -------------------------------------------------------------------------- | ----------------------------- |
| 🔒 Restrict group listing permissions to Directory Readers only            | Prevent broad group discovery |
| 🚫 Avoid assigning overly broad access (Owner/Contributor) at group levels | Minimize pivoting risk        |
| 📜 Monitor group membership changes and listing behaviors                  | Detect group mapping attempts |

✅ **Effect**: Hide access structures from attackers.

***

### 🖥️ Software Discovery → Security Software Discovery (T1518.001)

| Defensive Action                                            | Why It Matters                         |
| ----------------------------------------------------------- | -------------------------------------- |
| 🔒 Restrict who can view VM extensions and security pricing | Hide security tooling presence         |
| 🚫 Limit Defender for Cloud visibility to trusted teams     | Protect your security strategy details |
| 📜 Monitor for enumeration of security-related extensions   | Catch tooling reconnaissance           |

✅ **Effect**: Protect what you use to protect yourself.

***

### 🖥️ System Information Discovery (T1082)

| Defensive Action                                         | Why It Matters                                  |
| -------------------------------------------------------- | ----------------------------------------------- |
| 🔒 Apply strict identity permissions to VMs and metadata | No open `az vm show` permissions                |
| 🚫 Harden access to instance metadata                    | Limit system information leakage                |
| 📜 Audit VM inventory and public exposure regularly      | Keep cloud asset knowledge clean and controlled |

✅ **Effect**: Minimize attacker targeting options.

***

### 📍 System Location Discovery (T1614.001)

| Defensive Action                         | Why It Matters                                    |
| ---------------------------------------- | ------------------------------------------------- |
| 🔒 Restrict region listing capabilities  | Limit exposure of where your workloads live       |
| 📜 Monitor resource deployment locations | Detect rogue deployments outside standard regions |

✅ **Effect**: Hide geographical attack surface.

***

### 🌐 System Network Connections Discovery (T1049)

| Defensive Action                                            | Why It Matters                     |
| ----------------------------------------------------------- | ---------------------------------- |
| 🔒 Secure NIC and VNET peering visibility tightly with RBAC | Limit lateral mapping              |
| 🚫 Harden Azure VNET Peering with NSGs and route tables     | No free paths between environments |
| 📜 Monitor VNET peering changes and new NIC creation events | Detect network exploration         |

✅ **Effect**: Block lateral discovery.

***

## 📊 **Defensive Coverage Table (Discovery in Azure)**

| Attack Vector                        | Defensive Strategy                                     |
| ------------------------------------ | ------------------------------------------------------ |
| Account Discovery                    | Directory restrictions, Sign-In Log monitoring         |
| Cloud Infrastructure Discovery       | Least privilege RBAC, API anomaly detection            |
| Cloud Service Dashboard              | Portal access via CA policies, risky login detection   |
| Cloud Service Discovery              | API access control, anomaly detection                  |
| Cloud Storage Object Discovery       | Private endpoints, storage firewalls                   |
| Log Enumeration                      | RBAC protection, alert on mass log queries             |
| Network Service Discovery            | NSG enforcement, flow log monitoring                   |
| Network Sniffing                     | Disable captures, TLS encryption                       |
| Password Policy Discovery            | Strong password enforcement, limited policy visibility |
| Permission Groups Discovery          | Restrict group listing, monitor group usage            |
| Security Software Discovery          | Restrict extension visibility, monitor enumeration     |
| System Information Discovery         | Metadata protection, VM inventory control              |
| System Location Discovery            | Limit region discovery, rogue deployment monitoring    |
| System Network Connections Discovery | NIC/VNET security, peering monitoring                  |

***

## 🎯 Final Summary

Defending against Discovery in Azure focuses on:

* **Hiding and controlling resource visibility** (RBAC, API, Portal)
* **Restricting storage, logging, and network enumeration**
* **Hardening identity and system metadata exposure**
* **Detecting unauthorized reconnaissance behaviors early**
