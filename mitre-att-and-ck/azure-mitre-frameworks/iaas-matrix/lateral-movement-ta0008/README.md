# Lateral Movement TA0008

## **Lateral Movement Techniques in Azure Environments**

In Microsoft Azure, adversaries use Lateral Movement techniques to move between cloud services, subscriptions, VMs, and management interfaces. This is how attackers **expand their access**, **gain new privileges**, and **position for impact**.

In the cloud, lateral movement is often **token-based**, **API-based**, or **remote session-based**, without needing traditional on-prem "pivoting."

***

#### 🔀 Remote Services

***

**➡️ Cloud Services**

\| MITRE ID | **T1021.005** |

**Description**:\
Use authenticated access to Azure services like Azure Functions, AKS, Storage Accounts, App Services, Key Vaults, or Service Principals to move laterally across cloud resources.

**Azure Example**:

```bash
bashCopyEditaz functionapp list
az storage account keys list --account-name victimstorage
az aks get-credentials --resource-group victim-rg --name victim-cluster
```

✅ **Result**: Move from one cloud service to another within the same tenant or across tenants.

***

**➡️ Direct Cloud VM Connections**

\| MITRE ID | **T1021.001** |

**Description**:\
SSH or RDP into Azure VMs using valid credentials, compromised tokens, or lateral spread accounts.

**Azure Example**:

```bash
bashCopyEditssh azureuser@vm-public-ip
```

Or using Azure Bastion service if no public IP:

```bash
bashCopyEditaz network bastion ssh --name BastionHost --resource-group victim-rg --target-vm-name victim-vm
```

✅ **Result**: Move into virtual machines to harvest data or establish deeper persistence.

***

#### 🔑 Use Alternate Authentication Material

***

**➡️ Application Access Token**

\| MITRE ID | **T1550.001** |

**Description**:\
Steal Azure Managed Identity tokens, OAuth tokens, or Kubernetes service account tokens to authenticate to new cloud services or APIs without needing passwords.

**Azure Example**:

```bash
bashCopyEditcurl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"
```

✅ **Result**: Use stolen tokens to laterally authenticate across Azure APIs.

***

**➡️ Web Session Cookie**

\| MITRE ID | **T1550.004** |

**Description**:\
Steal Azure Portal session cookies and reuse them to access new Azure resources without re-authenticating.

**Azure Example**:

Reuse a stolen cookie to pivot within Azure Portal:

```bash
bashCopyEdit# Reuse stolen cookie in browser DevTools or curl to access Azure management APIs
```

✅ **Result**: Move laterally across Azure Portal resources or subscriptions using session replay.

***

## 📊 **Lateral Movement Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique      | MITRE ID  | Azure Example                                            |
| --------------------------- | --------- | -------------------------------------------------------- |
| Cloud Services              | T1021.005 | Move between Azure Functions, AKS, Storage, App Services |
| Direct Cloud VM Connections | T1021.001 | SSH/RDP into Azure VMs directly or via Azure Bastion     |
| Application Access Token    | T1550.001 | Steal and reuse Managed Identity/OAuth tokens            |
| Web Session Cookie          | T1550.004 | Replay Azure Portal session cookies for access           |

***

## 🎯 Final Summary

Defending against Lateral Movement in Azure focuses on:

* **Controlling and monitoring token usage and session authentication**
* **Restricting inter-service access via RBAC and network controls**
* **Detecting unusual access patterns across subscriptions and services**
* **Hardening VM access paths and Bastion exposure**
*
