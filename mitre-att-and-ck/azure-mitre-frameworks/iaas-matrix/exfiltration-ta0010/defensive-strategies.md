# Defensive Strategies

## **Defensive Strategies Against Exfiltration in Azure Environments**

In Azure, defending against Exfiltration means **locking down outbound data paths**, **monitoring cloud storage traffic**, and **detecting stealthy transfer attempts** before data leaves the environment.

The goal:\
➡️ **Prevent unauthorized data movement**\
➡️ **Detect suspicious transfers early**\
➡️ **Shut down attacker-controlled staging areas**

***

### 🌐 Exfiltration Over Alternative Protocol (T1048)

| Defensive Action                                                                                            | Why It Matters                                                                 |
| ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| 🔒 Restrict outbound Internet access using Azure NSGs, ASGs, and Azure Firewall rules                       | Block direct Internet exfil from Azure resources                               |
| 🚫 Force traffic to pass through Azure Firewall or third-party inspection appliances                        | Inspect HTTPS traffic for anomalies                                            |
| 📜 Enable Azure Monitor and Defender for Cloud to watch for abnormal outbound data volumes and destinations | Detect large data transfers over HTTPS, DNS tunneling, or other covert methods |
| 🛡️ Implement Azure DLP (Data Loss Prevention) policies on sensitive storage and endpoints                  | Prevent sensitive data from leaving the cloud unmonitored                      |

✅ **Effect**: HTTPS/DNS tunneling exfiltration gets detected and blocked early.

***

### ☁️ Transfer Data to Cloud Account (T1537)

| Defensive Action                                                                                                               | Why It Matters                                       |
| ------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| 🔒 Restrict who can create or update Storage Account connections, SAS tokens, and cross-tenant sharing policies (RBAC)         | Control who can stage data for transfer              |
| 🚫 Monitor and alert on cross-subscription, cross-tenant, or cross-cloud storage traffic (Azure Monitor, Defender for Storage) | Catch rogue cloud-to-cloud exfiltration              |
| 📜 Audit and review all outbound storage connections periodically                                                              | Spot rogue storage transfers to unknown destinations |
| 🛡️ Encrypt all storage account traffic and enforce logging on storage access                                                  | Make data movement traceable and harder to hide      |

✅ **Effect**: Attackers can’t quietly transfer data to another cloud account without detection.

***

## 📊 **Defensive Coverage Table (Exfiltration in Azure)**

| Attack Vector                          | Defensive Strategy                                                       |
| -------------------------------------- | ------------------------------------------------------------------------ |
| Exfiltration Over Alternative Protocol | Outbound restrictions, traffic inspection, DLP monitoring                |
| Transfer Data to Cloud Account         | Storage RBAC tightening, cross-tenant monitoring, storage access logging |

***

## 🎯 Final Summary

Defending against Exfiltration in Azure focuses on:

* **Blocking unnecessary outbound traffic and monitoring cloud-to-cloud transfers**
* **Inspecting all outbound HTTPS and DNS traffic patterns**
* **Detecting large or unusual data transfers early**
* **Restricting and auditing access to storage accounts and cloud connectors**
