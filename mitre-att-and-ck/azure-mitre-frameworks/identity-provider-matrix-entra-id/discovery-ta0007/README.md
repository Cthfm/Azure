# Discovery: TA0007

## **Discovery Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure Active Directory), adversaries use Discovery techniques to **enumerate identities, permissions, policies, and services** to plan lateral movement, privilege escalation, or targeting.

Discovery is the **reconnaissance phase** in cloud attacks — understanding the environment is key before action.

***

#### 🔍 Account Discovery → Cloud Account

\| MITRE ID | **T1087.004** |

**Description**:\
Enumerate Entra ID users, service principals, or managed identities to identify potential targets for phishing, credential theft, or escalation.

**Entra ID Example**:

```bash
bashCopyEditaz ad user list
az ad sp list
az ad signed-in-user show
```

✅ **Result**: Full directory listing of users, apps, service principals.

***

#### 🖥️ Cloud Service Dashboard

\| MITRE ID | **T1087.004 (extension)** |

**Description**:\
Access Azure Portal or use APIs to discover what services are deployed across subscriptions (e.g., VMs, Storage, App Services, Key Vaults).

**Entra ID Example**:

```bash
bashCopyEditaz account list
az resource list
az vm list
```

✅ **Result**: Broad visibility into active cloud services.

***

#### ☁️ Cloud Service Discovery

\| MITRE ID | **T1087.004 (extension)** |

**Description**:\
Query cloud APIs or dashboards to discover deployed services, configurations, and environments (e.g., Azure Resource Manager enumeration).

**Entra ID Example**:

```bash
bashCopyEditaz resource list --resource-type Microsoft.Compute/virtualMachines
az aks list
az keyvault list
```

✅ **Result**: Full service inventory for planning further attacks.

***

#### 🔑 Password Policy Discovery

\| MITRE ID | **T1201** |

**Description**:\
Query password policy settings to assess password complexity requirements, lockout thresholds, and MFA enforcement.

**Entra ID Example**:

* Review **Azure AD Password Protection** policies.
* Query Azure Active Directory password policies via Microsoft Graph (requires privilege).

✅ **Result**: Understand how easy password attacks might be.

***

#### 👥 Permission Groups Discovery → Cloud Groups

\| MITRE ID | **T1069.003** |

**Description**:\
Enumerate Entra ID groups to identify high-privilege groups like Global Admins, Application Admins, or owners of critical resources.

**Entra ID Example**:

```bash
bashCopyEditaz ad group list
az ad group member list --group <Group-Name>
```

✅ **Result**: Map out administrative control structures.

***

## 📊 **Discovery Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique    | MITRE ID              | Entra ID Example                           |
| ------------------------- | --------------------- | ------------------------------------------ |
| Cloud Account Discovery   | T1087.004             | Enumerate users, service principals        |
| Cloud Service Dashboard   | T1087.004 (extension) | Azure Portal or CLI resource discovery     |
| Cloud Service Discovery   | T1087.004 (extension) | List deployed services (VMs, storage, AKS) |
| Password Policy Discovery | T1201                 | Assess password and lockout settings       |
| Cloud Groups Discovery    | T1069.003             | Enumerate Entra ID groups and memberships  |

***

## 🎯 Final Summary

Defending against Discovery in Entra ID focuses on:

* **Restricting who can enumerate users, groups, and services**
* **Limiting exposure of sensitive service metadata**
* **Monitoring unusual enumeration patterns (e.g., mass user listing, group membership pulls)**

> **Discovery is the enemy’s map. Deny mapping = deny maneuvering.** 🛡️✅
