# Defensive Strategies

## **Defensive Strategies Against Collection in Azure Environments**

In Azure, defending against **Collection** means **locking down storage, databases, secrets**, **monitoring access patterns**, and **detecting bulk data movement** before it stages for exfiltration.

The goal:\
➡️ **Stop adversaries from gathering loot**\
➡️ **Detect when mass collection starts**\
➡️ **Shut down data staging paths**

***

### 📥 Automated Collection (T1119)

| Defensive Action                                                                                          | Why It Matters                                         |
| --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| 🔒 Apply least privilege RBAC on Storage Accounts, App Services, Databases                                | Users/identities can only access what they _need_      |
| 🚫 Enable soft delete and versioning on Storage Accounts                                                  | Prevent silent overwrites or deletes during mass pulls |
| 📜 Monitor for unusual bulk download patterns (e.g., using Azure Monitor metrics on storage transactions) | Detect mass data pulls                                 |
| 🛡️ Enable Defender for Storage (Defender for Cloud) to detect bulk extraction anomalies                  | Auto-detect large downloads, exfiltration behaviors    |

✅ **Effect**: Mass data collection trips alerts and gets blocked early.

***

### ☁️ Data from Cloud Storage (T1530)

| Defensive Action                                                                                    | Why It Matters                                |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| 🔒 Enforce private endpoints and firewall rules on all Storage Accounts                             | Block public blob access                      |
| 🚫 Rotate Storage Account keys regularly, use Azure Key Vault-backed access instead                 | Prevent attackers using stolen keys           |
| 📜 Monitor Storage Account SAS (Shared Access Signature) token usage and alert on wide-scope tokens | Detect unauthorized sharing of storage access |
| 🛡️ Require Storage Authentication via Azure AD (OAuth 2.0), not account keys                       | Stronger authentication prevents theft        |

✅ **Effect**: Attackers can’t casually enumerate or pull from storage.

***

### 🗄️ Data from Information Repositories (T1213)

| Defensive Action                                                                                     | Why It Matters                               |
| ---------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| 🔒 Secure Azure SQL and Cosmos DB with private endpoints, firewalls, and strict IAM                  | Protect databases from open queries          |
| 🚫 Lock down Key Vault access policies and use Role-Based Access Control (RBAC) for Key Vault access | Prevent secrets from being listed easily     |
| 📜 Monitor for excessive query operations (e.g., `SELECT *` across tables) and mass secret reads     | Alert on unusual DB or Vault access patterns |
| 🛡️ Enable Defender for Key Vault and Defender for SQL to monitor and block anomalous accesses       | Auto-block malicious data enumeration        |

✅ **Effect**: Structured data and secrets stay secure even if accounts are compromised.

***

### 🗃️ Remote Data Staging (T1074.002)

| Defensive Action                                                                                                          | Why It Matters                                  |
| ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| 🔒 Apply Azure Policy to restrict who can create new Storage Accounts or Storage Containers                               | Block attackers from setting up staging targets |
| 🚫 Monitor for abnormal outbound data transfers from Azure Storage Accounts or VMs (Azure Monitor, Defender for Storage)  | Detect data staging behaviors                   |
| 📜 Set alerts on cross-subscription and cross-region data movements (especially between trusted and unknown environments) | Catch data leakage attempts early               |
| 🛡️ Require encryption-in-transit and enforce logging on storage and network communications                               | Track staged data movement                      |

✅ **Effect**: Data can’t be quietly staged for exfiltration without tripping alarms.

***

## 📊 **Defensive Coverage Table (Collection in Azure)**

| Attack Vector                      | Defensive Strategy                                                 |
| ---------------------------------- | ------------------------------------------------------------------ |
| Automated Collection               | Least privilege RBAC, Defender for Storage anomaly detection       |
| Data from Cloud Storage            | Private endpoints, SAS token monitoring, Key Vault-backed access   |
| Data from Information Repositories | SQL/Key Vault protection, query monitoring, Defender for Databases |
| Remote Data Staging                | Restrict Storage creation, monitor outbound transfers, log staging |

***

## 🎯 Final Summary

Defending against Collection in Azure focuses on:

* **Locking down storage, database, and secrets access tightly**
* **Preventing mass download and data harvesting operations**
* **Monitoring for abnormal data staging activities**
* **Using Defender services to detect collection anomalies early**
