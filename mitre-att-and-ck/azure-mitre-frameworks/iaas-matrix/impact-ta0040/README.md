# Impact TA0040

## 🛡️ **Impact Techniques in Azure Environments**

In Microsoft Azure, adversaries use **Impact techniques** to disrupt availability, destroy data, impair recovery, hijack resources, or cause financial/resource loss.\
Impact actions often come **late in the attack chain**, once the attacker has achieved persistence and/or escalated privileges.

***

#### ❌ Account Access Removal

\| MITRE ID | **T1531** |

**Description**:\
Remove users, service principals, or role assignments in Azure AD (Entra ID) to disrupt operations or lock out legitimate administrators.

**Azure Example**:

```bash
bashCopyEditaz role assignment delete --assignee <user-id> --role Owner
az ad user delete --id admin@victimdomain.com
```

✅ **Result**: Admins locked out, services disrupted.

***

#### 💥 Data Destruction → Lifecycle-Triggered Deletion

\| MITRE ID | **T1485.001** |

**Description**:\
Abuse Azure Storage lifecycle policies or backup retention settings to auto-delete critical data.

**Azure Example**:

```bash
bashCopyEditaz storage account management-policy create --account-name victimstorage --policy @deletion-policy.json
```

✅ **Result**: Data deleted over time automatically, hard to recover.

***

#### 🔒 Data Encrypted for Impact

\| MITRE ID | **T1486** |

**Description**:\
Encrypt critical Azure data (e.g., blobs, databases) with unauthorized keys, denying access to legitimate owners.

**Azure Example**:

* Rotate Key Vault keys.
* Encrypt Storage Accounts or Azure SQL with unknown Customer-Managed Keys (CMKs).

```bash
bashCopyEditaz keyvault key rotate --vault-name victimvault --name storage-key
```

✅ **Result**: Data held hostage via encryption.

***

#### 🎨 Defacement → External Defacement

\| MITRE ID | **T1491.001** |

**Description**:\
Modify externally facing Azure resources like Web Apps, static sites, or blob-hosted websites to display defacement content.

**Azure Example**:

```bash
bashCopyEditaz webapp deployment source config-zip --src defaced.zip --name victim-webapp
```

✅ **Result**: Public defacement and reputational damage.

***

#### 🛑 Endpoint Denial of Service

***

**➡️ Service Exhaustion Flood**

\| MITRE ID | **T1499.001** |

**Description**:\
Flood Azure services (e.g., App Services, Functions) with traffic to exhaust compute or outbound connections.

**Azure Example**:

Use botnets or multiple VMs to overload Azure Web Apps.

✅ **Result**: Application unresponsive.

***

**➡️ Application Exhaustion Flood**

\| MITRE ID | **T1499.002** |

**Description**:\
Overwhelm Azure-hosted APIs, Functions, or Logic Apps with malformed requests, exhausting application logic or threading limits.

✅ **Result**: App or service crash.

***

**➡️ Application or System Exploitation**

\| MITRE ID | **T1499.003** |

**Description**:\
Exploit unpatched vulnerabilities in Azure-hosted services or VMs to cause system crashes or application denial.

**Azure Example**:

Exploit an RCE on a misconfigured VM or Web App.

✅ **Result**: Application/system crashes.

***

#### 🔄 Inhibit System Recovery

\| MITRE ID | **T1490** |

**Description**:\
Delete Azure backups, snapshots, Recovery Services Vaults, or purge soft-deleted Key Vaults to prevent recovery.

**Azure Example**:

```bash
bashCopyEditaz backup item delete --vault-name RecoveryVault --container-name StorageContainer --name VM1
az keyvault purge --name victimvault
```

✅ **Result**: No way to roll back after destructive actions.

***

#### 🌐 Network Denial of Service

***

**➡️ Direct Network Flood**

\| MITRE ID | **T1498.001** |

**Description**:\
Flood Azure VMs, Load Balancers, or App Gateways directly with SYN/UDP/ICMP traffic to exhaust bandwidth.

✅ **Result**: Network resource unavailable.

***

**➡️ Reflection Amplification**

\| MITRE ID | **T1498.002** |

**Description**:\
Use misconfigured Azure DNS or open services to reflect and amplify traffic toward a victim target (DDoS).

✅ **Result**: Amplified DDoS effect, possible collateral damage.

***

#### 🖥️ Resource Hijacking

***

**➡️ Compute Hijacking**

\| MITRE ID | **T1496.001** |

**Description**:\
Deploy crypto-mining software on Azure VMs, App Services, Kubernetes clusters, or Containers to hijack compute resources.

**Azure Example**:

```bash
bashCopyEditdocker run -d cryptominer:latest
```

✅ **Result**: Hidden resource theft, inflated bills.

***

**➡️ Bandwidth Hijacking**

\| MITRE ID | **T1496.002** |

**Description**:\
Use Azure-hosted services or VMs to tunnel attacker traffic (e.g., proxy, TOR relays), draining victim bandwidth.

✅ **Result**: Unexpected egress bills, reputational impact.

***

## 📊 **Impact Techniques in Azure (MITRE Mapped)**

| Technique/Subtechnique             | MITRE ID  | Azure Example                                     |
| ---------------------------------- | --------- | ------------------------------------------------- |
| Account Access Removal             | T1531     | Remove users/roles in Azure AD                    |
| Lifecycle-Triggered Deletion       | T1485.001 | Abuse Storage lifecycle to auto-delete            |
| Data Encrypted for Impact          | T1486     | Rotate encryption keys in Key Vault               |
| External Defacement                | T1491.001 | Replace Azure Web App or Blob Static Site content |
| Service Exhaustion Flood           | T1499.001 | Overload Azure Web Apps, APIs                     |
| Application Exhaustion Flood       | T1499.002 | Send malformed requests to crash apps             |
| Application or System Exploitation | T1499.003 | Exploit unpatched apps or VMs                     |
| Inhibit System Recovery            | T1490     | Delete backups, purge Key Vaults                  |
| Direct Network Flood               | T1498.001 | Flood Azure network resources                     |
| Reflection Amplification           | T1498.002 | Amplify attacks via misconfigured Azure DNS       |
| Compute Hijacking                  | T1496.001 | Deploy crypto-miners on Azure VMs/containers      |
| Bandwidth Hijacking                | T1496.002 | Use Azure VMs for proxy/tunneling                 |

***

## 🎯 Final Summary

Defending against Impact in Azure focuses on:

* **Protecting access control and backup mechanisms**
* **Hardening encryption key management**
* **Monitoring service usage, network traffic, and system health**
* **Detecting resource misuse early (compute, bandwidth, storage)**
