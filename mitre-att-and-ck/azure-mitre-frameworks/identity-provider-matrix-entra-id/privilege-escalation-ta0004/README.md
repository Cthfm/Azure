# Privilege Escalation: TA0004

## **Privilege Escalation Techniques in Entra ID (Azure Identity Environments)**

In Microsoft Entra ID (Azure Active Directory), adversaries escalate privileges by **abusing role assignments, modifying trust configurations, registering devices**, or **reusing valid but overprivileged accounts**.\
Privilege escalation often moves an attacker from **standard user** to **Global Admin** or other high-value roles — a **critical turning point** in cloud attacks.

***

#### 🚀 Abuse Elevation Control Mechanism → Temporary Elevated Cloud Access

\| MITRE ID | **T1548.001** |

**Description**:\
Misuse Azure Privileged Identity Management (PIM) or Conditional Access exceptions to temporarily elevate privileges, gain Global Admin, or escalate rights.

**Entra ID Example**:

* Attacker uses compromised credentials to activate eligible Global Admin roles through PIM without triggering alarms.

```bash
bashCopyEditaz role assignment create --assignee compromised_user --role "Global Administrator"
```

✅ **Result**: Temporary escalation to powerful roles without needing direct permanent assignment.

***

#### 👥 Account Manipulation

***

**➡️ Additional Cloud Credentials**

\| MITRE ID | **T1098.001** |

**Description**:\
Add new client secrets, certificates, or credentials to privileged service principals or apps to silently elevate access.

**Entra ID Example**:

```bash
bashCopyEditaz ad sp credential reset --id <privileged-SPN-id> --password 'P@ssw0rd!'
```

✅ **Result**: Hidden credential-based escalation paths.

***

**➡️ Additional Cloud Roles**

\| MITRE ID | **T1098.003** |

**Description**:\
Assign privileged Azure RBAC roles (e.g., Owner, Contributor) or Entra ID directory roles (e.g., Global Admin, Application Admin) to compromised or attacker-created accounts.

**Entra ID Example**:

```bash
bashCopyEditaz role assignment create --assignee attacker@domain.com --role "Owner"
```

✅ **Result**: Elevates attacker-controlled identities to high privilege.

***

**➡️ Device Registration**

\| MITRE ID | **T1098.004** |

**Description**:\
Register rogue devices to satisfy Conditional Access policies (e.g., compliant device requirements), indirectly escalating privilege by meeting CA criteria.

**Entra ID Example**:

* Register a device and use it to bypass high-privilege Conditional Access policies (e.g., login with trusted device condition).

✅ **Result**: Escalate access through compliant device status.

***

#### 🏢 Domain or Tenant Policy Modification → Trust Modification

\| MITRE ID | **T1484.002** |

**Description**:\
Modify domain federation settings (e.g., Azure B2B trust configurations, identity provider settings) to enable external accounts to gain privileged access.

**Entra ID Example**:

```bash
bashCopyEditaz ad external-identity delete --id compromised-external-idp
az ad external-identity create --display-name "AttackerIdP" --federation-settings @settings.json
```

✅ **Result**: Escalate privilege via rogue trusted external users or identity providers.

***

#### 👤 Valid Accounts

***

**➡️ Default Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Exploit overprivileged default accounts (guest users, automation accounts) that already have elevated roles in Entra ID.

**Entra ID Example**:

* Abusing a misconfigured Service Principal with Contributor or Owner rights.

✅ **Result**: Instantly gain high-level access using forgotten accounts.

***

**➡️ Cloud Accounts**

\| MITRE ID | **T1078.004** |

**Description**:\
Use stolen or compromised Entra ID user accounts that have direct or indirect high privileges (Global Admin, Application Admin, etc.).

**Entra ID Example**:

```bash
bashCopyEditaz login --username compromisedadmin@domain.com
az role assignment list
```

✅ **Result**: Immediate privilege escalation with no exploit required.

***

## 📊 **Privilege Escalation Techniques in Entra ID (MITRE Mapped)**

| Technique/Subtechnique          | MITRE ID  | Entra ID Example                                    |
| ------------------------------- | --------- | --------------------------------------------------- |
| Temporary Elevated Cloud Access | T1548.001 | Abuse PIM activations or CA exceptions              |
| Additional Cloud Credentials    | T1098.001 | Add secrets/certs to privileged SPNs                |
| Additional Cloud Roles          | T1098.003 | Assign "Global Admin" or "Owner" roles              |
| Device Registration             | T1098.004 | Register compliant rogue device                     |
| Trust Modification              | T1484.002 | Modify domain trust settings (B2B federation abuse) |
| Default Accounts                | T1078.004 | Abuse forgotten privileged default accounts         |
| Cloud Accounts                  | T1078.004 | Use compromised privileged users or SPNs            |

***

## 🎯 Final Summary

Defending against Privilege Escalation in Entra ID focuses on:

* **Hardening and monitoring role assignments and PIM activations**
* **Controlling device registrations and trust configurations**
* **Detecting abnormal credential modifications or additions**
* **Reducing the privilege footprint of default and cloud accounts**

