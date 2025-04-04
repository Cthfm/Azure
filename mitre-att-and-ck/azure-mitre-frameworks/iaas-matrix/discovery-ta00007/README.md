# Discovery TA00007

## **Discovery Techniques in Azure Environments**

In Microsoft Azure, adversaries use Discovery techniques to learn about cloud resources, accounts, network configurations, logging systems, and security tools. This knowledge helps them plan **lateral movement, privilege escalation, and impact** operations.

Cloud environments expose **rich metadata** if discovery isn't controlled — making early visibility critical.

***

#### 🔍 Account Discovery → **T1087**

***

**➡️ Cloud Account**

\| MITRE ID | **T1087.004** |

**Description**:\
List Azure AD users, service principals, managed identities, and other accounts.

**Azure Example**:

```bash
bashCopyEditaz ad user list
az ad sp list
```

✅ **Result**: Full view of available identities for targeting.

***

#### 🌩️ Cloud Infrastructure Discovery

\| MITRE ID | **T1580** |

**Description**:\
Enumerate Azure subscriptions, resource groups, VMs, Kubernetes clusters, and networking components.

**Azure Example**:

```bash
bashCopyEditaz resource list
az aks list
az vm list
```

✅ **Result**: Inventory of available cloud assets.

***

#### 📊 Cloud Service Dashboard

\| MITRE ID | **T1538** |

**Description**:\
Access Azure Portal or dashboards to manually discover available services, configurations, and security postures.

**Azure Example**:

Login to `portal.azure.com` and browse **Resource Groups**, **App Services**, **Key Vaults**.

✅ **Result**: GUI-based resource discovery.

***

#### ☁️ Cloud Service Discovery

\| MITRE ID | **T1526** |

**Description**:\
Programmatically query Azure APIs to find cloud services like Storage, App Services, Databases, etc.

**Azure Example**:

```bash
bashCopyEditaz storage account list
az sql server list
```

✅ **Result**: API-level enumeration of services.

***

#### 📂 Cloud Storage Object Discovery

\| MITRE ID | **T1619** |

**Description**:\
List blobs, files, and shares inside Azure Storage Accounts.

**Azure Example**:

```bash
bashCopyEditaz storage blob list --account-name victimstorage --container-name secrets
```

✅ **Result**: Discovery of exposed or misconfigured storage objects.

***

#### 📜 Log Enumeration

\| MITRE ID | **T1560** (closest match: Data from Local System) |

**Description**:\
Enumerate Azure Activity Logs, Diagnostic Logs, or SIEM logs to learn about operations and incidents.

**Azure Example**:

```bash
bashCopyEditaz monitor activity-log list
az monitor diagnostic-settings list
```

✅ **Result**: Discovery of logging practices and audit trails.

***

#### 🌐 Network Service Discovery

\| MITRE ID | **T1046** |

**Description**:\
Identify networked services like exposed VM public IPs, load balancers, Kubernetes API servers, App Gateways.

**Azure Example**:

```bash
bashCopyEditaz network public-ip list
az network lb list
```

✅ **Result**: Map cloud network surfaces.

***

#### 🌐 Network Sniffing

\| MITRE ID | **T1040** |

**Description**:\
Capture Azure VNET traffic to identify active services, open ports, and network protocols.

**Azure Example**:

Deploy a packet capture agent on a VM or use NSG flow logs.

✅ **Result**: Dynamic network mapping.

***

#### 🛡️ Password Policy Discovery

\| MITRE ID | **T1201** |

**Description**:\
Query Azure AD password policies to understand complexity, rotation, and lockout settings.

**Azure Example**:

```bash
bashCopyEditaz ad policy password list
```

✅ **Result**: Assess credential hardening posture.

***

#### 🛡️ Permission Groups Discovery → **Cloud Groups**

\| MITRE ID | **T1069.003** |

**Description**:\
List Azure AD security groups, M365 groups, and their members.

**Azure Example**:

```bash
bashCopyEditaz ad group list
az ad group member list --group <group-name>
```

✅ **Result**: Discover access control groupings.

***

#### 🖥️ Software Discovery → Security Software Discovery

\| MITRE ID | **T1518.001** |

**Description**:\
Identify what security agents, endpoint detection systems, or monitoring solutions are deployed in Azure.

**Azure Example**:

Query installed extensions or Defender coverage:

```bash
bashCopyEditaz vm extension list
az security pricing list
```

✅ **Result**: Visibility into deployed security tooling.

***

#### 🖥️ System Information Discovery

\| MITRE ID | **T1082** |

**Description**:\
Collect detailed information about Azure VMs, OS versions, and instance metadata.

**Azure Example**:

```bash
bashCopyEditaz vm show --name <vm-name> --resource-group <rg>
```

✅ **Result**: Target system profiling.

***

#### 📍 System Location Discovery

\| MITRE ID | **T1614.001** |

**Description**:\
Determine the Azure regions where resources are deployed.

**Azure Example**:

```bash
bashCopyEditaz account list-locations
az resource list --query '[].location'
```

✅ **Result**: Understand physical cloud footprint.

***

#### 🌐 System Network Connections Discovery

\| MITRE ID | **T1049** |

**Description**:\
Discover Azure VMs’ network connections, public IP mappings, and peering relationships.

**Azure Example**:

```bash
bashCopyEditaz network nic list
az network vnet peering list
```

✅ **Result**: Network relationship mapping.

***

## 📊 **Discovery Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique               | MITRE ID              | Azure Example                        |
| ------------------------------------ | --------------------- | ------------------------------------ |
| Cloud Account                        | T1087.004             | List Azure AD users, SPNs            |
| Cloud Infrastructure Discovery       | T1580                 | List Azure subscriptions, AKS, VMs   |
| Cloud Service Dashboard              | T1538                 | Browse Azure Portal for resources    |
| Cloud Service Discovery              | T1526                 | API enumeration of cloud services    |
| Cloud Storage Object Discovery       | T1619                 | List blobs/files in Azure Storage    |
| Log Enumeration                      | T1560 (closest match) | Query Activity Logs, Diagnostics     |
| Network Service Discovery            | T1046                 | List public IPs, Load Balancers      |
| Network Sniffing                     | T1040                 | Capture VNET traffic                 |
| Password Policy Discovery            | T1201                 | Read Azure AD password policies      |
| Cloud Groups                         | T1069.003             | Enumerate Azure AD groups            |
| Security Software Discovery          | T1518.001             | Identify Defender agents, extensions |
| System Information Discovery         | T1082                 | VM OS and instance metadata          |
| System Location Discovery            | T1614.001             | Azure region discovery               |
| System Network Connections Discovery | T1049                 | NICs, peerings, network mappings     |

***

## 🎯 Final Summary

Defending against Discovery in Azure focuses on:

* **Hardening identity and API access controls**
* **Restricting who can list resources and services (least privilege RBAC)**
* **Securing logs, secrets, and storage configurations**
* **Detecting enumeration and unauthorized reconnaissance activity**
